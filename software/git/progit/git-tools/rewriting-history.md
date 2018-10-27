# Changing the Last Commit
> You need to be careful with this technique because amending changes the SHA-1 of the commit.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch test
    git add README
    git commit -m 'C0'
    clear

执行

    git log
    git commit --amend -m 'C0'
    git log

**执行结果**

    me@mypc:~/test$ git log
    commit f429f3ea311be2fae3b889005fd2fe2ec0c5d244
    Author: me <me@example.com>
    Date:   Sat Oct 27 15:00:14 2018 +0800

        C0
    me@mypc:~/test$ git commit --amend -m 'C0'
    [master 1b31355] C0
     Date: Sat Oct 27 15:00:14 2018 +0800
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test$ git log
    commit 1b31355b21056f026225ab2bd92d7af9720fb7f9
    Author: me <me@example.com>
    Date:   Sat Oct 27 15:00:14 2018 +0800

        C0
    me@mypc:~/test$ 

即使没有修改任何文件， commit message 也一样， `--amend` 后 SHA1 依然改变了。

> if your amendments are suitably trivial (fixing a silly typo or adding a file you forgot to stage) such that the earlier commit message is just fine, you can simply make the changes, stage them, and avoid the unnecessary editor session entirely with:
> 
>     $ git commit --amend --no-edit


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch test
    git add README
    git commit -m 'C0'
    clear

执行

    git log
    git add test
    git commit --amend --no-edit
    git log

**执行结果**

    me@mypc:~/test$ git log
    commit 3d34994656bcd91017828e24be1fe2d1c81476ee
    Author: me <me@example.com>
    Date:   Sat Oct 27 15:02:02 2018 +0800

        C0
    me@mypc:~/test$ git add test
    me@mypc:~/test$ git commit --amend --no-edit
    [master 9ca8814] C0
     Date: Sat Oct 27 15:02:02 2018 +0800
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
     create mode 100644 test
    me@mypc:~/test$ git log
    commit 9ca88148eed2ad03b88a4a9c27b29a6ac6abefdc
    Author: me <me@example.com>
    Date:   Sat Oct 27 15:02:02 2018 +0800

        C0
    me@mypc:~/test$ 


# Changing Multiple Commit Messages

