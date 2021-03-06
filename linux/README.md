
# Commands/Tools
## command line editing
* frequent usage
  * M-: The Meta key is labeled ALT on many keyboards.
  * M-d: delete to the end of current word. 
* https://www.gnu.org/software/bash/manual/html_node/Readline-Killing-Commands.html#Readline-Killing-Commands
* https://www.gnu.org/software/bash/manual/html_node/Introduction-and-Notation.html#Introduction-and-Notation

## Long Running Process
```
nohup node server.js &
```

## Screen
```
$ screen -ls  # list existing screens
$ Ctrl-a d  # detach the screen
$ screen -r <>  # attach to a screen, if there is only one screen, no need to specify the name
```

## Mount Drive from Windows with Readonly Access
```
sudo mkdir /media/xxxx/Acer
sudo mount -t "ntfs" -ro "uhelper=udisks2,nodev,nosuid,uid=1000,gid=1000" "/dev/sda3" "/media/xxxx/Acer"
```

## Add Group
* http://man7.org/linux/man-pages/man5/login.defs.5.html
```
# /etc/login.defs
UID_MIN                  1000
UID_MAX                 60000
# System accounts
SYS_UID_MIN               201
SYS_UID_MAX               999
```
* system group vs normal group
  * https://askubuntu.com/questions/523949/what-is-a-system-group-as-opposed-to-a-normal-group
  * When you create a system user, by the fault the command doesn't create a home folder and its terminal is set to /bin/false, whereas for normal users these defaults doesn't apply.
## Add User
Ubuntu 16.04
```
sudo useradd -m xxx
sudo passwd xxx
# add user xx to "sudo" group, so that it can execute any command. 
# /etc/sudoers is pre-configured to grant permissions to all members of this group (i.e. "sudo" group)
# https://askubuntu.com/questions/7477/how-can-i-add-a-new-user-as-sudoer-using-the-command-line
# ??? take effect next loging ???
sudo adduser xxx sudo

# Change the default shell, e.g. /bin/bash, check the value by $SHELL
sudo chsh <user name> 
Enter the new value, or press ENTER for the default
        Login Shell []: /bin/bash
        
# sudo vim /etc/sudoers, add the following line at the end of it.
# execute command without password: https://askubuntu.com/questions/147241/execute-sudo-without-password
username ALL=(ALL) NOPASSWD: ALL
```
CentOS: useradd and adduser are the same
```
sudo useradd -m xxx
sudo passwd xxx
usermod -aG wheel username  # no sudo group here

visudo and uncomment these two lines (or vi /etc/sudoers
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL

## Same thing without a password
%wheel  ALL=(ALL)       NOPASSWD: ALL
```
Notes:
* Can also use /etc/suoders.d/ to add sudo permissions without changing /etc/sudoers
* https://linux.die.net/man/8/useradd
  * will it create a directory for -m -d

## Change Hostname
```
sudo hostname <new name> # take effect immediately
vi /etc/hostname
vi /etc/hosts # for future, and also sudo xxx will have warning about not recognizing the hostname.
127.0.0.1       localhost
127.0.1.1       <host name>

```

## Limit SSH Access
```
# sudo vim /etc/ssh/sshd_config
AllowUsers root xxxx

# sudo systemctl restart ssh
```

## SSH Connection Reset
* When ssh client see this error
```
$ ssh username@xx.xx.xx.xx
ssh_exchange_identification: read: Connection reset by peer
```
* Check server sshd log
Run
```
# on CentOS
systemctl status sshd or vi /var/log/secure

# See this error

refused connect from xx.xx.xx.xx (xx.xx.xx.xx)
```
* vi /etc/hosts.deny, /etc/hosts.allow
```
clean up /etc/hosts.deny
```
* a better way
```
sudo su
systemctl stop denyhosts
sed -i '/192.168/d' /var/lib/denyhosts/* /etc/hosts.deny
systemctl start denyhosts
exit
```

## SSH Keep Alive
https://stackoverflow.com/questions/25084288/keep-ssh-session-alive
```
# .ssh/config, chmod 600 .ssh/config
Host *
ServerAliveInterval 240
```
```
# CentOS, RedHat, Fedora
export TMOUT=0
```

## Who login/history
```
last [-10]
```

# Ubuntu

## gdebi - install packages with dependencies
https://askubuntu.com/questions/784656/could-not-find-package-gdebi
```
sudo apt-get install gdebi-core
```
