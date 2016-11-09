
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
