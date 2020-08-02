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



## 4. 代码分析

### 4.3 代码折叠
vim自带代码折叠
添加如下配置:
```
" 基于缩进或语法进行代码折叠
"set foldmethod=indent
set foldmethod=syntax
" 启动 vim 时关闭折叠代码
set nofoldenable
```
操作：
* za，打开或关闭当前折叠
* zM，关闭所有折叠
* zR，打开所有折叠。
### 4.6 标识符列表

#### 基于标签的标识符列表

tagbar（<https://github.com/majutsushi/tagbar> ）是一款基于标签的标识符列表

需要用到ctags

### 4.7 声明/定义跳转

#### 基于语义的声明/定义跳转

快捷键

```
nnoremap <leader>jc :YcmCompleter GoToDeclaration<CR>
" 只能是 #include 或已打开的文件
nnoremap <leader>jd :YcmCompleter GoToDefinition<CR>
```





### 4.8 内容查找

**ctrlsf**：<https://github.com/dyng/ctrlsf.vim> 

**安装:**

* windows:

  * 安装ag查找工具

    <https://github.com/k-takata/the_silver_searcher-win32>

    下载exe，添加ag.exe的路径到系统环境

  * 在_vimrc配置里面加入

    ```
    Plugin 'dyng/ctrlsf.vim'
    ```

**使用：**

命令模式键入

```
:CtrlSF
```

将自动提取光标所在关键字进行查找，你也可以指定 ack 的选项

```
:CtrlSF -i -C 1 [pattern] /my/path/
```

设置快捷键

```
" 使用 ctrlsf.vim 插件在工程内全局查找光标所在关键字，设置快捷键。快捷键速记法：search in project
nnoremap <Leader>sp :CtrlSF<CR>
```

查找结果在子窗口呈现，p将在右侧子窗口中给出该匹配项的完整代码，enter跳到对应的位置



### 4.9 内容替换

**vim-multiple-cursors：**多光标编辑功能

<https://github.com/terryma/vim-multiple-cursors>

用法:

按v 选中某个字符串 --> ctrl-n匹配选中第二个字符串





## 5. 代码开发

### 5.1 快速开关注释

**NERD Commenter**

<https://github.com/preservim/nerdcommenter>

\<leader\>cc 注释当前选中文本

\<leader\>cu 取消选中文本的注释







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





## 8. 其他辅助工具

### 8.4 markdown 即时预览

**markdown-preview:**

<https://github.com/iamcco/markdown-preview.nvim>

markdwon的编写教程

<https://github.com/adam-p/markdown-here/wiki>



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


### 浏览器vim插件
**surfingkeys**
**安装** 可以直接在google应用商店里面安装
**使用文档** https://github.com/brookhong/Surfingkeys
**快捷键:**
```
? help
t 搜索标签/历史
/ 查找
f+node 点击某个链接
v 切换到visual模式
T 切换标签栏
ab 添加到书签
b 打开书签
r 刷新
e 上滑一页
d 下滑一页
on 打开新的标签
```




### 快捷键

```

j 合并当前行和下一行
vip 选中所有行
r 替换
f + xxx  跳转到当前行的某个字符
v 选择字符 <C-n>选中下一个一样的字符
==============跳转
0 跳到行首
$ 跳到行尾
V 选中整行
<leader>js 跳转到声明的地方
<leader>jd 跳转到定义的地方

" 对所有行执行操作
如在选中的行后面插入 (<++>)
选中行 : normal A (<++>)

# 读取目录的文件名到vim中
:r !ls path

# 录制键盘宏
1. q a 开始录制 录制到a的寄存器
2. q 退出录制
3. @a 重放录制的内容
如果想重复重发5次: 5@a

# 递增 递减
Ctrl-a 递增一个数字
Ctrl-x 递减一个数字

# <操作> <动作>
如 
cw 修改一个词
d10h 往右删除10个字
df: 删除到找到的冒号

# 让当前行成为中心点
zz

# 注释/取消注释
;cc 注释
;uc 取消注释

# ==============分屏
” 普通快捷键
sp 上下分屏
vsp 左右分屏
" 自定义快捷键
" 往右边分屏
map sl :set splitright<CR>:vsplit<CR>
map sh :set nosplitright<CR>:vsplit<CR>
map sk :set nosplitbelow<CR>:split<CR>
map sj :set splitbelow<CR>:split<CR>
" 分屏跳转
map <LEADER>h <C-w>h
map <LEADER>j <C-w>j
map <LEADER>k <C-w>k
map <LEADER>l <C-w>l


" 分屏大小
map <up> :res +5<CR>
map <down> :res -5<CR>
map <left> :vertical resize -5<CR>
map <right> :vertical resize +5<CR>

" 分屏切换
map sv <C-w>t<C-w>H
map sh <C-w>t<C-w>K

# ================标签
" 新建一个标签
map tu :tabe<CR>
map th :-tabnext<CR>
map tl :+tabnext<CR>


;打印成html
:TOhtml


```

**自定义快捷键:**
```
" 保存
map S :w<CR>
" 退出
map Q :q<CR>
" 加载vimrc MYVIMRC需要设置成环境变量
map R :source $MYVIMRC<CR>

" 打开NERDTree 文件夹树
tt 
```

**设置:**
```
" 设置相对行号
set relativenumber
" 取消设置相对行号
" set norelativenumber
" 设置命令补全
set wildmenu
" 高亮
set hlsearch
" 一开始就运行不要高亮指令
exec "nohlsearch"
" 搜索的时候就高亮
set incsearch
" 忽略大小写
set ignorecase
" 设置智能匹配大小写
set smartcase
" 取消高亮
noremap <LEADER><CR> :nohlsearch<CR>

;===============配色
;避免配色有什么不对的  感觉没啥用
let &t_ut=''

```





### 我的_vimrc

```python
set nocompatible              " be iMproved, required
filetype off                  " required
" 设置相对行号
" set relativenumber
" 取消设置相对行号
set norelativenumber
" 设置命令补全
set wildmenu
" 高亮
set hlsearch
" 一开始就运行不要高亮指令
exec "nohlsearch"
" 搜索的时候就高亮
set incsearch
" 忽略大小写
set ignorecase
" 设置智能匹配大小写
set smartcase

" set the runtime path to include Vundle and initialize
"set rtp+=~/.vim/bundle/Vundle.vim/
"call vundle#begin()
set rtp+=$HOME/vimfiles/bundle/Vundle.vim/
call vundle#begin('$HOME/vimfiles/bundle/')

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
" Plugin 'klen/python-mode.git'

" YCM插件
Plugin 'Valloric/YouCompleteMe'

" nerdtree插件
Plugin 'https://github.com/scrooloose/nerdtree.git'

" ctrlsf 插件：全局搜索插件
Plugin 'dyng/ctrlsf.vim'

" 主题插件
Plugin 'chriskempson/base16-vim'
Plugin 'connorholyday/vim-snazzy'

" markdown-preview
Plugin 'iamcco/mathjax-support-for-mkdp'
Plugin 'iamcco/markdown-preview.vim'

" markdown插件
"Plugin 'suan/vim-instant-markdown'
" 多光标编辑
Plugin 'terryma/vim-multiple-cursors'

" markdown-preview
Plugin 'iamcco/markdown-preview.nvim', { 'do': { -> mkdp#util#install() }, 'for': ['markdown', 'vim-plug']}

" 注释插件
Plugin 'preservim/nerdcommenter'

" 光标下划线插件
Plugin 'itchyny/vim-cursorword'
" 关键词高亮插件
Plugin 'lfv89/vim-interestingwords'

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

" 取消高亮
noremap <LEADER><CR> :nohlsearch<CR>

" 保存
map S :w<CR>
" 退出
map Q :q<CR>
" 加载vimrc
map R :source $MYVIMRC<CR>

" 往右边分屏
map sl :set splitright<CR>:vsplit<CR>
map sh :set nosplitright<CR>:vsplit<CR>
map sk :set nosplitbelow<CR>:split<CR>
map sj :set splitbelow<CR>:split<CR>
" 分屏跳转
map <C-h> <C-w>h
map <C-j> <C-w>j
map <C-k> <C-w>k
map <C-l> <C-w>l

" 分屏大小
map <C-up> :res +5<CR>
map <C-down> :res -5<CR>
map <C-left> :vertical resize -5<CR>
map <C-right> :vertical resize +5<CR>

" 分屏切换
map sv <C-w>t<C-w>H
map sh <C-w>t<C-w>K

" 新建一个标签
map tu :tabe<CR>
map th :-tabnext<CR>
map tl :+tabnext<CR>


nmap <C-\>   <Plug>NERDCommenterToggle
vmap <C-\>   <Plug>NERDCommenterToggle<CR>gv


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

"set background=dark
colorscheme solarized
"colorscheme molokai
"colorscheme molokai-dark
"colorscheme phd
"colorscheme base16-default
"let g:molokai_original = 1
"let g:rehash256 = 1
"set background=dark
"set t_Co=256
"colo molokai
"colo lucius
"colo gruvbox
"colo jellybeans
" colo snazzy
" let g:SnazzyTransparent = 1


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
set foldmethod=indent
"set foldmethod=syntax
" 启动 vim 时关闭折叠代码
set nofoldenable

" 解决backspace键不能删除的问题
set backspace=indent,eol,start

" *.cpp 和 *.h 间切换
nmap <silent> <Leader>sw :FSHere<cr>

" 设置 tagbar 子窗口的位置出现在主编辑区的左边 
let tagbar_left=1 
" 设置显示／隐藏标签列表子窗口的快捷键。速记：identifier list by tag
nnoremap <Leader>l :TagbarToggle<CR> 
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
let g:tagbar_ctags_bin='C:\Users\ahwi\vimfiles\bundle\ctags\ctags.exe'

set encoding=utf-8  " The encoding displayed.
set fileencoding=utf-8  " The encoding written to file.


"let g:ycm_server_python_interpreter="C:\Users\ahwi\AppData\Local\Programs\Python\Python36\python3.exe"
"let g:ycm_python_binary_path="C:\Users\ahwi\AppData\Local\Programs\Python\Python36\python3.exe"

let g:pymode_python = 'python3'
set pythonthreedll=python36.dll

" 使用 NERDTree 插件查看工程文件。设置快捷键，速记：file list
map tt :NERDTreeToggle<CR>
" 设置NERDTree子窗口宽度
let NERDTreeWinSize=32
" 设置NERDTree子窗口位置
let NERDTreeWinPos="right"
" 显示隐藏文件
let NERDTreeShowHidden=1
" NERDTree 子窗口中不显示冗余帮助信息
let NERDTreeMinimalUI=1
" 删除文件时自动删除文件对应 buffer
let NERDTreeAutoDeleteBuffer=1


" YCM 补全菜单配色
" 菜单
highlight Pmenu ctermfg=2 ctermbg=3 guifg=#005f87 guibg=#EEE8D5
" 选中项
highlight PmenuSel ctermfg=2 ctermbg=3 guifg=#AFD700 guibg=#106900
" 补全功能在注释中同样有效
let g:ycm_complete_in_comments=1
" 允许 vim 加载 .ycm_extra_conf.py 文件，不再提示
let g:ycm_confirm_extra_conf=0
" 开启 YCM 标签补全引擎
let g:ycm_collect_identifiers_from_tags_files=1
" 引入 C++ 标准库tags
"set tags+=/data/misc/software/misc./vim/stdcpp.tags
" YCM 集成 OmniCppComplete 补全引擎，设置其快捷键
" inoremap <leader>; <C-x><C-o>
" 补全内容不以分割子窗口形式出现，只显示补全列表
set completeopt-=preview
" 从第一个键入字符就开始罗列匹配项
let g:ycm_min_num_of_chars_for_completion=1
" 禁止缓存匹配项，每次都重新生成匹配项
let g:ycm_cache_omnifunc=0
" 语法关键字补全			
let g:ycm_seed_identifiers_with_syntax=1

"let g:ycm_global_ycm_extra_conf="C:\Users\ahwi\vimfiles\bundle\YouCompleteMe\.ycm_extra_conf.py"

" 使用 ctrlsf.vim 插件在工程内全局查找光标所在关键字，设置快捷键。快捷键速记法：search in project
nnoremap <Leader>sp :CtrlSF<CR>


" 基于语义的声明/定义跳转
nnoremap <leader>jc :YcmCompleter GoToDeclaration<CR>
" 只能是 #include 或已打开的文件
nnoremap <leader>jd :YcmCompleter GoToDefinition<CR>

" 模板补全
" Track the engine.
Plugin 'SirVer/ultisnips'
" Snippets are separated from the engine. Add this if you want them:
Plugin 'honza/vim-snippets'
let g:UltiSnipsExpandTrigger="<leader><tab>"
let g:UltiSnipsJumpForwardTrigger="<leader><tab>"
let g:UltiSnipsJumpBackwardTrigger="<leader><s-tab>"


" markdown-preview ======================
" set to 1, nvim will open the preview window after entering the markdown buffer
" default: 0
let g:mkdp_auto_start = 0

" set to 1, the nvim will auto close current preview window when change
" from markdown buffer to another buffer
" default: 1
let g:mkdp_auto_close = 1

" set to 1, the vim will refresh markdown when save the buffer or
" leave from insert mode, default 0 is auto refresh markdown as you edit or
" move the cursor
" default: 0
let g:mkdp_refresh_slow = 0

" set to 1, the MarkdownPreview command can be use for all files,
" by default it can be use in markdown file
" default: 0
let g:mkdp_command_for_global = 0

" set to 1, preview server available to others in your network
" by default, the server listens on localhost (127.0.0.1)
" default: 0
let g:mkdp_open_to_the_world = 0

" use custom IP to open preview page
" useful when you work in remote vim and preview on local browser
" more detail see: https://github.com/iamcco/markdown-preview.nvim/pull/9
" default empty
let g:mkdp_open_ip = ''

" specify browser to open preview page
" default: ''
let g:mkdp_browser = ''

" set to 1, echo preview page url in command line when open preview page
" default is 0
let g:mkdp_echo_preview_url = 0

" a custom vim function name to open preview page
" this function will receive url as param
" default is empty
let g:mkdp_browserfunc = ''

" options for markdown render
" mkit: markdown-it options for render
" katex: katex options for math
" uml: markdown-it-plantuml options
" maid: mermaid options
" disable_sync_scroll: if disable sync scroll, default 0
" sync_scroll_type: 'middle', 'top' or 'relative', default value is 'middle'
"   middle: mean the cursor position alway show at the middle of the preview page
"   top: mean the vim top viewport alway show at the top of the preview page
"   relative: mean the cursor position alway show at the relative positon of the preview page
" hide_yaml_meta: if hide yaml metadata, default is 1
" sequence_diagrams: js-sequence-diagrams options
" content_editable: if enable content editable for preview page, default: v:false
let g:mkdp_preview_options = {
    \ 'mkit': {},
    \ 'katex': {},
    \ 'uml': {},
    \ 'maid': {},
    \ 'disable_sync_scroll': 0,
    \ 'sync_scroll_type': 'middle',
    \ 'hide_yaml_meta': 1,
    \ 'sequence_diagrams': {},
    \ 'flowchart_diagrams': {},
    \ 'content_editable': v:false
    \ }

" use a custom markdown style must be absolute path
" like '/Users/username/markdown.css' or expand('~/markdown.css')
let g:mkdp_markdown_css = ''

" use a custom highlight style must absolute path
" like '/Users/username/highlight.css' or expand('~/highlight.css')
let g:mkdp_highlight_css = ''

" use a custom port to start server or random for empty
let g:mkdp_port = ''

" preview page title
" ${name} will be replace with the file name
let g:mkdp_page_title = '「${name}」'


" example
nmap <C-s> <Plug>MarkdownPreview
nmap <M-s> <Plug>MarkdownPreviewStop
nmap <C-p> <Plug>MarkdownPreviewToggle

autocmd Filetype markdown inoremap ,f <Esc>/<++><CR>:nohlsearch<CR>c4l
autocmd Filetype markdown inoremap ,n ---<Enter><Enter>
autocmd Filetype markdown inoremap ,b **** <++><Esc>F*hi
autocmd Filetype markdown inoremap ,s ~~~~ <++><Esc>F~hi
autocmd Filetype markdown inoremap ,i ** <++><Esc>F*i
autocmd Filetype markdown inoremap ,d `` <++><Esc>F`i
autocmd Filetype markdown inoremap ,c ```<Enter><++><Enter>```<Enter><Enter><++><Esc>4kA
autocmd Filetype markdown inoremap ,h ====<Space><++><Esc>F=hi
autocmd Filetype markdown inoremap ,p ![](<++>) <++><Esc>F[a
autocmd Filetype markdown inoremap ,a [](<++>) <++><Esc>F[a
autocmd Filetype markdown inoremap ,1 #<Space><Enter><++><Esc>kA
autocmd Filetype markdown inoremap ,2 ##<Space><Enter><++><Esc>kA
autocmd Filetype markdown inoremap ,3 ###<Space><Enter><++><Esc>kA
autocmd Filetype markdown inoremap ,4 ####<Space><Enter><++><Esc>kA
autocmd Filetype markdown inoremap ,l --------<Enter>

" markdown-preview ======================

```

