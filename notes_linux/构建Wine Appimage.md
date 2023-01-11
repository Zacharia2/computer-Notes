https://wiki.winehq.org/Debian
https://github.com/Hackerl/Wine_Appimage
https://www.playonlinux.com/en/download.html

> 难点是，无法知道哪些库引用了绝对路径。

- 从wine官网缓存deb软件包到本地。（wine所有可执行文件、依赖）
- 下载fontconfig-config依赖
- 从debs目录解压所有deb包。
- 路径重定向
  - 使用libhookexecv、wine-preloader_hook重定向ld.so，复制已编译好的文件放入App/bin 目录。应用环境变量WINELDLIBRARY，传递指定目录的ld.so
  - 其它文件或许也可以这样做？
- 编写AppRun，设置环境变量应用路径pulseaudio、ld-linux.so重定向并使用libhookexecv执行命令。
- 打包WINE

`export var_name="value":$var_name` 其中 ‘:’ 意思为追加，再增加的路径。这种格式可以实现不断往一个变量中追加路径

```sh
export LD_LIBRARY_PATH="$HERE/usr/lib":$LD_LIBRARY_PATH 

export LD_LIBRARY_PATH="$HERE/usr/lib":$LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$HERE/usr/lib/i386-linux-gnu":$LD_LIBRARY_PATH
```



Linux环境变量：LD_LIBRARY_PATH环境变量用于在程序加载运行期间查找动态链接库时指定除了系统默认路径之外的其他路径，注意，LD_LIBRARY_PATH中指定的路径会在系统默认路径之前进行查找。


`$@ `传递给脚本或函数的所有参数


`apt download files` 用于下载软件包，其中 files指的是‘软件包A 软件包B……’

