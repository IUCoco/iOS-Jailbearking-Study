# iOS-Jailbearking-Study  
## iOS越狱学习  
iOS越狱就是发现iOS设备硬件或者软件的漏洞，获取更高的系统使用权限，开启root管理账号的过程。英文名字Jailbreak  
盘古越狱、太极团队、iPhone Dev Team、Chronic Dev Team,各种手机助手91手机助手、iTools、pp手机助手等。  
越狱好后自动安装Cydia软件  
> Cydia是一个类似苹果在线软件商店iTunes Store 的软件平台的客户端，它是在越狱的过程中被装入到系统中的，其中多数为iPhone、iPod Touch、iPad的第三方软件和补丁，主要都是弥补系统不足之用。Cydia是由Jay Freeman (Saurik)领导，Okori Group 以及UCSB大学合作开发。  

## 越狱后能做的事情  
查看iPhone的整个文件系统，通过工具iFunbox
- application下安装的是APP  
- Library  
- 通过Cydia安装不被AppStore接受的软件 openSSH(SecureShell)、Cycrip  
- 反编译某个APP的源代码  
- 通过Reveal查看别人的APP是怎样实现的  

### OpenSSH  
一、在WiFi的情况下

首先，我们必须保证iPhone是已经越狱的，关于越狱方法->盘古越狱。

第二，手机和pc要在同一网段内，这个大家都知道吧，通不通，ping一下就知道，ping iOSIP。点击已经连接的WiFi的右边的小箭头查看详情，记下iPhone当前网络IP地址。

第三，如果手机已经越狱了，手机上会自动安装cydia工具，打开cydia工具，在首页上会有安装openssh教程，照着cydia提供的教程一步一步做下去就可以。

最后，在pc上使用命令 `ssh root@iOSIP` 然后输入密码，越狱手机默认密码为`alpine`，此时便可以对这个越狱手机随意操作。

二、通过USB

首先，同样手机要越狱，越狱胡要安装openssh工具。

第二，通过USB访问，有没有WiFi无所谓了，但是你得在pc安装`usbmuxd`服务，没有的大家可以去http://cgit.sukimashita.com/usbmuxd.git/ 下载1.0.8版本。解压进入
  Python-client目录后，执行命令：python tcprelay.py –t 22:2222,这样就开通了一个从本机2222端口通往目标主机22号端口的通道，执行完后会出现Forwarding  local port 2222 to remote port 22

第三， 另起终端，执行命令ssh root@localhost –p 2222,然后提示输入密码，这是手机的密码，默认为alpine。

最后，此时，同样可以达到ssh访问手机的效果，而且比WiFi更快更稳定  
### Cycrip  
Cycript是由Cydia创始人Saurik推出的一款脚本语言，Cycript 混合了Objective-C与javascript语法的解释器，这意味着我们能够在一个命令中用Objective-C或者javascript，甚至两者兼用。
它能够挂钩正在运行的进程，能够在运行时修改应用的很多东西。

Cycript的安装简单，可在越狱设备上从Cydia自带源Cydia/Telesphoreo下载，直接打开设备上的Cydia然后搜索Cycript后安装即可。  
#### 基本使用
安装：可以在Cydia里搜索cycript来下载安装，可以配合MTerminal使用。

输入`cycript`，出现` cy#`提示符，说明已经成功启动Cycript。

`control+D`，来退出Cydia.

*********下面以SpringBoard为例*******
找到SpringBoard进程

获取到进程的id是 1181 ,然后用 cycript - p或cycript -p 命令注入这个进程


想要在SpringBoard界面弹出一个提示框，用cycript的话，只要两句代码就可以了，而且是实时注入的。
```  
cy# alertView = [[UIAlertView alloc] initWithTitle:@"test" message:@"Cyrill" delegate:nil cancelButtonTitle:@"OK" otherButtonTitles:nil]
#"<UIAlertView: 0x156f9f0a0; frame = (0 0; 0 0); layer = <CALayer: 0x156f96fc0>>"
cy# [alertView show]  
```  
参考链接：http://www.jianshu.com/p/56faacf24feb  

### Reveal  
Reveal可以查看其他APP的界面实现方式，必须越狱才行。在越狱的手机的Cydia中下载reveal loader，在设置里面选择将要在pc端检测的App即可配合使用  
Reveal的运行界面，其界面主要分成3部分：

左边部分是整个界面的层级关系，在这里可以以树形级层的方式来查看整个界面元素。  
中间部分是一个可视化的查看区域，用户可以在这里切换2D或3D的查看方式，这里看到的也是程序运行的实时界面。  
右边部边是控件的详细参数查看区域，当我们选中某一个具体的控件时，右边就可以显示出该控件的具体的参数列表。我们除了可以查看这些参数值是否正确外，还可以尝试修改这些值。所有的修改都可以实时反应到中间的实时预览区域。  
### hopper反编译  
暂时没找到合适破解版，闪退
