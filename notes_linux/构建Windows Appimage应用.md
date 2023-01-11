
>需要注意的是 虚拟目录 的设置。

## wine或者wine Appimage

其实在构建Windows Appimage时，不必将Wine放入每个应用中。完全可以将Wine Appimage的软链接放入/usr/bin，在各个Windows Appimage应用中调用Wine Appimage。 下载Wine Appimage，创建软链接：

```sh
ln $(pwd)/Wine-x86_64.AppImage /usr/bin/wine
```

## 构建应用AppDir

将应用Wine配置目录放入AppDir

之后通过设置 WINEPREFIX 变量，使得Wine以目录为起始，作为读写源。


## 虚拟目录

Wine需要对Appimage中的WINEPREFIX目录进行读写，但Appimage中的内容挂载出来是只读属性。 所以需要使用使用虚拟目录，将对WINEPREFIX的写操作重定向至$HOME，从而存储应用数据：
```sh
RO_DATADIR="$HERE/opt/apps.com.thunder.mini/"
RW_DATADIR="$HOME/.ThunderMini"
TOP_NODE="/tmp/.ThunderMini.unionfs"

mkdir -p $RW_DATADIR $TOP_NODE

$HERE/usr/bin/unionfs-fuse -o use_ino,nonempty,uid=$UID -ocow "$RW_DATADIR"=RW:"$RO_DATADIR"=RO "$TOP_NODE" || exit 1
```
将unionfs-fuse放入Appimage中，使用unionfs-fuse形成虚拟节点。 上面的命令将创建 TOP_NODE 虚拟节点，只读目录 RO_DATADIR 指向WINEPREFIX目录，而读写目录 RW_DATADIR 用来储存数据。 当对虚拟节点 TOP_NODE 进行读时，会到RO_DATADIR、RW_DATADIR中寻找文件。 当对 TOP_NODE 进行写时，会重定向至 RW_DATADIR。


## AppRun

创建运行脚本：
```sh
#!/bin/bash
command -v wine >/dev/null 2>&1 || { echo -e >&2 "I require wine.\nYou can download Wine-x86_64.AppImage from https://github.com/Hackerl/Wine_Appimage/releases.\nThen run: chmod 777 \$(pwd)/Wine-x86_64.AppImage; sudo ln -s \$(pwd)/Wine-x86_64.AppImage /usr/bin/wine"; exit 1; }

HERE="$(dirname "$(readlink -f "${0}")")"

export WINEDEBUG=-all

RO_DATADIR="$HERE/opt/apps.com.thunder.mini/"
RW_DATADIR="$HOME/.ThunderMini"
TOP_NODE="/tmp/.ThunderMini.unionfs"

mkdir -p $RW_DATADIR $TOP_NODE

$HERE/usr/bin/unionfs-fuse -o use_ino,nonempty,uid=$UID -ocow "$RW_DATADIR"=RW:"$RO_DATADIR"=RO "$TOP_NODE" || exit 1

function finish {
  echo "Cleaning up"
  killall $HERE/usr/bin/unionfs-fuse
}
trap finish EXIT

export WINEPREFIX="$TOP_NODE"
wine "c:\\Program Files\\Thunder Network\\MiniThunder\\Bin\\ThunderMini.exe" "$@"
```
最后的命令运行wine，必须保证指向Wine Appimage的软链接/usr/bin/wine存在。

## 打包运行

```sh
export ARCH=x86_64; ./appimagetool-x86_64.AppImage squashfs-root
```