使 working tree 中的文件与 index 或者 tree 中文件保持一致。


# git checkout paths
还原文件，丢掉本地的修改。


```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) e22eb1c] init commit
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
me@mypc:~/test/workspace$ git checkout -- README
me@mypc:~/test/workspace$ cat README 
me@mypc:~/test/workspace$ git status
On branch master
nothing to commit, working directory clean
me@mypc:~/test/workspace$ 
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
