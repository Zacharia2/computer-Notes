# Git版本管理工具

概述：一般发生在团队协作的版本管理语境中, 用来避免多人同时修改同一资源的锁机制

签入(check in)/签出(check out)是针对远程资源仓库而言的锁机制：

- 签出(check out from repository to local workspace)即是将资源下载到本地，进行修改，相当于给资源上锁。
- 签入(check in to repository from local workspace)即是在完成对资源的修改并提交后，将其上传到远程资源仓库，相当于给资源解锁。

`git config --global core.autocrlf input`
当一个以CRLF为行结束符的文件不小心被引入时你肯定想进行修正，把core.autocrlf设置成input来告诉 Git 在提交时把CRLF转换成LF，签出时不转换。
这样会在Windows系统上的签出文件中保留CRLF，会在Mac和Linux系统上，包括仓库中保留LF。

`git config --system core.longpaths true`
长文件名支持。
