CMD_MANNUA

1.Cmd

-   /k prompt 修改命令符
-   /k title 修改标题
-   /t:gf 修改前景色和背景色 G背景色 F前景色  
    0黑色 1蓝色 2绿色 3浅绿 4红色 5紫色 6黄色 7白色 8灰色 9浅蓝 A浅绿 B浅蓝 C浅红 D浅紫色 E浅黄 F亮白色

2.Dir 显示磁盘目录

-   /p 分屏查看内容
-   /w 只显示文件名

3.PingTTL 存在时间 初始值-返回值=路由器数

4.Netstat 显示网络连接、路由表和网络接口信息，统计正在连接的网络

-   -r 显示本机路由表的内容
-   -s 显示每个协议的使用状态
-   -n 以数字表格形式显示地址和端口
-   -a 显示所有主机的端口号

5.Winipcfg

6.Tracert 显示数据包到达目标主机所经过的路径，和到达每个节点的时间

-   格式：tracert ip [参数]...
-   -d 不解析目标主机的名字
-   -h 搜索到目标地址的最大跳跃数
-   -j 按照主机列表中的地址释放路由资源
-   -w 指定超时时间间隔，默认毫秒

7.IPConfig 显示当前TCP/IP配置的参数值

8.arp TCP/IP协议，用来确定对应IP地址的网卡物理地址（MAC）先ping

-   -a 查看高速缓存中的所有项目-a = -g
-   -a ip 只显示与该接口相关的内容
-   -s ip 手动配置静态项目
-   -d ip 手动删除静态项目

9.Route 显示、手动添加修改路由表

-   print 显示路由表中的当前项目
-   add 添加项目
-   change 修改数据的传输路由，不能修改数据的目的地
-   delete 删除路由

10.Md建立子目录

-   格式：md 盘符:路径（子目录名）

11.Rd删除子目录

-   格式：rd 盘符:路径（子目录名）

12.Path 路径设置 设备可执行文件的搜索路径，只对文件有效

-   格式：path [盘符1]目录[路径1];[盘符2]目录[路径2];..... path[盘符1][路径1]; 设置可执行文件的搜索路径 path 取消所有路径 path 显示目前所设的所有路径

13.Tree 显示磁盘目录结构

-   无参 只显示目录
-   /f 显示所有目录及目录下的文件
-   >prn 把所列目录及目录中的文件名打印输出

14.Delete 删除整个目录

15.Vol 显示磁盘卷标

-   格式：vol 盘符:

16.Copy 文件复制

-   copy 源文件 目标文件目录
-   “*”，“？”通配符
-   con 从键盘上输入数据建立文件

17.Xcopy 目录复制

-   格式：Xcopy 源目录 目标目录
-   /s 拷贝源目录下及子目录中的所有文件 否则 只拷贝源目录下文件
-   /s /e 支持拷贝空目录
-   /v 对拷贝的扇区进行校验

18.Type 显示文件内容 （ascll）

-   格式：type 源文件
-   more 分屏显示
-   >prn 打印文件内容

19.Ren 重命名文件

-   格式：ren 源文件 新文件名
-   允许使用通配符更改一组文件名，或扩展名。

20.Attrib 修改文件属性

-   r 设为只读
-   -r 取消只读
-   a 设为档案
-   -a 取消档案
-   h 设置隐藏
-   -h 取消隐藏
-   s 设为系统
-   -s 取消系统
-   /s 对当前目录下的所有子目录及文件做设置

21.Del 删除指定文件

-   /p 询问是否删除
-   不能删除隐藏或只读文件, 可以使用通配符

22.Mem查看当前内存使用情况

-   /c 显示内存使用情况
-   /f 显示常规内存剩余大小和UMB可用区域大小
-   /m 显示该模块性质及使用内存地址 、大小
-   /p 分屏查看

23.Echo 打开关闭回显功能，或显示消息

-   格式 echo [{on off}] [消息]

24.@ 隐藏命令符

25.Goto 跳转到指定标签

-   格式:goto 标签

26.rem 注释命令

27.pause

28.Call 调用另一个批处理并继续运行

-   格式 call 源文件名 (.bat .cmd)

29.start 调用外部程序 dos 命令 命令行程序

-   入侵常用参数
-   MIN 开始时最小化
-   Separate 在分开的空间内开始16位的应用程序
-   HIgh 在高优先级类别启动程序
-   Raltime 在reltime优先级启动程序
-   wait 启动程序并等待程序结束
-   parameters

30.mklink 创建软连接

-   mklink [] 快捷方式 源文件
-   /D 创建目录符号链接。默认为文件符号链接。
-   /H 创建硬链接而非符号链接。
-   /J 创建目录联接。
-   Link 指定新的符号链接名称。
-   Target 指定新链接引用的路径 (相对或绝对)。

技巧

取脚本运行目录 ~I - 删除任何引号(")，扩充 %I %~fI - 将 %I 扩充到一个完全合格的路径名 %~dI - 仅将 %I 扩充到一个驱动器号 %~pI - 仅将 %I 扩充到一个路径 %~nI - 仅将 %I 扩充到一个文件名 %~xI - 仅将 %I 扩充到一个文件扩展名 %~sI - 扩充的路径只含有短名 %~aI - 将 %I 扩充到文件的文件属性 %~tI - 将 %I 扩充到文件的日期/时间 %~zI - 将 %I 扩充到文件的大小

系统程序

control 打开控制面板

Appwiz.cpl 打开控制面版里添加删除程序

write 写字板

wiaacmgr 扫描仪和照相机向导

Msconfig 系统配置实用程序

mspaint 画图板

mstsc 远程桌面连接

magnify 放大镜实用程序

mmc 打开控制台

mobsync 同步命令

dxdiag 检查DirectX信息

devmgmt.msc 设备管理器

dfrg.msc 磁盘碎片整理程序

diskmgmt.msc 磁盘管理实用程序

dcomcnfg 打开系统组件服务

ddeshare 打开DDE共享设置

dvdplay DVD播放器

notepad 打开记事本

nslookup 网络管理的工具向导

ntbackup 系统备份和还原

narrator 屏幕“讲述人”

netstat -an (TC)命令检查接口

sysedit 系统配置编辑器

sigverif 文件签名验证程序

shrpubw 创建共享文件夹

secpol.msc 本地安全策略

services.msc 本地服务设置

sfc.exe 系统文件检查器

sfc /scannow-windows 文件保护

tsshutdn-60 秒倒计时关机命令

taskmgr 任务管理器

eventvwr 事件查看器

eudcedit 造字程序

explorer 打开资源管理器

packager 对象包装程序

perfmon.msc 计算机性能监测程序

regedit 注册表编辑器

rsop.msc 组策略结果集

rononce -p 15秒关机

regsvr32 /u *.dll停止dll文件运行

cmd.exe 命令提示符

chkdsk 磁盘检查

certmgr.msc 证书管理实用程序

calc 启动计算器

charmap 启动字符映射表

compmgmt.msc 计算机管理

cleanmgr 垃圾整理

ciadv.msc 索引服务程序

osk 打开屏幕键盘

odbcad32 ODBC数据源管理器

lusrmgr.msc 本机用户和组

logoff 注销命令

iexpress 木马捆绑工具，系统自带

Nslookup-IP 地址侦测器

fsmgmt.msc 共享文件夹管理器

utilman 辅助工具管理器

gpedit.msc 组策略

cleanmgr 垃圾整理

winver 检查Windows版本