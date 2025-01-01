# Dotfiles  
A repo of dotfiles for configuring a minimal Debian installation with an i3 window manager.  

## Information  
This collection of dotfiles was created to configure a reasonably useable i3 environment on a Debian minimal server with no desktop installed.  

## Apt packages to install  
### If apt doesn't appear to work  
You might have to update the apt sources list, located in `/etc/apt/sources.list`  
These sources should work reasonably well:  
```  
deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware  

deb http://security.debian.org/debian-security/ bookworm-security main contrib non-free non-free-firmware  

deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware  

deb http://deb.debian.org/debian bookworm-backports main contrib non-free non-free-firmware  

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware  
```  

### The basics  
First, switch to super user to install sudo with `su -`  
Then, `apt install sudo`  
Add the current user to the sudoers group with `usermod -aG sudo USERNAME`  
Log out and log back in again.  

Next, install the i3 window manager  
`sudo apt install xorg xinit i3`  

Install git to get the dotfiles from GitHub.  
`sudo apt install git`  
Check out this link for a write-up of how it works: [Manage dot files](https://medium.com/@simontoth/best-way-to-manage-your-dotfiles-2c45bb280049)  
But basically you need to first create a `.dotfiles` directory in your home directory:  
`cd ~`  
`mdkir .dotfiles`  
Then create an alias called "dotfiles" that invokes git on that directory.  
`alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'`  
Clone this repo.  
`git clone --bare git@github.com:tfalasco/dotfiles-debian-i3.git $HOME/.dotfiles`  
Update the dotfiles git configuration to not show untracked files, which helps clean up the git interface.  
`dotfiles config --local status.showUntrackedFiles no`  
Checkout the main branch.  
`dotfiles checkout`  

Install a browser  
`sudo apt install firefox-esr`  

Install a terminal text editor  
`sudo apt install vim`  

Install rofi for a better application launching experience  
`sudo apt install rofi`  

If you are struggling with Wi-Fi configuration, you may need to reinstall wireless-tools and install network-manager.  
`sudo apt install --reinstall wireless-tools`  
`sudo apt install network-manager`  
To configure a network-manager connection, consider using `nmtui`.  

Instead of using network-manager, you can edit `/etc/network/interfaces`, which will connect Wi-Fi automatically after boot but before login.  The contents should be:  
```
auto WFA  
iface WFA inet dhcp  
	wpa-ssid SSID  
	wpa-psk ”PSK”  
```  
`WFA` is the wifi adaptor name (which you can get from "ip a" in the terminal)  
`SSID` is the SSID of the network without quotes.  
`PSK` is the password of the network with quotes.  
Using the `etc/network/interfaces` file to configure a network interface will remove it from network-manager.  So either clear the `etc/network/interfaces` file content or rename the file if you are going to use network-manager.  

To modify touchpad functionality, you will need to run xinput.  
Check out this link for instructions on how to add configurations to the i3 config file: [Enable tap-to-click in i3](https://major.io/p/tray-icons-in-i3/)  
Note: the i3 config dotfile already contains modifications for the Elantech touchpad on an HP Pavillion laptop.  
`sudo apt install xinput`  

Install a file manager.  
`sudo apt install pcmanfm`  

Install snipping tools.  
`sudo apt install maim xclip xdotool`  
These are configured for keyboard shortcuts in the i3 config file.  
+ PrtScrn = Full screen snip, saved to file  
+ Shift + PrtScrn = Selection snip, saved to file  
+ Super + PrtScrn = Active window snip, saved to file  
+ Ctrl + PrtScrn = Full Screen snip to clipboard  
+ Ctrl + Shift + PrtScrn = Selection snip to clipboard  
+ Ctrl + Super + PrtScrn = Active window snip to clipboard  

Enable Audio.  
The i3 config file maps keyboard volume keys to volume controls.  
The i3status config file adds the current volume level to the status bar.  
`sudo apt install pavucontrol`  

Enable screen brightness control.  
The i3 config file maps keyboard brightness keys to brightness control.  
`sudo apt install brightnessctl`  

Enable printing.  
`sudo apt install cups`  
`systemctl enable --now cups`  

Add window theme support.  
`sudo apt install qt5ct lxappearance gtk-chtheme`  

### Some other niceties  
`sudo apt install build-essential`  for development tools  
`sudo apt install gdb`  for debugging  
`sudo apt install git-gui gitk`  for visual git tools  
`sudo apt install flatpak`  to install flatpaks  
`sudo apt install digikam`  for photo editing and management  
`sudo apt install shotwell`  for photo browsing  
`sudo apt install libreoffice`  for office suite  
`sudo apt install kcalc`  for calculator  
`sudo apt install vlc`  to play videos  
`sudo apt install ffmpeg`  to test your webcam  (with `ffplay /dev/video0`)  

## Non-apt packages  
These are some convenient packages to have, which are not available in the Debian apt repositories

### Visual Studio Code  
[VS Code download](https://code.visualstudio.com/download)  
`sudo apt install <name of the downloaded .deb file>`  

### Google Chrome  
[Google Chrome download](https://www.google.com/intl/en_pk/chrome/)  
`sudo apt install <name of the downloaded .deb file>`  