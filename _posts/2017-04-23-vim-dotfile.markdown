# VIM 配置
## space-vim
vim 神器配置：[space-vim](https://github.com/liuchengxu/space-vim)

## 常用插件
```vim
    " 自动格式化，中文排版
    Plug 'hotoo/pangu.vim'
    " 预览查询结果
    Plug 'osyo-manga/vim-over'
    " 彩虹括号
    Plug 'luochen1990/rainbow'
    " VIM Table Mode
    Plug 'dhruvasagar/vim-table-mode'
    Plug 'nvie/vim-flake8'
    Plug 'scrooloose/syntastic'
    Plug 'hynek/vim-python-pep8-indent'

    Plug 'Valloric/ycmd'
    Plug 'ayu-theme/ayu-vim'

    " 从 Insert Mode 切换到 Normal Mode 时 自动将输入法切换为英文
    Plug 'CodeFalling/fcitx-vim-osx'

    " 可视化剪贴板
    Plug 'vim-scripts/YankRing.vim'
```

## 常用配置
```vim

    " :bd 删除当前 buffer
    " :1,5bw Wipe 1~5 buffer
    " :xd 删除末尾空格

    " :YRShow 显示剪贴板的内容
    " :vs 纵向分割窗口
    " :split 横向分割窗口


    map    <Leader>n  :tabnext<CR>
    " Use Tab to switch buffer
    nnoremap <Leader><Tab> :Buffers<CR>
    nnoremap <Tab> :bn<CR>
    nnoremap <S-Tab> :bp<CR>

    " Make search results appear in the middle of the screen
    nnoremap n nzz
    nnoremap N Nzz
    nnoremap * *zz
    nnoremap # #zz
    nnoremap g* g*zz
    nnoremap g# g#zz

    " Ctag Location
    " let g:airline_powerline_fonts=1
    let Tlist_Ctags_Cmd="/usr/local/Cellar/ctags/5.8_1/bin/ctags"

    set expandtab
    set tabstop=4
    set shiftwidth=4
    set wrap
    set autoread
    " Enable folding
    set foldmethod=syntax
    set foldlevelstart=0
    " 代码折叠的层级
    set foldnestmax=3
    set foldlevel=0

    " 搜索时忽略大小写
    set ic
    " NERDTree 打开/关闭
    map <F4> :NERDTreeToggle<CR>
    map <Leader><F4> :NERDTreeMirror<CR> :NERDTreeFind<CR>
    " NERDTree 显示行号
    let g:NERDTreeShowLineNumbers=1
    " NERDTree 显示相对行号
    autocmd FileType nerdtree setlocal relativenumber
    " 设置 NerdTree 默认宽度
    let g:NERDTreeWinSize=50

    " Format Python Script
    nmap <Leader>pf :0,$!yapf<CR>
    let g:netrw_list_hide= '.*\.pyc$'
    set wildignore=*.pyc

    "tabs
    nmap <leader>tn :tabnew<cr>
    nmap <leader>tc :tabclose<cr>

    " 直接删除，不放到剪切板
    nnoremap d "_d
    vnoremap d "_d
    vnoremap D "_D
    vnoremap p "_dhp

    " disable arrow keys in normal mode
    noremap <Up> <Nop>
    noremap <Down> <Nop>
    noremap <Left> <Nop>
    noremap <Right> <Nop>

    "高亮行尾空格
    highlight ExtraWhitespace ctermbg=red guibg=red
    match ExtraWhitespace /\s\+$/
    autocmd BufWinEnter * match ExtraWhitespace /\s\+$/
    autocmd InsertEnter * match ExtraWhitespace /\s\+\%#\@<!$/
    autocmd InsertLeave * match ExtraWhitespace /\s\+$/
    autocmd BufWinLeave * call clearmatches()

    " 设置 cshtml 文件默认按照 HTML 进行高亮
    au BufRead,BufNewFile cshtml set filetype=html

    " fzf ag search
    " Search UserHome Folder
    nnoremap <Leader>f? :Files ~<CR>
    " Search current CWD
    nnoremap <Leader>ff :Files<CR>

    nnoremap <Leader>ag :execute 'Ag ' . input('Ag/')<CR>
    " search current word with Ag
    nnoremap <Leader>ac :call SearchWordWithAg()<CR>
    function! SearchWordWithAg()
        execute 'Ag' expand('<cword>')
    endfunction

    " 多光标操作
    let g:multi_cursor_use_default_mapping=0
    let g:multi_cursor_next_key='<C-m>'
    let g:multi_cursor_prev_key='<C-p>'
    let g:multi_cursor_skip_key='<C-x>'
    let g:multi_cursor_quit_key='<Esc>'

    " 格式 Json 字符串
    function FormatJSON(...)
      let code="\"
            \ var i = process.stdin, d = '';
            \ i.resume();
            \ i.setEncoding('utf8');
            \ i.on('data', function(data) { d += data; });
            \ i.on('end', function() {
            \     console.log(JSON.stringify(JSON.parse(d), null,
            \ " . (a:0 ? a:1 ? a:1 : 2 : 2) . "));
            \ });\""
      execute "%! node -e " . code
    endfunction
    map <Leader>fj :call FormatJSON(v:count)<CR>

    function JQFilter(name)
      echom "Example: '.data[].areaname'"
      " 筛选条件不为空则执行筛选
      if strlen(a:name)>0
          silent execute '!clear'
          " 复制筛选结果到剪贴板
          silent execute '!cat %|jq ' a:name '|pbcopy'
          " 打印出筛选结果
          execute '!cat %|jq ' a:name 
      endif
    endfunction
    " 调用 jq 筛选 Json 内容
    " !cat % | jq '.data[].areaname'
    nnoremap <Leader>jq :call JQFilter(input('jq/'))<CR>

    " 翻译当前光标所在单词
    nmap <Leader>t :!echo --==<C-R><C-w>==-- ;ici <C-R><C-W><CR>
```

## 技巧
- fzf
    - 在 Ag 窗口中使用 Tab 键可以选择多个文件，敲回车后选择的文件自动加载到 QuickFix 窗口
- 获取当前文件的路径和文件名
`!echo %:p`
- 获取当前文件的路径
`!echo %:p:h`
>%: 当前文件的相对路径
>%:p 当前文件的绝对路径
>%:p:h 当前文件的绝对目录
>%:h 当前文件的相对目录
- iw 与 aw 区别
    - iw: 光标所在位置当前单词
    - aw: 光标所在位置当前单词，及后面一个空格
- Ctrl+o: 在 Insert 模式下，执行一次 Normal 模式的命令，并回到 Insert 模式
- 【I: 显示当前文档中，包含当前光标所在单词的行
- ma: 在当前光标所在位置添加标签：a
- set paste: 粘贴代码时，不自动缩进
- 删除所有空行：g/^$/d
- 删除XML 中的注释：g/^\s\+<!.*/d
    - 删除以空格+<!开头的行
- :CtrlP：快速打开pwd下的文件
- 复制查询结果到剪切板
    - :g/XXX/y A
    - :let @+ = @
- ngt: 直接跳转到第 n 个 Tab
- verbose imap <c-j>: 查看<c-j> 组合键的映射
