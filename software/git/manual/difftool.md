# Synopsis


# Description


# Options


# Examples


# Demo
## `git difftool`


## `git difftool --tool-help`
Run `git difftool --tool-help` to see what is available on your system.

使用 `git difftool --tool-help` 命令来看你的系统支持哪些 Git Diff 插件。

执行

    git difftool --tool-help

### Linux
**执行结果**

    me@mypc:~/test$ git difftool --tool-help
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
    me@mypc:~/test$ 

在 Linux 中默认使用 gvimdiff


### Windows
**执行结果**

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


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-difftool.html
