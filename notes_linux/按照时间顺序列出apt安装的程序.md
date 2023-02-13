按照时间逆序列出apt安装的软件

```sh
for x in $(ls -1t /var/log/dpkg.log*); do 
      zcat -f $x |tac |grep -e " install " -e " upgrade "; 
done | awk -F ":a" '{print $1 " :a" $2}' |column -t

```