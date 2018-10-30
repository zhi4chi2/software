# Synopsis


# Description


# Options


# Examples


# Demo
## `git commit`
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


### `git commit -m`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    clear

执行

    git commit -m 'C0'

**执行结果**

FIXME


### `git commit -a/--all`
> Tell the command to automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

注意， `git commit -a` 只会 stage every file that is already tracked ，不会自动添加 untracked files


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


### `git commit --amend`
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


#### `git commit --amend --no-edit`
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


#### merge 后 amend
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


#### push 后 amend
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
    touch README
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    git push origin master
    clear

执行

    git log --oneline --graph --all --decorate
    echo 'C2' >> README
    git commit -a --amend -m 'C2'
    git log --oneline --graph --all --decorate
    cat README
    git push origin master

**执行结果**

FIXME

可见如果 commit 已经被 push 后再执行 amend ，会在再次 push 时与旧的 commit 造成冲突（修改了同样的行）。


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-commit.html
