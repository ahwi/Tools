## Git

### 搭建环境

**1.  安装git**

**2. 配置user name 和 email:**

```python
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。



### 创建版本库

**版本库**又名仓库，英文名repository

**初始化版本库：**

```python
git init
```

**把文件添加到版本库：**

* 添加文件:

  ```python
  使用命令git add <file>，注意，可反复多次使用，添加多个文件；
  使用命令git commit -m <message>，完成提交
  ```

* 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。
* 版本控制系统没办法跟踪二进制文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

**查看修改信息：**

```python
git status   查看工作区的状态
git diff <filename> 查看修改内容
```



### 版本回退

**查看log：**

```python
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```

**查看log的简略信息：**

```python
$ git log --pretty=oneline
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```

**版本回退：**





### 其他操作：

#### 利用git,使U盘作为仓库

**步骤1、首先U盘上创建一个repository 名称： fill_backup_repos**

```
git init –bare  fill_backup_repos  //裸库，没有work目录
```

**步骤2、电脑文件夹创建一个源项目 名称：git_myfill**

```
git init git_myfill 
//放入需要同步管理的文件
git add .    //添加文件、如果有不需要管理的文件，加入 .gitignore文件；
git commit -m "initialized."   //提交到本地仓库
git remote add usb F:/fill_backup_repos    //把u盘上的裸库fill_backup添加为远程仓库
git push usb master
```

**步骤3、在U盘上的fill_backup 裸仓库里头建立一个本地仓库**

```
git init  myfill //建一个本地仓库
git remote add usb F:/fill_backup_repos     //把u盘上的裸库fill_backup_repos添加为远程仓库
git pull myusb master   //完成代码同步
```

