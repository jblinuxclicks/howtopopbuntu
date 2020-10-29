# Tweaks for Pop OS 20.10
 These are the set of tweaks I use on my pop os. I have 2 PC's one of them is 7th Gen i5 laptop with ssd and other one is a 3rd Gen 6 years old desktop. These tweaks are added on the basis of my experience over 5 months using pop on them both.
  
## 1. Installation
 While doing a install there are certain things you need to know if you want a faster boot. On my laptop I select a clean install and let the interface do its job. While on my desktop I select advanced partition, now there is a reason for that. If I select clean install it creates 2 extra partitions one is for recovery which I never use. And second one is swap now you might thing that why should i not keep swap. Let me explain over period of last 3 months I witnessed the fact that my swap is never used because on my desktop I do pretty basic stuff. While on my laptop I build kernels so swap gets used time to time. Also if you keep these 2 extra partitions every time you boot systemd mounts them which make the boot slow.
 
 So Create 2 partitions
 - 512 mb for EFI boot
 - Remaining for EXT4 system
 
#### Q. Should I use Brtfs or Ext4?
**Ans.** Depends, Now brtfs is starting to become a trend since Fedora adopted it and it now ships with Fedora 33. Also, I have started to use this on my laptop but not my desktop. Now there is a reason for that, initial benchmarks show that brtfs is slower than ext4 though brtfs has more advanced features than ext4. So In my opinion if you have a older pc go for ext4 but if you have a newer one you can go for brtfs.

- [Reference to Fedora Trend](https://www.phoronix.com/scan.php?page=news_item&px=Fedora-33-Released)
- [Reference to Benchmarks b/w File Systems](https://www.unixmen.com/review-ext4-vs-btrfs-vs-xfs/)
- [Reference for How to brtfs on Pop os](https://mutschler.eu/linux/install-guides/pop-os-btrfs/)

## 2. Post Installation
 There is some basic things you need to do after its installation.
 
 - **Update your System** <br>
 *Get latest updates via terminal or pop shop.* <br>
 For Terminal use
 ```bash
 sudo apt update && sudo apt upgrade && flatpak update
 ```
 
 - **Proprietary Drivers** <br>
 *You can get proprietary drivers directly from Pop shop but you still get problems you can refer to a guide.*
 
 [Guide for NVIDIA](https://askubuntu.com/questions/61396/how-do-i-install-the-nvidia-drivers) <br>
 [Guide for AMD](https://linuxconfig.org/how-to-install-the-latest-amd-radeon-drivers-on-ubuntu-18-04-bionic-beaver-linux#:~:text=In%20order%20to%20get%20the,the%20form%20of%20a%20tarball.)
 
 - **Gnome Tweaks**
 ```bash
 sudo apt install gnome-tweaks
 ```
 ###### Tweaks I am using -
 
##### Minimise Button
 Minimise is a important button for gnome. I always wonder why they didn't add it. While I think you can live without it if you use Super key a lot but for me minimise button is very useful. You can also get the maximize button but its not that usefull because double clicking the windows does the job.<br>
 ![gnome-minimise](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/gnome-minimise.png)<br>
##### Battery Percentage
 This option is also a pretty useful option but only for a laptop.<br>
##### Optimising Font
 I use custom resolution on my pc so fonts seem small to me so it make it better I use 1.11x font with antialiasing to subpixel.<br>
 ![custom-font-size](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/custom-font-size.png)<br>
 
 - **Add custom resolution** </br>
 If your display supports higher refresh rate go for it. Because higher refresh rates are smoother. My display is capable for 120hz.<br>
 ![set-of-refreshrates](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/set-of-refreshrates.png)
 
 ##### To add custom resolution do this steps. 
 **1. Check xrandr**  <br>
 You can know the name of your display here generally it is eDP-1 if is hybrid it can be eDP-1-1
 ![xrandr](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/xrandr.png)
 <br>
 **2. Find resolution which will fit**  <br>
 My original maximum resolution is 1600 900 which is 16:9 aspect ratio. So if I choose a different aspect ratio some part of my display will be blacked out. <br>
 
 So, I can go for 1920x1080 or 1536x864 <br>
 *To find out which fits you best you can do tests by adding different resolutions*
 <br>
 **3. How to add?**
 ##### - cvt
 ```bash
 cvt 1920 1080 #Your custom resolution
 ```
 ![cvt](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/cvt.png)
 ##### - xrandr --newmode
 Copy line after modline 
 ```bash
 xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
 ```
 ![newmode](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/newmode.png)
 ##### - xrandr --addmode
 Add the resolution with display name
 ```bash
 xrandr --addmode eDP-1 "1920x1080_60.00"
 ```
 ![addmode](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/addmode.png)
 
 #### Done???
 **Well not quite**
 
 **Problem 1**: What about other refresh rates? <br>
 **Problem 2**: The resolution goes away after reboot. <br>
 
 ##### Solution for Problem 1:
 You have to experiment with cvt a bit to find which refresh rates should be.
 As my refresh rate is from 0 - 120. I did some expermientation and added some resolution. <br>
 
 Like if your refresh rate supports 120 you can directly do this.
 ```bash
 cvt 1920 1080 120
 ```
 <custom-120>
 
 Finally I added these resolutions
 ```bash
 xrandr --newmode "1920x1080_120.00"  369.50  1920 2080 2288 2656  1080 1083 1088 1160 -hsync +vsync
 xrandr --addmode eDP-1 "1920x1080_120.00"
 xrandr --newmode "1920x1080_119.91"  369.25  1920 2080 2288 2656  1080 1083 1088 1160 -hsync +vsync
 xrandr --addmode eDP-1 "1920x1080_119.91"
 xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
 xrandr --addmode eDP-1 "1920x1080_60.00"
 xrandr --newmode "1920x1080_59.89"  172.75  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
 xrandr --addmode eDP-1 "1920x1080_59.89"
 ```
 ##### Solution for Problem 2:
 Add all the final lines to .profile so every time a session is created the lines will run and resolution will be automatically added.
 ```bash
 sudo gedit ~/.profile
 ```
 ![profile](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/profile.png)
 
 Finally it will look like
 ![custom-resolution-final](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/custom-resolution-final.png)
 
 ## 3. Preferred Apps
 Pop os ships with a basic set of apps which generally every person uses but I don't use all of them and also I use some alternatives which I like better.
 
 #### - Chrome
 I prefer Chrome & Vivaldi, as Chrome is the most popular browser also I have been using Chrome since probably 2012 and Vivaldi is the fastest browser and is optimized for older hardware.
 
 To remove Firefox
 ```bash
 sudo apt remove --purge firefox*
 ```
 1. **Chrome**
 ```bash
 sudo apt install google-chrome-stable
 ```
 2. **Vivaldi**
 ```bash
 wget -qO- https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo apt-key add -
 sudo add-apt-repository 'deb https://repo.vivaldi.com/archive/deb/ stable main' 
 sudo apt update && sudo apt install vivaldi-stable 
 ```
 
 #### - Email Client
 I don't use email client for me chrome is enough.
 ```bash
 sudo apt remove --purge geary* && sudo apt autoremove
 ```
 
 Alternatives 
 
 1. **Evolution**
 ```bash
 sudo apt install evolution
 ```
 2. **Thunderbird**
 ```bash
 sudo apt install thunderbird
 ```
 3. **MailSpring** <br>
 Go [here](https://linuxconfig.org/how-to-install-mailspring-on-ubuntu-18-04-bionic-beaver-linux)
 
 #### - VLC Media player
 Best video player for any platform
 ```bash
 sudo apt install vlc
 ```
 
 Get rid of the stock video player
 ```bash
 sudo apt remove --purge totem* && sudo apt autoremove
 ```
 
 #### - Office
 I directly use chrome extension for the office which you can see [here](https://chrome.google.com/webstore/detail/editor-for-docs-sheets-sl/eahibemoondbjaojgcdnmjlnbjmgbbml)
 
 Remove LibreOffice
 ```bash
 sudo apt remove --purge libreoffice* && sudo apt autoremove
 ```
 
 Alternative, **WPS Office** <br>
 Get the deb package [here](https://www.wps.com/)
 
 #### - Useless apps (According to Me)
 Calculator
 ```bash
 sudo apt remove --purge gnome-calculator && sudo apt autoremove
 ```
 Calendar
 ```bash
 sudo apt remove --purge gnome-calendar && sudo apt autoremove
 ```
 Character Map
 ```bash
 sudo apt remove --purge Gucharmap* && sudo apt autoremove
 ```
 Contacts
 ```bash
 sudo apt remove --purge gnome-contacts* && sudo apt autoremove
 ```
 Document Scanner
 ```bash
 sudo apt remove --purge sane* simple-scan && sudo apt autoremove
 ```
 Gnome Fonts
 ```bash
 sudo apt remove --purge gnome-font-viewer && sudo apt autoremove
 ```
 Gnome Help
 ```bash
 sudo apt remove --purge yelp* && sudo apt autoremove
 ```
 Gnome Power Manager
 ```bash
 sudo apt remove --purge gnome-power-manager && sudo apt autoremove
 ```
 Pinyin (Only for Chinese users)
 ```bash
 sudo apt remove --purge ibus-libpinyin* && sudo apt autoremove
 ```
 Vim
 ```bash
 sudo apt remove --purge gvim* vim* && sudo apt autoremove
 ```
 Popsicle USB creator
 ```bash
 sudo apt remove --purge popsicle* && sudo apt autoremove
 ```
 Note - If you need a Live USB creator you can get [Etcher](https://www.balena.io/etcher/)
 
 #### - Social Apps
 1. **Telegram** <br>
 Personally I use Kotogram client
 ```bash
 flatpak install io.github.kotatogram
 ```
 2. **Whatsapp** <br>
 Gtkwhatsapp has better features
 ```bash
 flatpak install com.gigitux.gtkwhats
 ```
  
 #### - Programming Apps
 1. **Atom by GitHub**
 ```bash
 flatpak install atom #5th one
 ```
 2. **Pycharm**
 ```bash
 flatpak install pycharm-community
 ```
 3. **GitHub-Desktop**
 ```bash
 sudo apt install github-desktop
 ```
 4. **Java** <br>
 Go through [this](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04) to get the version you need.
 
 #### - Entertainment Apps
 1. **Spotify for Music**
 ```bash
 flatpak install spotify
 ```
 2. **Steam for Gaming**
 ```bash
 flatpak install steam #6th one
 ```
 3. **Multimedia Codecs**
 ```bash
 sudo apt install ubuntu-restricted-extras
 ```
 ## 4. Important Tweaks
 #### Setting Tweaks
 ###### Privacy Tweaks
 ![1](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/1.png)
 ![2](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/2.png)
 ![3](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/3.png)
 ![4](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/4.png)
 ###### Over Amplification
 ![sound](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/sound.png)
 #### Disable annoying Keyring
 Whenever you open Chrome/Vivaldi any browser the system asks for a key which according to me is very annoying. <br>
 *There is a easy way to disable this*
 ```steps
 Open app password and keys (Seahorse) > Go to Login > Change Password > Type old passpord continue > Don't type and password continue > Make unencrypted
 ```
 ![key](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/key.png)
 ![unen](https://github.com/themagicalmammal/pop-os-tweaks/blob/master/Screenshots/unen.png) <br>

