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
`sudo apt install build-essential`  
`sudo apt install gdb`  
`sudo apt install git-gui gitk`  
`sudo apt install flatpak`  
`sudo apt install digikam`  
`sudo apt install libreoffice`  
`sudo apt install kcalc`  
`sudo apt install vlc`  

## Non-apt packages  
These are some convenient packages to have, which are not available in the Debian apt repositories

### Visual Studio Code  
[VS Code download](https://code.visualstudio.com/download)  
`sudo apt install <name of the downloaded .deb file>`  

### Google Chrome  
[Google Chrome download](https://www.google.com/intl/en_pk/chrome/)  
`sudo apt install <name of the downloaded .deb file>`  