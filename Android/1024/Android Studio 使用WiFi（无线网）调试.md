### Android Studio 使用WiFi（无线网）调试
```
Android Studio使用WiFi（无线网）调试程序，可为Android studio安装插件的方法使用，不过Android studio的WiFi调试插件，只支持到Android studio的2.1版本

使用步骤：

首先安装adb WiFi 插件：

file——>setting——>plugins——>搜索框：输入 ADB WIFI——>安装——>重启android Studio

然后第一次启动时，先将用数据线联入电脑，然后：Tools——>Android——>ADB WiFi——>ADB restart ——>ADB usb to Wifi  提示连接到手机的IP地址后拔掉数据线，可以下次使用WiFi调试了
```