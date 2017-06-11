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

