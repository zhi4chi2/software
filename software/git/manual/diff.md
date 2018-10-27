# Synopsis


# Description


# Options


# Examples


# Demo
## `git diff`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1-1' >> CONTRIBUTING.md
    git add CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    clear

执行

    git diff

**执行结果**

FIXME


## `git diff --cached/--staged`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1-1' >> CONTRIBUTING.md
    git add CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    clear

执行

    git diff --staged
    git diff --cached

**执行结果**

FIXME


# hunk header

    @@ -k,l +n,m @@ TEXT

这叫做 hunk header 。其中的 TEXT 可以定制，参见

- https://git-scm.com/docs/gitattributes#_defining_a_custom_hunk_header
- https://stackoverflow.com/questions/28111035/where-does-the-excerpt-in-the-git-diff-hunk-header-come-from


好像不能不显示 hunk header 中的 TEXT ，参见 https://stackoverflow.com/questions/8614134/how-to-avoid-git-diff-putting-code-block-name-in-hunk-header


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-diff.html
