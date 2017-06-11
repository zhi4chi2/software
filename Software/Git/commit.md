如果没有实际的修改，则不提交
```bash
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
```


```bash
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
```


其中表示
- master - 分支
- 66a9bd9 - 校验和
- 1 file changed - 多少文件被修改
- 0 insertions(+), 0 deletions(-) - 多少行添加和删改过


默认用 vi 编辑提交说明


# -a
`git commit -a` 自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤


```bash
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git commit -a -m 'modify README'
[master 4d6484d] modify README
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ 
```


注意 -a 只能自动 stage 修改和删除的文件，不能自动 stage 新文件
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace/
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git commit -a -m 'init commit'
On branch master

Initial commit

Untracked files:
	README

nothing added to commit but untracked files present
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) b5200e1] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ 
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
