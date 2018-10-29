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


### 无修改
如果没有实际的修改，则 `git commit` 不实际提交

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    clear

执行

    git commit -m 'C0'
    git log

**执行结果**

FIXME


### 重复提交
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
    git commit -m 'C1'
    git log

**执行结果**

FIXME


## `git commit -m`
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

    git commit -m 'modified CONTRIBUTING.md, add README'

**执行结果**

    me@mypc:~/test$ git commit -m 'modified CONTRIBUTING.md, add README'
    [master 0a111d2] modified CONTRIBUTING.md, add README
     2 files changed, 3 insertions(+)
     create mode 100644 README
    me@mypc:~/test$ 


the commit has given you some output about itself:

- which branch you committed to (master),
- what SHA-1 checksum the commit has (0a111d2),
- how many files were changed(2),
- and statistics about lines added(3) and removed in the commit.


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
    git add README
    git commit -m 'C0'
    clear

执行

    git log
    git commit --amend -m 'C0'
    git log

**执行结果**

FIXME

即使没有修改任何文件， commit message 也一样， `--amend` 后 SHA1 依然改变了。


### `git commit --amend --no-edit`
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
    git add README
    git commit -m 'C0'
    clear

执行

    git log
    echo 'C0' >> README
    git commit -a --amend --no-edit
    git log

**执行结果**

FIXME


### merge 后 amend
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b testing
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout master
    git merge testing
    git checkout testing
    clear

执行

    git log --oneline --graph --all --decorate
    echo 'C2' >> README
    git commit -a --amend -m 'C2'
    git log --oneline --graph --all --decorate
    cat README
    git checkout master
    cat README
    git merge testing
    cat README

**执行结果**

FIXME


可见如果 commit 已经被 merge 后再执行 amend ，会在再次 merge 时与旧的 commit 造成冲突（修改了同样的行）。


### push 后 amend
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone ~/test/repo/demo
    cd demo/
    echo 'C0' > README
    git add .
    git commit -m 'C0'
    echo 'C1-1' >> README
    git commit -a -m 'C1'
    git push origin master
    clear

执行

    echo 'C1-2' >> README
    git commit --amend -a --no-edit
    git log --oneline --graph --all --decorate
    git push origin master

**执行结果**

FIXME

可见如果 commit 已经被 push 后再执行 amend ，会在再次 push 时与旧的 commit 造成冲突（修改了同样的行）。


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-commit.html
