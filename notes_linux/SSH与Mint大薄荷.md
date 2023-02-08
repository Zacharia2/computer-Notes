
sudo apt install ssh

同一局域网连接，检查是否在同一局域网

## SSH介绍

ssh结构 ：ssh和sshd

客户端：scp（远程拷贝）、slogin（远程登陆）、sftp（安全文件传输）。

服务器端：公共密钥认证、密钥交换、对称密钥加密、非安全连接。


## 防火墙 ufw

```sh
sudo ufw allow ssh
sudo ufw enable 
sudo ufw status
```

## 服务管理 systemd

```sh
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

## 查看ip与用户名

```sh
ifconfig
whoami
```


## 配置说明

> ssh命令中没有设置配置文件的命令。所以只能手动修改配置文件。

GSSAPI：通用安全服务应用程序接口。该接口是对各种不同的客户端服务器安全机制的封装，以消除安全接口的不同，降低编程难度。

> 一般 SSH 依次进行的认证方法的是 publickey, gssapi-keyex, gssapi-with-mic, password， 这个你可以ssh -v开启 debug 模式在连接日志看到。   一般用户只使用 password 认证方式，但前面 3 个认证过程系统还是会尝试，这就浪费时间了，也就造成 SSH 登录慢。


Kerberos是一种计算机网络授权协议，用来在非安全网络中，对个人通信以安全的手段进行身份认证。https://zhuanlan.zhihu.com/p/266491528


一句话来说，Kerberos 是一种基于加密 Ticket 的身份认证协议。Kerberos 主要由三个部分组成：Key Distribution Center (即KDC)、Client 和 Service。 


```bash
#	$OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

# 用于 OpenSSH 附带的默认sshd_config中的选项的策略是在可能的情况下
# 使用默认值指定选项，但保留注释。 未注释的选项将覆盖默认值。

Include /etc/ssh/sshd_config.d/*.conf



# Port：设置监听端口。
# AddressFamily：指定 sshd(8) 应当使用哪种地址族。取值范围是："any"(默认)、"inet"(仅IPv4)、"inet6"(仅IPv6)。
# ListenAddress，指定 sshd(8)监听的网络地址，默认监听所有地址。

#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::



# 设置私钥存储目录
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key
#HostKey /etc/ssh/ssh_host_ed25519_key



# 密码和密钥 Ciphers and keying
#RekeyLimit default none



# 日志 Logging
# SyslogFacility：设置Syslog消息类型。
# LogLevel：设置日志级别。

#SyslogFacility AUTH
#LogLevel INFO




# 认证 Authentication:

# LoginGraceTime：认证时限，限制用户必须在指定的时限内成功，0 表示无限制。默认值是 120 秒。
# PermitRootLogin：允许ROOT登录;StrictModes： 指定是否要求 sshd(8) 在接受连接请求前对用户主目录和相关的配置文件进行宿主和权限检查。
# MaxAuthTries： 指定每个连接最大允许的认证次数。默认值是 6 。
# MaxSessions：指定连接最大会话的数量。默认值是 10 。;

#LoginGraceTime 2m
#PermitRootLogin prohibit-password
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10


# 是否允许公钥认证。
#PubkeyAuthentication yes


# 预计将来默认忽略 .ssh/authorized_keys2
#AuthorizedKeysFile	.ssh/authorized_keys .ssh/authorized_keys2



#AuthorizedPrincipalsFile none

#AuthorizedKeysCommand none
#AuthorizedKeysCommandUser nobody



# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
# 为此，您还需要 /etc/ssh/ssh_known_hosts 中的主机密钥
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for HostbasedAuthentication
# 如果您不信任 .ssh/known_hosts 用于基于主机的身份验证，请更改为 yes
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
# 不要读取用户的 .rhosts 和 .shosts 文件
#IgnoreRhosts yes



# 密码验证设置
# 密码认证：PasswordAuthentication；允许空密码：PermitEmptyPasswords。
# 要禁用隧道明文密码，请在此处更改为否！

#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to yes to enable challenge-response passwords (beware issues with some PAM modules and threads)
# 是否允许质疑-应答(challenge-response)认证。（请注意某些 PAM 模块和线程的问题）
ChallengeResponseAuthentication no



# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes
#GSSAPIStrictAcceptorCheck yes
#GSSAPIKeyExchange no

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes



# AllowTcpForwarding：是否允许TCP转发。GatewayPorts：是否允许远程主机连接本地的转发端口。
# X11Forwarding：是否允许进行 X11 转发。PrintLastLog：显示上次登入的信息!
# TCPKeepAlive：指定系统是否向客户端发送 TCP keepalive 消息。
# PermitUserEnvironment：指定是否允许 sshd(8) 处理 ~/.ssh/environment 以及 ~/.ssh/authorized_keys 中的 environment= 选项。
#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
X11Forwarding yes
#X11DisplayOffset 10
#X11UseLocalhost yes
#PermitTTY yes
PrintMotd no
#PrintLastLog yes
#TCPKeepAlive yes
#PermitUserEnvironment no


# Compression：是否可以使用压缩指令?
# UseDNS：指定 sshd(8) 是否应该对远程名进行反向解析，以检查此主机名是否与其IP地址真实对应。
# PidFile：指定在哪个文件中存放SSH守护进程的进程号
# MaxStartups：同时允许几个尚未登入的联机画面?
# PermitTunnel：是否允许 tun(4) 设备转发。
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS no
#PidFile /var/run/sshd.pid
#MaxStartups 10:30:100
#PermitTunnel no
#ChrootDirectory none
#VersionAddendum none



# no default banner path
# 将这个指令指定的文件中的内容在用户进行认证前显示给远程用户。"none"表示禁用这个特性。
#Banner none



# Allow client to pass locale environment variables
# 指定客户端发送的哪些环境变量将会被传递到会话环境中。指令的值是空格分隔的变量名列表(其中可以使用'*'和'?'作为通配符)。
AcceptEnv LANG LC_*



# override default of no subsystems
# 配置一个外部子系统(例如，一个文件传输守护进程)。值是一个子系统的名字和对应的命令行(含选项和参数)。
Subsystem	sftp	/usr/lib/openssh/sftp-server



# Example of overriding settings on a per-user basis
# 基于每个用户重写设置的示例
# Match：引入一个条件块。如果 Match 行上指定的条件都满足，那么随后的指令将覆盖全局配置中的指令。
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	PermitTTY no
#	ForceCommand cvs server

```