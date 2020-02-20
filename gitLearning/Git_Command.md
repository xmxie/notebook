## 创建仓库

| 命令           | 作用                        |
| -------------- | --------------------------- |
| **git init**   | 把目录变成git可以管理的仓库 |
| **git add**    |                             |
| **git commit** | -m "distribution"           |

## 版本回溯

| 命令                       | 作用                                                         |
| -------------------------- | ------------------------------------------------------------ |
| **git status**             | 查看工作区状态                                               |
| **git diff**               | 查看修改文件                                                 |
| **git reset --hard**       | 版本回退，hard后接版本号或使用HEAD指针                       |
| **git reset HEAD \<file>** | 回退暂存区                                                   |
| **git restore **           | 最新版git的回退命令                                          |
| **git log**                | 查看提交历史<br>--pretty=oneline 仅显示一行信息              |
| **git reflog**             | 查看命令历史                                                 |
| **git checkout --file**    | 还原到当前分支最近的版本<br><u>git checkout \<branch>切换分支</u> |
| **git rm**                 | 从版本库中删除某文件                                         |

## 远程仓库

| 命令                                             | 作用                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| **ssh-keygen -t rsa -C "youremail@example.com"** | 生成RSA格式的SSH key                                         |
| **git remote**                                   | 完整用法：**git remote add origin git@server-name: path/repo-name.git**<br>关联远程仓库<br><u>git remote remove \<name></u> 删除远程仓库 |
| **git push**                                     | 第一次使用：**git push -u origin master**<br>将本地分支推送到远程仓库，第一次使用时 -u 来将本地的master分支和远程的master分支关联起来 |
| **git clone**                                    | 克隆项目到本地<br>默认git://协议时使用ssh，通过ssh支持的原声git 协议速度最快 |

## 分支管理

| 命令                               | 作用                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| **git branch \<branch_name>**      | 创建分支<br>git branch 本身用于查看所有分支<br><u>-d 用于删除分支<br>-D 强制删除分支</u> |
| **git checkout -b \<branch_name>** | 创建并切换分支<br>相当于以下两条命令<br>git branch dev<br>git checkout dev<br>**<u>git checkout -b dev origin/dev**</u> 创建远程origin的dev分支到本地 |
| **git merge \<name>**              | 合并分支<br><u>--no-ff 参数，禁用Fast forward</u>，创建新的commit，同时需要使用-m参数对commit进行描述（ <u>fast forward 合并就看不出来曾经做过合并</u>。） |
| ***git switch***                   | 最新版的git，用于切换分支的命令<br><u>-c 用于创建并切换分支</u> |
| **git stash**                      | 保存当前工作区<br><u>git stash list 显示stash临时保存的工作区<br>git stash pop 恢复并删除临时保存的工作区<br>git stash apply 恢复工作区，但不删除临时文件<br>git stash drop 删除临时保存的工作区</u> |
| **git cherry-pick \<id>**          | 复制一个特定的提交到当前分支                                 |
| **git pull**                       | 拉取远程仓库的最新更新                                       |
| **git rebase**                     | 将本地的提交整理为一条线，便于查看提交历                     |

## 标签管理

## 

| 命令                                      | 作用                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| **git tag \<name> \<id>(可选)**           | 为某一次提交打上tag<br>git tag -a \<tag_name> -m "distribution"<br>git tag 可以查看所有标签<br>git tag -d 删除标签 |
| **git push origin \<tag_name>**           | 将标签推送到远程<br><u>git push origin --tags</u> 推送所有本地标签 |
| **git push origin :refs/tags/<tag_name>** | 删除远程的标签（需先删除本地标签）                           |





### git 中文乱码问题

git config --global core.quotepath false