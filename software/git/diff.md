`git diff` 可以知道具体修改了什么地方


git diff 不能比较 untracked file
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace/
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README

nothing added to commit but untracked files present (use "git add" to track)
me@mypc:~/test/workspace$ git diff
me@mypc:~/test/workspace$ git diff --staged
me@mypc:~/test/workspace$ 
```


`git diff` 查看尚未暂存的文件更新了哪些部分
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace/
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) f21172f] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git diff
diff --git a/README b/README
index e69de29..ce01362 100644
--- a/README
+++ b/README
@@ -0,0 +1 @@
+hello
me@mypc:~/test/workspace$ 
```


若要查看已暂存的将要添加到下次提交里的内容，可以用 `git diff --cached` 命令。（ Git 1.6.1 及更高版本还允许使用 git diff --staged ，效果是相同的，但更好记些。）
```bash
me@mypc:~/test/workspace$ git diff --staged
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git diff --staged
diff --git a/README b/README
index e69de29..ce01362 100644
--- a/README
+++ b/README
@@ -0,0 +1 @@
+hello
me@mypc:~/test/workspace$ git diff
me@mypc:~/test/workspace$ 
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
