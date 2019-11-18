# VIM的配置

**参考博客**

```
https://github.com/yangyangwithgnu/use_vim_as_ide
```

**模块化的vim IDE:**

SpaceVim 

官网:

```
https://spacevim.org/cn/
```

可以省得配置，后面可以研究



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
    git clone https://github.com/gmarik/Vundle.vim.git ~/vimfiles/bundle/Vundle.vim

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



### 5.2 模板补全

**vim-snippets插件**

```
Plugin 'honza/vim-snippets'
let g:UltiSnipsExpandTrigger="<leader><tab>"
let g:UltiSnipsJumpForwardTrigger="<leader><tab>"
let g:UltiSnipsJumpBackwardTrigger="<leader><s-tab>"
```





### 5.3 智能补全

#### 基于语义的智能补全



##### 概述:

基于编译器的两颗语义补全插件

* GCCSense

* clang_complete

  * 特点：

    * 使用难度低
    * 维护时间长
    * 支持跨平台

  * 缺点：

    * 无法随键而全

    * 无法模糊搜索

    * 无法高速补全

使用语义补全插件:YCM(YouCompleteMe)

只在两种场景下触发语义补全:

* 补全标识符所在文件必须在buffer中(即文件已打开)
* 在对象键入"."  "->"  "::"

解决ycm的不足:OmniCppComplete

OmniCppComplete:

* 只要你在代码文件中#include了该标识符所在头文件即可

* 缺点：无法使用YCM的随键而全的特性

* 手动补全，快捷键：(备注:测试了没效果，暂时没搞懂20191116)

  ```
  " 原先的快捷键
  <C-x><C-o>
  " 设定后的快捷键: YCM 集成 OmniCppComplete 补全引擎，设置其快捷键
  inoremap <leader>; <C-x><C-o>
  ```



##### 使用YCM

第一步，通过 vundle 安装 YCM 插件：

```
Plugin 'Valloric/YouCompleteMe'
```







## 其他：

### 支持python

#### jedi插件

github路径

```
https://github.com/davidhalter/jedi-vim
```

通过vundel安装：

```
" jedi插件
Plugin 'davidhalter/jedi-vim'

"jedi插件配置-------------------
let g:jedi#popup_select_first = 0
```





### 安装ctags--支持工程间的跳转

参考博客:

```
https://www.cnblogs.com/aaronLinux/p/5720754.html
```

#### 安装软件：

```
#1 下载路径：
http://ctags.sourceforge.net/
#2 在解压后将文件夹中的ctags.exe复制到C:\Program Files\Vim\vim81下，并编辑_vimrc文件，添加以下内容：
set tags=tags; 
set autochdir
#3 将C:\Program Files\Vim\vim81加入环境变量中
#4 可以运行如下命令查看支持的语言:
ctags --list-languages
```

#### 使用:

```
#1 到所在工程路径下执行：
ctags -R
#2 可以使用：
按住“CTRL”键，点击对应的函数名或“CTRL+]”，会自动跳转到函数的定义部分，“CTRL+T”则返回；
```



### markdown-preview

网址:

<https://github.com/iamcco/markdown-preview.vim>

安装方法:

```
Plugin 'iamcco/mathjax-support-for-mkdp'
Plugin 'iamcco/markdown-preview.vim'
```

默认配置:

```
let g:mkdp_path_to_chrome = ""
" 设置 chrome 浏览器的路径（或是启动 chrome（或其他现代浏览器）的命令）
" 如果设置了该参数, g:mkdp_browserfunc 将被忽略

let g:mkdp_browserfunc = 'MKDP_browserfunc_default'
" vim 回调函数, 参数为要打开的 url

let g:mkdp_auto_start = 0
" 设置为 1 可以在打开 markdown 文件的时候自动打开浏览器预览，只在打开
" markdown 文件的时候打开一次

let g:mkdp_auto_open = 0
" 设置为 1 在编辑 markdown 的时候检查预览窗口是否已经打开，否则自动打开预
" 览窗口

let g:mkdp_auto_close = 1
" 在切换 buffer 的时候自动关闭预览窗口，设置为 0 则在切换 buffer 的时候不
" 自动关闭预览窗口

let g:mkdp_refresh_slow = 0
" 设置为 1 则只有在保存文件，或退出插入模式的时候更新预览，默认为 0，实时
" 更新预览

let g:mkdp_command_for_global = 0
" 设置为 1 则所有文件都可以使用 MarkdownPreview 进行预览，默认只有 markdown
" 文件可以使用改命令

let g:mkdp_open_to_the_world = 0
" 设置为 1, 在使用的网络中的其他计算机也能访问预览页面
" 默认只监听本地（127.0.0.1），其他计算机不能访问
```

键位绑定

```
nmap <silent> <F8> <Plug>MarkdownPreview        " 普通模式
imap <silent> <F8> <Plug>MarkdownPreview        " 插入模式
nmap <silent> <F9> <Plug>StopMarkdownPreview    " 普通模式
imap <silent> <F9> <Plug>StopMarkdownPreview    " 插入模式
```







### 我的_vimrc

```python
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
"set rtp+=~/.vim/bundle/Vundle.vim/
"call vundle#begin()
set rtp+=$VIM/vimfiles/bundle/Vundle.vim/
call vundle#begin('$VIM/vimfiles/bundle/')

" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
"Plugin 'gmarik/Vundle.vim'         "管理Vundle自身 

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
"Plugin 'tpope/vim-fugitive'
" plugin from http://vim-scripts.org/vim/scripts.html
" Plugin 'L9'
" Git plugin not hosted on GitHub
"Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
"Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim'}
" Install L9 and avoid a Naming conflict if you've already installed a
" different version somewhere else.
" Plugin 'ascenator/L9', {'name': 'newL9'}

" All of your Plugins must be added before the following line

Plugin 'altercation/vim-colors-solarized'
Plugin 'Lokaltog/vim-powerline'
Plugin 'octol/vim-cpp-enhanced-highlight'
".cpp .h文件间切换插件
Plugin 'derekwyatt/vim-fswitch'
" 标识符列表
Plugin 'majutsushi/tagbar'

" python-mode 支持python的自动补全等操作
Plugin 'klen/python-mode.git'

call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

" 定义快捷键的前缀，即<Leader>
let mapleader=";"

" 开启文件类型侦测
filetype on
" 根据侦测到的不同类型加载对应的插件
filetype plugin on

" 定义快捷键到行首和行尾
nmap LB 0
nmap LE $
" 设置快捷键将选中文本块复制至系统剪贴板
vnoremap <Leader>y "+y
" 设置快捷键将系统剪贴板内容粘贴至 vim
nmap <Leader>p "+p
" 定义快捷键关闭当前分割窗口
nmap <Leader>q :q<CR>
" 定义快捷键保存当前窗口内容
nmap <Leader>w :w<CR>
" 定义快捷键保存所有窗口内容并退出 vim
nmap <Leader>WQ :wa<CR>:q<CR>
" 不做任何保存，直接退出 vim
nmap <Leader>Q :qa!<CR>
" 依次遍历子窗口
nnoremap nw <C-W><C-W>
" 跳转至右方的窗口
nnoremap <Leader>lw <C-W>l
" 跳转至左方的窗口
nnoremap <Leader>hw <C-W>h
" 跳转至上方的子窗口
nnoremap <Leader>kw <C-W>k
" 跳转至下方的子窗口
nnoremap <Leader>jw <C-W>j
" 定义快捷键在结对符之间跳转
nmap <Leader>M %

" 让配置变更立即生效
autocmd BufWritePost $MYVIMRC source $MYVIMRC

" 开启实时搜索功能
set incsearch
" 搜索时大小写不敏感
set ignorecase
" 关闭兼容模式
set nocompatible
" vim 自身命令行模式智能补全
set wildmenu

" 配色方案
set background=dark
colorscheme solarized
"colorscheme molokai
"colorscheme phd

" 设置字体大小
set guifont=courier_new:h14

" 禁止光标闪烁
" set gcr=a:block-blinkon0
" 禁止显示滚动条
set guioptions-=l
set guioptions-=L
set guioptions-=r
set guioptions-=R
" 禁止显示菜单和工具条
set guioptions-=m
set guioptions-=T

" 总是显示状态栏
set laststatus=2
" 显示光标当前位置
set ruler
" 开启行号显示
set number
" 高亮显示当前行/列
set cursorline
"set cursorcolumn
" 高亮显示搜索结果
set hlsearch

" 设置 gvim 显示字体
"set guifont=YaHei\ Consolas\ Hybrid16

" 设置状态栏主题风格
 let g:Powerline_colorscheme='solarized256'

" 开启语法高亮功能
syntax enable
" 允许用指定语法高亮配色方案替换默认方案
syntax on


" 自适应不同语言的智能缩进
filetype indent on
" 将制表符扩展为空格
set expandtab
" 设置编辑时制表符占用空格数
set tabstop=4
" 设置格式化时制表符占用空格数
set shiftwidth=4
" 让 vim 把连续数量的空格视为一个制表符
set softtabstop=4

" 基于缩进或语法进行代码折叠
"set foldmethod=indent
set foldmethod=syntax
" 启动 vim 时关闭折叠代码
set nofoldenable

" 解决backspace键不能删除的问题
set backspace=indent,eol,start

" *.cpp 和 *.h 间切换
nmap <silent> <Leader>sw :FSHere<cr>

" 设置 tagbar 子窗口的位置出现在主编辑区的左边 
let tagbar_left=1 
" 设置显示／隐藏标签列表子窗口的快捷键。速记：identifier list by tag
nnoremap <Leader>ilt :TagbarToggle<CR> 
" 设置标签子窗口的宽度 
let tagbar_width=32 
" tagbar 子窗口中不显示冗余帮助信息 
let g:tagbar_compact=1
" 设置 ctags 对哪些代码标识符生成标签
let g:tagbar_type_cpp = {
    \ 'kinds' : [
         \ 'c:classes:0:1',
         \ 'd:macros:0:1',
         \ 'e:enumerators:0:0', 
         \ 'f:functions:0:1',
         \ 'g:enumeration:0:1',
         \ 'l:local:0:1',
         \ 'm:members:0:1',
         \ 'n:namespaces:0:1',
         \ 'p:functions_prototypes:0:1',
         \ 's:structs:0:1',
         \ 't:typedefs:0:1',
         \ 'u:unions:0:1',
         \ 'v:global:0:1',
         \ 'x:external:0:1'
     \ ],
     \ 'sro'        : '::',
     \ 'kind2scope' : {
         \ 'g' : 'enum',
         \ 'n' : 'namespace',
         \ 'c' : 'class',
         \ 's' : 'struct',
         \ 'u' : 'union'
     \ },
     \ 'scope2kind' : {
         \ 'enum'      : 'g',
         \ 'namespace' : 'n',
         \ 'class'     : 'c',
         \ 'struct'    : 's',
         \ 'union'     : 'u'
     \ }
\ }

set encoding=utf-8  " The encoding displayed.
set fileencoding=utf-8  " The encoding written to file.


let g:pymode_python = 'python3'
```

