

>我需要一个简单，开箱即用的可视化编辑软件。
>
>vim太过复杂，可能不是很适合我，它有优势，不过完全没有必要。不过可以放置Linux/终端使用场景中。


一个概念，`.vimrc`中的配置文件都是基于vimscript脚本的，`:echo` 、`:echom`两个命令其实就是脚本中的两个基础命令。vim底部的:操作则类似于vimscript实时执行的的控制台。


**插件，命令，快捷键，模式。——易用性的核心。**

Vim 的脚本语言被称为 Vimscript，是典型的动态命令式语言，提供了大多数常见的语言特性：变量、表达式、控制结构、内置函数、用户定义函数、一级字符串、高级数据结构（列表和字典）、终端和文件 I/O、正则表达式模式匹配、异常和集成调试器。


你最初接触到 Vim 脚本是在 vimrc 文件里。当 Vim 启动时它将读取该文件的内容并执行其中的命令。你可以在其中设置选项。你也可以在其中使用**任何以 ":" 开头的命令**,这些命令有时也被称作 **Ex 命令**或**命令行命令**。
语法文件其实也是 Vim 脚本。专为某种文件类型设定选项的文件也是。一个很复杂的宏可以被单独的定义在一个 Vim 脚本文件中。你可以自己想到其它的应用。

### Vimscript 变量

Vim自身的文档非常棒。它不仅是详细地，而且也是非常透彻的。 我们可以在这里找到设置软件的变量。命令`<:help>`

`:map <c-d> dd`
现在在键盘上按下Ctrl+d将执行dd命令。


### VIM模式详解

•插入模式（Insert Mode) 
•替换模式(Replace Mode) 
•可视化模式(Visual Mode) 
•选择模式(Select Mode) 
•命令行模式(Command-line Mode) 
•Ex模式(Ex Mode)

几个环境变量：`$VIM`（Vim的安装目录），`$MYVIMRC`（用户配置文件）**一般配置vim，应该将个性化设置存放在`$MYVIMRC`用户配置文件而不应修改系统配置文件。**` $VIMRUNTIME`（运行时目录）


>**Nvim：Neovim 0.5 使用 Lua语言 成为 Neovim 的脚本语言，用于插件开发和用户配置。**


### Vim插件
vim-plug支持源码托管在GitHub的插件，你可以在github.com/vim-scripts/上找到vim官网里所有插件的镜像。

自动加载(autoload)：你可以在函数名中使用多个#来表示子目录。`:call `插件`#somefile#Hello()`。
就是在`～/.vim/bundles/插件/autoload `下查找一个叫做`somefile.vim`的文件。

自动加载plug插件管理的begin函数并且输入目录作为参数。

```vim
call plug#begin('~/.vim/plugged')
" Shorthand notation for plugin
Plug 'foo/bar'           USER(foo)/APP(bar)
call plug#end()
```

### 默认安装目录（$VIM）下的文件

![](images/vimedit-1.jpeg)


### VIM键位图&常用命令

![](images/vimedit-2.png.jpg)

![](images/vimedit-3.jpg)
`<:q> 等价于 <C-q>`

![](images/vimedit-4.png)


其它参考资料：VIM学习笔记-开篇/目录https://zhuanlan.zhihu.com/p/37478384

### 配置文件`_vimrc.rc`
```rc
"VIM 配置文件
"
"    Startup - 编辑器启动时需要添加的一些配置
"    General - 通用配置
"    Lang & Encoding - 语言和编码
"    GUI - 界面
"    Format - 基本的代码格式
"    Keymap - 通用的快捷键
"    Plugin - 插件相关（包括和当前插件相关的配置和快捷键等）
"    Function - vimrc 里面用到的常用方法
"


" Startup {{{
" Vim with all enhancements
source $VIMRUNTIME/vimrc_example.vim

" Remap a few keys for Windows behavior
source $VIMRUNTIME/mswin.vim

" Mouse behavior (the Windows way)
behave mswin

" Use the internal diff if available.
" Otherwise use the special 'diffexpr' for Windows.
if &diffopt !~# 'internal'
  set diffexpr=MyDiff()
endif
function MyDiff()
  let opt = '-a --binary '
  if &diffopt =~ 'icase' | let opt = opt . '-i ' | endif
  if &diffopt =~ 'iwhite' | let opt = opt . '-b ' | endif
  let arg1 = v:fname_in
  if arg1 =~ ' ' | let arg1 = '"' . arg1 . '"' | endif
  let arg1 = substitute(arg1, '!', '\!', 'g')
  let arg2 = v:fname_new
  if arg2 =~ ' ' | let arg2 = '"' . arg2 . '"' | endif
  let arg2 = substitute(arg2, '!', '\!', 'g')
  let arg3 = v:fname_out
  if arg3 =~ ' ' | let arg3 = '"' . arg3 . '"' | endif
  let arg3 = substitute(arg3, '!', '\!', 'g')
  if $VIMRUNTIME =~ ' '
    if &sh =~ '\<cmd'
      if empty(&shellxquote)
        let l:shxq_sav = ''
        set shellxquote&
      endif
      let cmd = '"' . $VIMRUNTIME . '\diff"'
    else
      let cmd = substitute($VIMRUNTIME, ' ', '" ', '') . '\diff"'
    endif
  else
    let cmd = $VIMRUNTIME . '\diff'
  endif
  let cmd = substitute(cmd, '!', '\!', 'g')
  silent execute '!' . cmd . ' ' . opt . arg1 . ' ' . arg2 . ' > ' . arg3
  if exists('l:shxq_sav')
    let &shellxquote=l:shxq_sav
  endif
endfunction

" vim 文件折叠方式为 marker
augroup ft_vim
    au!

    au FileType vim setlocal foldmethod=marker
augroup END

" }}}



" General {{{
set noundofile
set nobackup
set noswapfile
set history=1024
set autochdir
set whichwrap=b,s,<,>,[,]
set nobomb
set backspace=indent,eol,start whichwrap+=<,>,[,]

" Vim 的默认寄存器和系统剪贴板共享
set clipboard+=unnamed

" 设置 alt 键不映射到菜单栏
set winaltkeys=no
" }}}


" Lang & Encoding {{{
set termencoding=utf-8
set langmenu=zh_CN.utf-8
set fileencodings=utf-8,gbk2312,gbk,gb18030,cp936
set fileencodings=ucs-bom,utf-8,chinese
set encoding=utf-8
set langmenu=zh_CN
let $LANG = 'en_US.UTF-8'
language messages zh_cn.utf-8
" }}}


" GUI {{{
colorscheme molokai   "设置主题
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
set cursorline
set hlsearch
set number
" 窗口大小
set lines=35 columns=140
" 分割出来的窗口位于当前窗口下边/右边
set splitbelow
set splitright
"不显示工具/菜单栏
set guioptions-=T
set guioptions-=m
set guioptions-=L
set guioptions-=r
set guioptions-=b
" 使用内置 tab 样式而不是 gui
set guioptions-=e
set nolist
set listchars=tab:▶\ ,eol:¬,trail:·,extends:>,precedes:<
set guifont=Ubuntu\ Mono:h12
" }}}


" Format {{{
set autoindent
set smartindent
set tabstop=4
set expandtab
set softtabstop=4

"自动语法高亮
syntax on
set t_Co=256
" }}}


" Keymap {{{
" 尽量不要修改系统默认配置的快捷键，非要设置的话选择好相应的模式

" }}}


" Plugin {{{

" }}}


" Function {{{
" Remove trailing whitespace when writing a buffer, but not for diff files.
" From: Vigil
" @see http://blog.bs2.to/post/EdwardLee/17961
function! RemoveTrailingWhitespace()
    if &ft != "diff"
        let b:curcol = col(".")
        let b:curline = line(".")
        silent! %s/\s\+$//
        silent! %s/\(\s*\n\)\+\%$//
        call cursor(b:curline, b:curcol)
    endif
endfunction
autocmd BufWritePre * call RemoveTrailingWhitespace()
" }}}

```