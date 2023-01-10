# WSL2 子系统、Hyper-V

虽然 WSL 2 确实使用 VM，但 VM 是在幕后管理和运行的，因此你将具有与 WSL 1 相同的用户体验。

WSL 2 中的 Linux 内核是 Microsoft 根据最新的稳定版分支（基于 kernel.org 上提供的源代码）构建的。此内核已专门针对 WSL 2 进行了调整，针对大小和性能进行了优化，以便在 Windows 上提供良好的 Linux 体验。 

WSL 1 使用的是由 WSL 团队构建的转换层。
WSL 2 包括了自己的 Linux 内核，具有完全的系统调用兼容性。

WSL1 提供与真实Linux内核类似的虚拟文件系统。在用户的系统上，我们提供了两个文件系统：VolFs 和 DriveFs。
WSL2使用Ext4文件系统 ，9p文件传输协议。



文件名：Hyper-V.cmd
```cmd
pushd "%~dp0"

dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt

for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"

del hyper-v.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL
```

- [ ] Hyper-V  系统组软件
- [ ] 适于Linux的Windows子系统
- [ ] 虚拟机平台
- [ ] WSL2 Linux 内核更新包

- [x] 选中状态
- [ ] 未选中状态


安装 WSL 2 之前，必须启用“虚拟机平台”可选功能。 计算机需要虚拟化功能才能使用此功能。

Windows 功能中的 “虚拟机平台” 功能的作用并不是向用户直接提供一个虚拟机工具，而是用来支持第三方虚拟机平台 (例如 VMware 等) 在 Windows 系统下运行。开启了此功能后，仍然需要您手动下载第三方虚拟机平台进行使用。
https://blog.csdn.net/S_ZaiJiangHu/article/details/127291863

关闭Hyper-V：【Win】关闭Hyper-v，无法彻底删除Hyper-V选项，即使是重置系统。
管理命令
1. Wsl
2. Wslconfig


常用命令
1. 列出已安装的 Linux 发行版，wsl -l -v。
2. 安装新的 Linux 发行版时将默认版本设置为 WSL 1 或 WSL 2，请使用命令 wsl --set-default-version <Version#>，将 <Version#> 替换为 1 或 2。
3. 设置与 wsl 命令一起使用的默认 Linux 发行版，wsl -s <DistributionName> ，将 <DistributionName> 替换为要使用的 Linux 发行版的名称。 例如，从 PowerShell/CMD 输入 wsl -s Debian，将默认发行版设置为 Debian。 现在从 Powershell 运行 wsl npm init 将在 Debian 中运行 npm init 命令。
4. 要在 PowerShell 或 Windows 命令提示符下运行特定的 WSL 发行版而不更改默认发行版，请使用命令 wsl -d <DistributionName>，将 <DistributionName> 替换为要使用的发行版的名称。

来自 < https://docs.microsoft.com/zh-cn/windows/wsl/install> 






将WSL2安装到自定义位置
	1. 安装包下载地址： https://docs.microsoft.com/zh-cn/windows/wsl/install-manual#downloading-distributions
	2. 用压缩软件解压提取appxbundle文件中的Ubuntu_2004.2021.825.0_x64.appx
	3. 解压Ubuntu_2004.2021.825.0_x64.appx文件，然后再解压的文件夹中找到ubuntu2004.exe，双击安装
	4. wsl -l -v 验证安装。




个性化配置(可选)

更换软件源
为了提高我们安装软件的速度，我们先将apt的源修改为清华源，或者其它源，下面是更换为清华源的步骤：

sudo mv /etc/apt/sources.list /etc/apt/sources.list.backup
        sudo nano /etc/apt/sources.list
将下面的内容粘贴到sources.list：


# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

sudo apt update

wget https://http.kali.org/kali/pool/main/k/kali-archive-keyring/kali-archive-keyring_2022.1_all.deb --no-check-certificate
https://mirrors.tuna.tsinghua.edu.cn/kali/pool/main/k/kali-archive-keyring/
#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free



解决dpkg: warning: files list file for package ：重新安装apt-get reinstall "$package"






Linux 报错Certificate verification failed: The certificate is NOT trusted.
原因为未安装ca-certificates

	1. 可以先编辑 /etc/apt/sources.list 文件临时使用http源
	2. 然后安装ca-certificates包
	3. 安装完成后编辑源 /etc/apt/sources.list 改回https
	4. 执行apt update更新，完成





Ohmyzsh

ohmyzsh主题： avit、bureau、agnoster、mortalscumbag、amuse
powerlevel10k应该特别好，这个主题。

sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"

powerlevel10k：git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
主题名：powerlevel10k/powerlevel10k

ls ~/.oh-my-zsh/themes
ls ~/.oh-my-zsh/plugins

 ~/.zshrc ：
	1. plugins=(其他的插件 zsh-autosuggestions)
	2. ZSH_THEME="主题名"

zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-synt
ax-highlighting

zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions






zsh主题pure
https://github.com/sindresorhus/pure#install
mkdir -p "$HOME/.zsh"
git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure"


# .zshrc
fpath+=$HOME/.zsh/pure
autoload -U promptinit; promptinit
prompt pure


