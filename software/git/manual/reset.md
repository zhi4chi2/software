# Synopsis


# Description


# Options


# Examples


# Demo
## `git reset <tree-ish> <paths>`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add *
    git commit -m 'C0'
    echo 'C1' >> README
    git add *
    clear

执行

    git reset HEAD README
    git status
    cat README

**执行结果**

FIXME


>   It’s true that `git reset` can be a dangerous command, especially if you provide the `--hard` flag. However, in the scenario described above, the file in your working directory is not touched, so it’s relatively safe.


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-reset.html
