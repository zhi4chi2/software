- rm - 删除本地
- git rm - 同时删除本地和库
- git rm --cached - 只删除库


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) bc495fd] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ rm README
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
    	deleted:    README
    
    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test/workspace$ git rm README
    rm 'README'
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	deleted:    README
    
    me@mypc:~/test/workspace$ git commit -m 'rm README'
    [master de91536] rm README
     1 file changed, 0 insertions(+), 0 deletions(-)
     delete mode 100644 README
    me@mypc:~/test/workspace$ ls
    me@mypc:~/test/workspace$ 


# git rm --cached
另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域删除再提交删除），但仍然希望保留在当前工作目录中。 


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 99cbee5] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ git rm --cached README
    rm 'README'
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	deleted:    README
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	README
    
    me@mypc:~/test/workspace$ git commit -m 'rm README'
    [master 52f89e1] rm README
     1 file changed, 0 insertions(+), 0 deletions(-)
     delete mode 100644 README
    me@mypc:~/test/workspace$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	README
    
    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test/workspace$ ls
    README
    me@mypc:~/test/workspace$ 


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) f9ee124] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ echo hello > README
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
    	modified:   README
    
    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git rm --cached README
    rm 'README'
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	deleted:    README
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	README
    
    me@mypc:~/test/workspace$ git commit -m 'rm README'
    [master fad77a8] rm README
     1 file changed, 0 insertions(+), 0 deletions(-)
     delete mode 100644 README
    me@mypc:~/test/workspace$ ls
    README
    me@mypc:~/test/workspace$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
    	README
    
    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test/workspace$ 


# git rm -f
如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f 。这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复。


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README 
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 9e42512] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ echo hello > README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	modified:   README
    
    me@mypc:~/test/workspace$ git rm README
    error: the following file has changes staged in the index:
        README
    (use --cached to keep the file, or -f to force removal)
    me@mypc:~/test/workspace$ git rm -f README
    rm 'README'
    me@mypc:~/test/workspace$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	deleted:    README
    
    me@mypc:~/test/workspace$ git commit -m 'rm README'
    [master 3d18b67] rm README
     1 file changed, 0 insertions(+), 0 deletions(-)
     delete mode 100644 README
    me@mypc:~/test/workspace$ ls
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
