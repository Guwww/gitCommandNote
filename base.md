    touch file  新建文件

    mkdir   新建文件夹  

进入项目才可以设置版本控制：

    git config --global user.name xxx   设置名字
    git config --global user.email xxx  设置邮箱
    git config --global --list 查看全局信息




对比操作：

    git diff    工作区和暂存区文件对比

    git diff --cached(--staged)  暂存区与版本库对比

    git diff master(分支名称)  git diff HEAD -- file    工作区与版本库对比 




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

    git branch  --merged		查看当前分支下所合并的分支

    git branch  --no--merged 	查看未合并的分支

    git branch  -d   file 	    删除分支 （未合并的分支不能删除）

    git branch -D file 	    强制删除未合并的分支

