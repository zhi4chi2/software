# Synopsis


# Description


# Options


# Examples


# Demo
## `git remote`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ 


### `git remote -v`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote -v

**执行结果**

    me@mypc:~/test/ticgit$ git remote -v
    origin  https://github.com/schacon/ticgit (fetch)
    origin  https://github.com/schacon/ticgit (push)
    me@mypc:~/test/ticgit$ 


## `git remote show` 
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote show origin

**执行结果**

    me@mypc:~/test/ticgit$ git remote show origin
    * remote origin
      Fetch URL: https://github.com/schacon/ticgit
      Push  URL: https://github.com/schacon/ticgit
      HEAD branch: master
      Remote branches:
        master tracked
        ticgit tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/ticgit$ 


## `git remote add` 
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote
    git remote add pb https://github.com/paulboone/ticgit
    git remote -v
    git fetch pb

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ git remote add pb https://github.com/paulboone/ticgit
    me@mypc:~/test/ticgit$ git remote -v
    origin  https://github.com/schacon/ticgit (fetch)
    origin  https://github.com/schacon/ticgit (push)
    pb  https://github.com/paulboone/ticgit (fetch)
    pb  https://github.com/paulboone/ticgit (push)
    me@mypc:~/test/ticgit$ git fetch pb
    remote: Enumerating objects: 22, done.
    remote: Counting objects: 100% (22/22), done.
    remote: Total 43 (delta 22), reused 22 (delta 22), pack-reused 21
    Unpacking objects: 100% (43/43), done.
    From https://github.com/paulboone/ticgit
     * [new branch]      master     -> pb/master
     * [new branch]      ticgit     -> pb/ticgit
    me@mypc:~/test/ticgit$ 


## `git remote remove` 
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    git remote add pb https://github.com/paulboone/ticgit
    clear

执行

    git remote
    git remote remove pb
    git remote

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    pb
    me@mypc:~/test/ticgit$ git remote remove pb
    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ 


> Once you delete the reference to a remote this way, all remote-tracking branches and configuration settings associated with that remote are also deleted.


## `git remote rename` 
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    git remote add pb https://github.com/paulboone/ticgit
    clear

执行

    git remote
    git remote rename pb paul
    git remote

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    pb
    me@mypc:~/test/ticgit$ git remote rename pb paul
    me@mypc:~/test/ticgit$ git remote
    origin
    paul
    me@mypc:~/test/ticgit$ 


> It’s worth mentioning that this changes all your remote-tracking branch names, too. What used to be referenced at `pb/master` is now at `paul/master`.


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-remote.html
