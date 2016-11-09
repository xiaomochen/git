
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

