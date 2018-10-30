# Synopsis


# Description


# Options


# Examples


# Demo
## `git clone <repository> <directory>`
>  Cloning into an existing directory is only allowed if the directory is empty.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git clone https://github.com/schacon/simplegit-progit.git my-simplegit
    ls -aF
    cd my-simplegit
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/schacon/simplegit-progit.git my-simplegit
    Cloning into 'my-simplegit'...
    remote: Enumerating objects: 13, done.
    remote: Total 13 (delta 0), reused 0 (delta 0), pack-reused 13
    Unpacking objects: 100% (13/13), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  my-simplegit/
    me@mypc:~/test$ cd my-simplegit
    me@mypc:~/test/my-simplegit$ ls -aF
    ./  ../  .git/  lib/  Rakefile  README
    me@mypc:~/test/my-simplegit$ 


### `git clone <repository>`
>  The "humanish" part of the source repository is used if no directory is explicitly given (`repo` for `/path/to/repo.git` and `foo` for `host.xz:foo/.git`).


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git clone https://github.com/schacon/simplegit-progit
    ls -aF
    cd simplegit-progit
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/schacon/simplegit-progit
    Cloning into 'simplegit-progit'...
    remote: Enumerating objects: 13, done.
    remote: Total 13 (delta 0), reused 0 (delta 0), pack-reused 13
    Unpacking objects: 100% (13/13), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  simplegit-progit/
    me@mypc:~/test$ cd simplegit-progit
    me@mypc:~/test/simplegit-progit$ ls -aF
    ./  ../  .git/  lib/  Rakefile  README
    me@mypc:~/test/simplegit-progit$ 

clone 到了 `/home/me/test/simplegit-progit` 目录下（自动创建此目录），库在 `/home/me/test/simplegit-progit/.git`


### `git clone --bare <repository> <directory>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    clear

执行

    git clone --bare ~/test/repo/demo
    ls -aF
    cd demo.git/
    ls -aF

**执行结果**

FIXME


### `git clone -o <repository> <directory>`
> “origin” is the default name for a remote when you run `git clone`. If you run `git clone -o booyah` instead, then you will have `booyah/master` as your default remote branch.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone -o booyah ~/test/repo/demo
    cd demo
    clear

执行

    git remote

**执行结果**

    me@mypc:~/test/workspace/demo$ git remote
    booyah
    me@mypc:~/test/workspace/demo$ 


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-clone.html
