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

------
