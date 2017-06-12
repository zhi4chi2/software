# 安装
大部分 Linux 发行版配备的是 vim(Vi Improved)。通常 vi 硬链接（或别名）到 vim

```bash
me@mypc:~$ vi
me@mypc:~$
```
可以看到版本，当前是 VIM version 7.4.1689


```bash
me@mypc:~$ which vi
/usr/bin/vi
me@mypc:~$ ls -l /usr/bin/vi
lrwxrwxrwx 1 root root 20 Jun 21 2016 /usr/bin/vi -> /etc/alternatives/vi
me@mypc:~$ ls -l /etc/alternatives/vi
lrwxrwxrwx 1 root root 17 Jun 21 2016 /etc/alternatives/vi -> /usr/bin/vim.tiny
me@mypc:~$ ls -l /usr/bin/vim.tiny
-rwxr-xr-x 1 root root 1064592 Nov 25 04:51 /usr/bin/vim.tiny
me@mypc:~$
```

所以在 Ubuntu 中是 vi 通过符号链接链接到 vim.tiny 的。

Ubuntu 只安装 vim 的最小版本，需要安装完全版 vim

```bash
me@mypc:~$ apt-cache search vim
exuberant-ctags - build tag file indexes of source code definitions
grilo-plugins-0.2-base - Framework for discovering and browsing media - Base Plugins
tmux - terminal multiplexer
vim - Vi IMproved - enhanced vi editor
vim-common - Vi IMproved - Common files
vim-doc - Vi IMproved - HTML documentation
vim-gnome - Vi IMproved - enhanced vi editor - with GNOME2 GUI
vim-gui-common - Vi IMproved - Common GUI files
vim-runtime - Vi IMproved - Runtime files
vim-tiny - Vi IMproved - enhanced vi editor - compact version
acr - autoconf like tool
alot - Text mode MUA using notmuch mail
alot-doc - Text mode MUA using notmuch mail - documentation
apvlv - PDF viewer with Vim-like behaviour
bicyclerepair - A refactoring tool for python
bleachbit - delete unnecessary files from the system
cernlib-base - CERNLIB data analysis suite - common files
clang-format-3.5 - Tool to format C/C++/Obj-C code
clang-format-3.6 - Tool to format C/C++/Obj-C code
clang-format-3.7 - Tool to format C/C++/Obj-C code
clang-format-3.8 - Tool to format C/C++/Obj-C code
colordiff - tool to colorize 'diff' output
context-modules - additional ConTeXt modules
cpl-plugin-vimos - ESO data reduction pipeline for VIMOS
cpl-plugin-vimos-calib - ESO data reduction pipeline calibration data downloader for VIMOS
cpl-plugin-vimos-doc - ESO data reduction pipeline documentation for VIMOS
cream - VIM macros that make the VIM easier to use for beginners
csvimp - CSV data import tool for xTuple applications
dmtcp - Checkpoint/Restart functionality for Linux processes
dmtcp-dbg - Debug package for dmtcp
editmoin - edit MoinMoin wiki pages with your favourite editor
ejabberd-mod-shcommands - execute shell commands via XMPP (dangerous!)
elvis-tiny - Tiny vi compatible editor for the base system
fim - a scriptable frame buffer and ascii art image viewer
get-flash-videos - video downloader for various Flash-based video hosting sites
global - Source code search and browse tools
glogg - Smart interactive log explorer using Qt
gramadoir - Irish language grammar checker (integration scripts)
hothasktags - Haskell ctags generator
jvim-canna - Japanized VIM (Canna version)
jvim-doc - Documentation for jvim (Japanized VIM)
kdesdk-scripts - scripts and data files for development
libcsvimp-dev - CSV data import tool for xTuple applications (development files)
liblatex-table-perl - Perl extension for the automatic generation of LaTeX tables
libocp-indent-lib-ocaml - OCaml indentation tool for emacs and vim - libraries
libocp-indent-lib-ocaml-dev - OCaml indentation tool for emacs and vim - development libraries
libtext-findindent-perl - module to heuristically determine indentation style
libtext-vimcolor-perl - syntax color text in HTML or XML using Vim
libvi-quickfix-perl - Perl support for vim's QuickFix mode
linuxdoc-tools - convert LinuxDoc SGML source into other formats
nescc - Programming Language for Deeply Networked Systems
netrik - text mode WWW browser with vi like keybindings
notmuch-vim - thread-based email index, search and tagging (vim interface)
nvi - 4.4BSD re-implementation of vi
nvi-doc - 4.4BSD re-implementation of vi - documentation files
ocaml-tools - tools for OCaml developers
ocp-indent - OCaml indentation tool for emacs and vim - runtime
openshot - Create and edit videos and movies
otags - tags file generator for OCaml
pms - Practical Music Search, an MPD client
powerline - prompt and statusline utility
python-editor - programmatically open an editor, capture the result - Python 2.7
python-ropemode - ropemode, a helper for using rope refactoring library in IDE
python3-editor - programmatically open an editor, capture the result - Python 3.x
ranger - File manager with an ncurses frontend written in Python
refdb-clients - Reference database and bibliography tool - clients
refdb-doc - Reference database and bibliography tool - doc
refdb-server - Reference database and bibliography tool - sql server
refdb-www - Reference database and bibliography tool - www server
ruby-ace-rails-ap - ajax.org Cloud9 Editor (Ace) for the Rails asset pipeline
ruby-fuubar - instafailing RSpec progress bar formatter
sen - Terminal user interface for docker engine
sisu - documents - structuring, publishing in multiple formats and search
supercollider-vim - SuperCollider mode for Vim
svtplay-dl - program to download videos from video on demand sites
tpp - text presentation program
txt2regex - A Regular Expression "wizard", all written with bash2 builtins
uzbl - Lightweight Webkit browser following the UNIX philosophy
vcsh - Version Control System for $HOME - multiple Git repositories in $HOME
vifm - flexible vi-like file manager using ncurses
vim-addon-manager - manager of addons for the Vim editor
vim-addon-mw-utils - Vim funcref library
vim-athena - Vi IMproved - enhanced vi editor - with Athena GUI
vim-athena-py2 - Vi IMproved - enhanced vi editor - with Athena GUI (Python2)
vim-autopep8 - vim plugin to apply autopep8
vim-conque - plugin for running interactive commands in a Vim buffer
vim-ctrlp - fuzzy file, buffer, mru, tag, etc. finder for Vim
vim-editorconfig - EditorConfig Plugin for Vim
vim-fugitive - Vim plugin to work with Git
vim-gnome-py2 - Vi IMproved - enhanced vi editor - with GNOME2 GUI (Python2)
vim-gocomplete - gocode integration for Vim
vim-gtk - Vi IMproved - enhanced vi editor - with GTK2 GUI
vim-gtk-py2 - Vi IMproved - enhanced vi editor - with GTK2 GUI (Python2)
vim-gtk3 - Vi IMproved - enhanced vi editor - with GTK3 GUI
vim-gtk3-py2 - Vi IMproved - enhanced vi editor - with GTK3 GUI (Python2)
vim-haproxy - syntax highlighting for HAProxy configuration files
vim-icinga2 - syntax highlighting for Icinga 2 config files in VIM
vim-khuno - Python flakes Vim plugin
vim-latexsuite - view, edit and compile LaTeX documents from within Vim
vim-migemo - VIM plugin for C/Migemo
vim-nox - Vi IMproved - enhanced vi editor - with scripting languages support
vim-nox-py2 - Vi IMproved - enhanced vi editor - with scripting languages support (Python2)
vim-pathogen - Manage your runtimepath with ease
vim-puppet - syntax highlighting for puppet manifests in vim
vim-python-jedi - autocompletion tool for Python - VIM addon files
vim-rails - vim development tools for Rails development
vim-scripts - plugins for vim, adding bells and whistles
vim-snipmate - Vim script that implements some of TextMate's snippets features.
vim-snippets - Snippets files for various programming languages.
vim-syntastic - Syntax checking hacks for vim
vim-syntax-docker - Docker container engine - Vim highlighting syntax files
vim-syntax-gtk - Syntax files to highlight GTK+ keywords in vim
vim-tabular - Vim script for text filtering and alignment
vim-tlib - Some vim utility functions
vim-ultisnips - snippet solution for Vim
vim-vimerl - Erlang plugin for Vim
vim-vimerl-syntax - Erlang syntax for Vim
vim-vimoutliner - script for building an outline editor on top of Vim
vim-voom - Vim two-pane outliner
vim-youcompleteme - fast, as-you-type, fuzzy-search code completion engine for Vim
vimhelp-de - Vi IMproved - Documentation files (German translation)
vit - full-screen terminal interface for Taskwarrior
youtube-dl - downloader of videos from YouTube and other sites
zathura - document viewer with a minimalistic interface
zathura-cb - comic book archive support for zathura
zathura-djvu - DjVu support for zathura
zathura-pdf-poppler - PDF support for zathura
zathura-ps - PostScript support for zathura
zeal - Simple offline API documentation browser
zeal-dbg - Debug symbols for zeal
zsh-antigen - manage your zsh plugins
me@mypc:~$ 
```

`apt-get install vim-gnome` 之后， vi 改为指向 /usr/bin/vim.gnome ， vim/gvim 也指向 /usr/bin/vim.gnome 。但是运行 gvim 显示 GUI
