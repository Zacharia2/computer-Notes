>相关参考信息:[Renaming user account doesn't change profile path - Windows Client | Microsoft Docs](https://link.zhihu.com/?target=https%3A//docs.microsoft.com/en-us/troubleshoot/windows-client/user-profiles-and-logon/renaming-user-account-not-change-profile-path)
>已剪辑自: [http://www-quic.zhihu.com/question/428394154/answer/2471999466](http://www-quic.zhihu.com/question/428394154/answer/2471999466)

开始：

1 - 注销或者退出当前账户登录，使用一个新的管理员账号登录，没有就先新建一个。注意别偷懒，直接使用当前账户修改自己的用户目录很危险，因为它正在使用呢。

注意，网上有一些方法是直接启用本地自带的Administrator隐藏账户，完成修改后再禁用，不需要新建一个，  
在“计算机管理”中找到“本地用户组”，点击打开，右侧可见Administrator用户，直接取消禁用，之后就可以在开始菜单切换到Administrator账户了  
但是这只适用于专业版，家庭版没有这个设置，不通用，还是建议新建一个比较好，回头直接删除就行了

2 - 用新建的管理员账户登录后，找到想要修改的用户文件夹，比如用户名原来是 小明，用户文件夹就是C:\Users\小明。如果想要修改为C:\Users\Ming，就直接重命名文件夹为Ming。

3 - 接着打开[注册表](https://www.zhihu.com/search?q=%E6%B3%A8%E5%86%8C%E8%A1%A8&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22:%22answer%22%2C%22sourceId%22:2471999466%7D)，找到如下位置，注意别弄错了，找到你要修改的账户对应的SID，点进去，通过ProfileImagePath判断一下哪一个才是。把右侧ProfileImagePath的值改为你刚才修改好的路径：C:\Users\Ming，也就是重新指定 用户配置路径

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList\<你的sid>\

![](修改win10用户文件夹名称-1.png)

这样就修改完成了，接着退出你新建的管理员账户，登录你修改后的账户Ming即可

第一步新建的管理员账户已经没用了，你完全可以删除掉，它只是我们用来修改 小明 的。