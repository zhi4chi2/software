术语

- start-point - a branch name, a commit-id, or a tag.  If this option is omitted, the current HEAD will be used instead.


# Synopsis


# Description


# Options


# Examples


# Demo
## `git branch`
### `git branch -v`
### `git branch -vv`
### `git branch --merged`
### `git branch --no-merged`


## `git branch <branchname> <start-point>`
### start-point
>  It may be given as a branch name, a commit-id, or a tag. If this option is omitted, the current HEAD will be used instead.


#### a remote-tracking branch
> When a local branch is started off a remote-tracking branch, Git sets up the branch (specifically the `branch.<name>.remote` and `branch.<name>.merge`configuration entries) so that `git pull` will appropriately merge from the remote-tracking branch.

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
    git branch my-serverfix origin/serverfix
    git branch -vv
    git remote show origin
    git config branch.my-serverfix.remote
    git config branch.my-serverfix.merge

**执行结果**

FIXME


注意：设置 upstream 只影响 pull 不影响 push ！


## `git branch -u/--set-upstream-to <branchname>`
## `git branch --unset-upstream <branchname>`
## `git branch -m <oldbranch> <newbranch>`
## `git branch -d <branchname>`


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-branch.html
