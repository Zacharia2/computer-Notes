https://www.jianshu.com/p/de013565eb74
/etc/default/grub

sudo update-grub

GRUB_CMDLINE_LINUX：一直生效
GRUB_CMDLINE_LINUX_DEFAULT：仅引导过程中生效


splash是一个不可或缺的参数，系统很多核心程序，都需要这个参数，且这个参数与可视化界面有关，没有就可能导致屏幕一片空白

quiet参数的作用：启动系统的过程中，如果没有quiet，那么内核就会输出很多内核消息，这些内核消息就包括的了系统启动过程中运行了哪些程序，如果系统运行正常，那么就不必要看到这些消息，所以就加上quiet

nomodeset：告诉内核，系统启动过程中，暂时不运行图像驱动程序。

text参数
