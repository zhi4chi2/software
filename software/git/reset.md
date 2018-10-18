# git reset HEAD paths
从 HEAD 复制 paths 到 index

    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git status
    On branch master
    
    Initial commit
    
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
    
    	new file:   README
    
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 0992174] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ echo hello > README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	modified:   README
    
    me@mypc:~/test/workspace$ git reset HEAD README
    Unstaged changes after reset:
    M	README
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
    	modified:   README
    
    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
