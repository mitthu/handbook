# Linux
## Wireless and Bluetooth
```bash
# Intel wifi
sudo rmmod iwlmvm
sudo rmmod iwlwifi
sudo modprobe iwlwifi power_save=disable power_level=5
sudo modprobe btusb reset=1
sudo rfkill unblock all

rmmod iwlmvm; rmmod iwlwifi
modprobe iwlwifi power_save=0 power_level=5
modinfo iwlwifi

## List wifi status
rfkill list wifi

rfkill unblock all
```

### Exculde files => rsync
```
.cache
.caches
Caches
.AppleDB
.TemporaryItems
.Trashes
.Spotlight-V100
.fseventsd
._*
.DS_Store
Thumbs.db
.apdisk
```

## Install Apps
* apt-cacher
* nfs-common
* git
* phpmyadmin
* python-moinmoin
* valgrind

## Awesome setup
```bash
# Use this setup because the official ubuntu package does not have the core gears module.
# Ref: https://launchpad.net/~klaus-vormweg/+archive/ubuntu/awesome
sudo add-apt-repository ppa:klaus-vormweg/awesome
sudo apt-get update
sudo apt-get install -y awesome

# Install dependencies
sudo apt-get install -y xscreensaver xtrlock xscreensaver xbacklight
```
