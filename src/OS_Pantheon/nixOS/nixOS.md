# NixOS on a Raspberry Pi 4

First you need to prepare the AArch64 image on your laptop:

```bash
$ nix-shell -p wget zstd
$ wget https://hydra.nixos.org/build/160738647/download/1/nixos-sd-image-22.05pre374583.cbe587c735b-aarch64-linux.img.zst
$ unzstd -d nixos-sd-image-22.05pre374583.cbe587c735b-aarch64-linux.img.zst
$ dmesg --follow
```

> You can pick a newer image by going to You can pick a newer image by going to [Hydra](https://hydra.nixos.org/job/nixos/trunk-combined/nixos.sd_image.aarch64-linux) job, clicking on a build and copying the link to the build product image. job, clicking on a build and copying the link to the build product image.

Your terminal should be printing kernel messages as they come in.

Plug in your SD card and your terminal should print what device it got assigned, for example ``/dev/sdX``.

Press ``ctrl-c`` to stop ``dmesg --follow``.

Copy NixOS to your SD card by replacing ``sdX`` with the name of your device:

```bash
$ sudo dd if=nixos-sd-image-22.05pre374583.cbe587c735b-aarch64-linux.img of=/dev/sdX bs=4096 conv=fsync status=progress
```

Once that command exits, **move the SD card into your Raspberry Pi and power it on**.

You should be greeted with a fresh shell!

In case the image doesn’t boot, it’s worth updating the [firmware](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#updating-the-bootloader) and retry booting the image again.

## Getting internet connection

Run ``sudo -i`` to get a root shell for the rest of the tutorial.

At this point we’ll need internet connection. If you can use an ethernet cable, plug it in.

In case you’re connecting to a wifi run ``iwconfig`` to see what is the name of your wireless network interface. In case it’s ```wlan0``` replace ```SSID``` and ```passphrase``` with ```makerspace``` ```gkgV8jID`` your data and run:

```bash
$ wpa_supplicant -B -i wlan0 -c <(wpa_passphrase 'SSID' 'passphrase') &
```

Once you see your terminal that connection is established, run ``host nixos.org`` to check the DNS resolves correctly.

In case you've made a typo, run ``pkill wpa_supplicant`` and start over.

## Updating the Firmware

To benefit from updates and bug fixes from the vendor, we will start by updating Raspberry Pi firmware:

```bash
$ nix-shell -p raspberrypi-eeprom
$ mount /dev/disk/by-label/FIRMWARE /mnt
$ BOOTFS=/mnt FIRMWARE_RELEASE_STATUS=stable rpi-eeprom-update -d  
```

## Installing NixOS

For initial installation we'll install [XFCE](https://www.xfce.org/) desktop environment with user ``Guest`` and ``SSH daemon``.

The script below is below is a configuration file, remember that NixOS is a decalaritve system and that its root directories are immutable therefore we must **configure -> deploy -> re-coonfigure -> deploy ...**

Using you the ``nano`` text editor you enter the following command as ``su``... ``nano /etc/nixos/configuration.nix`` 

```nix 
{config, pkgs, lib, ... }:

let
  user = "guest";
  password = "guest";
  SSID = "makerspace";
  SSIDpassword = "gkgV8jID";
  interface = "wlan0";
  hostname = "myhostname";
in {
  imports = ["${fetchTarball "https://github.com/NixOS/nixos-hardware/archive/936e4649098d6a5e0762058cb7687be1b2d90550.tar.gz" }/raspberry-pi/4"];

  fileSystems = {
    "/" = {
      device = "/dev/disk/by-label/NIXOS_SD";
      fsType = "ext4";
      options = [ "noatime" ];
    };
  };

  networking = {
    hostName = hostname;
    wireless = {
      enable = true;
      networks."${SSID}".psk = SSIDpassword;
      interfaces = [ interface ];
    };
  };

  environment.systemPackages = with pkgs; [ vim ];

  services.openssh.enable = true;

  users = {
    mutableUsers = false;
    users."${user}" = {
      isNormalUser = true;
      password = password;
      extraGroups = [ "wheel" ];
    };
  };

  # Enable GPU acceleration
  hardware.raspberry-pi."4".fkms-3d.enable = true;

  services.xserver = {
    enable = true;
    displayManager.lightdm.enable = true;
    desktopManager.xfce.enable = true;
  };

  hardware.pulseaudio.enable = true;
}
```

Of course if you have already read past the configuration above then you could always save some much needed time and do this in the terminal as ``su``:

```bash
$ curl -L https://tinyurl.com/nixos-rpi4-tutorial > /etc/nixos/configuration.nix
```

At the top of ``/etc/nixos/configuration.nix`` there are a few variables that you want to configure, most important being your wifi connection details, this time specified in declarative way.

Once you're ready to deploy your first configuration file:

```bash
$ nixos-install --root /
$ reboot
```

## Making Changes

It booted, congratulations!

To make further changes to the configuration, search through [NixOS options](https://search.nixos.org/options), edit ``/etc/nixos/configuration.nix`` and update your system.

However, we are going to make some changes to the configuration file now and redeploy. Re-open ``/etc/nixos/configuration.nix``. We need to change the keymapping, locale and dateTime, navigate to the line above ``networking = {`` and add the following configuration:

```nix
time.timeZone = "Europe/London";
```
Then find the line ``services.openssh.enable = true;`` and creat a new line underneath and enter the following:

```nix
i18n.defaultLocale = "en_GB.UTF-8";
console = {
	font = "Lat2-Terminus16";
	keyMap = "uk";
};
```

Next we are going to declaratively set the CPU governor, navigate to where the script has the line ``hardware.raspberry.pi."4".fkms-3d.enable = true;`` and create a new line and enter the following:

```nix
powerManagement.cpuFreqGovernor = "powersave";
```

Next modify the services.xserver to look like this:

```nix
services.xserver ={
	enable = true;
	layout = "gb";
};
``` 
Now write out so we can redeploy our script live.


```bash
	$ sudo -i
  $ nixos-rebuild switch
```