# 获取 Git 仓库

## 在现有目录中初始化仓库
在 Windows 下
```bash
$ cd /G/TempWork/201705/20170523/workspace

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/workspace
$ pwd
/G/TempWork/201705/20170523/workspace

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/workspace
$ git init
Initialized empty Git repository in G:/TempWork/201705/20170523/workspace/.git/

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/workspace (master)
$ ls -a
./  ../  .git/

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/workspace (master)
$
```

## 克隆现有的仓库
在 Windows 下
```bash
$ cd /G/TempWork/201705/20170523/remote-clone

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone
$ git clone https://github.com/zhi4chi2/hello-world.git myfirst
Cloning into 'myfirst'...
remote: Counting objects: 23, done.
Unpacking objects: 100% (23/23), done.
remote: Total 23 (delta 0), reused 0 (delta 0), pack-reused 23

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone
$
```

clone 到了 G:\TempWork\201705\20170523\remote-clone\myfirst 目录下，库在 G:\TempWork\201705\20170523\remote-clone\myfirst\.git

除了 https:// 协议外还可以使用 git:// 或者使用 SSH 传输协议。

# 记录每次更新到仓库

## 检查当前文件状态

在 Windows 下
```bash
$ cd myfirst/

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

在 Windows 下
```bash
$ echo 'hello' > hello.txt

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ ls
hello.txt  LICENSE  README.md

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello.txt

nothing added to commit but untracked files present (use "git add" to track)

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

## 跟踪新文件

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git add hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory.

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

## 暂存已修改文件

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ echo 'hello' >> README.md

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   hello.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git add README.md
warning: LF will be replaced by CRLF in README.md.
The file will have its original line endings in your working directory.

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md
        new file:   hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

`git add` 是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。 将这个命令理解为“添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ echo 'world' >> README.md

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md
        new file:   hello.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

## 状态简览

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status -s
MM README.md
A  hello.txt

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

含义
- ?? - 未跟踪文件
- A - 新添加到暂存区中的文件
- M - 出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在靠左边的 M 表示该文件被修改了并放入了暂存区。

## 忽略文件

文件 .gitignore 的格式规范如下
- 所有空行或者以 # 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式匹配
- 匹配模式可以以 / 开头防止递归
- 匹配模式可以以 / 结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上 ! 取反。

glob 模式是指 shell 所使用的简化了的正则表达式。
- \* 匹配零个或多个任意字符；
- \[abc\] 匹配任何一个列在方括号中的字符；
- ? 只匹配一个任意字符；
- 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。
- 使用两个星号 \*\* 表示匹配任意中间目录，比如 `a/**/z` 可以匹配 a/z, a/b/z 或 a/b/c/z 等。

GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 https://github.com/github/gitignore 找到它

例子
```
# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```

## 查看已暂存和未暂存的修改

`git diff` 可以知道具体修改了什么地方


不加参数的 `git diff` 查看尚未暂存的文件更新了哪些部分

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git diff
warning: LF will be replaced by CRLF in README.md.
The file will have its original line endings in your working directory.
diff --git a/README.md b/README.md
index caca183..3fdbb2a 100644
--- a/README.md
+++ b/README.md
@@ -1,2 +1,3 @@
 abc
 hello
+world

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

若要查看已暂存的将要添加到下次提交里的内容，可以用 `git diff --cached` 命令。（ Git 1.6.1 及更高版本还允许使用 git diff --staged ，效果是相同的，但更好记些。）

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git diff --staged
diff --git a/README.md b/README.md
index 8baef1b..caca183 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 abc
+hello
diff --git a/hello.txt b/hello.txt
new file mode 100644
index 0000000..ce01362
--- /dev/null
+++ b/hello.txt
@@ -0,0 +1 @@
+hello

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```


在本书中，我们使用 git diff 来分析文件差异。 但是，如果你喜欢通过图形化的方式或其它格式输出方式的话，可以使用 git difftool 命令来用 Araxis, emerge 或 vimdiff 等软件输出 diff 分析结果。 使用 git difftool --tool-help 命令来看你的系统支持哪些 Git Diff 插件。

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git difftool --tool-help
'git difftool --tool=<tool>' may be set to one of the following:
                vimdiff
                vimdiff2
                vimdiff3

The following tools are valid, but not currently available:
                araxis
                bc
                bc3
                codecompare
                deltawalker
                diffmerge
                diffuse
                ecmerge
                emerge
                examdiff
                gvimdiff
                gvimdiff2
                gvimdiff3
                kdiff3
                kompare
                meld
                opendiff
                p4merge
                tkdiff
                winmerge
                xxdiff

Some of the tools listed above only work in a windowed
environment. If run in a terminal-only session, they will fail.

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

## 提交更新

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git commit
[master 80bb1ba] test first commit
 2 files changed, 2 insertions(+)
 create mode 100644 hello.txt

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

其中表示
- master - 分支
- 80bb1ba - 校验和
- 2 files changed - 多少文件被修改
- 2 insertions(+) - 多少行添加和删改过

默认用 vi 编辑提交说明

## 跳过使用暂存区域

`git commit -a` 自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git commit -a -m 'commit second'
warning: LF will be replaced by CRLF in README.md.
The file will have its original line endings in your working directory.
[master 503641d] commit second
 1 file changed, 1 insertion(+)

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

## 移除文件

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ rm hello.txt

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    hello.txt

no changes added to commit (use "git add" and/or "git commit -a")

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git rm hello.txt
rm 'hello.txt'

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```


如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f 。这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复。

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ echo 'xx' > hello.txt

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git add hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory.

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git rm hello.txt
error: the following file has changes staged in the index:
    hello.txt
(use --cached to keep the file, or -f to force removal)

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git rm -f hello.txt
rm 'hello.txt'

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git rm --cached hello.txt
rm 'hello.txt'

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    hello.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        hello.txt


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```


## 移动文件
在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git mv hello.txt hello

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    hello.txt -> hello


bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

`git mv` 相当于运行了三条命令
1. mv hello.txt hello
1. git rm hello.txt
1. git add hello

如此分开操作， Git 也会意识到这是一次改名，所以不管何种方式结果都一样。

# 查看提交历史

`git log` 查看提交历史

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log
commit 503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master)
Author: me <me@example.com>
Date:   Tue May 23 11:26:58 2017 +0800

    commit second

commit 80bb1bae9f5e8568dda37a99ab2500c373693677
Author: me <me@example.com>
Date:   Tue May 23 11:20:05 2017 +0800

    test first commit

commit f9eba7725452e13e8b66561106a52513f9c99d34 (origin/master, origin/HEAD)
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Apr 26 15:20:30 2017 +0800

    Update README.md

commit 83af367cbb1876fd9aaf8603da39d5a6fb6c13d0
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:10:34 2017 +0800

    Update README.md

commit a6b1e206cfbb0008a046ea58395aed495f51c5e9
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:10:08 2017 +0800

    Update README.md

commit 4defa8bcf2bb662c9be606de79423633ae1cec1f
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:05:31 2017 +0800

    Update README.md

commit b2f983942ebe43708814957cb2a448c7db193f0b
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:02:19 2017 +0800

    Update README.md

commit c405af2fe21583593b06b8ec00ea8b6821692154
Merge: 8013063 6e3f0f9
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 14:43:08 2017 +0800

    Merge pull request #1 from zhi4chi2/readme-edits

    readme edits

commit 6e3f0f9bc420517f068ae0772a919c4476c84a86
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Tue Jan 10 17:53:44 2017 +0800

    finish edit readme

commit 8013063b903fb5aef404f8e7bcb43913253ddb7d
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Tue Jan 10 17:45:08 2017 +0800

    Initial commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

`git log -p` 显示每次提交的内容差异。

`git log -p -2` 显示最近两次提交。

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log -p -2
commit 503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master)
Author: me <me@example.com>
Date:   Tue May 23 11:26:58 2017 +0800

    commit second

diff --git a/README.md b/README.md
index caca183..3fdbb2a 100644
--- a/README.md
+++ b/README.md
@@ -1,2 +1,3 @@
 abc
 hello
+world

commit 80bb1bae9f5e8568dda37a99ab2500c373693677
Author: me <me@example.com>
Date:   Tue May 23 11:20:05 2017 +0800

    test first commit

diff --git a/README.md b/README.md
index 8baef1b..caca183 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 abc
+hello
diff --git a/hello.txt b/hello.txt
new file mode 100644
index 0000000..ce01362
--- /dev/null
+++ b/hello.txt
@@ -0,0 +1 @@
+hello

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

`git log --stat` 每次提交的简略的统计信息

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log --stat
commit 503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master)
Author: me <me@example.com>
Date:   Tue May 23 11:26:58 2017 +0800

    commit second

 README.md | 1 +
 1 file changed, 1 insertion(+)

commit 80bb1bae9f5e8568dda37a99ab2500c373693677
Author: me <me@example.com>
Date:   Tue May 23 11:20:05 2017 +0800

    test first commit

 README.md | 1 +
 hello.txt | 1 +
 2 files changed, 2 insertions(+)

commit f9eba7725452e13e8b66561106a52513f9c99d34 (origin/master, origin/HEAD)
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Apr 26 15:20:30 2017 +0800

    Update README.md

 README.md | 10 +---------
 1 file changed, 1 insertion(+), 9 deletions(-)

commit 83af367cbb1876fd9aaf8603da39d5a6fb6c13d0
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:10:34 2017 +0800

    Update README.md

 README.md | 1 +
 1 file changed, 1 insertion(+)

commit a6b1e206cfbb0008a046ea58395aed495f51c5e9
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:10:08 2017 +0800

    Update README.md

 README.md | 14 ++++++++------
 1 file changed, 8 insertions(+), 6 deletions(-)

commit 4defa8bcf2bb662c9be606de79423633ae1cec1f
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:05:31 2017 +0800

    Update README.md

 README.md | 10 ++++++----
 1 file changed, 6 insertions(+), 4 deletions(-)

commit b2f983942ebe43708814957cb2a448c7db193f0b
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:02:19 2017 +0800

    Update README.md

 README.md | 7 +++----
 1 file changed, 3 insertions(+), 4 deletions(-)

commit c405af2fe21583593b06b8ec00ea8b6821692154
Merge: 8013063 6e3f0f9
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 14:43:08 2017 +0800

    Merge pull request #1 from zhi4chi2/readme-edits

    readme edits

commit 6e3f0f9bc420517f068ae0772a919c4476c84a86
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Tue Jan 10 17:53:44 2017 +0800

    finish edit readme

 README.md | 3 +++
 1 file changed, 3 insertions(+)

commit 8013063b903fb5aef404f8e7bcb43913253ddb7d
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Tue Jan 10 17:45:08 2017 +0800

    Initial commit

 LICENSE   | 201 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 README.md |   2 +
 2 files changed, 203 insertions(+)

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ 
```

另外一个常用的选项是 --pretty。 这个选项可以指定使用不同于默认格式的方式展示提交历史。这个选项有一些内建的子选项供你使用。比如用 oneline 将每个提交放在一行显示，查看的提交数很大时非常有用。 另外还有 short，full 和 fuller 可以用，展示的信息或多或少有些不同

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log --pretty=oneline
503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master) commit second
80bb1bae9f5e8568dda37a99ab2500c373693677 test first commit
f9eba7725452e13e8b66561106a52513f9c99d34 (origin/master, origin/HEAD) Update README.md
83af367cbb1876fd9aaf8603da39d5a6fb6c13d0 Update README.md
a6b1e206cfbb0008a046ea58395aed495f51c5e9 Update README.md
4defa8bcf2bb662c9be606de79423633ae1cec1f Update README.md
b2f983942ebe43708814957cb2a448c7db193f0b Update README.md
c405af2fe21583593b06b8ec00ea8b6821692154 Merge pull request #1 from zhi4chi2/readme-edits
6e3f0f9bc420517f068ae0772a919c4476c84a86 finish edit readme
8013063b903fb5aef404f8e7bcb43913253ddb7d Initial commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```


但最有意思的是 format ，可以定制要显示的记录格式。这样的输出对后期提取分析格外有用。因为你知道输出的格式不会随着 Git 的更新而发生改变

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log --pretty=format:"%h - %an, %ar : %s"
503641d - me, 2 hours ago : commit second
80bb1ba - me, 2 hours ago : test first commit
f9eba77 - zhi4chi2, 4 weeks ago : Update README.md
83af367 - zhi4chi2, 4 months ago : Update README.md
a6b1e20 - zhi4chi2, 4 months ago : Update README.md
4defa8b - zhi4chi2, 4 months ago : Update README.md
b2f9839 - zhi4chi2, 4 months ago : Update README.md
c405af2 - zhi4chi2, 4 months ago : Merge pull request #1 from zhi4chi2/readme-edits
6e3f0f9 - zhi4chi2, 4 months ago : finish edit readme
8013063 - zhi4chi2, 4 months ago : Initial commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

git log --pretty=format 常用的选项参见文档 https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2


作者指的是实际作出修改的人，提交者指的是最后将此工作成果提交到仓库的人。 所以，当你为某个项目发布补丁，然后某个核心成员将你的补丁并入项目时，你就是作者，而那个核心成员就是提交者。

当 oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。这个选项添加了一些 ASCII 字符串来形象地展示你的分支、合并历史

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log --pretty=format:"%h %s" --graph
* 503641d commit second
* 80bb1ba test first commit
* f9eba77 Update README.md
* 83af367 Update README.md
* a6b1e20 Update README.md
* 4defa8b Update README.md
* b2f9839 Update README.md
*   c405af2 Merge pull request #1 from zhi4chi2/readme-edits
|\
| * 6e3f0f9 finish edit readme
|/
* 8013063 Initial commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

git log 的常用选项参见文档 https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2


## 限制输出长度

git log 还有许多非常实用的限制输出长度的选项，也就是只输出部分提交信息。例如 -2 只显示最近的两条提交。其中的 n 可以是任何整数，表示仅显示最近的若干条提交。


另外还有按照时间作限制的选项，比如 --since 和 --until 也很有用。

例如，下面的命令列出所有最近两周内的提交：

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log --since=2.weeks
commit 503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master)
Author: me <me@example.com>
Date:   Tue May 23 11:26:58 2017 +0800

    commit second

commit 80bb1bae9f5e8568dda37a99ab2500c373693677
Author: me <me@example.com>
Date:   Tue May 23 11:20:05 2017 +0800

    test first commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```


这个命令可以在多种格式下工作，比如说具体的某一天 "2008-01-15" ，或者是相对地多久以前 "2 years 1 day 3 minutes ago" 。

还可以给出若干搜索条件，列出符合的提交。用 --author 选项显示指定作者的提交，用 --grep 选项搜索提交说明中的关键字。 （请注意，如果要得到同时满足这两个选项搜索条件的提交，就必须用 --all-match 选项。否则，满足任意一个条件的提交都会被匹配出来）


另一个非常有用的筛选选项是 -S ，可以列出那些添加或移除了某些字符串的提交。比如说，你想找出添加或移除了某一个特定函数的引用的提交，你可以这样使用：

在 Windows 下
```bash
bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$ git log -Sworld
commit 503641d7e5515a1ef56734e6e7b4190fb6299373 (HEAD -> master)
Author: me <me@example.com>
Date:   Tue May 23 11:26:58 2017 +0800

    commit second

commit 4defa8bcf2bb662c9be606de79423633ae1cec1f
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Wed Jan 11 15:05:31 2017 +0800

    Update README.md

commit 8013063b903fb5aef404f8e7bcb43913253ddb7d
Author: zhi4chi2 <yu_huanchao@163.com>
Date:   Tue Jan 10 17:45:08 2017 +0800

    Initial commit

bruce@bruce-PC MINGW64 /G/TempWork/201705/20170523/remote-clone/myfirst (master)
$
```

最后一个很实用的 git log 选项是路径(path)， 如果只关心某些文件或者目录的历史提交，可以在 git log 选项的最后指定它们的路径。 因为是放在最后位置上的选项，所以用两个短划线(--)隔开之前的选项和后面限定的路径名。

限制 git log 输出的选项参见原文档

# 撤消操作

注意，有些撤消操作是不可逆的。 这是在使用 Git 的过程中，会因为操作失误而导致之前的工作丢失的少有的几个地方之一。

