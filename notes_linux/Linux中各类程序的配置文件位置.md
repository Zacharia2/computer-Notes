# Linux中各类程序的配置文件位置

Linux中各类程序的配置文件位置
1.启动引导程序配置文件
LILO /etc/lilo.conf 
GRUB /boot/grub/menu.lst
2.系统启动文件核脚本
主启动控制文件 /etc/inittab 
SysV启动脚本的位置 /etc/init.d、/etc/rc.d/init.d或/etc/rc.d 
SysV启动脚本链接的位置 /etc/init.d/rc.d、/etc/rc.d/rc.d或/etc/rc.d 
本地启动脚本 /etc/rc.d/rc.local、/etc/init.d/boot.local或/etc/rc.boot里的文件
3.网络配置文件
.建立网络接口的脚本 /sbin/ifup 
保存网络配置数据文件的目录 /etc/network、/etc/sysconfig/network和/etc/sysconfig/network-scripts 
保存解析DNS服务的文件 /etc/resolv.conf 
DHCP客户端的配置文件 /etc/dhclient.conf
4.超级服务程序配置文件和目录
inetd配置文件 /etc/inetd.conf 
TCP Wrappers配置文件 /etc/hosts.allow和/etc/hosts.deny 
xinetd配置文件 /etc/xinetd.conf和/etc/xinetd.d目录里的文件
5.硬件配置
内核模块配置文件 /etc/modules.conf
6.硬件访问文件
Linux设备文件 /dev目录里 
保存硬件和驱动程序数据的文件 /proc目录里
7.扫描仪配置文件
SANE主配置 /etc/sane.d/dll.conf 
特定扫描仪的配置文件 /etc/sane.d目录里以扫描仪型号命名的文件
8.打印机配置文件
BSD LPD核LPRng的本地打印机主配置文件 /etc/printcap 
CUPS本地打印机主配置和远程访问受权文件 /etc/cups/cupsd.conf 
BSD LPD远程访问受权文件 /etc/hosts.lpd 
LPRng远程访问受权文件 /etc/lpd.perms
9.文件系统
文件系统表 /etc/fstab 
软驱装配点 /floppy 、/mnt/floppy 或/media/floppy 
光驱装配点 /cdrom 、/mnt/cdrom 或/media/cdrom
10.shell 配置文件
bash 系统非登录配置文件 /etc/bashrc 、/etc/bash.bashrc 或/etc/bash.bashrc.local 
bash 系统登录文件 /etc/profile 和/etc/profile.d 里的文件 
bash 用户非登录配置文件 ~/.bashrc 
bash 用户登录配置文件 ~/.profile
11.XFree86 配置文件核目录
XFree86 主配置文件 /etc/XF86config 、/etc/X11/XF86Config 或/etc/X11/XF86Config-4字体服务程序配置文件 /etc/X11/fs/config 
Xft 1.x 配置文件 /etcX11/XftConfig 
Xft 2.0配置文件 /etc/fonts/fonts.conf 
字体目录 /usr/X11R6/lib/X11/fonts 和/usr/share/fonts
12.Web 服务程序配置文件
Apache 主配置文件 /etc/apache 、/etc/httpd 或/httpd/conf 里的httpd.conf 或httpd2.conf 文件 
MIME 类型文件 与Apache 主配置文件在同一目录里的mime.types 或apache-mime.types
13.文件服务程序配置文件
ProFTPd 配置文件 /etc/proftpd.conf 
vsftpd 配置文件 /etc/vsftpd.conf 
NFS 服务程序的输出定义文件 /etc/exports 
NFS 客户端装配的NFS 输出 /etc/fstab 
Samba 配置文件 /etc/samba/smb.conf 
Samba 用户配置文件 /etc/samba/smbpasswd
14.邮件服务程序www.linuxidc.com配置文件
sendmail 主配置文件 /etc/mail/sendmail.cf 
sendmail 源配置文件 /etc/mail/sendmail.mc 或/usr/share/sendmail/cf/cf/linux.smtp.mc 或其他文件 
Postfix 主配置文件 /etc/postfix/main.cf 
Exim 主配置文件 /etc/exim/exim.cf 
Procmail 配置文件 /etc/procmailrc 或~/.procmailrc 
Fetchmail 配置文件 ~/.fetchmailrc
15.远程登录配置文件
SSH 服务程序配置文件 /etc/ssh/sshd_config 
SSH 客户端配置文件 /etc/ssh/ssh_config 
XDM 配置文件 /etc/X11/xdm 目录下 
GDM 配置文件 /etc/X11/gdm 目录下 
VNC 服务程序配置文件 /usr/X11R6/bin/vncserver 启动脚本和~/.vnc 目录里的文件
16.其他服务程序配置文件
DHCP 服务程序配置文件 /etc/dhcpd.conf 
BIND 服务程序配置文件 /etc/named.conf 和/var/named/ 
NTP 服务程序配置文件 /etc/ntp.conf 
From < https://www.cnblogs.com/gongjingyun123--/p/11255992.html> 
