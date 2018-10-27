# Synopsis


# Description


# Options


# Examples


# Demo
## `git init`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git init
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git init
    Initialized empty Git repository in /home/me/test/.git/
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ 


## `git init --bare`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git init --bare
    ls -aF

**执行结果**

FIXME


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-init.html
