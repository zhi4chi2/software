文件状态(https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
- untracked - 既不在 last snapshot 中也不在 staging area 中。 `git add` 变为 staged
- tracked - 在 last snapshot 中
  - unmodified - 编辑文件则变为 modified ，删除文件则变为 untracked
  - modified - `git add` 变为 staged
  - staged - `git commit` 变为 unmodified


另可参见 https://try.github.io/levels/1/challenges/4


另外还有些状态
- unstaged - 应该就是 modified
- deleted - 使用 `git rm` 删除文件后。也是 staged ，等待被提交。


`git status` 的输出
- Untracked files - untracked
- Changes to be committed - tracked and staged to be committed 其下可能有 new file, modified, deleted
- Changes not staged for commit - 之前 tracked 如今修改(modified)之后没有 staged 其下可能有 modified


在新初始化的库中
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace/
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
me@mypc:~/test/workspace$ 
```


添加文件
```bash
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README

nothing added to commit but untracked files present (use "git add" to track)
me@mypc:~/test/workspace$ 
```


Untracked files 表示文件状态是 untracked


跟踪新文件
```bash
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README

me@mypc:~/test/workspace$ 
```


Changes to be committed 表示文件状态是 staged


提交
```bash
me@mypc:~/test/workspace$ git commit -m "init commit"
[master (root-commit) 6911d5e] init commit
 1 file changed, 1 insertion(+)
 create mode 100644 README
me@mypc:~/test/workspace$ git status
On branch master
nothing to commit, working directory clean
me@mypc:~/test/workspace$ 
```


然后再修改
```bash
me@mypc:~/test/workspace$ echo world >> README
me@mypc:~/test/workspace$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README

no changes added to commit (use "git add" and/or "git commit -a")
me@mypc:~/test/workspace$ 
```


Changes not staged for commit 表示文件在 modified 状态(a file that is tracked has been modified in the working directory but not yet staged)


再次调用 `git add` 使文件进入 staged 状态
```bash
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README

me@mypc:~/test/workspace$ 
```


再次提交
```bash
me@mypc:~/test/workspace$ git commit -m "modify README"
[master 49206f8] modify README
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ git status
On branch master
nothing to commit, working directory clean
me@mypc:~/test/workspace$ 
```


删除 README
```bash
me@mypc:~/test/workspace$ git rm README
rm 'README'
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	deleted:    README

me@mypc:~/test/workspace$ 
```


提交
```bash
me@mypc:~/test/workspace$ git commit -m "delete README"
[master 6d5d005] delete README
 1 file changed, 2 deletions(-)
 delete mode 100644 README
me@mypc:~/test/workspace$ git status
On branch master
nothing to commit, working directory clean
me@mypc:~/test/workspace$ 
```


# options
## -s
```bash
me@mypc:~/workspace/test$ git status -s
M  README
me@mypc:~/workspace/test$ 
```


含义
- ?? - 未跟踪文件
- A - 新添加到暂存区中的文件
- M - 出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在靠左边的 M 表示该文件被修改了并放入了暂存区。


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository

