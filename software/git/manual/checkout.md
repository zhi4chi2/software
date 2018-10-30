术语

- start_point - The name of a commit at which to start the new branch. Defaults to HEAD
- tree-ish -  commit, tag or tree. Tree to checkout from (when paths are given). If not specified, the index will be used.


# Synopsis


# Description


# Options


# Examples


# Demo
## `git checkout <branch>`
### 如果 `<branch>` 存在
> When switching branches, if you have local modifications to one or more files that are different between the current branch and the branch to which you are switching, the command refuses to switch branches in order to preserve your modifications in context.


### 如果 `<branch>` 不存在
> If `<branch>` is not found but there does exist a tracking branch in exactly one remote (call it `<remote>`) with a matching name, treat as equivalent to
> 
>     $ git checkout -b <branch> --track <remote>/<branch>

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
    git push --all origin
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch -vv
    git remote show origin
    git checkout serverfix
    git branch -vv
    git remote show origin

**执行结果**

FIXME


此时 `git checkout serverfix` 相当于 `git checkout -b serverfix --track origin/serverfix`


## `git checkout --detach <branch>`
## `git checkout <commit>`


## `git checkout -b <new_branch> <start_point>`
`-b` 必须存在，即不能 `git checkout <new_branch> <start_point>` 否则报 error

start_point 默认为 HEAD

> Specifying `-b` causes a new branch to be created as if git-branch(1) were called and then checked out. In this case you can use the `--track` or `--no-track` options, which will be passed to `git branch`.


### `git checkout -b <new_branch> --track <start_point>`
### `git checkout -b <new_branch> --no-track <start_point>`


## `git checkout <tree-ish> <paths>`
> updates the named paths in the working tree from the index file or from a named `<tree-ish>` (most often a commit).

>  The `<tree-ish>` argument can be used to specify a specific tree-ish (i.e. commit, tag or tree) to update the index for the given paths before updating the working tree.

如果没有指定 tree-ish 则 the index will be used.

所以有两种可能

- 如果没有指定 tree-ish - restore modified or deleted paths to their original contents from the index
- 如果指定 tree-ish - replace paths with the contents from a named `<tree-ish>` (most often a commit-ish).


### `git checkout <tree-ish> <paths>`
指定 tree-ish 时，用 tree-ish 的内容，同时更新 index 和 working directory


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > README
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    clear

执行

    git checkout HEAD~2 README
    cat README
    git status
    git diff --staged

**执行结果**

FIXME


### `git checkout -- <paths>`
不指定 tree-ish 时，用 index 的内容，仅更新 working directory

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > README.md
    git add *
    git commit -m 'C0'
    echo 'C1-1' >> README.md
    git add README.md
    echo 'C1-2' >> README.md
    clear

执行

    git status
    git checkout -- README.md
    git status
    cat README.md

**执行结果**

FIXME


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-checkout.html
