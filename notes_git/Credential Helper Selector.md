Credential Helper Selector，大意是：

- git 支持 ssh 和 https 两种协议，使用 https 协议的话，必须输入账号密码
- Credential Helper 是 git 自带的凭据管理工具，可以把账号和密码安全地保存起来，不必要每次都输入账号和密码

重新打开上面对话框的方式是在终端中输入 `git credential-helper-selector` 命令，然后按回车键即可。 
- cache 将凭据在内存中进行短时间的缓存；
- store 将凭据保存在磁盘上，长久有效；

我重新选择：manager-store，然后勾选 Always use this from now on，然后点击select。

![](/images/CredentialHelperSelector.png)
