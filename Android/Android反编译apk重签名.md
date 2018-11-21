### 工具下载

*   apktool ：[https://ibotpeaches.github.io/Apktool/install](https://ibotpeaches.github.io/Apktool/install)
*   dex2jar：[https://github.com/pxb1988/dex2jar](https://github.com/pxb1988/dex2jar)
*   jd-gui：[http://jd.benow.ca](http://jd.benow.ca/)

---

![image](http://upload-images.jianshu.io/upload_images/1965676-1c6141ffcb2bd3fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-86376082a4319f9f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>然后点击[find newest here](https://bitbucket.org/iBotPeaches/apktool/downloads/)下载apktool.jar，选择第一个下载最新版本

![image](http://upload-images.jianshu.io/upload_images/1965676-c301b04b0ceb5494.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>下载完把apktool_2.3.3.jar重命名为apktool.jar，然后把apktool.jar和apktool一起拷贝到/usr/local/bin路径下

![image](http://upload-images.jianshu.io/upload_images/1965676-b240abae734c40da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-cebbd9b2269ac1c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>这样环境就配好啦，打开终端，输入`apktool`命令，看到以下输出说明apktool配置成功

![image](http://upload-images.jianshu.io/upload_images/1965676-49334eab8b0fa083.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>新建个MyTest目录方便管理，随便放个test.apk进去作为测试包

![image](http://upload-images.jianshu.io/upload_images/1965676-7a5074dd679eb151.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

### 反编译

1.终端输入`cd /Users/zachary/zachary/MyTest`进入到测试apk所在目录，输入`apktool d test.apk`开始反编译

![image](http://upload-images.jianshu.io/upload_images/1965676-df9f1103bde8393d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.编译结束可以看到MyTest目录下多了个test文件夹，里面就是反编译以后的产物，我们想要的AndroidManifest.xml和res/.等资源文件

![image](http://upload-images.jianshu.io/upload_images/1965676-d85d96650ab0e3fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.此时资源文件反编译就完成了，下面继续反编译java代码，这是就要用到[dex2jar](https://github.com/pxb1988/dex2jar)和 [jd-gui](http://jd.benow.ca/)
下载完[dex2jar](https://github.com/pxb1988/dex2jar)和 [jd-gui](http://jd.benow.ca/)解压一下就可以了，复制到MyTest目录方便操作

![image](http://upload-images.jianshu.io/upload_images/1965676-df6b151aca00ab25.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.终端进入MyTest目录，输入命令`sh dex2jar-2.0/d2j-dex2jar.sh test.apk`（如果提示Permission Deny权限问题，先输入命令`chmod +x dex2jar-2.0/d2j-dex2jar.sh`改一下权限就好了）

![image](http://upload-images.jianshu.io/upload_images/1965676-d040eb68a08e68f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-55e0909b0b03621b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-b3b5f2ef3fd6fb0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

### 回编译

1.刚才我们执行`apktool d test.apk`反编译得到了test目录

![image](http://upload-images.jianshu.io/upload_images/1965676-1db690e004e4b306.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.回编译就是执行命令`apktool b test`

![image](http://upload-images.jianshu.io/upload_images/1965676-aa76929cb3689863.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-9f3b6a4e0ce2c57f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-6c2fb6f2ee006766.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.dist目录下存放的是重新打包后的apk文件

![image](http://upload-images.jianshu.io/upload_images/1965676-f5d70ee453c1912f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

### 重新签名

1.复制签名文件到dist目录下方便操作

![image](http://upload-images.jianshu.io/upload_images/1965676-ddb294969d3e4ac6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.终端进入dist目录，执行命令`jarsigner -verbose -keystore [your_key_store_path] -signedjar [signed_apk_name] [usigned_apk_name] [your_key_store_alias] -digestalg SHA1 -sigalg MD5withRSA`
字段说明：

*   [your_key_store_path]：密钥所在位置的绝对路径
*   [signed_apk_name]：签名后安装包名称
*   [usigned_apk_name]：未签名的安装包名称
*   [your_key_store_alias]：密钥的别名

因为我们把秘钥和test.apk放在同一路径，所以密钥所在位置的绝对路径直接填testkey就好啦，macjenkinskey是我的秘钥别名，别误会（邪恶.jpg）

![image](http://upload-images.jianshu.io/upload_images/1965676-c55451a87a5cd57a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.输一下密码，看不到输入的，开始签名

![image](http://upload-images.jianshu.io/upload_images/1965676-d0d77d73df1196ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.签完名后，在dist目录下就可以看到签完名后的apk了

![image](http://upload-images.jianshu.io/upload_images/1965676-131d12102f10c7ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.反编译的时候，也可以把test.apk的拓展名改成test.zip解压出来

![image](http://upload-images.jianshu.io/upload_images/1965676-6d0947000a8eb621.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-dc642962d19b0cca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.终端进入dex2jar-2.0路径下，执行命令`./d2j-dex2jar.sh classes.dex`

![image](http://upload-images.jianshu.io/upload_images/1965676-6ab71f8451c10fe9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-25792fd4aabb9213.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-e8b26125dc774aaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/1965676-ebb57fcd20f115b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
