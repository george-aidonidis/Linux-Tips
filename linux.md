# Linux tips

## Table of Contents
1. [General terminal tips](#general)
2. [Useful app](#useful)
    * [Node-js](#nodejs)
    * [zsh](#zsh)
3. [Git](#git)
4. [Gnome/Extensions](#extensions)

## General tips <div id="general"></div>

### Display disks nicely
```sh
sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```
Outputs:
```sh
NAME   FSTYPE   SIZE MOUNTPOINT LABEL
sda            74.5G            
├─sda1 ntfs     100M            Δεσμευμένο από το σύστημα
├─sda2 ntfs      52G            
├─sda3            1K            
├─sda5 ext4   238.4M /boot      
├─sda6 ext4     9.3G /          
├─sda7 swap     1.9G [SWAP]     
└─sda8 ext4    11.1G /home   
```

### How to check if something is installed:
```sh
which package
```
### How to uninstall an application or package
* List installed packages
```sh
dpkg --list
```
* Search for specific package
```sh
dpkg --list | grep package_name
```
* Uninstall package (--purge removes and config files)
```sh
sudo apt --purge remove package_name
```
* Uninstall and remove config and unused dependencies
```sh
sudo apt-get purge --auto-remove package_name
```
#### Arch
```sh
pacman -Qm
# or
yaourt -Qm
# remove
yaourt -Rsn package_name
```
### How to install a package
```sh
sudo dpkg -i package_name
```
### General apt commands 
* Remove unused packages
```sh
sudo apt-get autoremove 
```
* Clean files (remove downloaded archive files)
```sh 
sudo apt clean
```

## Useful packages <div id="useful"></div>

### nodejs on linux (nvm) <div id="nodejs"></div>
```sh
sudo apt update
sudo apt-get install build-essential libssl-dev

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash

source ~/.profile
source ~/.zshrc
nvm install xxx
```
More [here](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-debian-8)

### Zsh install on linux <div id="zsh"></div>

#### Arch
```sh
pacman -S zsh
```
#### Other distros
Prereq:
```bash
apt-get install zsh
apt-get install git-core
```
Getting zsh to work in ubuntu is weird, since `sh` does not understand the `source` command.  So, you do this to install zsh
```sh        
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
```
and then you change your shell to zsh
```sh
chsh -s `which zsh`
```
and then restart
```sh
sudo shutdown -r 0
```

This problem is explained in depth in [this issue](https://github.com/robbyrussell/oh-my-zsh/issues/227#issuecomment-825773)

## Useful packages

`Albert` a lightweight application launcher [info][https://albertlauncher.github.io/docs/installing/]

* Messenger client for linux

Download snapshot [here](https://aur.archlinux.org/packages/messengerfordesktop-bin/)
```sh
cd path/to/download/file
tar xfv messengerfordesktopblahblah
cd messengerfordesktopblahblah
makepkg -sic
cd ..
messengerfordesktopblahlbah
```
## Git <div id="git"></div>

#### Setup vim for git commit messages
```sh
syntax on
plugin indenting on
autocmd Filetype gitcommit spell textwidth=72
```
This will cause Vim to have syntax highlighting on, wrap at 72 characters and turn spell checking on.

_Line 2 will cause an error if the plugin (which??) is not installed_

## Graphics/Extensions <div id="extensions"></div>
#### Change window button position
```sh
gsettings set  org.gnome.desktop.wm.preferences button-layout 'close,maximize,minimize:'
```

#### Gnome Extensions

* [System Monitor](https://extensions.gnome.org/extension/120/system-monitor/)
* [Open Weather](https://extensions.gnome.org/extension/750/openweather)
* [Dash to dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
