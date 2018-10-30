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


### `git tag <tagname> -l/--list`
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
    clear

执行

    git tag v0.1
    git show v0.1
    cat ~/test/.git/refs/tags/v0.1

**执行结果**

FIXME


### `git tag <tagname> <commit>`
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
    clear

执行

    git tag v0.1 HEAD~
    git tag
    git show v0.1

**执行结果**

FIXME


### `git tag -a <tagname>`
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

    git tag -a v0.1 -m "my version 0.1"
    git tag
    git show v0.1

**执行结果**

FIXME


## `git tag -d <tagname>`
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
    clear

执行

    git tag
    git tag -d v0.1
    git tag

**执行结果**

FIXME


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-tag.html
