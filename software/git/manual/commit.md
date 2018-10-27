# Synopsis


# Description


# Options


# Examples


# Demo
## `git commit`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1' > README
    echo 'C1-1' >> CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    git add .
    clear

执行

    git commit

**执行结果**

      1 
      2 # Please enter the commit message for your changes. Lines starting
      3 # with '#' will be ignored, and an empty message aborts the commit.
      4 # On branch master
      5 # Changes to be committed:
      6 #       modified:   CONTRIBUTING.md
      7 #       new file:   README
      8 #
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    "~/test/.git/COMMIT_EDITMSG" 8L, 235C                         1,0-1         All


> You can see that the default commit message contains the latest output of the `git status` command commented out and one empty line on top.


如果直接按 `:q` 退出，则不会提交：

    me@mypc:~/test$ git commit
    Aborting commit due to empty commit message.
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        modified:   CONTRIBUTING.md
        new file:   README

    me@mypc:~/test$ 


`git commit` launches your editor of choice. (This is set by your shell’s `EDITOR` environment variable — usually vim or emacs, although you can configure it with whatever you want using the `git config --global core.editor` command as you saw in Getting Started).

执行

    git commit -m 'modified CONTRIBUTING.md, add README'

**执行结果**

    me@mypc:~/test$ git commit -m 'modified CONTRIBUTING.md, add README'
    [master 0a111d2] modified CONTRIBUTING.md, add README
     2 files changed, 3 insertions(+)
     create mode 100644 README
    me@mypc:~/test$ 


the commit has given you some output about itself:

- which branch you committed to (master),
- what SHA-1 checksum the commit has (d6d6248),
- how many files were changed,
- and statistics about lines added and removed in the commit.


## `git commit -v`
> For an even more explicit reminder of what you’ve modified, you can pass the `-v` option to `git commit`. Doing so also puts the diff of your change in the editor so you can see exactly what changes you’re committing.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1' > README
    echo 'C1-1' >> CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    git add .
    clear

执行

    git commit -v

**执行结果**

      1 
      2 # Please enter the commit message for your changes. Lines starting
      3 # with '#' will be ignored, and an empty message aborts the commit.
      4 # On branch master
      5 # Changes to be committed:
      6 #       modified:   CONTRIBUTING.md
      7 #       new file:   README
      8 #
      9 # ------------------------ >8 ------------------------
     10 # Do not touch the line above.
     11 # Everything below will be removed.
     12 diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
     13 index e69de29..3f0eca2 100644
     14 --- a/CONTRIBUTING.md
     15 +++ b/CONTRIBUTING.md
     16 @@ -0,0 +1,2 @@
     17 +C1-1
     18 +C1-2
     19 diff --git a/README b/README
     20 new file mode 100644
     21 index 0000000..e2cf5e7
     22 --- /dev/null
     23 +++ b/README
     24 @@ -0,0 +1 @@
     25 +C1
    ~                                                                               
    "~/test/.git/COMMIT_EDITMSG" 25L, 624C                        1,0-1         All


## `git commit -a/--all`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    touch README
    echo 'C1' >> CONTRIBUTING.md
    clear

执行

    git status
    git commit -a -m 'C1'
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   CONTRIBUTING.md

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        README

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ git commit -a -m 'C1'
    [master 6c436cf] C1
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ 

注意， `git commit -a` 只会 stage every file that is already tracked ，不会自动添加 untracked files


## `git commit --amend`
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


## `git commit --amend --no-edit`
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


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-commit.html
