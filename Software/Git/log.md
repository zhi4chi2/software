测试用库
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) 27d9a26] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ git config --global user.name eg
me@mypc:~/test/workspace$ git config --global user.email eg@example.com
me@mypc:~/test/workspace$ git checkout -b eg-branch
Switched to a new branch 'eg-branch'
me@mypc:~/test/workspace$ echo hello > README
me@mypc:~/test/workspace$ git commit -a -m 'eg change README'
[eg-branch 5a4f7f8] eg change README
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ echo world >> README
me@mypc:~/test/workspace$ git commit -a -m 'eg change README again'
[eg-branch cf6c02a] eg change README again
 1 file changed, 1 insertion(+)
me@mypc:~/test/workspace$ git config --global user.name me
me@mypc:~/test/workspace$ git config --global user.email me@example.com
me@mypc:~/test/workspace$ git checkout master
Switched to branch 'master'
me@mypc:~/test/workspace$ touch LICENSE
me@mypc:~/test/workspace$ git add LICENSE
me@mypc:~/test/workspace$ git commit -m 'add LICENSE'
[master 56cc08e] add LICENSE
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 LICENSE
me@mypc:~/test/workspace$ git merge eg-branch -m 'merge eg-branch'
Merge made by the 'recursive' strategy.
 README | 2 ++
 1 file changed, 2 insertions(+)
me@mypc:~/test/workspace$ git branch -d eg-branch
Deleted branch eg-branch (was cf6c02a).
me@mypc:~/test/workspace$ echo 'hello world' > README
me@mypc:~/test/workspace$ git commit -a -m 'me change README'
[master 5a8da9e] me change README
 1 file changed, 1 insertion(+), 2 deletions(-)
me@mypc:~/test/workspace$ git log
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:12 2017 +0800

    me change README

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    merge eg-branch

commit 56cc08e9863eec5b34a70a5b8b32363c5b0e44a1
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    add LICENSE

commit cf6c02a972281d1dfbe54b499c0835d893e5eccd
Author: eg <eg@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    eg change README again

commit 27d9a261a591cdc2ce1578cc7fc7a2413ea1ca99
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    init commit

commit 5a4f7f85e89edee75d31d68fb9c69050103f5321
Author: eg <eg@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    eg change README
me@mypc:~/test/workspace$ 
```


# Commit Limiting
git log 还有许多非常实用的限制输出长度的选项，也就是只输出部分提交信息。


如果只关心某些文件或者目录的历史提交，可以在 git log 选项的最后指定它们的路径。因为是放在最后位置上的选项，所以用两个短划线(--)隔开之前的选项和后面限定的路径名。


限制 git log 输出的选项参见原文档 https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History


## -n
例如 -2 只显示最近的两条提交。其中的 n 可以是任何整数，表示仅显示最近的若干条提交。


```bash
t 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:12 2017 +0800

    me change README

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    merge eg-branch
me@mypc:~/test/workspace$ 
```


## --since and --until
按照时间作限制的选项


例如，下面的命令列出所有最近两周内的提交：
```bash
me@mypc:~/test/workspace$ git log --since=2.weeks --oneline
5a8da9e me change README
32e5ce5 merge eg-branch
56cc08e add LICENSE
cf6c02a eg change README again
27d9a26 init commit
5a4f7f8 eg change README
me@mypc:~/test/workspace$ 
```


这个命令可以在多种格式下工作，比如说具体的某一天 "2008-01-15" ，或者是相对地多久以前 "2 years 1 day 3 minutes ago" 。


## --author
显示指定作者的提交
```bash
me@mypc:~/test/workspace$ git log --oneline --author=eg
cf6c02a eg change README again
5a4f7f8 eg change README
me@mypc:~/test/workspace$ 
```


## --grep
搜索提交说明中的关键字
```bash
me@mypc:~/test/workspace$ git log --oneline --grep change
5a8da9e me change README
cf6c02a eg change README again
5a4f7f8 eg change README
me@mypc:~/test/workspace$ 
```


## --all-match
如果要得到同时满足多个 --grep 搜索条件的提交，就必须用 --all-match 选项。否则，满足任意一个条件的提交都会被匹配
```bash
me@mypc:~/test/workspace$ git log --oneline --grep eg --grep change
5a8da9e me change README
32e5ce5 merge eg-branch
cf6c02a eg change README again
5a4f7f8 eg change README
me@mypc:~/test/workspace$ git log --oneline --grep eg --grep change --all-match
cf6c02a eg change README again
5a4f7f8 eg change README
me@mypc:~/test/workspace$ 
```


## -S
-S 可以列出那些添加或移除了某些字符串的提交。比如说，你想找出添加或移除了某一个特定函数的引用的提交
```bash
me@mypc:~/test/workspace$ git log --oneline -Sworld
cf6c02a eg change README again
me@mypc:~/test/workspace$ 
```


# Commit Ordering
默认 log 按照 reverse chronological order 排序，注意默认排序的 init commit 排在了 eg change README 之前！


指定顺序
```bash
me@mypc:~/test/workspace$ git log --oneline --date-order
5a8da9e me change README
32e5ce5 merge eg-branch
56cc08e add LICENSE
cf6c02a eg change README again
5a4f7f8 eg change README
27d9a26 init commit
me@mypc:~/test/workspace$ 
```


# COMMON DIFF OPTIONS
## -p
`git log -p` 显示每次提交的内容差异。
```bash
me@mypc:~/test/workspace$ git log -p -2
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:12 2017 +0800

    me change README

diff --git a/README b/README
index 94954ab..3b18e51 100644
--- a/README
+++ b/README
@@ -1,2 +1 @@
-hello
-world
+hello world

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    merge eg-branch
me@mypc:~/test/workspace$ 
```


## --stat
`git log --stat` 每次提交的简略的统计信息
```bash
me@mypc:~/test/workspace$ git log --stat -2
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:12 2017 +0800

    me change README

 README | 3 +--
 1 file changed, 1 insertion(+), 2 deletions(-)

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>
Date:   Sun Jun 11 13:28:11 2017 +0800

    merge eg-branch
me@mypc:~/test/workspace$ 
```


# Commit Formatting
## --pretty
这个选项可以指定使用不同于默认格式的方式展示提交历史。这个选项有一些内建的子选项供你使用。比如用 oneline 将每个提交放在一行显示，查看的提交数很大时非常有用。 另外还有 short，full 和 fuller 可以用，展示的信息或多或少有些不同
```bash
me@mypc:~/test/workspace$ git log --pretty=oneline
5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546 me change README
32e5ce54e340a114170b3192187c4aafcd4bd784 merge eg-branch
56cc08e9863eec5b34a70a5b8b32363c5b0e44a1 add LICENSE
cf6c02a972281d1dfbe54b499c0835d893e5eccd eg change README again
27d9a261a591cdc2ce1578cc7fc7a2413ea1ca99 init commit
5a4f7f85e89edee75d31d68fb9c69050103f5321 eg change README
me@mypc:~/test/workspace$ git log --pretty=short -2
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>

    me change README

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>

    merge eg-branch
me@mypc:~/test/workspace$ git log --pretty=full -2
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author: me <me@example.com>
Commit: me <me@example.com>

    me change README

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author: me <me@example.com>
Commit: me <me@example.com>

    merge eg-branch
me@mypc:~/test/workspace$ git log --pretty=fuller -2
commit 5a8da9ea5c10d07f68bd83bf7c69c8934c5b8546
Author:     me <me@example.com>
AuthorDate: Sun Jun 11 13:28:12 2017 +0800
Commit:     me <me@example.com>
CommitDate: Sun Jun 11 13:28:12 2017 +0800

    me change README

commit 32e5ce54e340a114170b3192187c4aafcd4bd784
Merge: 56cc08e cf6c02a
Author:     me <me@example.com>
AuthorDate: Sun Jun 11 13:28:11 2017 +0800
Commit:     me <me@example.com>
CommitDate: Sun Jun 11 13:28:11 2017 +0800

    merge eg-branch
me@mypc:~/test/workspace$ 
```


但最有意思的是 format ，可以定制要显示的记录格式。这样的输出对后期提取分析格外有用。因为你知道输出的格式不会随着 Git 的更新而发生改变
```bash
me@mypc:~/test/workspace$ git log --pretty=format:"%h - %an, %ar : %s"
5a8da9e - me, 10 minutes ago : me change README
32e5ce5 - me, 10 minutes ago : merge eg-branch
56cc08e - me, 10 minutes ago : add LICENSE
cf6c02a - eg, 10 minutes ago : eg change README again
27d9a26 - me, 10 minutes ago : init commit
5a4f7f8 - eg, 10 minutes ago : eg change README
me@mypc:~/test/workspace$ 
```


git log --pretty=format 常用的选项参见文档 https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History


author 指的是实际作出修改的人， committer 指的是最后将此工作成果提交到仓库的人。 所以，当你为某个项目发布补丁，然后某个核心成员将你的补丁并入项目时，你就是作者，而那个核心成员就是提交者。


# --graph
当 --pretty=oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。这个选项添加了一些 ASCII 字符串来形象地展示你的分支、合并历史


```bash
me@mypc:~/test/workspace$ git log --pretty=format:"%h %s" --graph
* 5a8da9e me change README
*   32e5ce5 merge eg-branch
|\  
| * cf6c02a eg change README again
| * 5a4f7f8 eg change README
* | 56cc08e add LICENSE
|/  
* 27d9a26 init commit
me@mypc:~/test/workspace$ 
```


git log 的常用选项参见文档 https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History

