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
* 撤销本次提交 -- 版本回退 git reset --hard {commit_id}

小结：

* 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用命令` git reset --hard {commit_id}`，不过前提是没有推送到远程库

> 注意：`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

### 删除文件
使用`git rm`删除文件（使用`git add`可以添加删除的修改）

## 远程仓库
**使用github当作你的远程仓库:**

1. 创建github用户

2. 在本地电脑生成ssh密钥

   `$ ssh-keygen -t rsa -C "youremail@example.com"`

   > 执行成功：
   >
   > 可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人

3. 将密钥提交到你的github的账号设置中
   * 登陆GitHub，打开“Account settings”，“SSH Keys”页面
   * 点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容

> 友情提示：在GitHub上免费托管的Git仓库，任何人都可以看到（但只有你自己才能改）。所以，不要把敏感信息放进去。

### 添加远程仓库
1. github上面创建一个仓库: 

    * 登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库。

    * 在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库

    * 目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

      ![image-20221029111258498](assets/image-20221029111258498.png)

    * 拷贝ssh链接

      `git@github.com:xxx/learngit.git`

2. 在本地的仓库下执行命令，关联远程仓库:
    ```
    git remote add origin git@github.com:michaelliao/learngit.git
    ```

    >  添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的。
    
3. 推送本地文件到github

    ```
    git push -u origin master
    ```
    第一次推送master分支,-u参数:Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

4. 后面的提交:
    ```
    git push origin master
    ```

**删除远程库**

想要删除远程库可以用`git remote rm <name>`，使用前可以用`git remote -v`查看远程库信息。

> 此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。


### 从远程库克隆

从远程仓库中克隆:
```
$ git clone git@github.com:xxx/gitskills.gi
```

git remote -v查看远程库信息：

```
origin  git@github.com:xxx/learngit.git (fetch)
origin  git@github.com:xxx/learngit.git (push)
```

## 分支管理

### 创建与合并分支

* 查看分支：git branch
* 创建分支：git branch <name>
* 切换分支：git checkout <name>或者git switch <name>
* 创建+切换分支：git checkout -b <name>或者git switch -c <name>
* 合并某分支到当前分支：git merge <name>
* 删除分支：git branch -d <name>

### 解决冲突
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交
`git log --graph`命令可以看到分支合并图



## 标签管理

### 创建标签

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。
- 用`git show <tagname>`查看标签信息。（标签不是按时间顺序列出，而是按字母排序的）

### 操作标签

- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。



## 自定义Git

### 忽略特殊文件

有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存数据库密码的配置文件。在Git工作区的根目录下创建一个特殊的`.gitignore`文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的`.class`文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

**小结**

- 忽略某些文件时，需要编写`.gitignore`；

- `.gitignore`文件本身要放到版本库里，并且可以对`.gitignore`做版本管理

- 不需要从头写`.gitignore`文件，GitHub已经为我们准备了各种配置文件：https://github.com/github/gitignore

- `git check-ignore -v {file}` 查看是哪条规则忽略了文件

- 有些文件被忽略规则过滤了，但是还想提交，又两种方法：

  - `git add -f {file}` 略过忽略规则，强制提交

  - 在`.gitignore`里面加入规则，如：

    ```txt
    # 不排除.gitignore和App.class:
    !.gitignore
    !App.class
    ```



## 使用图形化工具Source Tree

source tree是一款GUI工具

从官网下载：https://www.sourcetreeapp.com/



## 其他操作：

### 利用git,使U盘作为仓库

**步骤1：首先U盘上创建一个repository 名称： myProject**

```
# 路径为 F:\myProject
git init --bare  myProject  //裸库，没有work目录
```

**步骤2：电脑文件夹创建一个文件夹**

```
git init 
//放入需要同步管理的文件
git add .    //添加文件、如果有不需要管理的文件，加入 .gitignore文件；
git commit -m "initialized."   //提交到本地仓库
git remote add usb F:\myProject    //把u盘上的裸库myProject添加为远程仓库
git push -u usb master	// 首次提交需要-u 后面就不需要
```

**步骤3：在另一个目录建立一个本地仓库，测试是否可以拉去代码**

```
git init  myfill //建一个本地仓库
git remote add usb F:\myProject     //把u盘上的裸库fill_backup_repos添加为远程仓库
git pull usb master   //完成代码同步
```

> 经测试，把u盘的目录F:\myProject挪到其他地方，也可以使用

### 其他命令

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

## 常见问题
### windows中文乱码的问题

执行如下命令

```txt
$ git config --global core.quotepath false  		# 显示 status 编码
$ git config --global gui.encoding utf-8			# 图形界面编码
$ git config --global i18n.commit.encoding utf-8	# 提交信息编码
$ git config --global i18n.logoutputencoding utf-8	# 输出 log 编码

# =========下面这条没执行===
$ export LESSCHARSET=utf-8 (windows下为：set LESSCHARSET=utf-8)
# 最后一条命令是因为 git log 默认使用 less 分页，所以需要 bash 对 less 命令进行 utf-8 编码
```

参考：https://zhuanlan.zhihu.com/p/357002483

### git提交时”warning: LF will be replaced by CRLF“提示

使用 命令`git config --global core.autocrlf false`

参考：`https://www.cnblogs.com/sminocence/p/9357209.html`

