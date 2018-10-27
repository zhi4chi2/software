# Synopsis


# Description


# Options


# Examples


# Demo
## `git tag`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    git tag
    git tag v1.3
    git tag v0.1
    git tag

**执行结果**

    me@mypc:~/test$ git tag
    me@mypc:~/test$ git tag v1.3
    me@mypc:~/test$ git tag v0.1
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    me@mypc:~/test$ 


> This command lists the tags in alphabetical order; the order in which they appear has no real importance.


## `git tag <tagname>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag v1.4-lw
    git tag
    git show v1.4-lw
    cat ~/test/.git/refs/tags/v1.4-lw

**执行结果**

    me@mypc:~/test$ git tag v1.4-lw
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    v1.4-lw
    me@mypc:~/test$ git show v1.4-lw
    commit ba60ec05ae84634f29b1b21377780264b0ea6196
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:44:32 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ cat ~/test/.git/refs/tags/v1.4-lw
    ba60ec05ae84634f29b1b21377780264b0ea6196
    me@mypc:~/test$ 


## `git tag <tagname> <commit>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git add .
    git commit -m 'C1'
    git tag v0.2
    clear

执行

    git tag
    git log --pretty=oneline
    git tag -a v0.1 dbae2d -m 'my version 0.1'
    git tag
    git show v0.1

**执行结果**

    me@mypc:~/test$ git tag
    v0.2
    me@mypc:~/test$ git log --pretty=oneline
    13a69c42ece4f5f2010b8d33fac7dd7553af204f C1
    dbae2d40d93156fe731c9f821df985a991c4db1a C0
    me@mypc:~/test$ git tag -a v0.1 dbae2d -m 'my version 0.1'
    me@mypc:~/test$ git tag
    v0.1
    v0.2
    me@mypc:~/test$ git show v0.1
    tag v0.1
    Tagger: me <me@example.com>
    Date:   Sat Oct 27 13:47:39 2018 +0800

    my version 0.1

    commit dbae2d40d93156fe731c9f821df985a991c4db1a
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:47:12 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ 


## `git tag <tagname> -a`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag -a v1.4 -m "my version 1.4"
    git tag
    git show v1.4

**执行结果**

    me@mypc:~/test$ git tag -a v1.4 -m "my version 1.4"
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    v1.4
    me@mypc:~/test$ git show v1.4
    tag v1.4
    Tagger: me <me@example.com>
    Date:   Sat Oct 27 13:44:01 2018 +0800

    my version 1.4

    commit 4f4de5f7c7310bf5bcb1b27aea294326292a9af6
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:43:52 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ 


## `git tag <tagname> -d`
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


## `git tag <tagname> -l/--list`
> You can also search for tags that match a particular pattern.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag
    git tag -l "v1.*"

**执行结果**

    me@mypc:~/test$ git tag
    v0.1
    v1.3
    me@mypc:~/test$ git tag -l "v1.*"
    v1.3
    me@mypc:~/test$ 

> Listing tag wildcards requires `-l` or `--list` option


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-tag.html
