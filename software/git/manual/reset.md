术语

- tree-ish - HEAD, commit


# Synopsis


# Description


# Options


# Examples


# Demo
## `git reset <tree-ish> <paths>`
> resets the index entries for all `<paths>` to their state at `<tree-ish>`. (It does not affect the working tree or the current branch.)


### tree-ish
`<tree-ish>` defaults to HEAD

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add *
    git commit -m 'C0'
    echo 'C1' >> README
    git add *
    clear

执行

    git status
    git reset README
    git status
    cat README

**执行结果**

FIXME


### `git reset <tree-ish> <paths>`
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
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git reset HEAD~2 README
    git status
    git diff
    git diff --staged
    git add README
    git status

**执行结果**

FIXME


## `git reset <commit>`
> resets the current branch head to `<commit>` and possibly updates the index (resetting it to the tree of `<commit>`) and the working tree depending on `<mode>`. If `<mode>` is omitted, defaults to "--mixed".


### commit
`<commit>` defaults to HEAD

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add *
    git commit -m 'C0'
    echo 'C1' >> README
    git add *
    clear

执行

    git reset
    git status
    cat README

**执行结果**

FIXME


### `git reset <commit>`
相当于放弃了 `<commit>` 之后的提交，是 `git commit` 的反向。

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
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git log --oneline
    git reset HEAD~2
    git log --oneline
    git status
    git diff

**执行结果**

FIXME


### `git reset --soft <commit>`
> Does not touch the index file or the working tree at all

> This leaves all your changed files "Changes to be committed", as git status would put it.

实际相当于 undid `git commit`

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
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git log --oneline
    git reset --soft HEAD~2
    git log --oneline
    git status
    git diff --staged
    git commit -m 'C3'

**执行结果**

FIXME


### `git reset --mixed <commit>`
> Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.

实际相当于 undid `git commit` 并 unstaged

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
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git log --oneline
    git reset --mixed HEAD~2
    git log --oneline
    git status
    git diff
    git add README
    git commit -m 'C2'

**执行结果**

FIXME


### `git reset --hard <commit>`
> Resets the index and working tree. Any changes to tracked files in the working tree since `<commit>` are discarded.

实际相当于 undid `git commit` 并 unstaged ，且在 working directory 中丢弃曾经做的修改。

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
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git log --oneline
    git reset --hard HEAD~2
    git log --oneline
    git status

**执行结果**

FIXME


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-reset.html
