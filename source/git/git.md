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

```cmd
git init
```

**把文件添加到版本库：**

* 添加文件:

  ```cmd
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

* HEAD 指向当前版本
* git reset --hard commit_id 切换到指定版本
* 查看commit_id的方法:
    * git log 提交历史
    * git reflog 命令历史


### 工作区、版本库和暂存区
* 工作区(Working Directory):代码的目录
* 版本库(Repository):`.git`目录
* 暂存区(stage或叫index)
    * git add 提交到此目录
* master:Git会自动创建第一个主分支master
    * git commit 提交到此目录

![示意图](./image/workDirectory.jpg)
​    

### 撤销修改
* 丢弃工作区的修改: git checkout -- <file>
* 丢弃添加到暂存区的文件 git reset HEAD <file>
* 撤销本次提交 -- 版本回退

### 删除文件
使用`git rm`删除文件

## 远程仓库
**使用github当作你的远程仓库:**
1. 创建github用户
2. 在本地电脑生成ssh密钥
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
3. 将密钥提交到你的github的账号设置中

#### 添加远程仓库
1. github上面创建一个仓库: 
    `git@github.com:xxx/learngit.git`
2. 在本地的仓库下执行命令:
    ```
    git remote add origin git@github.com:michaelliao/learngit.git
    ```
3. 推送本地文件到github
    ```
    git push -u origin master
    ```
    第一次推送master分支,-u参数:Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
4. 后面的提交:
    ```
    git push origin master
    ```

5. 从远程仓库中克隆:
```
$ git clone git@github.com:xxx/gitskills.gi
```

### 分支管理
#### 创建与合并分支

* 查看分支：git branch
* 创建分支：git branch <name>
* 切换分支：git checkout <name>或者git switch <name>
* 创建+切换分支：git checkout -b <name>或者git switch -c <name>
* 合并某分支到当前分支：git merge <name>
* 删除分支：git branch -d <name>

#### 解决冲突
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交
`git log --graph`命令可以看到分支合并图













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


#### 其他命令
**git checkout**
1. 切换或者新建分支。
2. 将暂存区或者指定commit内容覆盖到工作区

### 分支

1. 创建dev分支，如何切换到dev分支

```
  $ git checkout -b dev
  Switched to a new branch 'dev'
```

1. -b 参数 相当于两条命令(创建和切换)

   ```
   $ git branch dev
   $ git checkout dev
   Switched to branch 'dev'
   ```

2. 查看当前分支 "git branch"

   ```
   $ git branch
   * dev
     master
   ```

3. 新的切换分支命令:

   ```
   git switch master
   ```



### 更新代码到本地

1. 从远程获取最新版本到本地:

   ```
   git fetch origin master
   ```

2. 比较本地的仓库和远程参考的区别

   ```
   git log -p master.. origin/master
   ```

3. 把远程下载下来的代码合并到本地仓库，远程的和本地的合并

   ```
   git merge origin/master
   ```

