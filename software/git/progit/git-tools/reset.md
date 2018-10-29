# The Three Trees

- HEAD
- Index
- Working Directory


## The HEAD
> HEAD is the pointer to the current branch reference, which is in turn a pointer to the last commit made on that branch

> The Git `cat-file` and `ls-tree` commands are “plumbing” commands that are used for lower level things


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

    git log
    git cat-file -p HEAD
    git ls-tree -r HEAD

**执行结果**

FIXME


## The Index
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > README
    git add .
    clear

执行

    git ls-files -s
    git commit -m 'C0'
    git ls-files -s
    echo 'C1' >> README
    git add .
    git ls-files -s

**执行结果**

FIXME


## The Working Directory


# The Workflow
# The Role of Reset
## `git reset --soft`
> The first thing `reset` will do is move what HEAD points to.

比如 HEAD 指向 master branch ，则 `git reset 9e5e6a4` 将移动 master branch 指向 commit 9e5e6a4

`git reset --soft` 只移动分支，不改变 stage area 。实际效果相当于 undid `git commit`

`git reset --soft` 后再次执行 `git commit` 相当于 `git commit --amend`


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > file.txt
    git add .
    git commit -m 'v1'
    echo 'v2' >> file.txt
    git commit -a -m 'v2'
    echo 'v3' >> file.txt
    git commit -a -m 'v3'
    clear

执行

    git log --all --oneline
    git reset --soft HEAD~
    git log --all --oneline
    git status
    git diff --staged
    git commit -m 'v3-1'
    git log --all --oneline

**执行结果**

FIXME


## `git reset --mixed`
`git reset --mixed` 会在 `git reset --soft` 基础上再修改 stage area ，实际相当于 undid `git commit` 再 unstaged

`git reset --mixed` 后再次执行 `git add`, `git commit` 才能恢复之前的 commit


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > file.txt
    git add .
    git commit -m 'v1'
    echo 'v2' >> file.txt
    git commit -a -m 'v2'
    echo 'v3' >> file.txt
    git commit -a -m 'v3'
    clear

执行

    git log --all --oneline
    git reset --mixed HEAD~
    git log --all --oneline
    git status
    git diff
    git add file.txt
    git commit -m 'v3-1'
    git log --all --oneline

**执行结果**

FIXME


## `git reset --hard`
`git reset --hard` 会在 `git reset --mixed` 基础上再修改 Working Directory ，实际相当于 undid `git commit` 再 unstaged 再丢弃曾经在 working directory 中做的修改

`git reset --hard` 后重新在 working directory 中做修改，然后再次执行 `git add`, `git commit` 才能恢复之前的 commit


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > file.txt
    git add .
    git commit -m 'v1'
    echo 'v2' >> file.txt
    git commit -a -m 'v2'
    echo 'v3' >> file.txt
    git commit -a -m 'v3'
    clear

执行

    git log --all --oneline
    git reset --hard HEAD~
    git log --all --oneline
    git status
    cat file.txt
    echo 'v3-1' >> file.txt
    git add file.txt
    git commit -m 'v3-1'
    git log --all --oneline

**执行结果**

FIXME

> In this particular case, we still have the v3 version of our file in a commit in our Git DB, and we could get it back by looking at our `reflog`, but if we had not committed it, Git still would have overwritten the file and it would be unrecoverable.


The `reset` command overwrites these three trees in a specific order

1. Move the branch HEAD points to (stop here if `--soft`)
2. Make the Index look like HEAD (stop here unless `--hard`)
3. Make the Working Directory look like the Index(stop here if `--hard`)


# Reset With a Path
> If you specify a path, `reset` will skip step 1, and limit the remainder of its actions to a specific file or set of files.

也就是说，如果指定 path ，则不改变 branch ，只改变 index 中的 path(a specific file or set of files)，实际相当于 unstaging

注意，这种方式(specify a path)不能与 `--hard` 一起使用，所以只会改变 index 不会改变 working directory

`git reset file.txt` 是 `git reset HEAD file.txt` 的 shorthand

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > file.txt
    git add .
    git commit -m 'v1'
    echo 'v2' >> file.txt
    git commit -a -m 'v2'
    echo 'v3' >> file.txt
    git commit -a -m 'v3'
    clear

执行

    echo 'v4' >> file.txt
    git add file.txt
    git status
    git reset file.txt
    git status

**执行结果**

FIXME


## `git reset <tree-ish> <paths>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > file.txt
    git add .
    git commit -m 'v1'
    echo 'v2' >> file.txt
    git commit -a -m 'v2'
    echo 'v3' >> file.txt
    git commit -a -m 'v3'
    clear

执行

FIXME 6b999fa

    git log --oneline
    git reset 6b999fa file.txt
    git status
    git diff file.txt
    git diff --staged file.txt
    git add file.txt
    git status

**执行结果**

FIXME


> It’s also interesting to note that like `git add`, the `reset` command will accept a `--patch` option to unstage content on a hunk-by-hunk basis. So you can selectively unstage or revert content.


# Squashing
> Say you have a series of commits with messages like “oops.”, “WIP” and “forgot this file”. You can use `reset` to quickly and easily squash them into a single commit that makes you look really smart. (Squashing Commits shows another way to do this, but in this example it’s simpler to use `reset`.)

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'v1' > a.txt
    git add .
    git commit -m 'v1'
    touch b.txt
    git add b.txt
    echo 'v2' >> a.txt
    git commit -a -m 'v2'
    echo 'v3' >> a.txt
    git commit -a -m 'v3'
    clear

执行

    git log --oneline
    git reset --soft HEAD~2
    git status
    git commit -m 'v4'
    git log --oneline
    cat a.txt
    ls b.txt

**执行结果**

FIXME


# Check It Out
## Without Paths
## With Paths
> It is just like `git reset [branch] file` in that it updates the index with that file at that commit, but it also overwrites the file in the working directory.


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    echo 'something' >> README
    git add .
    clear

执行

    git status
    git checkout HEAD README
    git status
    cat README

**执行结果**

FIXME


> It would be exactly like `git reset --hard [branch] file` (if `reset` would let you run that)

注意 reset 不能这样做，会报错 `fatal: Cannot do hard reset with paths.` 

> Also, like `git reset` and `git add`, `checkout` will accept a `--patch` option to allow you to selectively revert file contents on a hunk-by-hunk basis.


# Summary
