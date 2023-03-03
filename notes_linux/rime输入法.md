https://b23.tv/Aw5fWZw

新年好！
rime 是一个开源的跨平台输入法引擎，它的功能和可定制性非常强大，但是由于需要通过修改配置文件来设置，同时网上的资料也不是很多，因此有一定上手门槛。
由于 rime 只是一个输入法引擎，最终需要挂接具体的输入法软件来使用。fcitx 和 ibus 都支持 rime，虽然这两个输入法有挺大的区别，但如果使用 rime 则都是以外接 rime 引擎的方式运行，对输入法的配置都是通过修改 rime 的配置文件，fcitx 和 ibus 自己的很多配置是无效的，本文的配置方式同时适用于 fcitx 和 ibus 的 rime。
rime 的定制性是极其强大的，我对输入法的要求不高，只是配置了一下基本的功能，更进一步的设置请参考 rime 的官方 wiki（用户指南：https://github.com/rime/home/wiki/UserGuide和定制指南：https://github.com/rime/home/wiki/CustomizationGuide）
对于 windows 下的小狼毫输入法配置小鹤双拼，可以看我的投稿视频，或者专栏文章
安装 rime
以下包名适用于 Debian 和 archlinux
对于 fcitx，安装 fcitx-rime
对于 ibus，安装 ibus-rime
对于 fcitx5，安装 fcitx5-rime
之后需要启用 rime 输入源，fcitx 可以通过其设置工具设置，gnome 的 ibus 在 gnome 设置的键盘页面添加 rime 输入源。
下载输入方案
rime 的输入方案是独立维护的，一些发行版可能以 librime 或者类似的包提供输入方案的下载，由于输入方案也是作为配置文件的一部分，而我们对 rime 的定制涉及到修改输入方案，为了以后方便迁移配置不建议安装发行版打包的输入方案，而是自己下载需要的输入方案。
東風破
東風破(https://github.com/rime/plum)是 rime 项目提供的输入方案配置管理工具，它可以方便地下载并安装输入方案配置，适用于 linux 上的 rime 和 macos 上的鼠须管输入法
使用 plum 是十分简单的，执行下面的命令来将 plum 下载到当前目录：
curl -fsSL https://git.io/rime-install | bash
之后进入 plum 目录，以普通用户身份运行下面的命令：
./rime_install double_pinyin# 安装双拼方案
./rime_install emoji# 安装 emoji 方案
plum 会自动查找 rime 的配置目录然后下载输入方案到目录中，对于 ibus-rime，配置文件目录是 ~/.config/ibus/rime，对于 fcitx-rime，配置文件目录是 ~/.config/fcitx/rime，对于 fcitx5-rime 则是 ~/.config/fcitx5/rime
在 rime 的配置文件目录下就可以看到下载的输入方案
启用双拼
安装完双拼方案后会发现 rime 输入方案选单里是没有刚刚下载的双拼的，需要自己添加进去
在 rime 的配置文件目录下新建名为 default.custom.yaml 的文件，填入以下内容：
patch:
schema_list:
- {schema: double_pinyin_flypy}
这里使用的是小鹤双拼，自然码则是 double_pinyin，微软双拼是 double_pinyin_mspy，如果还需要其他输入方案，在 schema_list 下添加。
保存文件，重新部署 rime 生效，然后就可以打双拼了。
修改每页候选词数
rime 默认是每页显示 5 个候选词，要修改它，打开刚刚的 default.custom.yaml，在 patch 下（注意缩进）添加 "menu/page_size": 6（数字就是每页显示候选词个数）来自定义
修改后的 default.custom.yaml 应该像这样：
patch:
"menu/page_size": 6
schema_list:
- {schema: double_pinyin_flypy}
注意：rime 的配置文件都是 yaml 格式，如果配置文件不符合格式会使用默认配置（但不覆盖当前配置），请确保配置文件符合 yaml 语法
水平排列显示候选词
rime 默认是竖直显示候选词，我不太习惯，所以改成水平排列的
对于 ibus-rime，新建 ibus_rime.custom.yaml，对于 fcitx-rime 则应该是 fcitx_rime.custom.yaml，然后填入下面的内容：
patch:
"style/horizontal": true
网上流传的方法是把上面的内容保存为 ibus_rime.yaml，但是这样做已经过时了，现版本的 rime 会丢弃 ibus_rime.yaml 配置，应该使用 ibus_rime.custom.yaml 来代替。
模糊音设置
参考 明月拼音模糊音定制模板（https://gist.github.com/lotem/2320943），编辑 double_pinyin_flypy.schema.yaml 文件，在 speller/algebra 下的xform 字段之前添加对应的模糊音设置。我是前鼻音后鼻音不分，下面是我的配置文件的一部分：
speller:
alphabet: zyxwvutsrqponmlkjihgfedcba
delimiter: " '"
algebra:
- erase/^xx$/
- derive/^([jqxy])u$/$1v/
- derive/^([aoe])([ioun])$/$1$1$2/
- derive/([ei])n$/$1ng/# en =>eng, in =>ing
- derive/([ei])ng$/$1n/# eng =>en, ing =>in
- xform/^([aoe])(ng)?$/$1$1$2/
- xform/iu$/Q/
- xform/(.)ei$/$1W/
- xform/uan$/R/
其它的模糊音设置在定制模板里可以找到
启用 emoji
可以在打字的时候提供 emoji 建议
新建 double_pinyin_flypy.custom.yaml，将 emoji_suggestion.yaml 中的全部内容复制过来，保存，部署。
效果就像这样：
emoji 建议
配置文件同步
编辑 installation.yaml， 空白行填入 sync_dir: '同步目录'，然后修改 installation_id 的值为一个有意义的名字。Rime 执行同步时将会导出所有的配置文件和用户字典到 ~/同步目录/installation_id 文件夹下
我的 installation.yaml 配置如下：
distribution_code_name: "ibus-rime"
distribution_name: Rime
distribution_version: 1.5.0
install_time: "Mon Jan3 13:19:31 2022"
installation_id: "ibus-rime"
rime_version: 1.7.3
sync_dir: 'RimeSync'
以我的配置为例，执行同步后将会导出配置和用户字典在 ~/RimeSync/ibus-rime 文件夹下。
其中的 luna_pinyin.userdb.txt 文件就是明月拼音的用户字典文件（双拼方案是基于明月拼音的，使用明月拼音的词典），它记录了你的词频等信息，词库养得越久越好用。
要养成经常同步并备份的好习惯！
用户字典管理
rime 提供的词典管理工具是 rime_dict_manager，可以导入导出用户词库
导入用户词库
导入方法：
在 rime 的配置目录下执行 ：
rime_dict_manager -i 词典名 词典文件
对于明月拼音（以及双拼）,使用的词典是 luna_pinyin，所以命令应该是：
rime_dict_manager -i luna_pinyin 词典文件
注意：这个工具不会搜索 rime 的配置文件目录位置，只是在当前目录下生成转化的文件，所以必须在 rime 的配置文件目录下使用这个工具才能有效果！
导出用户词库
一般不需要手动进行这个操作，因为同步的时候会导出用户词库
导出方法：
在 rime 的配置目录下执行：
rime_dict_manager -e 词典名 输出的词典文件名
同时发布在我的个人博客

https://b23.tv/Aw5fWZw
