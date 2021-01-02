# MacOS



## Homebrew

Homebrew is the essential tools used for software management of MacOS


### Homebrew-services: 

Integrated with macOS's `launchclt` manager to install services provided by softwares provided by homebrew.

```shell
brew services list
brew services start nginx  #star service at login
brew services run nginx    #run but don't start it at login
brew services stop nginx
brew services restart nginx
```



### Fonts

Install the best terminal fonts: Inconsolata

```shell
brew tap homebrew/cask-fonts
brew cask install font-inconsolata
```

The `Menlo` can be a good alternative!





### Services

```shell
launchctl load ~/Library/LaunchAgents/com.demo.daemon.plist
launchctl unload ~/Library/LaunchAgents/com.demo.daemon.plist
```

Example plist file

```text
<key>StartCalendarInterval</key>
<dict>
  <key>Hour</key>
  <integer>3</integer>
  <key>Minute</key>
  <integer>15</integer>
  <key>Weekday</key>
  <integer>6</integer>
</dict>
```



### Web Server

```shell
#macos Forward Port 80 and 443 with Mac pfctl Port Forwarding
echo "rdr pass inet proto tcp from any to any port 80 -> 127.0.0.1 port 8080 rdr pass inet proto tcp from any to any port 443 -> 127.0.0.1 port 8443" | sudo pfctl -ef -
# remove:
sudo pfctl -F all -f /etc/pf.conf
show the status
sudo pfctl -s nat
```



### Making bootable USB

```shell
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ macOS\ High\ Sierra.app
```



### Shadowsocks-libev

```shell
ss-local -s ****** -p *** -l 1080 -k **** -m chacha20
```





## Software Recommendation

1. "Timerapp": timer

2. Mathpix: recognize the math formula from screenshoot

3. Dozer: hider the task bar 

## Common Problems

1. The clipboard did not work properly:

   Open "Active Monitor" find process `pboard`, force stop it and it will restart automatically. 

2. Reset NVRAM :" `option` + `command` + P + R", hold for 20s when reboot

3. Reset SMC: `shift` + `control` + `option`, hold for 10s when reboot

 



## Python

Conda: IPython Warning: Python is not installed as a framework. 

Solution:

1. Install python.app from conda
2. Modify the shebang of ipython in your virtual env to point to the pythonw  



##Disk Utilities

Remove linux partition:

```shell
diskutil list
diskutil eraseVolume free none diskXsY
```



## Applescript

```applescript
tell application "System Events"
	get properties of every menu bar item of every menu bar of process "SystemUIServer"
end tell
```



## Dark menu bar

```shell
# turn on
defaults write -g NSRequiresAquaSystemAppearance -bool Yes
# fix the notification center
defaults write com.apple.notificationcenterui NSRequiresAquaSystemAppearance -bool Yes
defaults write com.apple.Spotlight NSRequiresAquaSystemAppearance -bool Yes


# disable
defaults write -g NSRequiresAquaSystemAppearance -bool No
defaults write com.apple.notificationcenterui NSRequiresAquaSystemAppearance -bool No
defaults write com.apple.Spotlight NSRequiresAquaSystemAppearance -bool No
# desired app
defaults write com.apple.finder NSRequiresAquaSystemAppearance -bool No
defaults write com.apple.Safari NSRequiresAquaSystemAppearance -bool No
defaults write com.apple.iChat NSRequiresAquaSystemAppearance -bool No
cjhang>~% defaults write com.apple.iWork.Keynote NSRequiresAquaSystemAppearance -bool Yes
cjhang>~% defaults write com.apple.iWork.Pages NSRequiresAquaSystemAppearance -bool Yes
cjhang>~% defaults write com.apple.iWork.Numbers NSRequiresAquaSystemAppearance -bool Yes
cjhang>~% defaults write com.apple.Notes NSRequiresAquaSystemAppearance -bool Yes



# for individual app

ls /Users/yourname/Library/Preferences
defaults write *SOME PLIST* NSRequiresAquaSystemAppearance -bool Yes/No
```



## screenshot

```shell
defaults write com.apple.screencapture location ~/Pictures/Screenshots
```



remove system update red dot

```shell
defaults delete com.apple.preferences.softwareupdate LatestMajorOSSeenByUserBundleIdentifier && softwareupdate --list
```

