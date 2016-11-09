

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

------
