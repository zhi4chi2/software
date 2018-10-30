术语

- commit


# Synopsis


# Description


# Options
## path
> The `<paths>` parameters, when given, are used to limit the diff to the named paths (you can give directory names and get diff for all files under them).


# Examples


# Demo
## `git diff`
> view the changes you made relative to the index (staging area for the next commit).


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    git add .
    echo 'C0' > README.md
    clear

执行

    git diff

**执行结果**

FIXME


## `git diff --cached/--staged <commit>`
> view the changes you staged for the next commit relative to the named `<commit>`. Typically you would want comparison with the latest commit, so if you do not give `<commit>`, it defaults to HEAD. If HEAD does not exist (e.g. unborn branches) and `<commit>` is not given, it shows all staged changes. --staged is a synonym of --cached.

commit 默认是 HEAD


### `git diff --cached/--staged`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > README.md
    git add .
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
