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


# git checkout tag
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) 89cd2cb] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ git tag v0.1
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git commit -a -m 'modify README'
[master ed3cd14] modify README
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ cat README
hello
me@mypc:~/test/workspace$ git checkout v0.1
Note: checking out 'v0.1'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 89cd2cb... init commit
me@mypc:~/test/workspace$ cat README
me@mypc:~/test/workspace$ 
```


这时要注意不能修改并提交，因为 tag 不会移动。


所以如果要修改代码并提交，则应该如下，在 checkout tag 时新建 branch
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) 37a941a] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ git tag v0.1
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git commit -a -m 'modify README'
[master 79b2e9d] modify README
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ cat README
hello
me@mypc:~/test/workspace$ git checkout -b v0.1.1 v0.1
Switched to a new branch 'v0.1.1'
me@mypc:~/test/workspace$ cat README
me@mypc:~/test/workspace$ 
```


# git checkout branch
checkout 做两件事
- 使 HEAD 指向 branch
- 使 working directory 中的文件与 branch 的 snapshot 一致


```bash
FIXME
git branch testing
git log --oneline --decorate
echo hello > README
git commit -a -m 'modify README'
git checkout testing
git log --oneline --decorate
cat README
```


如果
- local branch name 不存在，且
- 只在 only one remote 上有指定 branch name 的 remote branch
则 `git checkout branch-name` 等价于 `git checkout -b branch-name --track remote/branch-name`


## -b
```bash
FIXME
git checkout -b testing
git log --oneline --decorate
```


## --track
其实 --track 是传给 `git branch` 命令的。此时如果不指定 -b 则使用 remote branch 的名字。


--track 是默认行为，参见 `git branch` 的 --track 参数。


```bash
FIXME
git branch
git checkout --track origin/serverfix
git branch
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
- https://git-scm.com/book/en/v2/Git-Basics-Tagging
- https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell