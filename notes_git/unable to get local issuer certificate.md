# git：unable to get local issuer certificate

使用git初始化一个项目时，尤其是通过git submodule update --init --remote初始化子模块时，可能会遇到下面这个错误：

SSL certificate problem: unable to get local issuer certificate

这是由于当你通过HTTPS访问Git远程仓库的时候，如果服务器上的SSL证书未经过第三方机构认证，git就会报错。原因是因为未知的没有签署过的证书意味着可能存在很大的风险。

解决办法就是通过下面的命令将git中的sslverify关掉：

`git config --global http.sslverify false`