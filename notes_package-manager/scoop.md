# scoop

> scoop必要组件： 7zip git innounp lessmsi dark sudo aria2
> scoop我的CLI软件：ffmpeg 、pandoc
>
> main：https://github.com/ScoopInstaller/Scoop



一、安装scoop
- 将scoop安装到自定义目录

```powershell
- $env:SCOOP='D:\Software\Scoop' # 先添加用户级别的环境变量 SCOOP
- [environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')

- Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
#下载安装Scoop（使用$env:SCOOP安装路径）
- scoop install <软件名> 安装到自定义目录
- scoop install <软件名@版本号>  安装特定版本的软件

- scoop install aria2
- Scoop bucket add extras
```

二、配置scoop
- scoop源配置: `scoop config SCOOP_REPO https://gitee.com/squallliu/scoop`

软件仓库bucket源：
软件源使用git版本管理，因此可以使用修改远程仓库的地址修改源地址加快速度。

```shell
cd $env:SCOOP\buckets\Main      
git remote set-url origin http://hub.fastgit.org/ScoopInstaller/Main

cd $env:SCOOP\buckets\Extras
git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Extras
```



- aria2相关配置
```
aria2-enabled (默认值: true)
aria2-retry-wait (默认值: 2)
aria2-split (默认值: 5)
aria2-max-connection-per-server (默认值: 5)
aria2-min-split-size (默认值: 5M)
```


全局安装
- $env:SCOOP_GLOBAL='D:GlobalScoopApps'
- [environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
- scoop install -g <软件名>   安装到默认全局目录


三、常用bucket
```powershell
#scoop bucket remove main
scoop bucket add main 'https://github.com/ScoopInstaller/Main'
scoop bucket add extras 'https://github.com/ScoopInstaller/scoop-extras'
scoop bucket add versions 'https://github.com/ScoopInstaller/Versions'
scoop bucket add jetbrains 'https://github.com/Ash258/Scoop-JetBrains'
scoop bucket add java 'https://github.com/ScoopInstaller/Java'
scoop bucket add dorado https://github.com/chawyehsu/dorado
scoop bucket add scoopet https://github.com/ivaquero/scoopet

#scoop bucket fastgit镜像
scoop bucket add main 'https://hub.fastgit.org/ScoopInstaller/Main'
scoop bucket add extras 'https://hub.fastgit.org/ScoopInstaller/scoop-extras'
scoop bucket add versions 'https://hub.fastgit.org/ScoopInstaller/Versions'
scoop bucket add jetbrains 'https://hub.fastgit.org/Ash258/Scoop-JetBrains'
scoop bucket add java 'https://hub.fastgit.org/ScoopInstaller/Java'
scoop bucket add dorado 'https://hub.fastgit.org/chawyehsu/dorado'
scoop bucket add scoopet 'https://hub.fastgit.org/ivaquero/scoopet'
```

在软件安装过程中通常会自动添加main bucket，可以通过scoop bucket rm main删除之后重新添加。之后修改链接可以使用如下内容：

```powershell
 cd $env:SCOOP\buckets\Main      这是一个git管理的文件夹
 git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Main
```





安装（ 使用 powershell）
	1. 在 PowerShell 中输入下面内容，保证允许本地脚本的执行：（仅第一次安装前需要执行）
	set-executionpolicy remotesigned -scope currentuser

	2. 然后执行下面的命令安装 Scoop：（稍微卡顿一些，等等就好）
	iex (new-object net.webclient).downloadstring('https://get.scoop.sh')


安装位置说明

卸载（软件的使用权归自己所有，一言不合即卸载）
注意： scoop 管理的软件都会卸载！！！
scoop uninstall scoop

手动删除 scoop 文件（当前用户目录下，同安装目录）

help 查看支持的命令：scoop help


查找软件：scoop search xxx软件包


安装软件：scoop install xxx软件包


卸载软件：scoop  uninstall xxx软件

查看软件官方页：scoop home xxx软件

查看软件详情

查看安装的软件列表：scoop list


更新软件：`scoop update`

查看软件列表：`scoop export >> xxx.txt`

查看 官方支持的 bucket：`scoop bucket known`

查看 bucket 命令帮助：`scoop bucket help`

添加 bucket：`scoop bucket add xxxbucket`

删除 bukcet：：`scoop bucket rm xxx仓库`






常用命令说明

```
alias       Manage scoop aliases # 管理指令的替身
bucket      Manage Scoop buckets # 管理软件仓库
cache       Show or clear the download cache # 查看与管理缓存
checkup     Check for potential problems # 做个体检
cleanup     Cleanup apps by removing old versions # 清理缓存与旧版本软件包
config      Get or set configuration values # 配置Scoop
create      Create a custom app manifest # 创建自定义软件包
depends     List dependencies for an app # 查看依赖
export      Exports (an importable) list of installed apps # 导出软件包列表
help        Show help for a command # 显示帮助指令
hold        Hold an app to disable updates # 禁止软件包更新
home        Opens the app homepage # 打开软件包主页
info        Display information about an app # 显示软件包信息
install     Install apps # 安装软件包的指令
list        List installed apps # 列出所有已安装软件包
prefix      Returns the path to the specified app # 查看软件包路径
reset       Reset an app to resolve conflicts # 恢复软件包版本
search      Search available apps # 搜索软件包
status      Show status and check for new app versions # 查看软件包更新状态
unhold      Unhold an app to enable updates # 启动软件包更新
uninstall   Uninstall an app # 卸载软件包的指令
update      Update apps, or Scoop itself # 更新软件包
virustotal  Look for app hash on virustotal.com # 查看哈希值
which       Locate a shim/executable (similar to 'which' on Linux) # 查看可执行程序路径
```