已剪辑自: https://www.cnblogs.com/garyw/p/13468491.html

本篇讲类unix系统下的用以模拟运行Windows程序的wine。会从普通使用者的比较实用的角度去讲。有专为国内用户准备的内容。

本篇面向有Linux经验但对wine不熟悉的人。

wine可靠吗？该不该用？

wine是不可靠的，自用可以，生产环境和严格环境中千万别用。

一般越旧的Windows程序wine越容易模拟运行成功（或部分功能成功）。请先在官方wine Application Database上查你想运行的程序的别人的模拟结果（官方搜索不好用，可以用Google加 site:appdb.winehq.org），看Test Results：
	• Rating一列由运行结果好到坏为Platinum、Gold、Silver、Bronze、Garbage
	• 看他们当时所用的wine版本和程序版本。有些是用很旧的wine测试的结果不好，新版本wine或许已不一样
	• 结果好的，你打算做，那么点击此条结果，看提交者所描述的正常功能、不可用功能、未测试功能，及他所留的建立过程和操作方法
	• 无近期结果或近期仍然Silver以下的就放弃吧。也可以自己尝试，但这对普通人来说，顺利则已，不顺利则是一大大大坑

## 基础知识和操作
WINEARCH环境变量

这个WINEARCH 决定了你模拟的Windows是32位或是64位的x86。对应的值为win32及win64，如果你的Unix系统是64位的它就默认是win64。

发行版所提供的wine一般都有32位及64位两个包，直接对应所模拟的Windows位数，包里面的Unix二进制及运行库也都是对应位数。

以我的经验来看，使用32位更容易成功。

WINEPREFIX环境变量

WINEPREFIX是很重要的，默认值为~/.wine。

wine会在它所指定的路径下创建drive_c/等几个文件（夹），其中包含了Windows环境配置、它的C盘文件等等。

建议把你安装的不同的Windows程序分给不同的WINEPREFIX，便于打包和隔离。当你要启动这个Windows程序前也记得要设置WINEPREFIX。

在你用一个空WINEPREFIX目录第一次启动wine时，它会问你是否下载mono和gecko。一般情况选否即可。

启动Windows程序及路径处理

命令wine 路径/xxx.exe 参数（可以是文件路径）就可以通过wine运行exe。路径可以是Unix路径，也可以是（在有WINEPREFIX情况下的）Windows路径，wine会自动判断。
以WINEPREFIX是默认值情况下为例：
wine notepad.exe c:/abc.txt
wine notepad.exe ~/.wine/drive_c/abc.txt
 
上面两条命令效果一样。
对wine来说，你Unix系统里的其他文件（即模拟的C盘之外的文件）的Windows路径都以Z盘开头：
wine notepad.exe z:/home/username/.wine/drive_c/abc.txt
 
wine也提供了winepath这个命令来转换Unix和Windows之前的路径，但一般用不上。
安装Windows程序及之后
要安装一个Windows程序，一般就是在设置好WINEPREFIX和WINEARCH后，运行安装包
wine 安装包.exe
wine msiexec /i 安装包.msi
 
安装好后，安装程序所生成的Windows开始菜单项会被自动加入你的Linux系统的启动器中。.desktop文件里已经有了WINEPREFIX和WINEARCH。安装程序所产生的文件扩展名关联、图标等等“垃圾”也会进入Linux中。
如果你不喜欢垃圾，可以清理，参考官方FAQ
 甚至你可以在安装前就禁止它在Unix中产生任何菜单、文件关联等物件（参考这里）：
 export WINEDLLOVERRIDES=winemenubuilder.exe=d wine setup.exe
我自己是总把垃圾清理掉的。如果你也清理了，没有了安装程序创建的菜单和文件关联，可以按如下方法自己弄：
写一个自己的脚本：
#!/bin/bash

# 取得此bash脚本所在路径
script=$(readlink -f "$0")
scriptpath=$(dirname "$script")

# 这里设置好WINEPREFIX
export WINEPREFIX="$scriptpath"

wine "c:\Program Files\xxxx\xxxx.exe" "$1"
 
把这个脚本放在WINEPREFIX目录下使用。
自己确定好此WINEPREFIX目录放在何处后，可以手动将文件后缀与这个脚本关联，具体可以参考我写的另一篇《Linux关联文件扩展名和打开程序》。
winecfg
winecfg命令会打开一个GUI的、应对此WINEPREFIX的wine环境配置。
里面可以设置要模拟的Windows版本。
还可以设置某个DLL文件使用内建、原装、内建先于原装、原装先于内建、停用之中的哪种。默认情况下都是使用内建的。如果想使用原装，则必须把真正的Windows DLL放入WINERPEFIX的系统目录中，其中大部分是用winetricks来搞。
这个对于一个程序是否能成功模拟比较关键，但需要一些技术知识，本篇不细谈。官方wine Application Database中，提交者一般会给出他们所使用的设置。
winetricks
有官方背景的一个工具。其主页位于Github。发行版也会带它，但不一定最新，最好用最新的。它能帮用户方便配置wine环境，或安装一些基本DLL，运行库如VC runtime、.NET。
例如winetricks dotnet45 vcrun2010 。也支持一些大型应用如office2007pro（需要自己准备光盘或iso）、7zip、qq、qqintl（这些安装时它自己从网上下载）。可以用winetricks list-all来看看它支持什么。
因为是老外维护的，所以winetricks有许多东西要把语言设置成英文才可以安装成功。
经我试验，winetricks中许多也只能在32位或64位一种情况下，或某个wine版本之上或之下才能成功，而winetricks却不记录或提供这些信息，很奇怪。
稍微进阶一点的wine使用
语言设置为英文
有时尝试了多次都失败，而export LANG=en_US.utf8后就成功了。其中有些Windows程序安装时需要把语言设置成英文，运行时又可以用中文运行。神奇吧 !-_-!
wine卡死了或程序退出不彻底
如果在wine中运行notepad，会有以下进程在Unix中：

```
23770 23765 notepad.exe     notepad.exe
23774 23765 wineserver      /usr/bin/wineserver
23780 23765 services.exe    C:\windows\system32\services.exe
23783 23765 winedevice.exe  C:\windows\system32\winedevice.exe
23793 23765 plugplay.exe    C:\windows\system32\plugplay.exe
23798 23765 winedevice.exe  C:\windows\system32\winedevice.exe
23805 23765 explorer.exe    C:\windows\system32\explorer.exe /desktop
```

那些看似名为.exe结尾的进程实际上在Unix中是wine-preloader。每一个运行中的WINEPREFIX会有一套以上进程。
正常情况下，如上例，notepad.exe退出后其余也会自动退出。但wine无法正常自行彻底退出是常有的。例如若用wine运行QQ，常常出现QQ.exe退出但TXPlatform.exe死活不自己退出的情况，甚至可能你点击了QQ界面上的叉，只是界面消失，实际的exe进程都卡住不退。卡住不退的情况也属于所模拟的程序功能仅部分正常。
使用wineserver -k来告诉wine杀死本WINEPREFIX的所有进程。但这招有时也不灵，那么需要手动清理，比较麻烦。
因此，有了这一个脚本——wineprc，只需要一条命令，快速列出或杀死卡住的wine，可以指定一个WINEPREFIX或全部wine进程。
一些国内常用Windows软件的现成资源
	1. winetricks_zh（ https://github.com/hillwoodroc/winetricks-zh ）是一个国人维护的winetricks。想装国内软件时可以先来这里看看，比官方winetricks更符合国内情况。支持QQ、微信、同花顺、大智慧等等。
	2. 深度（Deepin）是国内的Linux发行版，它已经装备好了一些wine好的国内软件。但许多是不能直接拿到其他发行版上来用的。深度会自己修改wine的源代码，他们提供的wine好的东西许多是基于他们的wine。
	3. 别人打包的AppImage，例如这个打包好的QQ（ https://github.com/askme765cs/Wine-QQ-TIM)。许多人是拿深度所做的打包成AppImage。自行在网上搜索一下会有，但别人打包的水平有高有低，兼容性有好有坏。可靠度和风险自行评估。
	4. Github上的用户 countstarlight 所维护的从深度wine那边移植往Arch Linux的腾讯通信软件：
	
		• deepin-wine-qq-arch
		• deepin-wine-tim-arch
		• deepin-wine-wechat-arch
手动下载wine的各个版本
wine已经广泛被各个发行版仓库收录了，但有些情况下需要手动下载wine的各种版本：
	1. 发行版提供的wine太旧
	2. 某些东西在旧版本中正常，新版本反而不正常（有时这可以通过调整配置解决，但这也是坑）
可以下载各个版本的wine的发行版通用二进制的地方：
经我测试，下载后解包，不要改变目录关系，使用里面的wine二进制即可以，一般是比较portable的。
下载时注意是32位还是64位的x86。不是根据你的真实cpu位数来，而是根据你需要模拟的Windows位数来。
总结
wine是坑！能用则用，不能用别留恋。两台电脑一台Linux一台Windows是最好方案。
另外最好也知道，proton是Valve为他们的游戏弄的wine衍生版，部分steam游戏使用它；crossover是wine的一个商业应用。如果真要弄wine，有时也可以寻找这些资源。


启动不同的WINE PREFIX（前缀，预制环境、容器），只需要设置环境变量就可以了。
WINEPREFIX是很重要的，默认值为~/.wine。wine会在它所指定的路径下创建drive_c/等几个文件（夹），其中包含了Windows环境配置、它的C盘文件等等
WINEPREFIX="/home/username/.newprefix/" wine + 应用程序
WINEarch=win32或者win64
