# VIM的配置

## 2. 插件管理：

vim 自身希望通过在 .vim/ 目录中预定义子目录管理所有插件：

* 子目录 doc/ 存放插件帮助文档

* plugin/ 存放通用插件脚本

vim 的各插件打包文档中通常也包含上述两个（甚至更多）子目录，用户将插件打包文档中的对应子目录拷贝至 .vim/ 目录即可完成插件的安装

一般情况下这种方式没问题，但我等重度插件用户，.vim/ 将变得混乱不堪。使用vundle可用解决这个问题



<font color=red>gvim安装vundle:</font>

```python
1. 安装 Git, 然后把 Git安装目录/cmd 加入到环境变量 PATH 中. 加入之后, 可能需要重启一下电脑才行, 否则最后执行安装插件命令时, 会提示 git 不是内部命令的错误.
2. 把下面这段拷贝到 Git安装目录/cmd/curl.cmd 文件中(自己新建个)
@rem Do not use "echo off" to not affect any child calls.
@setlocal
@rem Get the abolute path to the parent directory, which is assumed to be the
@rem Git installation root.
@for /F "delims=" %%I in ("%~dp0..") do @set git_install_root=%%~fI
@set PATH=%git_install_root%\bin;%git_install_root%\mingw\bin;%PATH%
@if not exist "%HOME%" @set HOME=%HOMEDRIVE%%HOMEPATH%
@if not exist "%HOME%" @set HOME=%USERPROFILE%
@curl.exe %*
这两步做完之后, 在 cmd 窗口里输入 git --version 回车, 然后 curl --version, 如果这两个命令都有输出, 说明 Git 和 Curl 配好了
3. 然后到 Gvim 安装目录中, 右键, git bash, 然后执行下面的命令:
    git clone https://github.com/gmarik/Vundle.vim.git vimfiles/bundle/Vundle.vim

4. 编辑 _vimrc, 这一步和在 Linux 中的差不多, 注意一点:
把如下代码, 
set rtp+=~/.vim/bundle/Vundle.vim/
call vundle#begin()
替换成

set rtp+=~/vimfiles/bundle/Vundle.vim/
let path='~/vimfiles/bundle'
call vundle#begin(path)
剩下的就和 Linux 中的一样了.

5. 如：
set rtp+=~/vimfiles/bundle/Vundle.vim/
let path='~/vimfiles/bundle'
call vundle#begin(path)
Plugin 'altercation/vim-colors-solarized'
Plugin 'pydiction'
Plugin 'VundleVim/Vundle.vim'
Plugin 'Lokaltog/vim-powerline'
Plugin 'octol/vim-cpp-enhanced-highlight'
" 插件列表结束
call vundle#end()
```



### 基本操作：

* 安装插件

```python
:PluginInstall
```

* 卸载插件：

  要卸载插件，先在 .vimrc 中注释或者删除对应插件配置信息，然后在 vim 中执行

  ```python
  :PluginClean
  ```

* 更新插件：

  ```python
  :PluginUpdate
  ```



## 3 界面美化

### 3.1 主题风格：

