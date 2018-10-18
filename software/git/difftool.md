可以使用 git difftool 命令来用 Araxis, ecmerge 或 vimdiff 等软件输出 diff 分析结果。


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


# --tool-help
使用 git difftool --tool-help 命令来看你的系统支持哪些 Git Diff 插件。


在 Linux 中

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


在 Windows 下

    bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
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
    
    bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
    $


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
