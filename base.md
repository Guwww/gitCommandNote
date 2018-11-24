    touch file  新建文件

    mkdir   新建文件夹  

    cd:    切换目录

    cd: .. 回退到上一个目录

    pwd     显示当前目录路径

    ls  列出当前目录中所有文件




进入项目才可以设置版本控制：

    git config --global user.name xxx   设置名字
    git config --global user.email xxx  设置邮箱
    git config --global --list 查看全局信息




对比操作：

    git diff    工作区和暂存区文件对比

    git diff --cached(--staged)  暂存区与版本库对比

    git diff master(分支名称)  git diff HEAD -- file    工作区与版本库对比 


查看文件状态：

    git status (未追踪Untracked，已修改Modifed，已暂存)

    git status -s 简化打印状态。

    ?? untracked file

    A(green)    git add 的 file

      M(red)    change  but not git add 

    M(green)M(red)      change and git add git commit  and  again change 

    M(green)    change and git add

    D       delete




撤销操作：

    (1)git checkout -- file

        (1)file在工作区change,没有add到暂存区，==>撤销修改就回到和版本库一模一样的状态
        
        (2)file add到暂存区，又再次change ==>撤销修改就回到添加到暂存区后的状态。 
            tips: git checkout -- file 命令中的--很重要，没有--，就变成了“切换分支”命令.

    (2)git reset HEAD file   add到暂存区的文件(未commit)，撤回到工作区

    (3)file 不仅add了，而且commit了。可以用版本回退操作。
            前提是：还没有把自己的本地版本库推送到远程。

    <!-- git commit --amend  撤销提交操作(2次修改，1个添加提交，)  更改上次提交 -->



删除操作：

    工作区文件 (没添加到暂存区)  可以随时删除

    file add到暂存区=>删除操作

        git rm file  工作区 暂存区 都会删除

        (1) git rm -f   file	工作区 暂存区 都会删除

        (2) git rm --cached  file	  只删除暂存区  不删除工作区

            tips:删除操作后，需要git  commit操作。


移动操作：

    git mv file nextfile/file  移动文件到另一个文件夹

    git mv oldname newname  or  工作区直接重命名文件 （原理：删除原文件，重新命名一个文件，赋值源文件的内容 ==>） 
    
    后续 需要删除 git rm 原file   git add 新命名file


版本回退操作：

    git log --pretty=oneline    打印版本号   
    git reflog      获取commit_id 


    git reset --hard  HEAD^     回到过去上一个版本

    git reset --hard HEAD~num   回到过去的num个版本

    git reset --hard commit_id  回到commit_id(过去未来都可以)版本   在版本之间来回穿梭



分支操作：

    git  branch     查看分支

    git  branch  file   创建分支

    git checkout file   切换分支

    git checkout -b  file      创建 切换 分支

    git merge file      合并分支
        tips:合并某个分支，需要先切换到主分支。

    git branch --merged		查看当前分支下所合并的分支

    git branch --no--merged 	查看未合并的分支

    git branch -d file 	    删除分支 （未合并的分支不能删除）

    git branch -D file 	    强制删除未合并的分支



 克隆远程库操作：

    git clone url  就可以实现克隆到本地制定的文件夹下



分支冲突解决：

    当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

    解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

    git log --graph --oneline --decorate 查看合并分支图


分支管理策略：

    通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

    如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

    git merge --no-ff -m '描述文字'  branchName

    合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，
    
    而fast forward合并就看不出来曾经做过合并。

Bug分支：

    git stash  隐藏暂存区的修改。

    使用条件：
        
        1.add 并 commit  是正常的普通的dev分支，切换分支会隐藏
        
        2.新文件 add 没有 commit    stash 切换分支也会隐藏
        
        3.修改的文件 没有 add   stash  切换分支也会隐藏

        4.没有add没有commit是普通文件，切换分支也不会隐藏起来


    git stash apply  恢复  git stash drop 删除stash

    git stash pop  恢复并删除

    git stash list 查看stash内容

    git stash apply stash@{0}  恢复制定stash



多人协作：

    git remote     查看远程库

    git remote -v   详细信息

    git push origin branchName 推送到远程
    

    master分支是主分支，因此要时刻与远程同步.

    dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步.

    bug分支只用于在本地修复bug，就没必要推到远程


    git checkout -b dev origin/dev   创建远程origin的dev分支到本地

    开发人员都改这个文件 发生冲突  先 git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送

    git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接:

        git branch -set--upstream-to==origin/dev dev

    再 pull  




多人协作的工作模式通常是：

    首先，可以试图用git push origin <branch-name>推送自己的修改；

    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    如果合并有冲突，则解决冲突，并在本地提交；

    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

    如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，

    用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。






