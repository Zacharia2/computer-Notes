# scoop安装、配置

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
cd $env:SCOOP\buckets\Main      
git remote set-url origin http://hub.fastgit.org/ScoopInstaller/Main

cd $env:SCOOP\buckets\Extras
git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Extras



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