# Getting a Git Repository
## Initializing a Repository in an Existing Directory
示例

    mkdir workspace
    cd workspace/
    git init
    ls -aF

**运行结果**

FIXME

    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ ls -aF
    ./  ../  .git/
    me@mypc:~/test/workspace$ 


## Cloning an Existing Repository
示例

    ls -aF
    git clone https://github.com/zhi4chi2/demo
    ls -aF
    cd demo
    ls -aF

**运行结果**

FIXME

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo
    Cloning into 'demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  demo/
    me@mypc:~/test$ cd demo
    me@mypc:~/test/demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/demo$ 


clone 到了 `/home/me/test/demo` 目录下（自动创建此目录），库在 `/home/me/test/demo/.git`


GitHub 的 git clone url 可以加 .git 也可以省略。


示例

    ls -aF
    git clone https://github.com/zhi4chi2/demo.git my-demo
    ls -aF
    cd my-demo
    ls -aF

**运行结果**

FIXME

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo.git my-demo
    Cloning into 'my-demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  my-demo/
    me@mypc:~/test$ cd my-demo
    me@mypc:~/test/my-demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/my-demo$ 


除了 https:// 协议外还可以使用 git:// 或者使用 SSH 传输协议（例如 `user@server:path/to/repo.git` ）。



# Recording Changes to the Repository
working directory 中文件的状态(<https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository>)

- untracked - 既不在 last snapshot 中也不在 staging area 中的文件。 `git add` 后变为 staged
- tracked
    - unmodified - 编辑文件则变为 modified ，删除文件则变为 untracked
    - modified - `git add` 后变为 staged
    - staged - `git commit` 后变为 unmodified

参见原文档 Figure 8. The lifecycle of the status of your files.


## Checking the Status of Your Files
预处理

    mkdir workspace
    cd workspace/
    git init

示例

    git status
    echo 'My Project' > README
    git status

**运行结果**

FIXME


## Tracking New Files
预处理

    mkdir workspace
    cd workspace/
    git init
    echo 'My Project' > README

示例

    git add README
    git status

**运行结果**

FIXME


## Staging Modified Files
预处理

    mkdir workspace
    cd workspace/
    git init
    echo 'hello' > CONTRIBUTING.md
    git add CONTRIBUTING.md
    git commit -m 'commit CONTRIBUTING.md'
    echo 'My Project' > README
    echo 'world' >> CONTRIBUTING.md

示例

    git status
    git add CONTRIBUTING.md
    git status
    echo '# test line' >> CONTRIBUTING.md
    git status
    git add CONTRIBUTING.md
    git status

**运行结果**

FIXME


## Short Status
示例

    git status -s
    git status
    git rm README
    git status
    git commit -m "delete README"
    git status

**运行结果**

FIXME



## Ignoring Files
文件 `.gitignore` 的格式规范(rules for the patterns)如下

- 所有空行或者以 # 开头的行都会被 Git 忽略。
- Standard glob patterns work, and will be applied recursively throughout the entire working tree.
- 匹配模式可以以 / 开头防止递归
- 匹配模式可以以 / 结尾指定目录
- 不忽略指定模式的文件或目录，可以在模式前加上 ! 取反。


glob 模式是指 shell 所使用的简化了的正则表达式。

- \* 匹配零个或多个任意字符；
- \[abc\] 匹配任何一个列在方括号中的字符；
- ? 只匹配一个任意字符；
- 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。
- 使用两个星号 \*\* 表示匹配任意中间目录，比如 `a/**/z` 可以匹配 a/z, a/b/z 或 a/b/c/z 等。


例子

    # ignore all .a files
    *.a
    
    # but do track lib.a, even though you're ignoring .a files above
    !lib.a
    
    # only ignore the TODO file in the current directory, not subdir/TODO
    /TODO
    
    # ignore all files in any directory named build
    build/
    
    # ignore doc/notes.txt, but not doc/server/arch.txt
    doc/*.txt
    
    # ignore all .pdf files in the doc/ directory and any of its subdirectories
    doc/**/*.pdf


GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 <https://github.com/github/gitignore> 找到它


> In the simple case, a repository might have a single `.gitignore` file in its root directory, which applies recursively to the entire repository. However, it is also possible to have additional `.gitignore` files in subdirectories. The rules in these nested `.gitignore` files apply only to the files under the directory where they are located. (The Linux kernel source repository has 206 `.gitignore` files.)
> 
> It is beyond the scope of this book to get into the details of multiple `.gitignore` files; see `man gitignore` for the details.


## Viewing Your Staged and Unstaged Changes
> There is another way to look at these diffs if you prefer a graphical or external diff viewing program instead. If you run `git difftool` instead of `git diff`, you can view any of these diffs in software like emerge, vimdiff and many more (including commercial products). Run `git difftool --tool-help` to see what is available on your system.


### git difftool
示例

    git difftool

**运行结果**

FIXME

    me@mypc:~/test/workspace$ git difftool --staged
    
    This message is displayed because 'diff.tool' is not configured.
    See 'git difftool --tool-help' or 'git help config' for more details.
    'git difftool' will now attempt to use one of the following tools:
    meld opendiff kdiff3 tkdiff xxdiff kompare gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare emerge vimdiff
    
    Viewing (1/1): 'README'
    Launch 'gvimdiff' [Y/n]: y
    2 files to edit
    
    (gvim:5160): GLib-GObject-WARNING **: cannot retrieve class for invalid (unclassed) type '<invalid>'
    me@mypc:~/test/workspace$ 


### `git difftool --tool-help`
使用 `git difftool --tool-help` 命令来看你的系统支持哪些 Git Diff 插件。

示例

    git difftool --tool-help

#### Linux
**运行结果**

FIXME

    me@mypc:~/workspace/test$ git difftool --tool-help
    'git difftool --tool=<tool>' may be set to one of the following:
            araxis
            gvimdiff
            gvimdiff2
            gvimdiff3
            vimdiff
            vimdiff2
            vimdiff3
    
    The following tools are valid, but not currently available:
            bc
            bc3
            codecompare
            deltawalker
            diffmerge
            diffuse
            ecmerge
            emerge
            kdiff3
            kompare
            meld
            opendiff
            p4merge
            tkdiff
            winmerge
            xxdiff
    
    Some of the tools listed above only work in a windowed
    environment. If run in a terminal-only session, they will fail.
    me@mypc:~/workspace/test$ 


在 Linux 中默认使用 gvimdiff


#### Windows
**运行结果**

FIXME

    me@mypc MINGW64 ~/test (master)
    $ git difftool --tool-help
    'git difftool --tool=<tool>' may be set to one of the following:
                    vimdiff
                    vimdiff2
                    vimdiff3
    
    The following tools are valid, but not currently available:
                    araxis
                    bc
                    bc3
                    codecompare
                    deltawalker
                    diffmerge
                    diffuse
                    ecmerge
                    emerge
                    examdiff
                    gvimdiff
                    gvimdiff2
                    gvimdiff3
                    kdiff3
                    kompare
                    meld
                    opendiff
                    p4merge
                    tkdiff
                    winmerge
                    xxdiff
    
    Some of the tools listed above only work in a windowed
    environment. If run in a terminal-only session, they will fail.
    
    me@mypc MINGW64 ~/test (master)
    $


## Committing Your Changes
参见 [git commit](/Software/Git/commit.md)


## Skipping the Staging Area
参见 [git commit](/Software/Git/commit.md)


## Removing Files
参见 [git rm](/Software/Git/rm.md)


## Moving Files
参见 [git mv](/Software/Git/mv.md)


# 查看提交历史
参见 [git log](/Software/Git/log.md)


# 撤消操作
注意，有些撤消操作是不可逆的。这是在使用 Git 的过程中，会因为操作失误而导致之前的工作丢失的少有的几个地方之一。


参见 [git commit](/Software/Git/commit.md), [git reset](/Software/Git/reset.md), [git checkout](/Software/Git/checkout.md)


# Working with Remotes
参见 [git remote](/Software/Git/remote.md), [git fetch](/Software/Git/fetch.md), [git push](/Software/Git/push.md), [git pull](/Software/Git/pull.md)


# Tagging
参见 [git tag](/Software/Git/tag.md), [git show](/Software/Git/show.md), [git push](/Software/Git/push.md), [git checkout](/Software/Git/checkout.md)


# Git Aliases
参见 [git config](/Software/Git/config.md)

