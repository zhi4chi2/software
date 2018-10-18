几种使用方式

- git config name value
- git config -l/--list
- git config name


# git config name value

    me@mypc:~$ git config --global user.name me
    me@mypc:~$ git config --global user.email me@example.com
    me@mypc:~$ 


# git config -l/--list
在 Linux 下

    me@mypc:~$ git config --list
    user.email=me@example.com
    user.name=me
    me@mypc:~$ 


在 windows 下

    bruce@bruce-PC MINGW64 ~
    $ git config --list
    core.symlinks=false
    core.autocrlf=true
    core.fscache=true
    color.diff=auto
    color.status=auto
    color.branch=auto
    color.interactive=true
    help.format=html
    rebase.autosquash=true
    http.sslcainfo=D:/Git/mingw64/ssl/certs/ca-bundle.crt
    diff.astextplain.textconv=astextplain
    filter.lfs.clean=git-lfs clean -- %f
    filter.lfs.smudge=git-lfs smudge -- %f
    filter.lfs.required=true
    filter.lfs.process=git-lfs filter-process
    credential.helper=manager
    user.name=me
    user.email=me@example.com
    
    bruce@bruce-PC MINGW64 ~
    $


Git 会从不同的文件中读取同一个配置，因此可能有重复的配置名，则将使用最后一个配置。


# git config name
可以使用 `git config name` 检查配置实际起作用的值。

    me@mypc:~$ git config user.name
    me
    me@mypc:~$ git config user.email
    me@example.com
    me@mypc:~$ 


# file option

- --global
- --system
- --local
- -f/--file


`git config` 配置变量存储在

- /etc/gitconfig - 使用 --system 选项， applied to every user on the system and all their repositories.
- ~/.gitconfig 或 ~/.config/git/config - 使用 --global 选项， affects all of the repositories you work with on your system.
- .git/config - **默认**，使用 --local 选项， specific to that single repository


local 优先级最高， system 最低

在 windows 下对应

- `D:\Git\etc\gitconfig`
- `C:\Users\$USER\.gitconfig`
- `.git\config`


> If you are using version 2.x or later of Git for Windows, there is also a system-level config file at `C:\Documents and Settings\All Users\Application Data\Git\config` on Windows XP, and in `C:\ProgramData\Git\config` on Windows Vista and newer. This config file can only be changed by `git config -f <file>` as an admin.

当使用 Git for Windows 2.x 时，在 Windows 下还有一个 system level config file 在 C:\ProgramData\Git\config 下，但只能通过 git config -f 修改。


# options
## --unset and --remove-section

    me@mypc:~$ cat .gitconfig
    [user]
    	email = me@example.com
    	name = me
    me@mypc:~$ git config --global x.y xxyy
    me@mypc:~$ cat .gitconfig
    [user]
    	email = me@example.com
    	name = me
    [x]
    	y = xxyy
    me@mypc:~$ git config --global --unset x.y
    me@mypc:~$ cat .gitconfig
    [user]
    	email = me@example.com
    	name = me
    [x]
    me@mypc:~$ git config --global --remove-section x
    me@mypc:~$ cat .gitconfig
    [user]
    	email = me@example.com
    	name = me
    me@mypc:~$ 


# variables
Each variable must belong to some section

    me@mypc:~$ git config --global x xx
    error: key does not contain a section: x


可用的 variables

- user.name
- user.email


## core.quotepath
用以显示中文文件名。


## core.editor
默认使用 vim ，可以修改为 emacs

    git config --global core.editor emacs


在 Windows 下可以改为 Notepad++

    git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"


## credential.helper


## alias

    me@mypc:~/test/workspace$ git config --global alias.ci commit
    me@mypc:~/test/workspace$ git ci
    On branch v0.1.1
    nothing to commit, working directory clean
    me@mypc:~/test/workspace$ cat ~/.gitconfig
    [user]
    	email = me@example.com
    	name = me
    [alias]
    	ci = commit
    me@mypc:~/test/workspace$ 


可以加参数

    me@mypc:~/test/workspace$ git config --global alias.last 'log -1 HEAD'
    me@mypc:~/test/workspace$ git last
    commit 37a941aa5926a36648a2e217cec7ad368f18e420
    Author: me <me@example.com>
    Date:   Sun Jun 11 17:06:47 2017 +0800
    
        init commit
    me@mypc:~/test/workspace$ 


外部命令(not Git subcommand)前加 !

    me@mypc:~/test/workspace$ git config --global alias.visual '!xlogo'
    me@mypc:~/test/workspace$ git visual
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup
- https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
- https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches
