
前言

好多天没折腾那些流行的 Linux 发行版了，今天抽了点时间体验了一下 distrowatch 上排名第一的 Manjaro，尝试了几个不同桌面环境的版本，总体来说颜值跟性能都是不错的，加上依靠 Arch 的最丰富软件源，比较适合追求体验最新开源软件的 Linux 爱好者使用。详细的体验心得，等体验一段时间之后再做评论。下面就列一下在 Manjaro 下必须掌握的基本技能【貌似是上手每一个Linux 发行版的第一步课程】

1. 切换国内最快的软件源
大多数 Linux 发行版都是来自国外，自然官方仓库地址也在国外，所以一般情况下安装完 Linux 发行版之后做的第一件事就是切换源为国内的源。源的切换操作，大部分发行版也都支持 GUI 切换，这里只列出在命令行下如何擦操作

# 1. 第一部分使用 pacman-mirrors 更新官方软件源
## 1.1 按照地区自动更新为最快最稳定的软件源镜像地址

`sudo pacman-mirrors --country China`

## 1.2. 恢复默认软件源操作
`sudo pacman-mirrors --interactive --default`


## 1.3 软件源更新之后，我们一般会进行系统更新
`sudo pacman -Syyu# 软件源更新完成之后进行系统软件更新操作`


## 1.4 查看所有可用的地区信息
`sudo pacman-mirrors -l`

参考翻译自： https://wiki.manjaro.org/index.php?title=Use_pacman-mirrors_to_Set_the_Fastest_Download_Server

2. 使用 pacman 管理软件

# 2. 第二部分使用 pacman 管理软件
## 2.1 同步并且更新你的系统
`sudo pacman -Syyu`

## 2.2 在软件仓库中搜索软件
`sudo pacman -Ss [software package name]`

## 2.3 查看已安装软件

`sudo pacman -Qs [software package name]`
`sudo pacman -Qi [software package name]`# 附带详细信息
`sudo pacman -Qii [software package name]`# 附带更加详细的包信息
`sudo pacman -Ql`# 列出所有安装的软件包

## 2.4 查看软件的详细依赖
`sudo pactree [software package name]`

## 2.5 查看系统中那些没有被使用软件依赖包（orphans）
`sudo pacman -Qdt`

## 2.6 自动移除那些系统中没有被使用的依赖包【类似于Debian下的 sudo apt autoremove --purge】
`sudo pacman -Rs $(pacman -Qdtq)`

## 2.7 下载并安装软件包
`sudo pacman -Syu [software package name]`# 从软件仓库安装
`yay -S [software package name]`# Packages from the AUR
`sudo pacman -U [/package_path/][software package name.pkg.tar.xz]`# 从本地安装

`pacman -U http://www.examplepackage/repo/examplepkg.tar.xz`# 从网络安装【非官方仓库】

## 2.8 卸载软件

`sudo pacman -R [software package name]`
`sudo pacman -Rs [software package name]`# 同时删除依赖
`sudo pacman -Rns [software package name]`# 删除软件及其依赖，还有pacman生成的配置文件，即更彻底的删除

## 2.9 清空缓存【默认情况下安装软件会先来缓存中查看是否已经下载过，没有再去下载，软件安装后通常下载缓存还在】

`sudo pacman -Sc`
`sudo pacman -Scc` # 更彻底的清理

关于 pacman 常用就这些了，更多请使用 man pacman OR pacman -h 去查看
参考翻译自： https://wiki.manjaro.org/index.php?title=Pacman_Overview
From < https://csdnimg.cn/release/phoenix/template/new_img/articleReadEyes.png> 
