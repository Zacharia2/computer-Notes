https://www.jianshu.com/p/de013565eb74

/etc/default/grub

sudo update-grub

GRUB_CMDLINE_LINUX：一直生效
GRUB_CMDLINE_LINUX_DEFAULT：仅引导过程中生效


splash是一个不可或缺的参数，系统很多核心程序，都需要这个参数，且这个参数与可视化界面有关，没有就可能导致屏幕一片空白

quiet参数的作用：启动系统的过程中，如果没有quiet，那么内核就会输出很多内核消息，这些内核消息就包括的了系统启动过程中运行了哪些程序，如果系统运行正常，那么就不必要看到这些消息，所以就加上quiet

nomodeset：告诉内核，系统启动过程中，暂时不运行图像驱动程序。

text参数


编辑Grub
$ sudo vim /etc/default/grub
更改文件
把下面一行：
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
替换为：
GRUB_CMDLINE_LINUX_DEFAULT="text"
取消如下一行的注释：
#GRUB_TERMINAL=console
保存退出。
更新grub
$ sudo update-grub
执行下面命令默认启动到命令行：
$ sudo systemctl set-default multi-user.target
重启系统
$ sudo reboot或者init 6
如果想回到启动是进入桌面系统 执行如下命令启动到桌面：
$ sudo systemctl start lightdm
要恢复默认启动到桌面，执行：
$ systemctl set-default graphical.target
重启系统
$ sudo reboot或者init 6
