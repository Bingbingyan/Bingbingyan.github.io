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
```

## 常用配置
```vim

    " :bd 删除当前 buffer
    " :1,5bw Wipe 1~5 buffer
    " :xd 删除末尾空格

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

    " 格式 Json 字符串
    map <Leader>fj :%!python -m json.tool<CR>

    "tabs
    nmap <leader>tn :tabnew<cr>
    nmap <leader>tc :tabclose<cr>

    " disable arrow keys in normal mode
    noremap <Up> <Nop>
    noremap <Down> <Nop>
    noremap <Left> <Nop>
    noremap <Right> <Nop>

    "高亮行位空格
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
```
