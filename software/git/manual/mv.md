# Synopsis


# Description


# Options


# Examples


# Demo
## `git mv`
> Unlike many other VCS systems, Git doesn’t explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. However, Git is pretty smart about figuring that out after the fact

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    git add .
    git commit -m 'C0'
    clear

执行

    git mv README.md README
    git status

**执行结果**

    me@mypc:~/test$ git mv README.md README
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        renamed:    README.md -> README

    me@mypc:~/test$ 


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    git add .
    git commit -m 'C0'
    clear

执行

    mv README.md README
    git rm README.md
    git add README
    git status

**执行结果**

    me@mypc:~/test$ mv README.md README
    me@mypc:~/test$ git rm README.md
    rm 'README.md'
    me@mypc:~/test$ git add README
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        renamed:    README.md -> README

    me@mypc:~/test$ 

> Git figures out that it’s a rename implicitly, so it doesn’t matter if you rename a file that way or with the `mv` command. The only real difference is that `git mv` is one command instead of three — it’s a convenience function. More importantly, you can use any tool you like to rename a file, and address the add/rm later, before you commit.


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-mv.html
