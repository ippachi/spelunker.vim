# spelunker.vim
Spelunker.vim is a plugin that improved [Vim's spell checking function](https://vim-jp.org/vimdoc-en/options.html#'spell').  
It supports both Camel Case and Snake Case and provides a smart way to correct spelling.
This plugin have a whitelist for each programming language (currently JS, PHP, Ruby, CSS, HTML and Vim Script).

## 1.Installation
### vim-plug
```
Plug 'kamykn/spelunker.vim'
```

### NeoBundle
```
NeoBundle 'kamykn/spelunker.vim'
```

## 2.Usage
### 2.i. Settings
If you are using Vim's `spell`, turn it off (because it will highlight the same words).

```
set nospell
```

### 2.ii. Options
Spelunker.vim offers the following options.

```
" Enable spelunker.vim. (1 / 0) (default 1)
let g:enable_spelunker_vim = 1

" Setting for start checking min length of character. (default 4)
let g:spelunker_target_min_char_len = 4

" Setting for max suggest words list length. (default 15)
let g:spelunker_max_suggest_words = 15

" Setting for max highlight words each buffers. (default 100)
let g:spelunker_max_hi_words_each_buf = 100

" Override highlight group name of wrong spell words. (default 'SpelunkerSpellBad')
let g:spelunker_spell_bad_group = 'SpelunkerSpellBad'

" Override highlight group name of complex or compound words. (default 'SpelunkerComplexOrCompoundWord')
let g:spelunker_complex_or_compound_word_group = 'SpelunkerComplexOrCompoundWord'

" Override highlight setting.
highlight SpelunkerSpellBad cterm=underline ctermfg=247 gui=underline guifg=#9e9e9e
highlight SpelunkerComplexOrCompoundWord cterm=underline ctermfg=NONE gui=underline guifg=NONE

" Disable default autogroup. (default 0 - check all file types)
let g:spelunker_disable_auto_group = 1
" then specify custom autogroup with file types you want to check:
augroup spelunker
  autocmd!
  autocmd BufWinEnter,BufWritePost *.vim,*.js,*.jsx,*.json,*.md call spelunker#check()
augroup END
```

![spelunker_highlight_group](https://user-images.githubusercontent.com/7608231/48882590-71e57600-ee5e-11e8-9b1a-16191c1ac3b9.png)

## 3.Commands
### 3.i. Correct wrong spell.

**ZL / Zl**  
In a buffer with many camel cases, it will suggest same case words. (And snake case also too.)  
This suggestion list is generated by `spellsuggest()`.  
Move the cursor over the wrong spelling and enter the following commands

```
" Correct all words in buffer to word you selected.
ZL

" For under cursor word only.
Zl
```

`ZL` command works like this.  
![spelunker_zl](https://user-images.githubusercontent.com/7608231/48882608-89246380-ee5e-11e8-88e3-958b47353ddb.gif)

**ZC / Zc**  
You can also edit directly like a Vim's `c` command.

```
" Correct all words in buffer to word you typed.
ZC

" For under cursor word only.
Zc
```

`ZC` command works like this.  
![spelunker_zc](https://user-images.githubusercontent.com/7608231/48882594-7c077480-ee5e-11e8-83fe-68691bb13823.gif)

**ZF / Zf**  
ZF command is correcting word to automatically selected words. (This is like a "I'm feeling lucky"!)

```
" Correct all words in buffer.
ZF

" For under cursor word only.
Zf
```

![spelunker_zf](https://user-images.githubusercontent.com/7608231/50171177-16ab8400-0335-11e9-8eae-6ce1b249babd.gif)

**These functions work on not only wrong spelling, but also correct spelling!**

### 3.ii. Add words to spellfile.
Spelunker.vim use `spell` commands provided by Vim as default.  
You can add under cursor word to `spellfile` with following commands (like a Vim commands):

```
" Add selected word to spellfile
" => zg
Zg

" => zw
Zw

" => zug
Zug

" => zuw
Zuw

" Add selected word to the internal word list
" => zG
ZG

" => zW
ZW

" => zuG
ZUG

" => zuW
ZUW
```

FYI:
http://vim-jp.org/vimdoc-en/spell.html#zg

### 3.iii. Add all misspelled words in buffer to spellfile.
When there are many misspelled words, it is possible to add them all to the `spellfile`.

```
:SpelunkerAddAll
```

## 4.Whitelist
### 4.i. Whitelist applied to all programming languages.
Commonly used words are set to be excluded.  
Compound words and complex words may be highlighted incorrectly, but another highlight group (SpelunkerComplexOrCompoundWord) is being adapted.

Please see the code for details.  
https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list.vim

### 4.ii. Whitelist adapted according to programming language.
Currently only JS (TypeScript), PHP, Ruby, HTML, CSS and Vim Script are supported.  
Other programming languages will be added in the future.  

| Programming language | White list |
| --- | --- |
| Vim Script | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_vim.vim|
| PHP | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_php.vim |
| JS (TypeScript) | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_javascript.vim |
| Ruby | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_ruby.vim |
| HTML | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_html.vim |
| CSS, LESS, SCSS(Sass) | https://github.com/kamykn/spelunker.vim/blob/master/autoload/spelunker/white_list_css.vim |

### 4.iii. User's whitelist.
You can add your whitelist setting.
It is very easy to add.
Please add to .vimrc as follows:

```
" example
let g:spelunker_white_list_for_user = ['kamykn', 'vimrc']
```
