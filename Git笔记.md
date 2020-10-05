# Git笔记

+++

#### 初始化一个git库

git init

#### 添加文件

git add

#### 提交git

git commit -m "对更改有效的描述"

#### 查看修改内容

git diff

#### 查看修改记录

git log

#### 版本回退

git reset --hard HEAD

ps. 上一个版本就是`HEAD^`; 

上上一个版本就是`HEAD^^`; 

往前100个版本就是`HEAD~100`

#### 版本恢复

git reset --hard commit_id

#### 查看提交历史

git reflog

#### 查看文本内容

cat <file>

#### 撤销修改

先删除该删除的内容

用命令`git checkout -- <file>`可以直接丢弃工作区的修改

用命令 `git reset HEAD <file>`可以把暂存区的修改撤销掉，重新放回工作区，然后进行上一行修改

#### 删除文件

手动删完文件，然后 `git rm <file>` 删掉，再 `git commit`

删完发现删错了，如果版本库里还有，通过 `git checkout -- <file>`可以恢复到最新版本

ps. `git checkout` 其实是==版本库里的版本替换工作区的版本==，无论工作区是修改还是删除，都可以“一键还原”，可以说最近一次add的内容会丢失

+++

#### 添加远程库

关联远程库 `git remote add origin git@git.com:server_name/repo_name.git`

第一次推送master分支内容 `git push -u origin master`

ps. 加上参数 `-u` 不仅推送master，还把本地 `master` 和远程 `master` 关联起来，以后推送或拉去可以简化命令

此后关联 `git push origin master`

#### 从远程库中克隆

`git clone git@github.com:server_name/repo_name.git`

***

#### 创建与合并分支

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

丢弃一个没有被合并过的分支，可通过`git branch -D <name>`强行删除

#### 解决冲突

git无法自动合并分支时，就必须首先解决冲突（手动更改为我们希望的内容），然后再提交，再合并。

`git log --graph`可以看到分支合并图

#### 分支管理策略

==key==

合并时，`git merge --no--ff -m"描述“ <name>`

`--no--ff`参数表示禁用`Fast forward`

`-m`本次合并要创建一个新的commit

ps. `--no--ff`合并后的历史有分支；`fast forward`合并后看不出来曾经做过合并

#### Bug分支

`git stash` 可以把当前工作现场“储藏”起来

`git stash list` 查看储藏的工作现场

>两种办法可以恢复工作现场
>
>> * `git stash apply`恢复，但是stash内容并不删除，要用`git stash drop`删除
>> * `git stash pop`恢复的同时把stash内容也删了

==key==

把master分支上修复的bug合并到当前分支可用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支