# Aliases and bash customization

#### Questions:
> - How do I customize my bash environment?

#### Objectives:
> - Create aliases.
>>
> - Add customizations to the `.bashrc` and `.bash_profile` files.
>>
> - Change the prompt in a bash environment.

<details>
<summary><b>TL;DR</b></summary>
<p></p>

> - Aliases are used to create shortcuts or abbreviations
>>
> - The `.bashrc` and `.bash_profile` files allow us to customize our bash environment.
>>
> - The `PS1` system variable can be changed to customize your bash prompt.
</details>

---

Bash allows us to customize our environments to fill our own particular needs.

## Aliases

Sometimes we need to use long commands that have to be typed over and over again.  Fortunately, the `alias` command allows us to create shortcuts for these long commands.

As an example, let's create aliases for going up one, two, or three directories.

```sh
alias up='cd ..'
alias upup='cd ../..'
alias upupup='cd ../../..'
```

Let's try these commands out.

```sh
cd /usr/local/bin
upup
pwd
```
Output:.
```sh
/usr
```

We can also remove a shortcut with `unalias`.

```sh
unalias upupup
```

If we create one of these aliases in a bash session, they will only last until the end of that session. Fortunately, bash allows us to specify customizations that will work whenever we begin a new bash session.

## Bash customization files

Bash environments can be customized by adding commands to the `.bashrc`, `.bash_profile`, and `.bash_logout` files in our home directory.  The `.bashrc` file is executed whenever entering interactive non-login shells whereas `.bash_profile` is executed for login shells.  If the `.bash_logout` file exists, then it will be run after exiting a shell session.

Let's add the above commands to our `.bashrc` file.

Be careful to append to `.bashrc`, with `>>`. for concatenate, rather than one `>` which would overwrite.
```sh
echo "alias up='cd ..'" >> ~/.bashrc
tail -n 1 ~/.bashrc
```
Output:
```sh
alias up='cd ..'
```

We can execute the commands in `.bashrc` using `source`, so this creates the alias `up` which we can then use in directory `/usr/local/bin`:

```sh
source ~/.bashrc
cd /usr/local/bin
up
pwd
```
Output:
```sh
/usr/local
```
Having to add customizations to two files can be cumbersome.  It we would like to always use the customizations in our `.bashrc` file,  then we can add the following lines to our `.bash_profile` file.

```sh
if [ -f $HOME/.bashrc ]; then
        source $HOME/.bashrc
fi
```
Furthermore, and what is seen as good practice it to have a seperate alias file which is sourced in a similar way.

```sh
if [ -f $HOME/.bash_aliases ]; then
        source $HOME/.bash_aliases
fi
```

Within this file you could place

```sh
#GIT
alias gst="git status"
alias ga="git add"
alias gaa="git add ."
alias gcm="git commit -m"
alias gpl="git pull"
alias gps="git push"
gc ()
{
  git clone git@github.com:"$1""/""$2"
}

alias ls="lsd"
alias layout="~/.config/i3/layouts/layout.sh"
alias off="sudo shutdown -h now"
alias cat="bat -p"
alias cccu="cd ~/Universities/CCCU/"
```

Of course, `alias cat="bat -p"`, `"alias cccu="cd ~/Universities/CCCU/""`,`alias layout="~/.config/i3/layouts/layout.sh"`,`alias ls="lsd"`... will not work on your system unless you have the same packaged, file structure etc.

## Customizing your prompt

We can also customize our bash prompt by setting the `PS1` system variable. To set our prompt to be `$ `, then we can run the command

```sh
export PS1="$ "
```

To set the prompt to `$ ` for all bash sessions, add this line to the end of `.bashrc`.

Further [bash prompt customizations](https://www.howtogeek.com/307701/how-to-customize-and-colorize-your-bash-prompt) are possible. 

To have our prompt be `username@hostname[directory]: `, we would set...

```sh
export PS1="\u@\h[\W]: "
```

... where `\u` represents username, `\h` represents hostname, and `\W` represents the current directory.  

[Back to Contents Page](introduction.md)