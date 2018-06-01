#git Note

##创建Git版本库
mkdir learngit
cd learngit
pwd
Users/XXX/learngit

-git init


##将文件放入Git仓库
1.git add,
git add readme.txt
2.提交 git commit
git commit -m 'wrote a readme file' 

##git status
获取仓库当前的状态

##git diff
版本比较
提交修改同样需要两部
git add readme.txt
git commit -m 'add XXX'

git log
##版本回退
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

##工作区和暂存区
-工作区
你在电脑中的目录 learngit

###版本库（repository）
工作区中含有一个隐藏目录 .git, 这个就是Git的版本库
版本库中含有很多东西，其中最重要的是stage（或者叫index）的暂存区，
还用Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD

###缓存区
将文件添加到版本库是两步执行：
git add 实际就是将文件修改添加到暂存区
git commit 实际上就是把暂存区的所有内容提交到当前分支
简单理解为需要提交的文件修改放到暂存区，然后一次性提交暂存区的所有修改

实践：先修改gitNote,再添加一个LICENSE的文件. 
查看git status。
使用git add LICENSE后查看git status。
然后使用git commit。


##管理修改
git比其他版本控制系统设计的优秀，因为Git跟踪管理的是修改，而非文件。
可以做个测试：
1对GitNote.md做一个修改，新加内容，然后添加.
2再做一次修改
3提交，并查看状态
发现此时第二次的修改没有被提交，显示Changes not staged for commit
第二次的修改未被放入暂存区，commit只提交stage中的修改，所以第二次的修改未被提交。

总结：git commit 只会提交已经add到暂存区的修改，没有添加是不会被提交的

###撤销修改
-场景1：乱改了工作区某个文件，想直接丢弃工作区修改使用 git checkout -- file
-场景2：乱改了工作区某个文件，并add到了暂存区，想要丢弃分两步，第一步使用git reset HEAD file，回到场景1， 再git checkout -- file
-场景3：已经提交了不合适的修改，想要撤回版本，(前提是未推送到远程版本库)参考版本回退 git reset -hard HEAD^

###删除文件
Git中，删除也是一种修改操作，新添加一个新文件test.txt,add then commit,then rm test.txt
使用git status 查看，显示文件被删除
此时有两种选择：
1.删除 git rm test.txt     git commit -m 'remove test.txt' (手动删除，再add change to stage, 效果和git rm 是一样的)
2.恢复 git checkout -- test.txt


##远程仓库
-在用户目录下.ssh 创建ssh key
$ ssh-keygen -t rsa -C "youremail@example.com"
将id_rsa.pub内容复制到GitHub中的ssh

###添加远程库
1.在GitHub新创建一个仓库
2.git remote add origin git@github.com:XXX/learngit.git
3.git push -u origin master
以后每次本地提交后，只需要使用下面的命令即可推送最新修改
4.git push origin master

###从远程库克隆
假设从零开发，最好是先创建远程库，然后从远程库克隆
1.首先在GitHub创建一个新的仓库，gitskills，勾选创建readme.md.
2.git clone git@github.com:michaelliao/gitskills.git

##分支管理
###创建分支
git checkout -b dev
git checkout  add -b parameter mean create branch and switch to new branch
git branch dev
git checkout dev

git branch查看当前分支：
git branch： 会列出所有分支，在当前分支前标记*

git checkout master :切换到master
git merge dev ： merge Dev 到 master
git branch -d dev

查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

###解决冲突
准备一个新的分支feature1分支
git branch feature1 git checkout feature1     git checkout -b feature1
修改readme.md 

在分支feature1上提交

git add readme.md  git commit -m 'modify readme in feature1'

切换到master

git checkout master

Git会提示我们当前master的分支比远程的master分支要超前一个提交

在master分支上修改readme.md

提交

git add readme.md  git commit -m 'modify readme in master'

合并两个分支

git merge feature

产生冲突，需要手动解决。git status 也可以告诉我们冲突的文件：

查看readme的内容，解决冲突，提交
git add readme.md git commit -m 'conflict fixed'

删除分支feature1
git branch -d feature1

##分支管理策略
--no-ff方式的merge
git merge --no-ff -m 'merge with no-off' dev

总结：
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

##Bug分支
当接到修复任务的时候，创建一个分支issue-101，但是当前正在Dev上进行的工作还没有提交，且目前只进行到一半还没有办法提交。
使用stash功能，可以将当前工作现场存储起来，等待以后恢复

git stash list 查看所有的stash
git stash apply 恢复/git stash drop删除
git stash pop恢复并删除
git stash apply stash@{0}

###小结
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

##Feature 分支
创建一个新的分支进行工作 git checkout -b feature
开发完毕后，提交代码 
切回dev,准备合并 git checkout dev
取消分支开发。git branch -d feature 销毁失败，提示分支没有被合并
强行删除 git branch -D feature

##多人协作
当从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对于起来了，并且，仓库的默认名为origin
查看远程仓库信息：git remote
详细信息：git remote -v

###推送分支
推送分支，就是把该分支的所有本地提交推送到远程库。要制定本地分支。止痒，Git就把该分支推送到远程库随影的远程分支上：
git push origin master
git push origin dev

###抓取分支
多人协作时，大家都会网master和Dev分支上推送各自的修改
clone远程库时，默认情况下只能看到本地的master分支。使用git branch 查看
如果需要在Dev分支上开发，就必须创建远程origin的dev分支到本地，使用 git checkout -b dev origin/dev 创建本地分支

###push冲突
*假设你和别人都往origin/dev分支推送了他的提交，且修改了相同的文件，并试图推送
推送失败，因为你的推送和别人有冲突，此时Git会提示我们，先用git pull把最新的提交从origin/dev抓下来，然后在本地合并，解决冲突，再推送
*假如git pull 也失败了，原因是没有指定本地dev与远程分支origin/dev的链接，根据提示设置dev 和 origin/dev的链接： git branch --set-upstream-to=origin/dev dev
*再 git pull,然后手动合并冲突，提交，push

因此多人协作工作模式通常是：
*首先，可以试图用git push origin <branch-name>推送自己的修改；
*如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
*如果合并有冲突，则解决冲突，并在本地提交；
*没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
*如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。


##rebase
rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

##标签管理
##创建标签
git checkout master
git tag <name>

查看标签 git tag

标签对应的是最新提交的commit，如果要为以前的commit打tag,需要找到对应的commit id。
git tag v0.9 f52c833

创建带有说明的标签 -a 指定标签名，-m指定说明文字
git tag -a v0.1 -m 'version 0.1 released' 1094adb

小结

命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；

命令git tag可以查看所有标签。

命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
