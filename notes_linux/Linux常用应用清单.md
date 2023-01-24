# Linux系统首选：Linux Mint大薄荷
DEB系备选deepin、 Ubuntukylin、openKylin、Batocera/RetroBat（游戏系统）、nixos（配置管理包系统）。

输入法：manjaro-asian-input-support-fcitx5（manjaro配置好的输入法包），ibus-rime，fcitx5-rime，大薄荷已经配置好fcitx-sunpinyin等中文输入法。（如果出现依赖错误，就直接删除fcitx的所有软件包从新安装就可解决）

桌面环境：Cinnamon（简单、稳定高效），GNOME42
* 插件：空格快速预览：gnome-sushi
* 插件：剪贴板管理器：Clipboard Indicator 
* GNOME Tweaks
* 剪贴板：GPaste，Glipper
* 相册：pix相册



文件管理器：ranger（终端文件管理）。

自适应屏幕亮度/温度工具：Gammy（aur）自己编译。

SysMonTask: 一个具有 Windows 任务管理器外观的系统监控器

SwitchHosts：hosts解析管理工具，支持直接对host文件进行编辑，添加自己的host解析规则，支持在多个host方案直接快速的切换，如解决GitHub速度慢的问题——GitHub520。

常用的字体，以及字体包。可以拷贝Win系统。推荐的字体：方正书宋、霞鹜文楷

----

**使Linux变得更加易用：**

> 安卓兼容层（xdroid）/Win兼容层（Wine）/Mac OS兼容层（darling）
> Linux原生应用：deb，更加简单的：appimage（重要） Flatpak（基于容器的应用分发工具）
> 浏览器：一些扩展应用，在线的文档编辑，图片处理，视频网站，邮件，本地安装的web应用。
> 这些都可以使Linux安装和使用软件更加容易。
>
> deb>flatpak>snap
>

AppImage Pool：一个帮助你寻找和管理 AppImage 的应用商店 | Linux 中国

appimage-installer：这个工具能在十几秒内快速的将一个AppImage文件部署到开始菜单，并且设置好图标和名称。

AppImageLauncher：可以自动将 AppImage 程序快捷方式添加到桌面环境的程序启动器/菜单(包括程序图标和合适的说明)中。

扩展，来自Win的软件使用/打包：wine ➕ appimage ；github项目Wine_Appimage

扩展，还有些功能可以通过浏览器实现，比如一些安装在本地的web应用/网络上的web应用。

Apifox：API 文档、API 调试、API Mock、API 自动化测试

----



**常用的软件**

1. 绘图软件：krita
2. 照片管理软件：DigiKam（全平台）、 gThumb
3. 图像处理：gimp
4. 截图软件：Snipaste（期待）/flameshot/大薄荷自带截图
5. 剪贴板软件：CopyQ，
6. office软件：WPS office /LibreOffice
7. 3D软件：Blender
8. 视频播放：mpv / Kaffeine
9. 音频播放：Audacious / foobar2000 / foobox5（https://github.com/dream7180/foobox-cn/）lxmusic 落雪 / Rhythmbox/ Spotify
10. 音频剪辑：Audacity/Ardour音频剪辑
11. 视频剪辑：Shotcut视频剪辑
12. 视频处理：HandBrake视频转换工具
13. 科学上网，V2Ray
14. 文件搜索：JEverything（java实现： 待完善），locate，Catfish，Tracker
15. 可视化磁盘空间：filelight / GdMap / Baobab / Spacesniffer（Win10）
16. 浏览器：火狐浏览器 / Edge浏览器。
17. 在线音乐：Cocomusic（QQ音乐） / 网易音乐
18. 下载工具Motrix，qbittorrent，

	* 命令行的wget,curl,aria2
	* XDM(Xtreme Download Manager)/代替idm
19. 压缩/解压缩： 360压缩/7zip
20. 兼容层安卓：XDroid /Kydroid/alien dalvik/anbox
21. 兼容层Windows和Macos：wine和darling（Darwin/macOS emulation layer for Linux）/Bottles更加顺滑地以最小的调整来运行你喜欢的 Windows 应用程序。
22. 虚拟机：VMware
23. 屏幕捕获：Captura，OBS studio 
24. 游戏：Steam， Proton 兼容层
25. 常用的命令工具：ffmpeg、lynx
26. 流程图绘制软件 yEd（全平台）非常nice。和亿图差不多好像。
27. 软路由 zerotier
28. Linuxbrew（Mac OS 的 Homebrew 分支，支持mac和linux，用法完全相同）详情页： https://ostechnix.com/linuxbrew-common-package-manager-linux-mac-os-x/  搜索可用的软件包： https://sitemap.filecroco.com/a/1.html
29. tigervnc、TightVNC
30. wireshark（抓包工具）
31. ToDesk远程桌面。
32. rclone、 wsgidav（较好的webdav客户端）
33. 网络抓包工具：wireshark，科来网络分析系统，fiddler
34. Tiny Core Linux或许是最小的Linux GUN
35. MaoXian web clipper，最好的开源网页剪藏浏览器插件
36. Syncthing 跨平台同步软件，简单易用，功能强大
37. wine-mono（wine版.net框架） wine-gecko（wine版web渲染框架）
38. 让tty界面（Linux控制台）支持中文：zhcon和fbterm。
39. barrier，开源全平台鼠标键盘共享软件。
40. Liferea（Linux 订阅阅读器）支持各种格式例如 RSS/RDF。
41. Etcher：（全平台）USB 镜像写入器
42. Collision：GTK应用用于验证你的文件。
43. 用sigil矫正一下目录（epub编辑器）
44. caddy webdav与http服务器。
45. 纯文本比对软件，Meld



**电子学习工具**

1. Mnemosyne（类似SuperMemo）
2. WikidPad（全平台）
3. CMapTools概念地图（concept map）（全平台），Freemind
4. treesheets 树状表
5. 免费开源yyds阅读器--okular（kde）或者koodo reader
6. tidgi：tiddlywiki 全平台单文件HTML 笔记软件超厉害der。
7. 渐进式学习与渐进式阅读、墨屉wiki。
8. 记忆软件：supermemo18（已完成打包，发布在哔哩哔哩）
9. learning_with_texts（web版语言学习工具）
10. Anki 记忆卡片（全平台，包括移动端）
11. 思维导图：VYM (View Your Mind)/ximind Linux
12. 词典翻译：goldendict / CopyTranslator9.0
13. PDF：MuPDF /  wondershare pdf felment（Win10）/ foxit PDF reader / bookxnote(win)
14. 笔记写作：TiddlyWiki、typore，Joplin笔记软件 Nixnote Obsidian
15. 阅读与图书管理：calibrate 
16. 笔记草稿（手写）软件： Xournal++（全平台，包名：xournalpp）/  Lorien /Rnote( 正在开发中 )





**命令行软件**

1. ranger（内容浏览/预览）
2. ncdu (可视化的空间分析程序
3. sox（音频处理）
4. wget、curl、aria2
5. vim、 less（vim触摸支持）
6. nmap
7. ssh
8. dirb （网站目录扫描）
9. openssl
10. translate-shell （CLI翻译）
11. ArozOS（Web桌面操作系统）
12. w3m , links2 ,lynx（终端浏览器）
13. mpv (支持音频)
14. lighttpd，apache2，nginx
15. fortune
16. imagemagick
17. figlet (字符画工具)
18. FFmpeg
19. Hexo（静态博客框架）
20. nodejs（npm包管理器）
21. proot-distro
22. lrzsz（lsx/lsix 显示缩略图）
23. mc（Midnight Commander 可以修改主题，electricblue256，sand256，gotar，https://phplego.github.io/mc/ ）
24. open-vm-tools，这个装上之后虚机就有了显示驱动，屏幕可以自适应大小
25. open-vm-tools-desktop，作用主要是主机和虚拟机之间的复制粘贴。其实，大文件的拖放也可以利用Share文件夹。
26. Neofetch 是一个酷炫的系统信息工具。

VCDS（汽车诊断软件）OBD，pcmscan，OBD-II 终端，torque，elm327，laptimer，dashcommand

----

Linux换源：Linux mint（大薄荷）可以使用开始菜单 - 软件源管理器 用鼠标设置。显卡驱动也是一样的容易。



gpg密钥操作：
未知的公共密匙 C1A60EACE707FDA5) 错误： 一个或多个 PGP 签名无法校验！
解决方法：`gpg --recv-keys C1A60EACE707FDA5`   



由于没有公钥，无法验证下列签名： NO_PUBKEY 76F1A20FF987672F
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 76F1A20FF987672F`



Linux 报错Certificate verification failed: The certificate is NOT trusted.
安装ca-certificates




Linux软件安装好安装知道名字就可以了，就是卸载不好卸载，只能一个个的盲目地卸载或者卸载依赖尤其是编译时安装的依赖，软件编译好了，系统环境被污染的严重，而且不够直观，如果有软件可以按类别卸载就好了。。。。。。

appimage打包，建议不要使用源码编译收集文件，不如使用人家编译好的二进制包deb，rpm，然后使用解压命令将所有二进制包以及需要的依赖系统依赖全部解压到指定目录，然后打包成为appimage使用。

-----

Ubuntu源分成两个：官方的（源）、个人的（ppa）。

ppa源PPA是Personal Package Archives首字母简写。翻译为中文意思是：个人软件包文档。
虽然Ubuntu官方软件仓库尽可能囊括所有的开源软件，但仍有很多软件包由于各种原因不能进入官方软件仓库。

为了方便Ubuntu用户使用，launchpad.net提供了个人软件包集，即PPA，允许用户建立自己的软件仓库，通过Launchpad进行编译并发布为2进制软件包，作为apt-get源供其他用户下载和更新。
在Launchpad网站上的每一个用户和团队都可以拥有一个或多个PPA。通常PPA源里的软件是官方源里没有的，或者是最新版本的软件。

PPA也被用来对一些打算进入Ubuntu官方仓库的软件，或者某些软件的新版本进行测试。





Manjaro换源

```shell
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
```



----

Appimage-installer工具，AUR 包的问题，https://gitee.com/deepin-opensource/appimage-installer/issues/I421HL

深度科技社区Maicss分享：深度科技社区Maicss分享：https://bbs.deepin.org/zh/post/220754


----

AppImage官网：AppImage官网：https://appimage.org/



超赞的 Linux 软件：这个仓库收集了对任何用户/开发者都超赞的 Linux 应用软件。
https://alim0x.gitbooks.io/awesome-linux-software-zh_cn/content/