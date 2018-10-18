从 remote branch checkout 创建 local branch 后， local branch 叫做 tracking branch ， remote branch 叫做 upstream branch

- tracking branch
- upstream branch


在 tracking branch 上执行 `git pull` 会自动找到 remote 和 branch


`git clone` 时自动创建 master branch track origin/master


在 tracking branch 上可以用 {@u}/@{upstream} 引用对应的 upstream branch


# git branch


# git branch branchname
创建分支就是创建了一个文件(41 字节，包括 40 字节的 SHA-1 和一个换行)。其中是一个 pointer 指向当前的 commit object


    FIXME
    git branch testing
    git log --oneline --decorate
    echo hello > README
    git commit -a -m 'modify README in master'
    git checkout testing
    git log --oneline --decorate
    echo world > README
    git commit -a -m 'modify README in testing'
    git log --oneline --decorate --graph --all


# -d

    FIXME
    git branch testing
    git branch
    git branch -d testing
    git branch


# -D


# -v


# -vv


# --merged / --no-merged

    FIXME
    
    git branch -d testing


# --tracked
当 start point 是 remote branch 时， --tracked 是默认行为。通过设置 branch.autoSetupMerge = false 可以改变为 --no-track 。如果设为 always 则不论 start point 是 local/remote branch 都 tracked

    git branch --track next origin/next


# -u/--set-upstream-to

    FIXME
    git push origin next
    git branch -u origin/next


# Reference
- https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell
- https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging
- https://git-scm.com/book/en/v2/Git-Branching-Branch-Management
- https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches