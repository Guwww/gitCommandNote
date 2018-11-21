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
git  rm file  工作区文件手动删除  可以对应删除暂存区的

git rm -f   file ,  git rm  file 	工作区 暂存区 都会删除

git rm --cached  file	  只删除暂存区  不删除工作区