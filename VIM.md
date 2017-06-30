# VIM

## command
+ d  
  delete
+ h/j/k/l  
  move left/down/up/right
+ v  
  enter VISUAL mode
+ :e
+ :w
+ :q
+ :syntax enable
+ :colorscheme darkblue
+ :pwd
+ :so %  
  source the current file as vimrc


## vimrc
```
syntax enable
colorscheme darkblue
set backspace=indent,eol,start      " Make backspace behave like every other editor.

let mapleader = ','                 " The default leader is \, but a comma is much better.
"---------------------------------  Mappings  ---------------------------------"
" Make it easy to edit the vimrc file.
nmap <leader>ev :tabedit $MYVIMRC<cr>
" Make a simple highlight search removal
nmap <leader><space> :nohlsearch<cr>

"-------------------------------  Auto-Commands  -------------------------------"
" Automatically source the vimrc file on save.
autocmd BufWritePost .vimrc source %

"---------------------------------   Search   ---------------------------------"
set hlsearch
set incsearch
```
