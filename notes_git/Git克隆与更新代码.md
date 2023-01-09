# Git克隆与更新代码

⼀、克隆项⽬

git clone https://github.com/defnngj/project-name

⼆、更新项⽬
这次更新我们项⽬做了较⼤的变更，创建⽂件的⽂件与⽂件夹，并且删除了原有⽂件。
通过“git status” 命令查看当前变更。通过变更信息可以看出，删除了test_case.py⽂件。这个删除只是在项⽬⽬录下进⾏删除，Git对此⽂件留有记忆，所以要通过 “git rm” 命令将其删除。
如果删除的是⽂件同样⽤此命令，例如，“git rm test_case/”。
如果删除的⽂件名带空格，则需要通过双引号将⽂件名引起来，例如，“git rm “test case.py” ”。
“git add” 命令对当前⽬录下的⽂件添加跟踪。
“git commit” 命令将添加⽂件提交到本地仓库。
“git push” 将本地项⽬提交到远程仓库GitHub。
除第⼀次下载项⽬需要通过 “git clone” 将项⽬克隆到本地外,后续再使⽤ “git pull” 命令时会直接将更新拉取到本地。
提⽰: 为了避免冲突我们应该形成良好的习惯，在每次 push 代码之前先把服务器上最新的代码 pull 到本地。


切换到分支B `git checkout B` 
添加可执行文件权限 `git add --chmod=+x path/to/file`
    

