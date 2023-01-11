
在网上看了很多，所有 Docker、虚拟机、编译安装、以及各种另辟蹊径的答案，都是面向日常繁重的业务没时间折腾而不得已做出的妥协和让步。

而我们面向技术的，**“从来都喜欢正面硬刚！”**

硬刚 Linux 软件安装依赖问题的办法有很多，我给他分为两大类！

**“一类合法，另一类暴力。”**

## 先说合法的解决方案

也是所有人都知道的解决方案：

```sh
sudo apt-get install xxxxx
```

一般情况下，它会连带软件的依赖一起安装。如果这个过程中依赖安装失败，就执行：

```sh
sudo apt-get -f install
```

一次不行两次，只要源里有，只要能保证依赖关系是顺畅的，再多的依赖多执行几次都能装完。

如果有依赖源里找不到。这个坑就踩不过去了，解决办法是：找到缺失的库的安装包手动下载下来。然后通过 `sudo dpkg -i xxxx.deb` 安装。

需要手动下载安装包的寻找主要有两个途径：

1.  百度找，直接搜包名 + 版本号并带上关键字 deb
2.  通过源。

百度直接找库就不多说了，额外说一下通过源怎么找。

你在网上搜 ubuntu 国内源。会找到很多类似这样的写法：

```text
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
```

这其实即是给`apt-get`工具配置的源地址，也是个实际的网址，你可以直接从浏览器里访问到，比如上面这个：

```text
https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
```

它其实代表的是：`https://mirrors.tuna.tsinghua.edu.cn/ubuntu/pool/xenial/` 这个路径下的 `main`、`restricted`、`universe`、`multiverse` 这几个目录。

`apt-get` 工具会在这四个的目录下自动检索对应的软件包下载并安装。

在一些特殊情况，比如机器网络受限，但浏览器开了代理可以访问外网的情况下。`apt-get` 无法从源里获取软件，你可以从这里手动找到对应的软件包下载下来然后使用 `dpkg` 安装。

刚才说道 `apt-get install` 无法修复依赖，通过手动下载然后把这些缺失的安装包装上之后，就可以通过 `apt-get` 把刚才装不上的包装上。

这是非常合理合法的解决方案。

再补充一种合法技巧，可以尝试用：

```text
apt-get install 本地软件包
```

这是因为：

**“依赖检测”** 和 **“软件安装”** 不是 `apt-get` 做的，而是 `dpkg` 做的。依赖不满足 **“自动修复依赖”** 才是 `apt-get` 做的。

所以，如果你下载了一个 deb 安装包通过 `dpkg` 安装，但依赖不满足的话，他只会提示你依赖缺失，但他不会自动寻找并安装依赖，虽然你仍然可以去下载安装缺失的依赖，但他如果缺失十个八个的，你再手动下载然后 `dpkg` 安装也不现实了。

举个例子：我这里下载了一个搜狗输入法的安装包，`dpkg -i` 无法安装，但是可以通过 `apt-get install` 装上：

![](images/Pasted%20image%2020230111094829.png)

要注意：通过 `apt-get` 安装本地软件一定要写路径，相对绝对都可以，但不能只写包名。不然它会去源里面找不会装本地的。

**上面的方案几乎可以解决 80% 的安装依赖问题。总结一下**：

-   安装软件就用：`sudo apt-get install xxxx`
-   遇到依赖问题：`sudo apt-get -f install`
-   如果有缺失无法安装，就去网上下，缺什么下什么，下载下来后 `sudo apt-get install ./xxxx` 把缺的包安装上，再装原来的包。


Ubuntu系统依赖的通用解决工具: https://github.com/sherlcok314159/ubuntu-requirements-solve


apt安装软件包的时候，有时会出现安装出错，然后你remove的时候又出现了循环依赖的提示。这个时候，`apt auto remove`，`apt --fix-broken install` 等等命令都是不起作用的。

这个时候你需要使用dpkg，如下

`dpkg --remove --force-remove-reinstreq [需要卸载的包名]`，一个一个把依赖的包都卸载掉，轻松解决。

  
  
作者：FancyGo  
链接：https://zhuanlan.zhihu.com/p/572827131  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


### 下列软件包有未满足的依赖关系/但是它将不会被安装/无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系

1.  什么 依赖冲突 安装什么库。
2.  若错误中出现 >=的情形，直接安装这个库依赖。比如：
```bash
libglib2.0-dev : 依赖: libmount-dev (>= 2.28) 但是它将不会被安装
那么直接执行如下命令即可安装。

sudo apt install libmount-dev
```

3.  若出现了`=`，就安装等号后面的这个版本。
```sh
libx11-dev : 依赖：libx11-6 (=2:1.6.12-1)

# 那么执行命令安装，即可。
sudo apt-get install libx11-6=2:1.6.12-1
```

4. 最后再回头安装目标软件。


## 如何知道缺了哪个linux依赖库？

1.查看依赖的库：  
```sh
objdump -x xxx.so | grep NEEDED
```

2.查看可执行程序依赖的库：  
```sh
objdump -x 可执行程序名 | grep NEEDED
```

3.查看缺少的库：

```sh
ldd xxx.so  
```

如果某个依赖的库不存在，会打印类似“xxx.so not found”的提示