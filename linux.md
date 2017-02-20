# Linux tips

### Display disks nicely
```sh
sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```

### How to check if something is installed:
```sh
which package
```

### Change window button position
```sh
gsettings set  org.gnome.desktop.wm.preferences button-layout 'close,maximize,minimize:'
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

### nodejs on linux (nvm)
```sh
sudo apt update
sudo apt-get install build-essential libssl-dev

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash

source ~/.profile
source ~/.zshrc
nvm install xxx
```

More [here][https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-debian-8]

### Zsh install on linux

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

