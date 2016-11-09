# git 学习笔记 汇总

------
------



# Git 学习笔记 --- 安装和基本配置

------

# 基本资料

**GitHub地址**
> https://github.com/



感谢 **廖雪峰**同学写的博客，帮助我更好的学习GitHub。
**廖雪峰博客地址**
> http://www.liaoxuefeng.com

**廖雪峰GitHub教程地址**
>http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

**注： 该笔记是给我自己用的，以便自己能够快速浏览，帮助自己更快的学会GitHub。** 
**如果要学习的话，推荐移步廖雪峰的博客来学习！**


------

**安装Git**
--------
**检测 GitHub 是否被安装（查询版本）**

> git --version

**CentOS 下安装**
>  yum install git 

**Ubuntu 安装**
> sudo apt-get install git



**配置用户名和邮件（全局）**
--------
> git config --global user.name "Your Name"
> git config --global user.email "email@example.com"



**SSH Key的配置**
--------
> 切换到用户根目录 看看有没有.ssh 目录
> 
> cd 
> ls -a
> cd .ssh 
> ls
> 
> 这个目录下应该包含两个文件
> id_rsa和id_rsa.pub两个文件， 这两个就是SSH Key的秘钥对。
> id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
> 
> 如果没有则 生成
> **生成命令** 
> **ssh-keygen -t rsa -C "你的邮箱地址"**
> 

**生成过程**

```shell 
# 输入命令 
[root@www ~]# ssh-keygen -t rsa -C "812069449@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 

# 输入密码 可留空 
Enter passphrase (empty for no passphrase): 

# 再次输入密码
Enter same passphrase again: 

# 文件生成后的路径 
# 私钥路径
Your identification has been saved in /root/.ssh/id_rsa.
# 公钥路径
Your public key has been saved in /root/.ssh/id_rsa.pub.

```
**将生成的密钥 配置到远端服务器**
----------

**读公钥内容 **
> cat  ~/.ssh/id_rsa.pub


**在浏览器打开 GitHub  并配置值**
> 网址：https://github.com/settings/keys
![这里写图片描述](http://images2015.cnblogs.com/blog/446475/201512/446475-20151207095523105-1244401158.jpg)


**测试ssh key是否成功**
> ssh -T git@github.com



*** 安装和基本配置 笔记内容结束 ***

------



# Git 学习笔记 --- 工作区 和 暂存区

------

# 创建一个仓库
------

首先登录GitHub并进入主页
> 网址：https://github.com/

![首页](http://img.blog.csdn.net/20160826113405758)
![创建仓库](http://img.blog.csdn.net/20160826113444344)
![这里写图片描述](http://img.blog.csdn.net/20160826113634314)
![这里写图片描述](http://img.blog.csdn.net/20160826113643454)


**关联仓库到本地**
-------

**首先本地需要创建一个文件夹用来存储**
>mkdir  test

**初始化Git  环境**
> cd test  
> git init 

**克隆远程环境**
> git clone https://github.com/xiaomochen/test.git

**关联远程环境**
> git remote add origin git@github.com:xiaomochen/test.git

**查看远程仓库信息**
>  查看基本信息
>  git remote
>  
>  查看详细信息
>  git remote -v
>  

**新文件提交**
-------
**添加一个文件到暂存区**
> git add  readme.txt  

**将暂存区的操作 提交到当前分支**
> git  commit   -m  '这里是描述'

**查看当前 仓库的状态信息**
> git status

**新文件提交实例**
---
> 
> 新增一个文件
> touch new.html
> 
> 
> 向文件填写内容
> echo "this is new file" > new.html
> 
> 
> 将文件提交到暂存区（实际上就是做个记录）
> git add new.html
> 
> 提交这个版本
> git commit -m  '我提交了一个文件'
> 
> 第一次 提交的时候 带上 -u 参数  以关联分支
> git push -u origin master



**版本撤回**
----

**查看版本历史信息**
> git log
> 
> 格式化显示 （一行一行的显示）
> git log --pretty=oneline 


**查看所有的版本历史信息  包括未来的**
如果你退回了某个版本后 想要返回到 最新的版本就要用到这个命令
> git reflog


**重置到某个版本**
> git reset  -- hard   版本编号
> 

**重置到上一个版本**
HEAD 			表示的是 最新的版本
HEAD^  		表示的是 上一个版本
HEAD^^ 		表示的是 上面的第二个版本  **^**的个数就是 版本的个数
HEAD~100  表示的是 前第100个版本

>  git reset --hard HEAD^






**冲突处理**
----

**同步线上的数据到本地**
> git pull  

**查看两个版本的 数据差别**
> git diff  

**查看工作区和版本库里面最新版本的区别**
> git  diff  HEAD -- readme.txt



**实例场景：**
> 猴子A 修改了test.html 文件提交后，
> 正好猴子B 也在修改这个文件，
> 猴子B 提交的时候GitHub会返回一个错误信息
![这里写图片描述](http://img.blog.csdn.net/20160822165556732)
大致的意思是：
　　更新被拒绝，因为远程版本库包含您本地尚不存在的提交。这可能是另外一个版本库已经推送了相同的引用。再次推送前，您可能需要先合并远程变更。

**PS：  git 并不会像 SVN 那样自动合并内容，如果有冲突，只能通过手工自己修改**


**解决流程解析**
1.	首先需要把远程的数据的拉下来
2.	然后手动修改文件，选择需要保留的数据
3.	提交最新的代码

**解决冲突实例**
> 先更新文档
> git pull
> 
> 查看冲突
> git diff
>  
> 编辑文件并保存 
> vim  冲突的文件 
>  
> 提交修改
> git add 冲突的文件
>  
> 合并到当前分支 
> git commit -m '新增了 xxx 功能'
>  
> 提交到远程 
> git push

**撤销修改**
---
> git checkout -- readme.txt

注意中间是两个 - 

命令 **git checkout -- readme.txt** 意思就是，把readme.txt文件在工作区的修改全部撤销。
这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

**删除文件**
---

**删除本地文件**
> rm -rf  test

**删除库中的文件**
> git rm test.txt

**实例**
> 
> 删除本地文件
> rm -rf  test
> 
> 删除库中的文件
> git rm test.txt
> 
> 提交删除操作
> git commit -m "remove test.txt"
> 

**如果是删错了 版本库里还有的话  可以恢复**
> git checkout -- test.txt

**用reset 也可以达到同样的目的   HEAD 表示库中的最新版本**
> git reset HEAD test.txt



*** 工作区 和 暂存区  笔记内容结束 ***
-----







# Git 学习笔记 --- 分支管理

-----



**查看本地分支**
> git branch 

-----------
 
**查看所有分支  包括线上的**
> git branch -a

-----------
 
**根据当前分支 创建新分支**
> git branch  [name]
> git branch  dev

-----------
 
**根据当前分支 创建并切换分支**
> git checkout -b [name]
> git checkout -b dev

-----------
 
**指定基础分支 创建新分支**
> git checkout -b   新分支名  基础分支名
> 
> 本地的
> git checkout -b feature-x develop
> 
> 线上的 
> git checkout -b feature-x  origin/develop

-----------
 
**关联线上的分支**
> git branch --set-upstream 本地分支名    线上分支名
> 
> git branch --set-upstream dev origin/dev

-----------
 
**切换分支**
> git checkout  [name]
> 
> git checkout  dev

-----------
 
**将新分支推送到远程**
> git push origin test


-----------
 
**删除分支**
注意删除的分支不能是 当前正在使用的分支
> git branch -d  [要删除的分支名]
> 
> git branch -d  dev

-----------
 
**删除远程分支**
将一个空分支 push 到线上的 xxx 分支  相当于删除
> git push origin :branch-name

-----------

**强制删除分支**
如果这个分支中还有 未提交的数据  那么 删除该分支的时候是拒绝的
提示用以下命令  强制删除
> git branch -D feature-vulcan

-----------
 
**合并分支**
> git merge [要合并的分支名]
> 
> 快进模式
> git merge  dev
>
>
> 普通模式
> git merge --no-ff  dev -m  '合并了一个分支'


-----------

 
**分支模式**
------

**no-ff**指的是强行关闭fast-forward方式。

**fast-forward**方式就是当条件允许的时候，git直接把HEAD指针指向合并分支的头，完成合并。属于“快进方式”，不过这种情况如果删除分支，则会丢失分支信息。因为在这个过程中没有创建commit

**git merge --squash** 是用来把一些不必要commit进行压缩，比如说，你的feature在开发的时候写的commit很乱，那么我们合并的时候不希望把这些历史commit带过来，于是使用--squash进行合并，此时文件已经同合并后一样了，但不移动HEAD，不提交。需要进行一次额外的commit来“总结”一下，然后完成最终的合并。

> 图示：

![图示](http://img.blog.csdn.net/20160826101434026)
![图示](http://img.blog.csdn.net/20160826101448827)

---------------
**分支模式小结：**
*--**no-ff**：不使用fast-forward方式合并，保留分支的commit历史*
*--**squash**：使用squash方式合并，把多次分支commit历史压缩为一次* 

---------------

**Git分支管理策略**
---
> 移步 http://www.ruanyifeng.com/blog/2012/07/git.html 有详细介绍

**分支管理策略小结：**

|分支名|作用|临时分支?|
|:---|:---|:---|
|master|对外发布的正式分支|否 线上的主要分支|
|develop|开发分支|否 线上本地都可以有|
|feature|功能分支|是临时分支 用完即删|
|release|预发布分支|是临时分支 用完即删|
|fixbug|修补bug分支|是临时分支 用完即删|


------

stash 功能
----

**保存当前工作区**
> git stash

----
 
**显示 已经保存过的 工作区列表**
> git stash list

----
 
**恢复 已经保存的工作区**
> git stash apply

----
 
**删除 已经保存的工作区**
> git stash drop 

----
 
**恢复并删除 已经保存的工作区**
> git stash pop

---

**使用场景**
>修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

> 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。



*** 分支管理 笔记内容结束 ***

-------




# Git 学习笔记 --- 标签管理

------


**查看标签列表**
> git tag 

---

**给当前分支 打上一个 标签**
默认标签是打在最新提交的commit上的。
> git  tag  [标签名称]

---

**给指定的commit id 打上一个标签**
>git tag [标签名] [commit id]
> 
>git tag v0.9 6224937

---

**还可以创建带有说明的标签**
> git tag -a [名称] -m [描述]  [commit id]
> 
> git tag -a v0.1 -m "version 0.1 released" 3628164

----

**查看指定标签的信息**
>  git show  [标签名]
>  
>  git show v0.9

------

**删除标签**
> git tag -d [标签名]
> 
> git tag -d v0.9

---

**推送标签到远程仓库**
> git push origin [标签名]、
> 
> git push origin v.1.0
> 

---

**一次性推送 全部尚未推送到远程的本地标签**
> git push origin --tags
> 

--- 

**删除远程 标签**
> git push origin [标签路径]
> 
> git push origin :refs/tags/v0.9



*** 标签管理 笔记内容结束 ***

-------




# Git 学习笔记 --- 自定义Git

-------


GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。
所有配置文件可以直接在线浏览：**https://github.com/github/gitignore**

---

#忽略特殊文件

主要编辑 工作区根目录下的 **.gitignore** 文件

忽略文件的原则是：
	
 - 忽略操作系统自动生成的文件，比如缩略图等；

 - 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；

 -  忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

---

**创建 .gitignore 文件**
> touch  .gitignore 

---

**编辑完成后 要提交到 远程**
> git add .gitignore 
> git commit  -m '提交配置文件'
> git push

---

**.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！**

---

**如果添加不上 很有可能是因为.gitignore 的配置 而被忽略  **
**如果你确实想添加该文件 则需要在 add 后面 加个 -f 参数**
> git  add  -f  .gitignore 

**或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：**
> git check-ignore -v App.class

**忽略特殊文件 小结**

 - 忽略某些文件时，需要编写.gitignore；
 
 - .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
 
 ----
 
# 配置别名

**新增别名**

例： 配置一个st 的命令  来代替 status 
> git config --global alias.[名称]  [对应的命令]
> 
> git config --global alias.st status
> 

当然还有别的命令可以简写，很多人都用co表示checkout，ci表示commit，br表示branch：

> git config --global alias.co checkout
> git config --global alias.ci commit
> git config --global alias.br branch

**以后提交就可以这么写**
> git ci -m "bala bala bala..."

**除了 直接指定命令  后面可以跟个 命令组成的 字符串**

例如 **撤销修改**

**之前的**
> git reset HEAD file

**配置命令**
> git config --global alias.unstage 'reset HEAD'

**配置命令之后的**
> git  unstage  test.html
> 
>  实际执行的是
>  git reset HEAD test.html


配置一个**git last**，让其显示最后一次提交信息：
> git config --global alias.last 'log -1'

配置一个**lg**, 让其显示分支日志
```shell
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
**试一下 git  lg  的效果** 

![这里写图片描述](http://img.blog.csdn.net/20160826183544545)


# 配置文件

配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在**.git/config**文件中：

```shell
	$ cat .git/config 
	[core]
	    repositoryformatversion = 0
	    filemode = true
	    bare = false
	    logallrefupdates = true
	    ignorecase = true
	    precomposeunicode = true
	[remote "origin"]
	    url = git@github.com:michaelliao/learngit.git
	    fetch = +refs/heads/*:refs/remotes/origin/*
	[branch "master"]
	    remote = origin
	    merge = refs/heads/master
	[alias]
	    last = log -1
```
别名的配置就是放在 **alias** 下， 可以直接编辑。

而当前用户的Git配置文件放在**用户主目录下**的一个隐藏文件**.gitconfig**中
```shell
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```

-----

**配置小结**
---

**仓库的配置文件路径**
> **.git/config**

-----

**个人的配置文件路径**
> **用户主目录/.gitconfig**

----

**忽略文件**的 配置文件的路径 
　　　　**项目根目录下的 .gitignore**
　　　　该配置修改后　也可以做版本管理


----

**配置别名**
>  git config --global **alias.**[别名]    [命令 或者 命令字符串]


*** 自定义Git 笔记内容结束 ***

---------

