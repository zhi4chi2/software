# 获取 Git 仓库

## 在现有目录中初始化仓库
在 windows 下
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