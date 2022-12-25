# Reference

## Keypoints


----
| Topic | Summary |
|    ---   |     ---     |
| 0. [Installation](../Shell/installation.md)  | |
| 1. [Manual Pages](./manfiles.md) |- `man command` displays the manual page for a given command. <br><br> - `[OPTION]...` means the given command can be followed by one or more optional flags.<br><br> - Flags specified after ellipsis are still optional but must come after all other flags.<br><br>- While inside the manual page,use `/` followed by your pattern to do interactive searching. |
| 2. [Working Remotely](./workremote.md) |- SSH is a secure alternative to username/password authorization <br><br> - SSH keys are generated in public/private pairs. Your public key can be shared with others. The private keys stays on your machine only. <br><br> - The `ssh` and `scp` utilities are secure alternatives to logging into, and copying files to/from remote machine |
| 3. [Permissions](./permissions.md)| - Correct permissions are critical for the security of a system. <br><br> - File permissions describe who and what can read, write, modify, and access a file. <br><br> - Use `ls -l` to view the permissions for a specific file. <br><br> - Use `chmod` to change permissions on a file or directory. |
| 4. [Directory structure](./dirstruct.md) |	Understanding the concept of Unix directory structure |
| 5. [Job control](./jobs.md) | - When we talk of ‘job control’, we really mean ‘process control’ <br><br> - A running process can be stopped, paused, and/or made to run in the background <br><br> - A process can be started so as to immediately run in the background <br><br> - Paused or backgrounded processes can be brought back into the foreground <br><br> - Process information can be inspected with `ps`|
| 6. [Aliases and bash customization](./aliases.md)	| - Aliases are used to create shortcuts or abbreviations <br><br> - The `.bashrc` and `.bash_profile` files allow us to customize our bash environment. <br><br> - The `PS1` system variable can be changed to customize your bash prompt. |
| 7. [Shell Variables](./shellvars.md) | - Shell variables are by default treated as strings <br><br> - The `PATH` variable defines the shell’s search path <br><br> - Variables are assigned using `“=”` and recalled using the variable’s name prefixed by `“$”`|
| 8. [The Unix Shell](./unixshell.md)	||
| 9. [AWK](./awk.md)	||

## Glossary 

#### remote login
: FIXME

#### remote login server
: FIXME

#### SSH daemon
: FIXME

#### secure shell
: FIXME

#### SSH key
: FIXME

#### SSH protocol
: FIXME

#### command
: FIXME

#### user name
: FIXME

#### user ID
: FIXME

#### user group
: FIXME

#### user group name
: FIXME

#### user group ID
: FIXME

#### access control lists
: FIXME

#### search path
: FIXME

[Back to Contents Page](introduction.md)