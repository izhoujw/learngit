git Note

-创建Git版本库
mkdir learngit
cd learngit
pwd
Users/XXX/learngit

-git init


-将文件放入Git仓库
--1.git add,
git add readme.txt
--2.提交 git commit
git commit -m 'wrote a readme file' 

-git status
获取仓库当前的状态
-git diff
版本比较
提交修改同样需要两部
git add readme.txt
git commit -m 'add XXX'

-git log
版本回退
显示从最近到最远的提交日志
添加--pretty=online参数，精简输出

-git reset --hard HEAD^
回退到上一个版本

-git reset --hard HEAD^^
上上个版本

-git reset --hard HEAD~100
往前100个版本

-git reset --hard 1094a
恢复到被还原的版本
需要找到需要被还原的版本号：比如 1094a....

Git版本回退，是将只想当前版本的HEAD指针，指向上一个版本

-git reflog
记录每一次命令
找到你需要的版本号即可会退到此版本： git reset --hard commit_id

-工作区
你在电脑中的目录 learngit

-版本库（repository）
工作区中含有一个隐藏目录 .git, 这个就是Git的版本库
版本库中含有很多东西，其中最重要的是stage（或者叫index）的暂存区，还用Git伟我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD

-缓存区
将文件添加到版本库是两步执行：
git add 实际就是将文件修改添加到暂存区
git commit 实际上就是把暂存区的所有内容提交到当前分支
简单理解为需要提交的文件修改放到暂存区，然后一次性提交暂存区的所有修改

实践：先修改gitNote,再添加一个LICENSE的文件







