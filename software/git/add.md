`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。


`git add` 是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。将这个命令理解为“添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。


# -A/--all
working tree 中所有文件都被 add


add untracked and modified
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) e1be218] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ touch LICENSE
me@mypc:~/test/workspace$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
me@mypc:~/test/workspace$ git add -A
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   LICENSE
	modified:   README

me@mypc:~/test/workspace$ 
```


add deleted
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) d783006] init commit
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
me@mypc:~/test/workspace$ git add -A
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	deleted:    README

me@mypc:~/test/workspace$ 
```


add renamed
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) ca47456] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ mv README README.txt
me@mypc:~/test/workspace$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    README

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.txt

no changes added to commit (use "git add" and/or "git commit -a")
me@mypc:~/test/workspace$ git add -A
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    README -> README.txt

me@mypc:~/test/workspace$ 
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
