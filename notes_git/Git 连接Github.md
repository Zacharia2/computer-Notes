

	1. 配置ssh：$ssh-keygen -t ed25519 -C "your_email@example.com" 
		a. 按下enter(默认位置创建文件)  /c/Users/you/.ssh/id_algorithm
		b. 填写两次密码
		c. 添加ssh私钥到github账号：复制公钥信息到剪贴板，点击头像打开并设置，点击setting，点击new ssh key。
	2. 测试连接可行性：ssh -T git@github.com ，和公钥匹配时则键入yes
	3. 修改/.git/config 文件 url 字段为仓库Clone选项中的ssh连接。

大功告成。



git config --global user.name "Zacharia2"

git config --global user.email "1947114574@qq.com"