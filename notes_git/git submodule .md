# git子模块

添加子模块：`git submodule add https://github.com/L-M-Sherlock/sm18-lazy-package`

克隆子模块：`git clone --recursive https://github.com/L-M-Sherlock/supermemo.guru-cn.git`


```yaml
gitmodules文件
[submodule "myrepo_path/submodule_path"]
    path = myrepo_path/submodule_path
    url = https://github.com/L-M-Sherlock/sm18-lazy-package
    fetch = +refs/heads/*:refs/remotes/origin/*
    ignore = all


[submodule "sm18-lazy-package"]
    path = sm18-lazy-package
    url = https://github.com/L-M-Sherlock/sm18-lazy-package
```