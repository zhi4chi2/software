merge 有三种结果

- fast forward
- auto merge - 创建 merge commit
- merge conflict


# fast forward

    FIXME
    git checkout -b testing
    echo hello > README
    git commit -a -m 'modify README in testing'
    git checkout master
    git merge testing
    git branch -d testing


# auto merge

    FIXME
    git checkout -b testing
    echo hello > README
    git commit -a -m 'modify README in testing'
    git checkout master
    touch LICENSE
    git add --all
    git commit -m 'add LICENSE'
    git merge testing
    git log --oneline --graph
    git branch -d testing


自动创建的 merge commit 有多个 parent


# merge conflict

    FIXME
    git checkout -b testing
    echo hello > README
    git commit -a -m 'modify README in testing'
    git checkout master
    echo world > README
    git commit -a -m 'modify README in master'
    git merge testing
    git status
    vi README
    git add README
    git status
    git commit -m 'merge branch testing. conflicts: README'
    git branch -d testing


# Reference
- https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging