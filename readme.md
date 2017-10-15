# Linux tips (mostly arch)

This a small guide that I use to setup my linux enviroment. It covers some basic comands along with a few packages.

## Table of Contents
1. [General terminal tips](#general-tips)
    * [Display disks nicely](#display-disks-nicely)
    * [Folder info](#folder-info)
    * [How to check if a package is installed](#how-to-check-if-a-package-is-installed)
    * [How to uninstall an application or package](#how-to-uninstall-an-application-or-package)
    * [How to install a package](#how-to-install-a-package)
    * [General apt commands](#general-apt-commands)
    * [Copy and paste from terminal](#copy-and-paste-from-terminal)
2. [Arch](#arch)
    * [How to keep arch up to date](#how-to-keep-arch-up-to-date)
    * [Delete old packages from pacman cache](#delete-old-packages-from-pacman-cache)
    * [Aur update](#aur-update)
    * [Languages](#languages)
    * [Steam](#steam)
3. [Useful apps](#useful-packages)
    * [Node-js](#nodejs-on-linux)
    * [zsh](#zsh-install-on-linux)
3. [Git](#git)
    * [Setup vim for git commit messages](#setup-vim-for-git-commit-messages)
    * [Use vim as a globar git editor](#use-vim-as-a-globar-git-editor)
4. [Graphics or Extensions](#graphics-or-extensions)
    * [Change window button position](#change-window-button-position)
    * [Terminal themes](#terminal-themes)
    * [Gnome Extensions](#gnome-extensions)
5. [Problems](#problems)
    * [Touchpad settings](#touchpad-settings)
    * [Yaourt building problems](#yaourt-building-problems)
    * [GDM or LIGHTDM login does not appear on primary monitor](#gdm-or-lightdm-login-does-not-appear-on-primary-monitor)
    * [GDM bluetooth speakers](#gdm-bluetooth-speakers)
    * [GDM fingerprint reader](#gdm-fingerprint-reader)
    * [Docker](#docker)
    * [GruvBox](#gruvbox-on-gnome)
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
### Folder info
* Display size of given folder
```bash
du -sh /path/to/folder
```
* Produce a list of all the folders in /path/to/folder and their sizes
```bash
du -h --max-depth=1 /path/to/folder
```
* Organize the list from smallest to largest
```bash
du -h --max-depth=1 /path/to/folder | sort -nk1
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

### Copy and Paste from terminal
* You can always copy/paste things from/to terminal by using `ctrl + shift + c` and `ctrl + shift + v`.
* In case you need to copy things directly to clipboard (like `pbcopy` on Mac Os) you can use the `xclip` package.

```sh
# Ubuntu
sudo apt install xclip
# Or for Arch
sudo pacman -S xclip

# You can then pipe the output into xclip to be copied into the clipboard:
cat file | xclip

# If you want to paste somewhere else other than a X application, try this one:
cat file | xclip -selection clipboard
```

* To simplify life, you can set up an alias in your `.bashrc` or `.zshrc` file:

```sh
alias "xc=xclip"
alias "xcc=xclip -selection clipboard"
alias "xv=xclip -o"
```
Terminal 1:

    pwd | c

Terminal 2:

    cd `v`

_Notice the ` ` around v. This executes v as a command first and then substitutes it in-place for cd to use._
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

This is to update the database, just like in Debian or Ubuntu:
```sh
sudo aptitude update # Ubuntu's similar command
```

### Delete old packages from pacman cache
* Pacman ships with a useful tool `paccache` for this. By default, paccache will remove all but the last three versions of an installed package.
* You can change this number with the `-k`, `--keep` switch.

* There is also a -d, --dryrun switch to preview your changes:
```bash
paccache -d
```

* Perform the delete of packages:
```bash
paccache -r
```
* See paccache [docs](https://wiki.archlinux.org/index.php/pacman#Cleaning_the_package_cache) for more.
### Aur update
- Upgrade aur packages.

```sh
yaourt -Syu --aur
```

### Languages

In order to change the system language or just a add new language, on arch, you might need to edit the `/etc/locale.conf` and then you have to find the language that you need and uncomment it.

```sh
sudo vi /etc/locale.gen
sudo locale-gen
```

### Steam

Steam is not officially supported on arch. Keep in mind that you need to install some 32-bit packages (even if you have 64-bit system, took me some time to figure this out).


* Enable the [multilib](https://wiki.archlinux.org/index.php/Multilib) repository

Navigate to `pacman`'s conf file:
```sh
sudo vi /etc/pacman.conf
```
and uncomment the following lines:
```sh
# [multilib]
# Include = /etc/pacman.d/mirrorlist
```

* Install Steam:

```sh
sudo pacman -S steam
```
and Steam should now be installed on your arch system.

* Helpful links:
Please check the following links for more details on how to install drivers for your graphics card.

[Installing Steam on Antergos](https://antergos.com/wiki/hardware/installing-steam/)

[Official arch wiki for steam](https://wiki.archlinux.org/index.php/steam)
## Useful packages

### nodejs on linux

The best way to have node js on your system is with [nvm](https://github.com/creationix/nvm)

_Please check latest version by visiting [nvm](https://github.com/creationix/nvm)_
```sh
sudo pacman -Syu
sudo pacman -S build-essential libssl-dev

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

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

#### Use vim as a global git editor

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
* [Better volume indicator](https://extensions.gnome.org/extension/759/better-volume-indicator/)

#### Other useful programs/addons

* [cmus Music Player](https://cmus.github.io/)
## Problems
#### Touchpad settings

You might encounter a problem with mousepad/trackpad settings on gnome (missing settings on GUI mouse settings). In order to fix you have to remove the synaptics driver (i.e. `xf86-input-synaptics`). It might also be a good idea to remove any configuration files related to this (like the in `/etc/X11/xorg.conf.d/50-synaptics.conf`).

#### Yaourt building problems

When building large packages (like an IDE) you might get an error message that say `The device is out of space`. Chances are that yaourt is building things on tmp folder on swap/ram. You can specify another directory for building these packages (although it's going to be a bit slower) like this:

Open `/etc/yaourtc` (open with an editor) and find the following line:

```sh
#TMPDIR="/tmp"
```

Change it to:

```sh
TMPDIR="/home/$USER/tmp"
```

#### GDM or LIGHTDM login does not appear on primary monitor

When using two monitors or more you might don't get the login screen on your primary monitor. So, in order to fix this you can:

1) Set primary monitor from `Settings` --> `Displays`
2) Copy your monitor settings on your login manager folder

* For LIGHTDM
```sh
sudo cp ~/.config/monitors.xml /var/lib/lightdm/.config/
```

* For GDM
```sh
sudo cp ~/.config/monitors.xml /var/lib/gdm/.config/
```

#### GDM bluetooth speakers

When using gdm you might encounter the problem of connecting to bluetooth speakers but the device will not appear on output settings. As [docs](https://wiki.archlinux.org/index.php/Bluetooth_headset) specifies:

> When using GDM, another instance of PulseAudio is started, which "captures" your bluetooth device connection. This can be prevented by masking the pulseaudio socket for the GDM user by doing the following:

```sh
mkdir -p ~gdm/.config/systemd/user
ln -s /dev/null ~gdm/.config/systemd/user/pulseaudio.socket
```

#### GDM fingerprint reader
If your laptop supports a fingerprint reader you can use it with [fprint](https://wiki.archlinux.org/index.php/Fprint). There is also an aur package [Fingerprint-gui](https://wiki.archlinux.org/index.php/Fingerprint-gui) but I could not make it to work properly.

#### Docker

If you get an error that it's not running you might need to add yourself to docker group:

```sh
sudo gpasswd -a $USER dockerd
```

#### GruvBox on Gnome

You can use the themes that are available [here](https://github.com/Mayccoll/Gogh).
Remember to have enabled the setting `Run command as login shell` enabled (gnome terminal settings --> Profile preferences --> Command tab --> Check `Run command as login shell`).

Install GruvBox by running and selecting the GruvBox theme number:
```sh
wget -O gogh https://git.io/vQgMr && chmod +x gogh && ./gogh && rm gogh
```
