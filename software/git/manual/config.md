术语

- file-option - `--system`/`--global`/`--local`/`--file <filename>`/`-f <filename>`/`--blob`
- type - `--int`/`--bool`/`--bool-or-int`/`--path`


# Synopsis


# Description


# Options


# Files


# Environment


# Examples


# Configuration File
## Syntax
## Includes
## Conditional includes
## Example
## Values
## Variables


# Demo
## `git config name value`
执行

    git config --global user.name me
    git config --global user.email me@example.com

**执行结果**

    me@mypc:~$ git config --global user.name me
    me@mypc:~$ git config --global user.email me@example.com
    me@mypc:~$ 


## `git config name`
预处理

    cd
    git config --global user.name me
    git config --global user.email me@example.com
    clear

执行

    git config user.name
    git config user.email

**执行结果**

    me@mypc:~$ git config user.name
    me
    me@mypc:~$ git config user.email
    me@example.com
    me@mypc:~$ 


## `git config -l/--list`
预处理

    cd
    git config --global user.name me
    git config --global user.email me@example.com
    rm -rf test
    mkdir test
    cd test/
    git init
    git config --local user.name test
    git config --local user.email test@example.com
    clear

执行

    git config --list

**执行结果**

    me@mypc:~/test$ git config --list
    user.name=me
    user.email=me@example.com
    core.repositoryformatversion=0
    core.filemode=true
    core.bare=false
    core.logallrefupdates=true
    user.name=test
    user.email=test@example.com
    me@mypc:~/test$ 


> You may see keys more than once, because Git reads the same key from different files (`/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

Git 会从不同的文件中读取同一个配置，因此可能有重复的配置名(如例子中的 `user.name`/`user.email`)，则将使用最后一个配置。


