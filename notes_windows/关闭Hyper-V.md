bcdedit /set hypervisorlaunchtype off  

之后在输入以下命令查看是否关闭

bcdedit /enum  

如果关闭了会看到最后一行显示

hypervisorlaunchtype    Off  

（可选）运行输入services.msc

![[/images/Pasted image 20230110161505.png]]

找到HV主机服务，禁用，然后关闭重启电脑即可。 最后，我们的[虚拟机](https://so.csdn.net/so/search?q=%E8%99%9A%E6%8B%9F%E6%9C%BA&spm=1001.2101.3001.7020)就能正常打开了。