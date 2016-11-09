git 学习笔记

# Git 学习笔记 --- 安装和基本配置

-------


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


-----

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

生成过程
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

安装和基本配置 结束 
------












