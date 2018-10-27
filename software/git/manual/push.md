# Synopsis


# Description


# Options


# Examples


# Demo
## `git push`
## `git push <remote>`
## `git push <remote> <refspec>`
## `git push <remote> <tagname>`
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
    git clone ~/test/repo/demo
    cd demo/
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git push origin
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ git push origin v0.1
    Total 0 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new tag]         v0.1 -> v0.1
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    d45f08c3fb1b689f4ae056a8553b949dc51570a2
    me@mypc:~/test/workspace/demo$ 


## `git push <remote> :refs/tags/<tagname>`
> In order to update any remotes, you must use `git push <remote> :refs/tags/<tagname>`:

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
    git clone ~/test/repo/demo
    cd demo/
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git push origin v0.1
    clear

执行

    git tag
    git tag -d v0.1
    git tag
    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin :refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

    me@mypc:~/test/workspace/demo$ git tag
    v0.1
    me@mypc:~/test/workspace/demo$ git tag -d v0.1
    Deleted tag 'v0.1' (was f3c3ab0)
    me@mypc:~/test/workspace/demo$ git tag
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    f3c3ab08fb68dea0b18c9f5233bf2f1355be1afe
    me@mypc:~/test/workspace/demo$ git push origin :refs/tags/v0.1
    To /home/me/test/repo/demo
     - [deleted]         v0.1
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ 


## `git push --tags`
> If you have a lot of tags that you want to push up at once, you can also use the `--tags` option to the `git push` command. This will transfer all of your tags to the remote server that are not already there.

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
    git clone ~/test/repo/demo
    cd demo
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v0.2
    git push origin
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2
    git push origin --tags
    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2

**执行结果**

    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.2
    cat: /home/me/test/repo/demo/refs/tags/v0.2: No such file or directory
    me@mypc:~/test/workspace/demo$ git push origin --tags
    Total 0 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new tag]         v0.1 -> v0.1
     * [new tag]         v0.2 -> v0.2
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    bf1022a27662771ed32c934c34b2e2abe50d4068
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.2
    bf1022a27662771ed32c934c34b2e2abe50d4068
    me@mypc:~/test/workspace/demo$ 


## `git push -u/--set-upstream`


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-push.html
