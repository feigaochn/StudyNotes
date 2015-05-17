# Mac OS X system settings


* Show hidden files

```sh
defaults write com apple Finder AppleShowAllFiles YES
```

* 开启Mac App Store 更多功能 Debug 菜单

```sh
defaults write com.apple.appstore ShowDebugMenu -bool true
```

* Mac OS X系统下，几乎绝大部分文件夹中都包含 .DS_Store 隐藏文件，这里保存着针对这个目录的特殊信息和设置配置，例如查看方式，图标大小以及这个目录的一些附属元数据。如果需要禁止系统创建，那么可以在终端中运行如下代码并回车

```sh
// sudo find / -name ".DS_Store" -depth -exec rm {} \;
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```

* Turn off Dashboard

```sh
defaults write com.apple.dashboard mcx-disabled -boolean true
killall Dock
```

* To allow text selection in the Quick Look window:

```sh
defaults write com.apple.finder QLEnableTextSelection -bool true
killall Finder
```

* default icons

```sh
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources
```

* Turn on retina resolution support for non retina Mac

```sh
sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true
```

* Since OS X 10.9 mavericks, the behavior of the power button has changed. Now, when you quickly press this button, it will OS X be placed in standby mode. With the following command you can use the power button function rollback to previous versions of OS X.

```sh
defaults write com.apple.loginwindow PowerButtonSleepsSystem -bool no
```

* Disable "Stay on front" for OSX help windows

```sh
defaults write com.apple.helpviewer DevMode -bool true
```

* Change Dashboard background (10.9)

```sh
/System/Library/CoreServices/Dock.app/Contents/Resources/dbgrid{,@2x}.png
```

* Clear duplicate items in "Open With ..."

```sh
/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain user
```

* Change default directory for screen capture

```sh
defaults write com.apple.screencapture location /path/to/screencaptures
killall SystemUIServer
```

* update `locate` database

```sh
sudo /usr/libexec/locate.updatedb
```

* Reset the Mac Dock to Default State and Default Icons in OS X

```sh
defaults delete com.apple.dock; killall Dock
```

* reset launchpad icons

```sh
rm Library/Application\ Support/Dock/*.db; killall Dock
```

