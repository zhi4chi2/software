# Changing the Last Commit
> You need to be careful with this technique because amending changes the SHA-1 of the commit.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    echo 'something' > test
    git add README
    git commit -m 'Initial Commit'
    clear

执行

    git log
    git commit --amend -m 'Initial Commit'
    git log

**执行结果**

FIXME

> if your amendments are suitably trivial (fixing a silly typo or adding a file you forgot to stage) such that the earlier commit message is just fine, you can simply make the changes, stage them, and avoid the unnecessary editor session entirely with:
> 
>     $ git commit --amend --no-edit


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    echo 'something' > test
    git add README
    git commit -m 'Initial Commit'
    clear

执行

    git log
    git add test
    git commit --amend --no-edit
    git log

**执行结果**

FIXME


# Changing Multiple Commit Messages
