## 什么是 AUR？

AUR 表示Arch 用户仓库(Arch User Repository)。它是针对基于 Arch 的 Linux 发行版用户的社区驱动的仓库。它包含名为 PKGBUILD 的包描述，它可让你使用 makepkg 从源代码编译软件包，然后通过 pacman（Arch Linux 中的软件包管理器）安装。

创建 AUR 的目的是组织和共享社区中的新软件包，并帮助加速将流行的软件包纳入社区仓库。

进入官方仓库的大量新软件包都从 AUR 开始。在 AUR 中，用户可以贡献自己的软件包构建（PKGBUILD 和相关文件）。

AUR 社区可以对 AUR 中的软件包进行投票。如果一个软件包变得足够流行（假设它具有兼容的许可证和良好的打包技术），那么可以将其加入 pacman 直接访问的社区仓库中。

简而言之，AUR 是开发人员在 Arch 仓库中正式包含新软件之前向 Arch Linux 用户提供新软件的一种方式。

## 你应该使用 AUR 吗？有什么风险？

使用 AUR 就像过马路一样。如果你谨慎操作，应该就没问题。

如果你刚接触 Linux，建议你在建立有关 Arch/Manjaro 和 Linux 的基础知识之前不要使用 AUR。

的确，任何人都可以将软件包上传到 AUR，但受信任用户（TU）负责监视上传的内容。尽管 TU 对上传的软件包执行质量控制，但不能保证 AUR 中的软件包格式正确或没有恶意。

在实践中，AUR 似乎很安全，但理论上讲它可以造成一定程度的损害，但前提是你不小心。从 AUR 构建软件包时，聪明的 Arch 用户总是检查 PKGBUILD 和 *.install 文件。

此外，TU（受信任用户）还会删除 AUR 中包含在 core/extra/community 中的软件包，因此它们之间不应存在命名冲突。AUR 通常会包含软件包的开发版本（cvs/svn/git 等），但它们的名称会被修改，例如 foo-git。

对于 AUR 软件包，pacman 会处理依赖关系并检测文件冲突，因此，除非你默认使用 –force 选项，否则你不必担心用另一个包中的文件会覆盖另一个包的文件。如果这么做了，你可能会遇到比文件冲突更严重的问题。

## 在 Arch Linux 上安装 AUR 助手

一般我们用aurman或者yay

Yay 是 Arch Linux 下基于 CLI 的最佳 AUR 助手，使用 Go 语言编写。Yay 是基于 yaourt、apacman 和 pacaur 设计的。

这是最合适推荐给新手的 AUR 助手。类似于 Pacman，其使用方法和 pacman 中的命令和选项很相似，可以让用户在搜索过程中找到匹配的软件包提供程序，并进行选择。

安装Yay：

```sh
sudo pacman -S git go base-devel
git clone [https://aur.archlinux.org/yay.git](https://aur.archlinux.org/yay.git)
cd yay
makepkg -si
```


安装 aurman：
```bash
git clone [https://aur.archlinux.org/aurman.git](https://aur.archlinux.org/aurman.git)
cd aurman
makepkg -si
```


## 不使用 AUR 助手安装 AUR 软件包

如果你不想使用 AUR 助手，那么也可以自行从 AUR 安装软件包。

在 AUR 页面上找到要安装的软件包后，建议确认“许可证”、“流行程度”、“最新更新”、“依赖项”等，作为额外的质量控制步骤。
```shell
1.  git clone [package URL]
2.  cd [package name]
3.  makepkg -si
```


例如。假设你要安装 telegram 桌面包：

```shell
1.  git clone https://[aur.archlinux.org/telegram-desktop-git.git](http://aur.archlinux.org/telegram-desktop-git.git)
2.  cd telegram-desktop-git
3.  makepkg -si
```


From < [https://blog.csdn.net/f8qg7f9yd02pe/article/details/105525030](https://blog.csdn.net/f8qg7f9yd02pe/article/details/105525030)>