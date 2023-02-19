拷贝证书指定目录下：`/usr/share/ca-certificates/`

修改权限：`a+r /usr/share/ca-certificates/name(x-net).crt`

安装证书：`dpkg-reconfigure ca-certificates `