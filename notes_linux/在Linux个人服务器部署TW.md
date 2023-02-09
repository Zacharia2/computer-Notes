

## tiddlywiki

- 创建 TiddlyWiki 目录 `mkdir ~/wiki `

- 在 TiddlyWiki 目录下创建基本文件 `tiddlywiki wiki --init server`

- 创建用户权限文本 vim ~/wiki/users.csv

users.csv 文本内容：

```text
username,password
johndoe,445566
```
其中首行为必填项，第二行为用户名和明文密码，英文小写逗号，不包含任何空格。


- 启动wiki：`tiddlywiki +plugins/tiddlywiki/tiddlyweb +plugins/tiddlywiki/filesystem ~/wiki --listen host=0.0.0.0 port=4040`

`tiddlywiki wiki --listen credentials=users.csv "readers=(anon)" "writers=(authenticated)" host=0.0.0.0 port=4040`



## PM2

- 赋予 tw.sh 权限 `chmod +x /root/tw.sh`
- 通过 pm2 守护进程运行 TiddlyWiki `pm2 start /root/tw.sh`
- 保存当前状态 `pm2 save`
- 设置开机自启 `pm2 startup`