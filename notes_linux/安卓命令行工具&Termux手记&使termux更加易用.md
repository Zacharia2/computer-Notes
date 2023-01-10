Termux / Utermux（termux魔改版）
Aid Learning（AidLux）

web应用，本地的命令应用。ssh。

最有趣的地方：用于练习vim和vim的插件。以及Python的应用（包含pip的软件）

termux可以改终端配置文件（`.bashrc`）自动执行脚本命令。
`$PREFIX/etc/bash.bashrc`

查看服务命令：`ps aux`、`service`、`chkconfig`

### 命令行 | termux常用软件列表
1.  termux-ohmyzsh （访问GitHub主页）
2.  play-audio（音频支持）
3.  termux-pulseaudio，pulseaudio（Proot容器音频支持）
4.  sox（音频处理）
5.  Python
6.  git     
7.  wget
8.  vim  
9.  tar  
10.  less（vim触摸支持）
11.  nmap（端口扫描）
12.  whatportis 
13.  ssh
14.  curl
15.  dirb （网站目录扫描）
16.  aria2
17.  openssl
18.  translate-shell （CLI翻译）
19.  termimage（图片显示）
20.  ArozOS（Web桌面操作系统）
21.  w3m , links2 ,lynx（终端浏览器）
22.  finux（web termux文件管理器）
23.  mpv (支持音频)
24.  lighttpd，apache2，nginx
25.  fortune
26.  imagemagick
27.  figlet (字符画工具)
28.  FFmpeg
29.  Hexo（静态博客框架）
30.  nodejs（npm包管理器）
31.  proot-distro
32.  lrzsz（lsx/lsix 显示缩略图）
33.  ranger（内容浏览/预览）
34.  mc（Midnight Commander 可以修改主题，electricblue256，sand256，gotar，https://phplego.github.io/mc/）
35.  ncdu (可视化的空间分析程序)



以下需要桌面环境
1.  tigervnc
2.  TightVNC
3.  noVNC（网页版）

---


### Termux快捷键

音量减代替部分CTRL键。
音量加+V -> 显示音量控制
音量加+Q -> 显示额外的按键视图
音量加+T -> Tab键


音量加+1 -> F1（和音量增加+2→F2等）
音量加+0 -> F10


音量加+L -> | （管道字符）
音量加+H -> 〜（波浪号字符）


音量加+P -> 上一页
音量加+N -> 下一页


音量键加 + B 和 音量键加 + F ，可在单词之间来回 移动。功能与 ctrl+shift+->/<- 相似


Ctrl+K -> 从光标删除到行尾 home ➕ Ctrl k
Ctrl+L -> 清除终端
Ctrl+D -> 注销终端会话

---


TermuxWiki：
https://wiki.termux.com/wiki/Main_Page

termux仅包含home，usr。

`$PREFIX`  指向usr
如：` ./configure --prefix=$PREFIX && make && make install`
`$PREFIX`，可以做根目录。`$prefix/etc`


`$HOME`  指向home
`$HOME/storage/shared/我的dropbox`
`rclone serve webdav $HOME/storage/shared/我的dropbox/`


Termux-Api 是 Termux 软件的一个插件，需要安装额外的 APK 包。并且命令行中也需要使用 $ apt install termux-api 命令安装具体的工具。
它提供了一种以 API 的形式直接访问 Android 系统硬件和资源（如相机、电池、WiFi、短信、通讯录、指纹、GPS等）的途径。

其它信息来源：微信-termux，https://www.bilibili.com/read/mobile?id=5041443

`apt list`命令可以看到所有可用的软件。


termux-ohmyzsh软件，chcolor命令首选颜色
1. elementary.colors
2. elio.colors


### 有关termux的命令          

- termux-open
- termux-open-url
- termux-reload-settings             
- termux-reset
- termux-am               
   
- termux-restore
- termux-backup             
  
- termux-setup-storage
- termux-change-repo      （快速切换软件源）
- termux-wake-lock
- termux-fix-shebang          
- termux-wake-unlock
- termux-info

### 高效进行目录切换：目录栈

pushd 、 popd 、 dirs

目录栈 就是一个保存目录的栈结构，该栈结构的顶端永远都存放着当前目录

1. dirs：显示目录栈内容，常用参数-p每行显示一条记录；-v每行显示一条记录，同时展示该记录在栈中的index；-c清空目录栈。
2. pushd：压入目录栈。pushd + 目录：切换到该目录并且将该目录置于目录栈的栈顶。pushd +/-n 就是直接切换到对应索引值的目录。pushd (不带任何参数)：目录栈最顶层的两个目录进行交换。
3. popd：弹出目录栈。popd +/-n将目录栈中的第n个元素删除。将目录栈中的栈顶元素出栈。当前目录也会发生相应的切换。

注意，最顶部的元素永远跟当前目录一致，如果你在其它目录下查看目录栈，第一个元素将对应发生改变。注意，pushd +/-n既可以用加号，也可以用减号。如果是加号的话，将从目录栈由n到0数，而用减号的话，将从目录栈由0到n数。pushd和popd执行完成默认执行dirs显示目录栈的内容。

有关目录的命令：cd、ls、du、pwd、tree

删除软连接rm –rf /target
注意：不要在后文件名后面加斜杆 “/” 否则会删除文件夹的内容

GL4ES：用于GLES硬件的OpenGL

SoX（即 Sound eXchange）是一个跨平台（Windows，Linux，MacOS 等）的命令行实用程序，可以将各种格式的音频文件转换为需要的其他格式。


https://www.jianshu.com/p/3489a1cf81d1

![](/images/termux-1.jpg)