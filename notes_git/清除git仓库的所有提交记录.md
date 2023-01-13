
# 如何清除git仓库的所有提交记录，成为一个新的干净仓库

1. 切换到新的分支

    `git checkout --orphan tmp_branch`

2. 缓存所有文件（除了.gitignore中声明排除的）

    `git add -A`

3. 提交跟踪过的文件（Commit the changes）

    `git commit -am "commit message"`

4. 删除master分支（Delete the branch）

    `git branch -D main` # 注意：你的主分支也可能是master

5. 重命名当前分支为main（Rename the current branch to main）

   `git branch -m main`  # 注意：你的主分支也可能是main

6. 提交到远程master分支 （Finally, force update your repository）

    `git push -f origin main` # 注意：你的主分支也可能是main

通过以上几步就可以简单地把一个Git仓库的历史提交记录清除掉了，不过最好还是在平时的开发中严格要求一下提交日志的规范，尽量避免在里面输入一些敏感信息进来。
