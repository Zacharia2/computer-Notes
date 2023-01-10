## 1. 更新系统
	命令	解释
	pacman -Syu	对整个系统进行更新（常用）
	pacman -Syy	强制更新
	pacman -Syudd	使用 -dd跳过所有检测
## 2. 搜索包
	命令	解释
	pacman -Ss keyword	在仓库中搜索含关键字的包（常用）pacman -Ss '^fcitx-'
	pacman -Qs keyword	搜索已安装的包（常用）pacman -Qs '^fcitx-'
	pacman -Qi package_name	查询本地安装包的详细信息
	pacman -Ql package_name	列出该包的文件
	pacman -Fs keyword	按文件名查找软件库
	pacman -Si package_name	显示远程软件包的详尽的信息
	pacman -Qii package_name	使用两个 -i 将同时显示备份文件和修改状态
	pacman -Ql package_name	要获取已安装软件包所包含文件的列表
	pacman -Fl package_name	查询远程库中软件包包含的文件
	pacman -Qk package_name	检查软件包安装的文件是否都存在
	pacman -Fo /path/to/file_name	查询文件属于远程数据库中的哪个软件包
	pacman -Qdt	要罗列所有不再作为依赖的软件包(孤立orphans)
	pacman -Qet	要罗列所有明确安装而且不被其它包依赖的软件包
	pactree package_name	要显示软件包的依赖树
	whoneeds package_name	检查一个安装的软件包被那些包依赖pkgtoolsAUR中的whoneeds
	pactree -r package_name	检查一个安装的软件包被那些包依赖
## 3. 安装包
	命令	解释
	pacman -S package_name	执行 pacman -S firefox 将安装 Firefox（常用）
	pacman -Sy package_name	将在同步包数据库后再执行安装。
	pacman -Sv package_name	在显示一些操作信息后执行安装。
	pacman -U local_package_name	安装本地包，其扩展名为pkg.tar.gz或pkg.tar.xz
	pacman -U url	安装一个远程包（不在 pacman 配置的源里面）
## 4. 删除包
	命令	解释
	pacman -R package_name	该命令将只删除包，保留其全部已经安装的依赖关系
	pacman -Rs package_name	在删除包的同时，删除其所有没有被其他已安装软件包使用的依赖关系（常用）
	pacman -Rsc package_name	在删除包的同时，删除所有依赖这个软件包的程序
	pacman -Rd package_name	在删除包时不检查依赖
## 5. 其他用法
	pacman -Sw package_name	只下载包，不安装。
	pacman -Sc	清理未安装的包文件（常用）包文件位于 /var/cache/pacman/pkg/ 目录
	pacman -Scc	清理所有的缓存文件（常用）
