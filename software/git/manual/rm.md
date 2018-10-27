> You can pass files, directories, and file-glob patterns to the `git rm` command. That means you can do things such as:
>     $ git rm log/\*.log
> Note the backslash (`\`) in front of the `*`. This is necessary because Git does its own filename expansion in addition to your shell’s filename expansion.


最佳实践：删除 tracked file

同时从 working tree 和 staging area 中删除

- unmodified - `git rm`
- modified - 先 `git checkout --` 再 `git rm`
- staged - `git rm -f`

如果仅从 staging area 删除，但在 working tree 中保留则使用 `git rm --cached`

应该不会需要只在 working tree 中删除！如果确实需要，使用 Linux 系统命令 `rm` 即可。


# Synopsis


# Description


# Options


# Examples


# Demo
## `git rm`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    clear

执行

    ls -aF
    git rm PROJECTS.md
    ls -aF
    git status

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  PROJECTS.md
    me@mypc:~/test$ git rm PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        deleted:    PROJECTS.md

    me@mypc:~/test$ 


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    clear

执行

    ls -aF
    rm PROJECTS.md
    ls -aF
    git status
    git rm PROJECTS.md
    git status

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  PROJECTS.md
    me@mypc:~/test$ rm PROJECTS.md
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ git status
    On branch master
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    PROJECTS.md

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ git rm PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        deleted:    PROJECTS.md

    me@mypc:~/test$ 


## `git rm -f`
> If you modified the file and added it to the staging area already, you must force the removal with the `-f` option. This is a safety feature to prevent accidental removal of data that hasn’t yet been recorded in a snapshot and that can’t be recovered from Git.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    echo 'C1' >> PROJECTS.md
    git add .
    clear

执行

    git status
    git rm -f PROJECTS.md
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        modified:   PROJECTS.md

    me@mypc:~/test$ git rm -f PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        deleted:    PROJECTS.md

    me@mypc:~/test$ 


## `git rm --cached`
> Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore` file and accidentally staged it, like a large log file or a bunch of `.a` compiled files. To do this, use the `--cached` option

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

    git rm --cached README
    git status
    ls -aF

**执行结果**

    me@mypc:~/test$ git rm --cached README
    rm 'README'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        deleted:    README

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        README

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  README
    me@mypc:~/test$ 


# Examples
