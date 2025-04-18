## 介绍

* 名字：Vim
* 语言：英文
* 平台：Windows
* 翻译：语言包
* 类型：文件管理
---
* 评分：10
* 评价：最为强大的全能文本编辑器。
* 封面：
![](https://alist.linmoumoulinny.top/p/Webdav/VPS/Storages/Vim/-2091442061.1.jpg)
* 图片：
![](https://alist.linmoumoulinny.top/p/Webdav/VPS/Storages/Vim/PixPin_2025-04-16_04-03-16.jpg)
* 简介：Vim 是一个类似于 Vi 的高度可定制的文本编辑器，在 Vi 的基础上改进和增加了很多特性。
---
* 现文件名：\[gVim]\[9.1.0]\[CHS].7z
* 原文件名：
	* gvim_9.1.0_x86_signed.exe
	* gvim_9.1.0_x64_signed.exe
* 大小：
	* 9.8912 MB
	* 10.4535 MB
* 散列：
	* 6B0282FDFA28AA2858D22BC2D5CC6F56
	* C9791F723EAD996CEE2B96AE5ACB6B11
* 引用页：[https://www.vim.org/download.php]()
* 主链接：
	* [https://github.com/vim/vim-win32-installer/releases/download/v9.1.0/gvim_9.1.0_x86_signed.exe]()
	* [https://github.com/vim/vim-win32-installer/releases/download/v9.1.0/gvim_9.1.0_x64_signed.exe]()
* 标准链接：
	* [ed2k://|file|gvim_9.1.0_x86_signed.exe|10371624|6B0282FDFA28AA2858D22BC2D5CC6F56|h=QONVG6E6UPSSSZL7EPDRVRO5WRVMBPQ5|/]()
	* [ed2k://|file|gvim_9.1.0_x64_signed.exe|10961248|C9791F723EAD996CEE2B96AE5ACB6B11|h=UNMTBK67Y37CBVIE2RMHR4AZDOHAMEH7|/]()
* 下载方式：浏览器

## 安装方法

* 下载后解压缩。
* 运行“gvim_9.1.0_x64_signed.exe”安装。

## 使用技巧

### 设置

Vim 的配置文件在安装目录下的“\_vimrc”。它没有后缀名，但其实是个文本文件。可以用编辑器打开。

这是我个人向设置：

```
set autoread										" 自动更新，当文件在外部被修改时。
set autowrite										" 自动保存。
set clipboard+=unnamed					" 共享剪切板。
set nobackup										" 不备份。
set noundofile										" 无撤销文件。
set noswapfile										" 无 swap 文件。
set noexpandtab									" 避免“\<Tab>”转为空格。
set wrap												" 自动换行。
set hlsearch											" 搜索时高亮。
set ignorecase										" 查找大小写不敏感，
set smartcase										" 如果有一个大写字母则切换到大小写敏感查找。
set guifont=Cascadia\ Mono:h18		" 设置字体。
set number											" 设置行号。
set ruler												" 显示标尺。
set showmatch									" 高亮显示匹配的括号。
set ambiwidth=double							" 设置为双倍字符宽度。

let mapleader=" `"								" 设置先导键为“`”。

syntax enable										" 自动开启语法高亮。

autocmd VimEnter * :startinsert			" 预设编辑模式。


" 预设为窗口最大化。
if has('win32') || has('win64')    
	au GUIEnter * simalt ~x
else    
	au GUIEnter * call MaximizeWindow()
endif 
function! MaximizeWindow()    
	silent !wmctrl -r :ACTIVE: -b add,maximized_vert,maximized_horz
endfunction

" 定义全局函数：判断是否在文件最后一行，并根据情况移动。
function! MoveDownOrEnd()
    let l:current_line = line('.')
    let l:current_col = col('.')
    let l:view = winsaveview()
    " 尝试向下移动一个屏幕行。
    execute "normal! gj"
    let l:new_view = winsaveview()
    " 判断视图是否未改变（无法滚动/移动）且光标位于窗口最后一行。
    if l:view.lnum == l:new_view.lnum && l:view.topline == l:new_view.topline
        \ && winline() == winheight(0)
        execute "normal! $"
    else
        call winrestview(l:new_view)
    endif
endfunction

" 将方向键键映射
nnoremap <silent> <Up> gk
inoremap <silent> <Up> <C-o>gk
snoremap <silent> <Up> gk
vnoremap <silent> <Up> gk
nnoremap <silent> <Down> :call MoveDownOrEnd()<CR>
inoremap <silent> <Down> <C-o>:call MoveDownOrEnd()<CR>
snoremap <silent> <Down> gj
vnoremap <silent> <Down> gj
nnoremap <silent> <Left> h
snoremap <silent> <Left> h
vnoremap <silent> <Left> h
nnoremap <silent> <Right> l
snoremap <silent> <Right> l
vnoremap <silent> <Right> l

" 将“\<Ctrl>＋q”映射到可视模式；将“\<Ctrl>＋w”映射到可视行模式。
nnoremap <silent> <C-q> v
inoremap <silent> <C-q> <C-o>v
snoremap <silent> <C-q> <C-o>v
vnoremap <silent> <C-q> <C-o>v
nnoremap <silent> <C-w> V
inoremap <silent> <C-w> <C-o>V
snoremap <silent> <C-w> <C-o>V
vnoremap <silent> <C-w> <C-o>V

" 其他键位映射。
nnoremap <silent> <C-k> gg
snoremap <silent> <C-k> gg
vnoremap <silent> <C-k> gg
nnoremap <silent> <C-j> G
snoremap <silent> <C-j> G
vnoremap <silent> <C-j> G
nnoremap <silent> <C-h> ^
snoremap <silent> <C-h> ^
vnoremap <silent> <C-h> ^
nnoremap <silent> <C-l> $
snoremap <silent> <C-l> $
vnoremap <silent> <C-l> $
```

## 操作

### 模式

1. 正常模式：我们进入 Vim 的时候就是正常模式。这种模式下可以使用相应命令进行操作。在任何其他模式下，按“\<Esc>”键，可以进入正常模式。
2. 插入模式：正常模式下，按“a”或“i”键，可以进入插入模式。在这种模式下，可以对文件进行编辑。这里我们在“\_vimrc”设置了“autocmd VimEnter * :startinsert”，则预设即为编辑模式。
3. 命令模式：正常模式下，按“:”（小写冒号）键，可以进入插入模式。在命令模式中可以执行一些输入并执行一些 Vim 或插件提供的指令，就像在 shell 里一样。
4. 可视模式：正常模式下，按“v”键，可以进入可视模式，可以进行块选取。这里我们在“\_vimrc”设置后绑定为“\<Ctrl>＋q”键。正常模式下，按“V”键，可以进入可视行模式：即立即选取一行。这里我们在“\_vimrc”设置后绑定为“\<Ctrl>＋w”键。
5. 选择模式：用鼠标拖选区域的时候，就进入了选择模式。在这个模式下，选择完后，敲任何按键就直接输入并替换选择的文本了。
6. 替换模式：正常模式下，按“r”键，可以进入替换模式，进行单字替换，替换完后进入正常模式。正常模式下，按“R”键，可以进入替换模式，进行连续替换。

### 命令

#### 移动 

| 键位       | 原键位 | 功能                                                 |
| ---------- | ------ | ---------------------------------------------------- |
| \<Left>    | h      | 光标向左移动，用 5h 表示光标向左移动 5 次。          |
| \<Down>    | j      | 光标向下移动一行。用 5j 表示光标向下移动 5 次。      |
| \<Down>    | gj     | 光标向下移动一屏幕行（一行内被折叠的分行）。         |
| \<Up>      | k      | 光标向上移动一行。用 5k 表示光标向上移动 5 次。      |
| \<Up>      | gk     | 光标向上移动一屏幕行（一行内被折叠的分行）。         |
| \<Right>   | l      | 光标向右移动。用 5l 表示光标向右移动 5 次。          |
| \<Ctrl>＋k | gg     | 跳转到文本最上方。                                   |
| \<Ctrl>＋j | G      | 跳转到文本最下方。                                   |
| H          |        | 光标移动到屏幕上部可见行的开头。                     |
| M          |        | 光标移动到屏幕中间可见行的开头。                     |
| L          |        | 光标移动到屏幕下部可见行的开头。                     |
| \<Ctrl>＋h | ^      | 光标移动到行首。                                     |
| \<Ctrl>＋l | $      | 光标移动到行尾。                                     |
| %          |        | 光标在配对出现的符号时候，移动到另一侧。             |
| w          |        | 跳转到下一个单词的开头，以标点符号、空格作为分隔符。 |
| b          |        | 跳转到上一个单词的开头，以标点符号、空格作为分隔符。 |
| f＋x       |        | 同一行内，向右跳转到第一个“x”。                    |
| F＋x       |        | 同一行内，向左跳转到第一个“x”。                    |

#### 插入 

| 键位 | 原键位 | 功能                         |
| ---- | ------ | ---                          |
| a    |        | 光标所在的字符之后插入。     |
| i    |        | 光标所在的字符之前插入。     |
| A    |        | 光标所在行的行尾插入。       |
| I    |        | 光标所在的字符之前插入。     |
| o    |        | 光标所在行的下一行行首插入。 |
| O    |        | 光标所在行的上一行行首插入。 |

#### 修改 

| 键位       | 原键位 | 功能                                                |
| ---------- | ------ | --------------------------------------------------- |
| \<Ctrl>＋x | d      | 剪切，用 5d 表示剪切 5 个字符。                     |
| \<Ctrl>＋c | y      | 复制，用 5y 表示复制 5 个字符。                     |
| \<Ctrl>＋v | p      | 粘贴，用 5p 表示粘贴 5 个字符。                     |
| D          | dd     | 剪切一行，用 5dd 表示剪切 5 行。                    |
| Y          | yy     | 复制一行，用 5yy 表示复制 5 行。                    |
| \<Del>     | x      | 删除当前光标所在处的字符，用 5x 表示删除 5 个字符。 |
| \<Ctrl>＋z | u      | 撤销上一步操作，用 5u 表示撤销 5 次。               |
| \<Ctrl>＋y |        | 反撤销上一步操作。                                  |
| cw         |        | 删除光标处一个单词，并进入插入模式。                |
| ci(        |        | 删除括号内的内容，并进入插入模式。                  |
| c^         |        | 删除至行首，并进入插入模式。                        |
| c$         |        | 删除至行尾，并进入插入模式。                        |

#### 搜索 

| 键位            | 原键位 | 功能                                |
| --------------- | ------ | ----------------------------------- |
| /abc            |        | 向下搜索 abc 这个词一次。           |
| ?abc            |        | 向上搜索 abc 这个词一次。           |
| /\<abc>         |        | 向下精确匹配搜索 abc 这个词一次。   |
| /\\t            |        | 向下搜索 \<Tab> 这个符号一次。      |
| /\\s            |        | 向下搜索 \<Space> 这个符号一次。    |
| n               |        | 跳到下一个匹配项。                  |
| N               |        | 跳到上一个匹配项。                  |
| *               |        | 向下搜索光标所在单词一次。          |
| #               |        | 向上搜索光标所在单词一次。          |
| :s/abc/def      |        | 行内替换 abc 为 def 一次。          |
| :s/abc/def/g    |        | 行内替换所有 abc 为 def。           |
| :%s/abc/def/g   |        | 全文替换 abc 为 def。               |
| :%s/abc/def/gc  |        | 全文替换 abc 为 def，要求每次确认。 |

#### 文件操作 

| 键位 | 原键位 | 功能             |
| ---- | ------ | ---------------- |
| :q   |        | 退出。           |
| :q!  |        | 强制不保存退出。 |
| :w   |        | 写入。           |
| :wq  |        | 保存并退出。     |
| :wq! |        | 强制保存并退出。 |

## 插件

### 插件的安装

安装 vim-plug，下载 plug.vim 文件，放在安装文件夹下“vimfiles\autoload\”内。
[https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim]()
[ed2k://|file|plug.vim|84862|0962D8DA52E133CC8AE92EC6D0928A41|h=Q5Q5ZLM4N37MIW332E4AOBAT2YLHIIH7|/]()

在“\_vimrc”文件内，添加内容：

```
" 安装插件。
call plug#begin()

Plug 'vim-airline/vim-airline'

Plug 'Chiel92/vim-autoformat'
let g:autoformat_verbosemode=0 " 详细模式。
let g:autoformat_autoindent = 0
let g:autoformat_retab = 1
let g:autoformat_remove_trailing_spaces = 1
let g:formatdef_hl_js='" js-beautify" '
let g:formatdef_hl_c='" clang-format -style=\" {BasedOnStyle: LLVM, UseTab: Never, IndentWidth: 4, PointerAlignment: Right, ColumnLimit: 150, SpacesBeforeTrailingComments: 1}\" " ' " 指定格式化的方式, 使用配置参数。
let g:formatters_c = ['hl_c']
let g:formatters_cpp = ['hl_c']
let g:formatters_json = ['hl_js']
let g:formatters_js = ['hl_js']
let g:formatdef_sqlformat = '" sqlformat --keywords upper -" '
let g:formatters_sql = ['sqlformat']
" 保存时自动格式化指定文件类型代码
" au BufWrite *:Autoformat
" autocmd BufWrite *.sql,*.c,*.py,*.java,*.js:Autoformat " 设置发生保存事件时执行格式化。

Plug 'preservim/nerdtree'

Plug 'Xuyuanp/nerdtree-git-plugin' " 目录树 git 状态显示
" 设置“<F1>”开启和关闭 NerdTree。
map <F1> :NERDTreeToggle<CR>
let NERDTreeChDirMode=1
let NERDTreeShowBookmarks=1 " 显示书签
let NERDTreeIgnore=['\~$', '\.pyc$', '\.swp$'] " 设置忽略文件类型
let NERDTreeWinSize=25 " 窗口大小

Plug 'mbbill/undotree'
" 设置“<F2>”开启和关闭 Undotree。
map <F2> :UndotreeToggle<CR>

Plug 'easymotion/vim-easymotion'  
let g:EasyMotion_smartcase = 1
" let g:EasyMotion_startofline = 0 " keep cursor colum when JK motion.
map <Leader><leader>h <Plug>(easymotion-linebackward)
map <Leader><Leader>j <Plug>(easymotion-j)
map <Leader><Leader>k <Plug>(easymotion-k)
map <Leader><leader>l <Plug>(easymotion-lineforward)
" 重复上一次操作。
map <Leader><leader>. <Plug>(easymotion-repeat)

call plug#end()
```

最后，启动 Vim，安装插件。

```
:PlugInstall
```

![](https://alist.linmoumoulinny.top/p/Webdav/VPS/Storages/Vim/PixPin_2025-04-16_05-14-39.jpg)
