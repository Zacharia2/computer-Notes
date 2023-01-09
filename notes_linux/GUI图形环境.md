X Window   
Xorg是 X11 窗口系统的一个开源实现。
X包括X server和X client，它们之间通过X protocol通信。X将protocol（协议）封装为命令原语（X command primitives），以库的形式（xlib或者xcb）向client提供接口。X client（即应用程序）利用这些API，可以向X server发起2D或3D的绘图请求。
X作为Windowing system中的一种，只提供了实现GUI环境的基本框架，其它的UI设计所需的button、menu、window title-bar styles等基本元素，则是由第三方的应用程序提供。这些应用程序主要包括：窗口管理器（window manager）、GUI工具集（GUI widget toolkit）和桌面环境（desktop environment）。
GUI工具集是Windowing system之上的进一步的封装。提供尽可以绘制基本图形的Api，这样一些框架就可以根据X封装出更便于使用的工具。例如Microwindows、GTK+、QT等。
linux-->X服务器<-[X协议]->窗口管理器（桌面环境）-->X应用程序。
linxu 窗口管理器（WM)：
图形用户界面的视窗系统中，窗口管理器（Window Manager）是控制窗口行为与位置的软件。

linux 桌面环境：
桌面环境可能仅仅是一个简单的窗口管理器， 也可能是一个像 KDE 或者 GNOME这样的完整桌面应用程序套件。
	现代重量级的桌面环境
1）Unity
2）Gnome
传统的重量级桌面环境
1）Cinnamon
2）KDE
3）Zorin Desktop
传统的轻量级桌面环境
1）MATE
2）XFCE
3）LXDE
4）Enlightenment

Linux显示管理器（display manager）
显示管理器或登录管理器是一个在启动最后显示的图形界面,即登录界面(显示管理器),是进到桌面环境之前的用户登录界面。
注意: 如果使用 桌面环境,应该尽量使用对应的显示管理器。
	• XDM: X 显示管理器 (xorg-xdm)
	• GDM: GNOME 显示管理器 (gdm)
	• KDM: KDE 显示管理器 (kdebase-workspace)
	• SLiM: 简单登录管理器 (slim)
Warning: slim登录管理器已经停止开发，不推荐使用
	• LXDM: LXDE 显示管理器 (独立于桌面环境) (lxdm)
	• Qingy: getty 使用 DirectFB 的替代者 (qingy)
	• wdm: WINGs 显示管理器 (wdm)
	• CDM: 控制台显示管理器 (available in the AUR: cdm-git)
	• LightDM: Ubuntu 开发的 GDM 替代品，使用 WebKit (位于AUR: lightdm, lightdm-bzr)
From < https://blog.csdn.net/sole_cc/article/details/42804355> 
