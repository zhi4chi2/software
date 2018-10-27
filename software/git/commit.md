如果没有实际的修改，则不提交

    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    On branch master
    
    Initial commit
    
    nothing to commit
    me@mypc:~/test/workspace$ git log
    fatal: your current branch 'master' does not have any commits yet
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 451f81a] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ git commit -m 'again'
    On branch master
    nothing to commit, working directory clean
    me@mypc:~/test/workspace$ git log
    commit 451f81a8c7cee47944e037b7a59968b991e91ca9
    Author: me <me@example.com>
    Date:   Sun Jun 11 10:17:51 2017 +0800
    
        init commit
    me@mypc:~/test/workspace$ 


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 66a9bd9] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
- https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things

