术语

- start_point
- tree-ish


# Synopsis


# Description


# Options


# Examples


# Demo
## `git checkout <branch>`
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


## `git checkout <new_branch> <start_point>`


## `git checkout -- <paths>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    echo 'C0' > CONTRIBUTING.md
    git add *
    git commit -m 'C0'
    git mv README.md README
    git add *
    echo 'C1' >> CONTRIBUTING.md
    clear

执行

    git status
    git checkout -- CONTRIBUTING.md
    git status
    cat CONTRIBUTING.md

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        renamed:    README.md -> README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   CONTRIBUTING.md

    me@mypc:~/test$ git checkout -- CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        renamed:    README.md -> README

    me@mypc:~/test$ cat CONTRIBUTING.md
    C0
    me@mypc:~/test$ 


> It’s important to understand that `git checkout -- <file>` is a dangerous command. Any changes you made to that file are gone — Git just copied another file over it.


## `git checkout -b <new_branch> <start_point>`


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-checkout.html
