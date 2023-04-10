#### 分支

##### 创建

git branch <branch name>

##### 切换

git checkout <branch name>

##### 修改当前分支名称

git branch -m <oldname>  <newname>

##### 发布到github/gitee/...

git push origin <branch name>

##### 把本地分支push到远程服务器

git push origin  <local branch name>: <remote branch name>

*<u>经过验证：如果远程没有相应的分支名会自动创建</u>*



##### github远程端删除一个分支

git push origin :<branch name>  (分支名前的冒号代表删除)

or

git push origin –-delete newBranch

(ps: 注意删除远程分支后，如果有对应的本地分支，本地分支并不会同步删除！



##### 克隆

git clone -b <branch name>  <ssh address>

![image-20210329111552380](C:\Users\JW\AppData\Roaming\Typora\typora-user-images\image-20210329111552380.png)

![image-20210329111706046](C:\Users\JW\AppData\Roaming\Typora\typora-user-images\image-20210329111706046.png)  （复制ssh地址）

eg：若要克隆test分支的代码

​		git clone -b test git@gitee.com:jinfengjeff21/daobo-vue.git



##### 上传

git add .

git commit -m "<memo>"

git pull

git push origin <branch name>



##### 查看远程分支

git branch -r

##### 查看本地分支

git branch

##### 查看本地及远程所有分支

git branch -a



#### ***远程仓库（remote）***

##### 显示

git remote -v

##### 添加

git remote add  <remote name>  <remote url> 

##### 修改远程仓库地址

git remote set-url origin 仓库地址



#### 拉取远程分支到本地

1.创建本地分支并拉取远程分支

git checkout -b 本地分支 origin/远程分支



2.本地分支与远程分支建立映射关系

git branch --set-upstream-to origin/远程分支名  本地分支名



#### 版本管理

##### 查看分支历史版本

git log 

##### 版本回滚

方法：删除远程分支，再提交

①保证当前工作区干净，且与远程分支代码一致

git pull origin <branch name>

②备份当前分支（如果需要）

③恢复到指定的分支版本

git resset --hard  <version hash>

④删除当前分支的远程分支

git push origin :currentBranch

或

git push origin --delete currentBranch

[参考](#github远程端删除一个分支)

⑤把当前分支提交到远程

git push origin <branch name>



### git push出现问题

本地远程分支名不一

git默认的push.default是simple模式（要求两边分支同名），而upstream模式则不做这个要求

使用命令

**git config --global push.default upstream**



如果是一个空的仓库，本地代码往上推：

本地git init、创建分支、添加remote地址后

使用命令

git push --set-upstream  <remote name>  <branch name> 



### git pull出现问题

There is no tracking information for the current branch.

Please specify which branch you want to merge with.

使用命令
git branch --set-upstream-to=org/<remote branch name>  <local branch name>

使远程分支和本地分支建立映射关系



# 本地代码中途创建本地仓库并推到远程仓库记录

## 1.git init，git add .  , git commit

## 2.git remote add <远程仓库名> <远程仓库地址> 

或者

git remote add origin <远程仓库地址> 



如： 远程库名：ConfigDemo 默认分支：main

​		本地分支：master



## 3.git branch --set-upstream-to=main(或origin)/<远程分支名>  <本地分支名>

这个 " / " 不是或的意思

可以先 git branch -a 查看本地分支和远程分支 （我是 git add remote 和 git fetch了之后才出现远程分支）

如：本地分支：***main***  远程分支：***main***/***main***

​	git branch --set-upstream-to=***main***/***main*** ***main



## 4.git pull

​	出现错误：fatal: refusing to merge unrelated histories

​	在本命令后加上  ***--allow-unrelated-histories*** 再次使用

## 5.git pull --allow-unrelated-histories

## 6.git push

**DONE**！



# 一些问题记录

在另一个文件夹（路径）想新建本地仓库并提交到远程（另一个仓库）
使用 git init 提示  "Initialized empty Git repository in D:/personal/Android/TimeHelper/.git/"
使用 git status 提示

fatal: detected dubious ownership in repository at 'D:/personal/Android/TimeHelper'
'D:/personal/Android/TimeHelper' is owned by:
        'S-1-5-32-544'
but the current user is:
        'S-1-5-21-376051431-3133538921-2203576763-2736'



*解决办法提示*

git config --global --add safe.directory D:/personal/Android/TimeHelper

使用该指令后就正常了，gitee 文件路径后出现了   ”（master）“
