# Linux tips (mostly arch)

## Table of Contents
1. [General terminal tips](#general-tips)
    * [Display disks nicely](#display-disks-nicely)
    * [How to check if a package is installed](#how-to-check-if-a-package-is-installed)
    * [How to uninstall an application or package](#how-to-uninstall-an-application-or-package)
    * [How to install a package](#how-to-install-a-package)
    * [General apt commands](#general-apt-commands)
2. [Arch](#arch)
    * [How to keep arch up to date](#how-to-keep-arch-up-to-date)
    * [Aur update](#aur-update)
    * [Languages](#languages)
3. [Useful app](#useful-packages)
    * [Node-js](#nodejs-on-linux)
    * [zsh](#zsh-install-on-linux)
3. [Git](#git)
    * [Setup vim for git commit messages](#setup-vim-for-git-commit-messages)
4. [Graphics or Extensions](#graphics-or-extensions)
    * [Change window button position](#change-window-button-position)
    * [Gnome Extensions](#gnome-extensions)
    * [Terminal themes](#terminal-themes)

## General tips

### Display disks nicely
```sh
sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```
Outputs:
```sh
NAME   FSTYPE     SIZE MOUNTPOINT LABEL
sda             465.8G            
├─sda1 ext4       255M /boot      Boot
├─sda2 ext4     461.7G /          Root
├─sda3              1K
├─sda3 swap       3.9G [SWAP]     Swap
```

### How to check if a package is installed:
```sh
which package_name
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
* Uninstall package with apt (--purge removes and config files)
```sh
sudo apt --purge remove package_name
```
* Uninstall and remove config and unused dependencies with apt
```sh
sudo apt-get purge --auto-remove package_name
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

## Arch
* List installed packages
```sh
pacman -Qm
# or for the aur repos
yaourt -Qm
```
* Remove a package
```sh
# remove
yaourt -Rsn package_name
```
### How to keep arch up to date
```sh
sudo pacman -Syu
```
`S`: Synchronize packages
`y`: Refresh
`u`: Restrict/filter output to packages that are out-of-date on the local system.

This is to update the database, just like
in Debian or Ubuntu.
```sh
sudo aptitude update
```

### Aur update
- Upgrade aur packages.

```sh
yaourt -Syu --aur
```

### Languages

In order to change the system language on arch you might need to edit the `/etc/locale.conf` and then you have to find the language that you need and uncomment it.

```sh
sudo vi /etc/locale.gen 
sudo locale-gen 
```

## Useful packages

### nodejs on linux

The best way to have node js on your system is with [nvm](https://github.com/creationix/nvm)

```sh
sudo pacman -Syu
sudo pacman -S build-essential libssl-dev

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash

# load profiles again
source ~/.profile
source ~/.zshrc
nvm install xxx
```

### Zsh install on linux

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

#### `Albert`
* A lightweight application launcher [info](https://albertlauncher.github.io/docs/installing/)

#### Messenger client for linux

* Download snapshot [here](https://aur.archlinux.org/packages/messengerfordesktop-bin/)
```sh
cd path/to/download/file
tar xfv messengerfordesktop-bin
cd messengerfordesktop-bin
makepkg -sic
cd ..
messengerfordesktop-bin
```
### Git

#### Setup vim for git commit messages
```sh
syntax on
plugin indenting on
autocmd Filetype gitcommit spell textwidth=72
```
This will cause Vim to have syntax highlighting on, wrap at 72 characters and turn spell checking on.

Use vim as a globar git editor

```sh
git config --global core.editor "vim"
```

## Graphics or Extensions
#### Change window button position
```sh
gsettings set  org.gnome.desktop.wm.preferences button-layout 'close,maximize,minimize:'
```

Install arc theme:

```sh
yaourt -S gtk-theme-arc-git
```

[Arc-Theme](https://aur.archlinux.org/packages/gtk-theme-arc-git)

#### Terminal themes
[Terminal themes](https://github.com/Mayccoll/Gogh)

#### Gnome Extensions

* [System Monitor](https://extensions.gnome.org/extension/120/system-monitor/)
* [Open Weather](https://extensions.gnome.org/extension/750/openweather)
* [Dash to dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
* [Clipboard indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)