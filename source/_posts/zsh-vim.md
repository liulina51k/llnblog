title: 'zsh & vim'
date: 2015-12-09 22:56:59
categories: Linux 学习笔记
tags: Linux 学习笔记
---
今天主要介绍linux中的`zsh`，以及`vim`部分相关内容,以后若了解的更多，会继续介绍,本文摘自池建强macshuo.com相关文章。
<!--more-->
### 安装zsh
```
sudo yum install zsh //Redhat Linux
sudo apt-get install zsh //Ubuntu Linux
```

### 安装oh my zsh
自动安装：
```
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```
手动安装
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
安装完成后设置当前用户使用 zsh：chsh -s /bin/zsh ,退出当前会话重新打开一个终端窗口，你就可以见到这个彩色的提示了！

### 自定义设置
```
alias cls='clear'
alias ll='ls -l'
alias la='ls -a'
alias l='ls -al'
alias ld='ls -ald'
alias vi='vim
```

### 插件相关介绍
autojump 插件安装 (linux下)
```
//1.下载最新版本
git clone git://github.com/joelthelion/autojump.git
//2.解压缩后进入目录，执行
./install.py
//3.最后把以下代码加入.zshrc
[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh
```
安装完毕，重新退出，测试!

### .vimrc 基本配置
```
syn on                      "语法支持

"common conf {{             通用配置
set ai                      "自动缩进
set bs=2                    "在insert模式下用退格键删除
set showmatch               "代码匹配
set laststatus=2            "总是显示状态行
set expandtab               "以下三个配置配合使用，设置tab和缩进空格数
set shiftwidth=4
set tabstop=4
set cursorline              "为光标所在行加下划线
set number                  "显示行号
set autoread                "文件在Vim之外修改过，自动重新读入
set autoindent              "自动缩排

set ignorecase              "检索时忽略大小写
set fileencodings=uft-8,gbk "使用utf-8或gbk打开文件
set hls                     "检索时高亮显示匹配项
set helplang=cn             "帮助系统设置为中文
set foldmethod=syntax       "代码折叠
"}}

" conf for tabs, 为标签页进行的配置，通过ctrl h/l切换标签等
let mapleader = ','
nnoremap <C-l> gt
nnoremap <C-h> gT
nnoremap <leader>t : tabe<CR>
"conf for plugins {{ 插件相关的配置
"状态栏的配置
"powerline{
set guifont=PowerlineSymbols\ for\ Powerline
set nocompatible
set t_Co=256
let g:Powerline_symbols = 'fancy'
"}
"pathogen是Vim用来管理插件的插件
"pathogen{
"call pathogen#infect()
"}

"}}
```
暂时先介绍到这里!
