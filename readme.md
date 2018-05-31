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

实践：先修改gitNote,再添加一个LICENSE的文件. 
查看git status。
使用git add LICENSE后查看git status。
然后使用git commit。


-管理修改
git比其他版本控制系统设计的优秀，因为Git跟踪管理的是修改，而非文件。
可以做个测试：
第一步，对GitNote.md做一个修改，新加内容，然后添加.
第二步，再做一次修改
第三部，提交，并查看状态
发现此时第二次的修改没有被提交，显示Changes not staged for commit
第二次的修改未被放入暂存区，commit只提交stage中的修改，所以第二次的修改未被提交。

总结：git commit 只会提交已经add到暂存区的修改，没有添加是不会被提交的

-撤销修改






