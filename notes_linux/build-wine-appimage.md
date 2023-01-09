
https://wiki.winehq.org/Debian
https://github.com/Hackerl/Wine_Appimage

- 从wine官网缓存deb软件包到本地。（wine所有可执行文件、依赖）
-下载fontconfig-config依赖
- 从debs目录解压所有deb包。
- 路径重定向
  - 编译libhookexecv、wine-preloader_hook，放入App/bin 目录。应用环境变量WINELDLIBRARY，传递指定目录的ld.so
- 编写AppRun，设置环境变量应用路径pulseaudio、ld-linux.so重定向并使用libhookexecv执行命令。
- 打包WINE



`export LD_LIBRARY_PATH="$HERE/usr/lib":$LD_LIBRARY_PATH `
其中 ‘:’ 意思为追加，再增加的路径。


这种格式可以实现不断往一个变量中追加路径
```sh
export LD_LIBRARY_PATH="$HERE/usr/lib":$LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$HERE/usr/lib/i386-linux-gnu":$LD_LIBRARY_PATH
```

Linux环境变量：

LD_LIBRARY_PATH环境变量用于在程序加载运行期间查找动态链接库时指定除了系统默认路径之外的其他路径，注意，LD_LIBRARY_PATH中指定的路径会在系统默认路径之前进行查找。


FONTCONFIG_PATH环境变量,无或默认为/etc/fonts目录。


`$@ `传递给脚本或函数的所有参数


构建AppImage

下载官方的AppImageKit(appimagetool-x86_64.AppImage): https://github.com/AppImage/AppImageKit/releases/latest

运行即可

```sh
ARCH=x86_64 ./appimagetool-x86_64.AppImage AppDir
```

apt download files ,files指的`依赖包 软件包 软件包。。。`
