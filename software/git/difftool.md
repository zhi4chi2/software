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


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
