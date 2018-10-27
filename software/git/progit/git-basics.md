# Getting a Git Repository
## Initializing a Repository in an Existing Directory
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git init
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git init
    Initialized empty Git repository in /home/me/test/.git/
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ 


## Cloning an Existing Repository
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git clone https://github.com/schacon/simplegit-progit
    ls -aF
    cd simplegit-progit
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/schacon/simplegit-progit
    Cloning into 'simplegit-progit'...
    remote: Enumerating objects: 13, done.
    remote: Total 13 (delta 0), reused 0 (delta 0), pack-reused 13
    Unpacking objects: 100% (13/13), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  simplegit-progit/
    me@mypc:~/test$ cd simplegit-progit
    me@mypc:~/test/simplegit-progit$ ls -aF
    ./  ../  .git/  lib/  Rakefile  README
    me@mypc:~/test/simplegit-progit$ 

clone 到了 `/home/me/test/simplegit-progit` 目录下（自动创建此目录），库在 `/home/me/test/simplegit-progit/.git`


### `git clone <repository> <directory>`
GitHub 的 git clone url 可以加 .git 也可以省略。

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git clone https://github.com/schacon/simplegit-progit.git my-simplegit
    ls -aF
    cd my-simplegit
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/schacon/simplegit-progit.git my-simplegit
    Cloning into 'my-simplegit'...
    remote: Enumerating objects: 13, done.
    remote: Total 13 (delta 0), reused 0 (delta 0), pack-reused 13
    Unpacking objects: 100% (13/13), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  my-simplegit/
    me@mypc:~/test$ cd my-simplegit
    me@mypc:~/test/my-simplegit$ ls -aF
    ./  ../  .git/  lib/  Rakefile  README
    me@mypc:~/test/my-simplegit$ 

> Git has a number of different transfer protocols you can use. The previous example uses the `https://` protocol, but you may also see `git://` or `user@server:path/to/repo.git`, which uses the SSH transfer protocol.

除了 https:// 协议外还可以使用 git:// 或者使用 SSH 传输协议（例如 `user@server:path/to/repo.git` ）。


# Recording Changes to the Repository
> Remember that each file in your working directory can be in one of two states: tracked or untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.
> 
> Untracked files are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area.

working directory 中文件的状态

- untracked - 既不在 last snapshot 中也不在 staging area 中的文件。 `git add` 后变为 staged
- tracked
    - unmodified - 编辑文件则变为 modified ，删除文件则变为 untracked
    - modified - `git add` 后变为 staged
    - staged - `git commit` 后变为 unmodified

参见原文档 Figure 8. The lifecycle of the status of your files.


## Checking the Status of Your Files
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    clear

执行

    git status
    echo 'My Project' > README
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master

    Initial commit

    nothing to commit (create/copy files and use "git add" to track)
    me@mypc:~/test$ echo 'My Project' > README
    me@mypc:~/test$ git status
    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ 


## Tracking New Files
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    clear

执行

    git add README
    git status

**执行结果**

    me@mypc:~/test$ git add README
    me@mypc:~/test$ git status
    On branch master

    Initial commit

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)

	    new file:   README

    me@mypc:~/test$ 

与文档中不一致的地方：文档中是 `(use "git reset HEAD <file>..." to unstage)`

只有在 `Initial commit` 时才会这样，否则如文档。

> The `git add` command takes a path name for either a file or a directory; if it’s a directory, the command adds all the files in that directory recursively.


## Staging Modified Files
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1' > README
    git add README
    echo 'C1-1' >> CONTRIBUTING.md
    clear

执行

    git status
    git add CONTRIBUTING.md
    git status
    echo 'C1-2' >> CONTRIBUTING.md
    git status
    git add CONTRIBUTING.md
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    new file:   README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ git add CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md
	    new file:   README

    me@mypc:~/test$ echo 'C1-2' >> CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md
	    new file:   README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ git add CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md
	    new file:   README

    me@mypc:~/test$ 


## Short Status
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch Rakefile
    mkdir lib
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1-1' >> Rakefile
    echo 'C1' >> lib/simplegit.rb
    touch lib/git.rb
    git add .
    echo 'C1' >> README
    echo 'C1-2' >> Rakefile
    touch LICENSE.txt
    clear

执行

    git status -s

**执行结果**

    me@mypc:~/test$ git status -s
     M README
    MM Rakefile
    A  lib/git.rb
    M  lib/simplegit.rb
    ?? LICENSE.txt
    me@mypc:~/test$ 


> There are two columns to the output - the left-hand column indicates the status of the staging area and the right-hand column indicates the status of the working tree.


## Ignoring Files
文件 `.gitignore` 的格式规范(rules for the patterns)如下

- 所有空行或者以 # 开头的行都会被 Git 忽略。
- Standard glob patterns work, and will be applied recursively throughout the entire working tree.
- 匹配模式可以以 / 开头防止递归
- 匹配模式可以以 / 结尾指定目录
- 不忽略指定模式的文件或目录，可以在模式前加上 ! 取反。


> Glob patterns are like simplified regular expressions that shells use.

glob 模式是指 shell 所使用的简化了的正则表达式。

- \* 匹配零个或多个任意字符；
- \[abc\] 匹配任何一个列在方括号中的字符；
- ? 只匹配一个任意字符；
- 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。
- 使用两个星号 \*\* 表示匹配任意中间目录，比如 `a/**/z` 可以匹配 a/z, a/b/z 或 a/b/c/z 等。


例子

    # ignore all .a files
    *.a
    
    # but do track lib.a, even though you're ignoring .a files above
    !lib.a
    
    # only ignore the TODO file in the current directory, not subdir/TODO
    /TODO
    
    # ignore all files in any directory named build
    build/
    
    # ignore doc/notes.txt, but not doc/server/arch.txt
    doc/*.txt
    
    # ignore all .pdf files in the doc/ directory and any of its subdirectories
    doc/**/*.pdf


GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 <https://github.com/github/gitignore> 找到它


> In the simple case, a repository might have a single `.gitignore` file in its root directory, which applies recursively to the entire repository. However, it is also possible to have additional `.gitignore` files in subdirectories. The rules in these nested `.gitignore` files apply only to the files under the directory where they are located. (The Linux kernel source repository has 206 `.gitignore` files.)
> 
> It is beyond the scope of this book to get into the details of multiple `.gitignore` files; see `man gitignore` for the details.


## Viewing Your Staged and Unstaged Changes
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1' > README
    git add README
    echo 'C1-1' >> CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    clear

执行

    git status
    git diff

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    new file:   README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ git diff
    diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
    index 9c4156d..64ee11b 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1 +1,3 @@
     C0
    +C1-1
    +C1-2
    me@mypc:~/test$ 


> That command compares what is in your working directory with what is in your staging area. The result tells you the changes you’ve made that you haven’t yet staged.
> 
> If you want to see what you’ve staged that will go into your next commit, you can use `git diff --staged`. This command compares your staged changes to your last commit

执行

    git diff --staged

**执行结果**

    me@mypc:~/test$ git diff --staged
    diff --git a/README b/README
    new file mode 100644
    index 0000000..e2cf5e7
    --- /dev/null
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ 


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1-1' >> CONTRIBUTING.md
    clear

执行

    git add CONTRIBUTING.md
    echo '# test line' >> CONTRIBUTING.md
    git status
    git diff
    git diff --cached

**执行结果**

    me@mypc:~/test$ git add CONTRIBUTING.md
    me@mypc:~/test$ echo '# test line' >> CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ git diff
    diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
    index ae45e64..3ec9016 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1,2 +1,3 @@
     C0
     C1-1
    +# test line
    me@mypc:~/test$ git diff --cached
    diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
    index 9c4156d..ae45e64 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1 +1,2 @@
     C0
    +C1-1
    me@mypc:~/test$ 


### `git difftool`
> There is another way to look at these diffs if you prefer a graphical or external diff viewing program instead. If you run `git difftool` instead of `git diff`, you can view any of these diffs in software like emerge, vimdiff and many more (including commercial products).

执行

    git difftool

**执行结果**

    me@mypc:~/test$ git difftool

    This message is displayed because 'diff.tool' is not configured.
    See 'git difftool --tool-help' or 'git help config' for more details.
    'git difftool' will now attempt to use one of the following tools:
    meld opendiff kdiff3 tkdiff xxdiff kompare gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare emerge vimdiff

    Viewing (1/1): 'CONTRIBUTING.md'
    Launch 'gvimdiff' [Y/n]: 
    2 files to edit

    (gvim:3859): GLib-GObject-WARNING **: cannot retrieve class for invalid (unclassed) type '<invalid>'
    me@mypc:~/test$ 


### `git difftool --tool-help`
Run `git difftool --tool-help` to see what is available on your system.

使用 `git difftool --tool-help` 命令来看你的系统支持哪些 Git Diff 插件。

执行

    git difftool --tool-help

#### Linux
**执行结果**

    me@mypc:~/test$ git difftool --tool-help
    'git difftool --tool=<tool>' may be set to one of the following:
		    araxis
		    gvimdiff
		    gvimdiff2
		    gvimdiff3
		    vimdiff
		    vimdiff2
		    vimdiff3

    The following tools are valid, but not currently available:
		    bc
		    bc3
		    codecompare
		    deltawalker
		    diffmerge
		    diffuse
		    ecmerge
		    emerge
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
    me@mypc:~/test$ 

在 Linux 中默认使用 gvimdiff


#### Windows
**执行结果**

    me@mypc MINGW64 ~/test (master)
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
    
    me@mypc MINGW64 ~/test (master)
    $


## Committing Your Changes
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    echo 'C1' > README
    echo 'C1-1' >> CONTRIBUTING.md
    echo 'C1-2' >> CONTRIBUTING.md
    git add .
    clear

执行

    git commit

**执行结果**

      1 
      2 # Please enter the commit message for your changes. Lines starting
      3 # with '#' will be ignored, and an empty message aborts the commit.
      4 # On branch master
      5 # Changes to be committed:
      6 #       modified:   CONTRIBUTING.md
      7 #       new file:   README
      8 #
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    ~                                                                               
    "~/test/.git/COMMIT_EDITMSG" 8L, 235C                         1,0-1         All


> You can see that the default commit message contains the latest output of the `git status` command commented out and one empty line on top.


如果直接按 `:q` 退出，则不会提交：

    me@mypc:~/test$ git commit
    Aborting commit due to empty commit message.
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md
	    new file:   README

    me@mypc:~/test$ 


`git commit` launches your editor of choice. (This is set by your shell’s `EDITOR` environment variable — usually vim or emacs, although you can configure it with whatever you want using the `git config --global core.editor` command as you saw in Getting Started).

> For an even more explicit reminder of what you’ve modified, you can pass the `-v` option to `git commit`. Doing so also puts the diff of your change in the editor so you can see exactly what changes you’re committing.

执行

    git commit -v

**执行结果**

      1 
      2 # Please enter the commit message for your changes. Lines starting
      3 # with '#' will be ignored, and an empty message aborts the commit.
      4 # On branch master
      5 # Changes to be committed:
      6 #       modified:   CONTRIBUTING.md
      7 #       new file:   README
      8 #
      9 # ------------------------ >8 ------------------------
     10 # Do not touch the line above.
     11 # Everything below will be removed.
     12 diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
     13 index e69de29..3f0eca2 100644
     14 --- a/CONTRIBUTING.md
     15 +++ b/CONTRIBUTING.md
     16 @@ -0,0 +1,2 @@
     17 +C1-1
     18 +C1-2
     19 diff --git a/README b/README
     20 new file mode 100644
     21 index 0000000..e2cf5e7
     22 --- /dev/null
     23 +++ b/README
     24 @@ -0,0 +1 @@
     25 +C1
    ~                                                                               
    "~/test/.git/COMMIT_EDITMSG" 25L, 624C                        1,0-1         All

执行

    git commit -m 'modified CONTRIBUTING.md, add README'

**执行结果**

    me@mypc:~/test$ git commit -m 'modified CONTRIBUTING.md, add README'
    [master 0a111d2] modified CONTRIBUTING.md, add README
     2 files changed, 3 insertions(+)
     create mode 100644 README
    me@mypc:~/test$ 


the commit has given you some output about itself:

- which branch you committed to (master),
- what SHA-1 checksum the commit has (d6d6248),
- how many files were changed,
- and statistics about lines added and removed in the commit.


## Skipping the Staging Area
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch CONTRIBUTING.md
    git add .
    git commit -m 'C0'
    touch README
    echo 'C1' >> CONTRIBUTING.md
    clear

执行

    git status
    git commit -a -m 'C1'
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ git commit -a -m 'C1'
    [master 6c436cf] C1
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ 

注意， `git commit -a` 只会 stage every file that is already tracked ，不会自动添加 untracked files


## Removing Files
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    clear

执行

    ls -aF
    git rm PROJECTS.md
    ls -aF
    git status

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  PROJECTS.md
    me@mypc:~/test$ git rm PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    deleted:    PROJECTS.md

    me@mypc:~/test$ 


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    clear

执行

    ls -aF
    rm PROJECTS.md
    ls -aF
    git status
    git rm PROJECTS.md
    git status

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  PROJECTS.md
    me@mypc:~/test$ rm PROJECTS.md
    me@mypc:~/test$ ls -aF
    ./  ../  .git/
    me@mypc:~/test$ git status
    On branch master
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    deleted:    PROJECTS.md

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ git rm PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    deleted:    PROJECTS.md

    me@mypc:~/test$ 


### `git rm -f`
> If you modified the file and added it to the staging area already, you must force the removal with the `-f` option. This is a safety feature to prevent accidental removal of data that hasn’t yet been recorded in a snapshot and that can’t be recovered from Git.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch PROJECTS.md
    git add .
    git commit -m 'C0'
    echo 'C1' >> PROJECTS.md
    git add .
    clear

执行

    git status
    git rm -f PROJECTS.md
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   PROJECTS.md

    me@mypc:~/test$ git rm -f PROJECTS.md
    rm 'PROJECTS.md'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    deleted:    PROJECTS.md

    me@mypc:~/test$ 


### `git rm --cached`
> Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore` file and accidentally staged it, like a large log file or a bunch of `.a` compiled files. To do this, use the `--cached` option

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    git rm --cached README
    git status
    ls -aF

**执行结果**

    me@mypc:~/test$ git rm --cached README
    rm 'README'
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    deleted:    README

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ ls -aF
    ./  ../  .git/  README
    me@mypc:~/test$ 


> You can pass files, directories, and file-glob patterns to the `git rm` command. That means you can do things such as:
>     $ git rm log/\*.log
> Note the backslash (`\`) in front of the `*`. This is necessary because Git does its own filename expansion in addition to your shell’s filename expansion.


最佳实践：删除 tracked file

同时从 working tree 和 staging area 中删除

- unmodified - `git rm`
- modified - 先 `git checkout --` 再 `git rm`
- staged - `git rm -f`

如果仅从 staging area 删除，但在 working tree 中保留则使用 `git rm --cached`

应该不会需要只在 working tree 中删除！如果确实需要，使用 Linux 系统命令 `rm` 即可。


## Moving Files
> Unlike many other VCS systems, Git doesn’t explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. However, Git is pretty smart about figuring that out after the fact

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    git add .
    git commit -m 'C0'
    clear

执行

    git mv README.md README
    git status

**执行结果**

    me@mypc:~/test$ git mv README.md README
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    renamed:    README.md -> README

    me@mypc:~/test$ 


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    git add .
    git commit -m 'C0'
    clear

执行

    mv README.md README
    git rm README.md
    git add README
    git status

**执行结果**

    me@mypc:~/test$ mv README.md README
    me@mypc:~/test$ git rm README.md
    rm 'README.md'
    me@mypc:~/test$ git add README
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    renamed:    README.md -> README

    me@mypc:~/test$ 


> Git figures out that it’s a rename implicitly, so it doesn’t matter if you rename a file that way or with the `mv` command. The only real difference is that `git mv` is one command instead of three — it’s a convenience function. More importantly, you can use any tool you like to rename a file, and address the add/rm later, before you commit.


# Viewing the Commit History
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/simplegit-progit
    cd simplegit-progit/
    clear

执行

    git log

**执行结果**

    me@mypc:~/test/simplegit-progit$ git log
    commit ca82a6dff817ec66f44342007202690a93763949
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Mon Mar 17 21:52:11 2008 -0700

        changed the verison number

    commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Sat Mar 15 16:40:33 2008 -0700

        removed unnecessary test code

    commit a11bef06a3f659402fe7563abf99ad00de2209e6
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Sat Mar 15 10:31:28 2008 -0700

        first commit
    me@mypc:~/test/simplegit-progit$ 


## `git log -p/--patch`
> One of the more helpful options is `-p` or `--patch`, which shows the difference (the patch output) introduced in each commit. You can also limit the number of log entries displayed, such as using `-2` to show only the last two entries.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/simplegit-progit
    cd simplegit-progit/
    clear

执行

    git log -p -2

**执行结果**

    me@mypc:~/test/simplegit-progit$ git log -p -2
    commit ca82a6dff817ec66f44342007202690a93763949
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Mon Mar 17 21:52:11 2008 -0700

        changed the verison number

    diff --git a/Rakefile b/Rakefile
    index a874b73..8f94139 100644
    --- a/Rakefile
    +++ b/Rakefile
    @@ -5,7 +5,7 @@ require 'rake/gempackagetask'
     spec = Gem::Specification.new do |s|
         s.platform  =   Gem::Platform::RUBY
         s.name      =   "simplegit"
    -    s.version   =   "0.1.0"
    +    s.version   =   "0.1.1"
         s.author    =   "Scott Chacon"
         s.email     =   "schacon@gmail.com"
         s.summary   =   "A simple gem for using Git in Ruby code."

    commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Sat Mar 15 16:40:33 2008 -0700

        removed unnecessary test code

    diff --git a/lib/simplegit.rb b/lib/simplegit.rb
    index a0a60ae..47c6340 100644
    --- a/lib/simplegit.rb
    +++ b/lib/simplegit.rb
    @@ -18,8 +18,3 @@ class SimpleGit
         end
       
     end
    -
    -if $0 == __FILE__
    -  git = SimpleGit.new
    -  puts git.show
    -end
    \ No newline at end of file
    me@mypc:~/test/simplegit-progit$ 


## `git log --stat`
> if you want to see some abbreviated stats for each commit, you can use the `--stat` option

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/simplegit-progit
    cd simplegit-progit/
    clear

执行

    git log --stat

**执行结果**

    me@mypc:~/test/simplegit-progit$ git log --stat
    commit ca82a6dff817ec66f44342007202690a93763949
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Mon Mar 17 21:52:11 2008 -0700

        changed the verison number

     Rakefile | 2 +-
     1 file changed, 1 insertion(+), 1 deletion(-)

    commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Sat Mar 15 16:40:33 2008 -0700

        removed unnecessary test code

     lib/simplegit.rb | 5 -----
     1 file changed, 5 deletions(-)

    commit a11bef06a3f659402fe7563abf99ad00de2209e6
    Author: Scott Chacon <schacon@gmail.com>
    Date:   Sat Mar 15 10:31:28 2008 -0700

        first commit

     README           |  6 ++++++
     Rakefile         | 23 +++++++++++++++++++++++
     lib/simplegit.rb | 25 +++++++++++++++++++++++++
     3 files changed, 54 insertions(+)
    me@mypc:~/test/simplegit-progit$ 


## `git log --pretty`
`--pretty` changes the log output to formats other than the default.

A few prebuilt options are available for you to use.

- oneline
- short
- full
- fuller
- format


### `git log --pretty=oneline`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/simplegit-progit
    cd simplegit-progit/
    clear

执行

    git log --pretty=oneline

**执行结果**

    me@mypc:~/test/simplegit-progit$ git log --pretty=oneline
    ca82a6dff817ec66f44342007202690a93763949 changed the verison number
    085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test code
    a11bef06a3f659402fe7563abf99ad00de2209e6 first commit
    me@mypc:~/test/simplegit-progit$ 


### `git log --pretty=format`
> The most interesting option is `format`, which allows you to specify your own log output format. This is especially useful when you’re generating output for machine parsing — because you specify the format explicitly, you know it won’t change with updates to Git

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/simplegit-progit
    cd simplegit-progit/
    clear

执行

    git log --pretty=format:"%h - %an, %ar : %s"

**执行结果**

    me@mypc:~/test/simplegit-progit$ git log --pretty=format:"%h - %an, %ar : %s"
    ca82a6d - Scott Chacon, 11 years ago : changed the verison number
    085bb3b - Scott Chacon, 11 years ago : removed unnecessary test code
    a11bef0 - Scott Chacon, 11 years ago : first commit
    me@mypc:~/test/simplegit-progit$ 

format 中可用选项参见原文档中 Table 1. Useful options for `git log --pretty=format`

> You may be wondering what the difference is between author and committer. The author is the person who originally wrote the work, whereas the committer is the person who last applied the work. So, if you send in a patch to a project and one of the core members applies the patch, both of you get credit — you as the author, and the core member as the committer.


## `git log --graph`
FIXME

`git log` 可用选项参见原文档中 Table 2. Common options to `git log`


## Limiting Log Output
> However, the time-limiting options such as `--since` and `--until` are very useful. For example, this command gets the list of commits made in the last two weeks:
> 
>     $ git log --since=2.weeks
> 
> This command works with lots of formats — you can specify a specific date like `"2008-01-15"`, or a relative date such as `"2 years 1 day 3 minutes ago"`.


> You can also filter the list to commits that match some search criteria. The `--author` option allows you to filter on a specific author, and the `--grep` option lets you search for keywords in the commit messages.

> You can specify more than one instance of both the `--author` and `--grep` search criteria, which will limit the commit output to commits that match any of the `--author` patterns and any of the `--grep` patterns; however, adding the `--all-match` option further limits the output to just those commits that match all `--grep` patterns.


> Another really helpful filter is the `-S` option (colloquially referred to as Git’s “pickaxe” option), which takes a string and shows only those commits that changed the number of occurrences of that string. For instance, if you wanted to find the last commit that added or removed a reference to a specific function, you could call:
> 
>     $ git log -S function_name


> The last really useful option to pass to `git log` as a filter is a path. If you specify a directory or file name, you can limit the log output to commits that introduced a change to those files. This is always the last option and is generally preceded by double dashes (`--`) to separate the paths from the options.


参见原文档中 Table 3. Options to limit the output of `git log`

> Depending on the workflow used in your repository, it’s possible that a sizable percentage of the commits in your log history are just merge commits, which typically aren’t very informative. To prevent the display of merge commits cluttering up your log history, simply add the log option `--no-merges`.


# Undoing Things
## `git commit --amend`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    touch forgotten_file
    git add README.md
    clear

执行

    git commit -m 'initial commit'
    git add forgotten_file
    git log --stat
    git commit --amend -m 'Initial Commit'
    git log --stat

**执行结果**

    me@mypc:~/test$ git commit -m 'initial commit'
    [master (root-commit) bea95c5] initial commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README.md
    me@mypc:~/test$ git add forgotten_file
    me@mypc:~/test$ git log --stat
    commit bea95c5c869c0293f8e2a15960fcbb220b3f938b
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:30:58 2018 +0800

        initial commit

     README.md | 0
     1 file changed, 0 insertions(+), 0 deletions(-)
    me@mypc:~/test$ git commit --amend -m 'Initial Commit'
    [master 86b1d53] Initial Commit
     Date: Sat Oct 27 13:30:58 2018 +0800
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README.md
     create mode 100644 forgotten_file
    me@mypc:~/test$ git log --stat
    commit 86b1d53045f65f522920762fd5eab45a268c64bd
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:30:58 2018 +0800

        Initial Commit

     README.md      | 0
     forgotten_file | 0
     2 files changed, 0 insertions(+), 0 deletions(-)
    me@mypc:~/test$ 


## Unstaging a Staged File
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    echo 'C0' > CONTRIBUTING.md
    git add *
    git commit -m 'C0'
    echo 'C1' >> CONTRIBUTING.md
    git mv README.md README
    clear

执行

    git add *
    git status
    git reset HEAD CONTRIBUTING.md
    git status
    cat CONTRIBUTING.md

**执行结果**

    me@mypc:~/test$ git add *
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   CONTRIBUTING.md
	    renamed:    README.md -> README

    me@mypc:~/test$ git reset HEAD CONTRIBUTING.md
    Unstaged changes after reset:
    M	CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    renamed:    README.md -> README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ cat CONTRIBUTING.md
    C0
    C1
    me@mypc:~/test$ 


>   It’s true that `git reset` can be a dangerous command, especially if you provide the `--hard` flag. However, in the scenario described above, the file in your working directory is not touched, so it’s relatively safe.


## Unmodifying a Modified File
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README.md
    echo 'C0' > CONTRIBUTING.md
    git add *
    git commit -m 'C0'
    git mv README.md README
    git add *
    echo 'C1' >> CONTRIBUTING.md
    clear

执行

    git status
    git checkout -- CONTRIBUTING.md
    git status
    cat CONTRIBUTING.md

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    renamed:    README.md -> README

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   CONTRIBUTING.md

    me@mypc:~/test$ git checkout -- CONTRIBUTING.md
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    renamed:    README.md -> README

    me@mypc:~/test$ cat CONTRIBUTING.md
    C0
    me@mypc:~/test$ 


> It’s important to understand that `git checkout -- <file>` is a dangerous command. Any changes you made to that file are gone — Git just copied another file over it.


# Working with Remotes

- managing remote repositories
    - add remote repositories
    - remove remotes
    - manage various remote branches and define them as being tracked or not
- pushing and pulling data to and from them


## Showing Your Remotes
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote
    git remote -v

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ git remote -v
    origin	https://github.com/schacon/ticgit (fetch)
    origin	https://github.com/schacon/ticgit (push)
    me@mypc:~/test/ticgit$ 


## Adding Remote Repositories
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote
    git remote add pb https://github.com/paulboone/ticgit
    git remote -v
    git fetch pb

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ git remote add pb https://github.com/paulboone/ticgit
    me@mypc:~/test/ticgit$ git remote -v
    origin	https://github.com/schacon/ticgit (fetch)
    origin	https://github.com/schacon/ticgit (push)
    pb	https://github.com/paulboone/ticgit (fetch)
    pb	https://github.com/paulboone/ticgit (push)
    me@mypc:~/test/ticgit$ git fetch pb
    remote: Enumerating objects: 22, done.
    remote: Counting objects: 100% (22/22), done.
    remote: Total 43 (delta 22), reused 22 (delta 22), pack-reused 21
    Unpacking objects: 100% (43/43), done.
    From https://github.com/paulboone/ticgit
     * [new branch]      master     -> pb/master
     * [new branch]      ticgit     -> pb/ticgit
    me@mypc:~/test/ticgit$ 


## Fetching and Pulling from Your Remotes

    git fetch <remote>

> The command goes out to that remote project and pulls down all the data from that remote project that you don’t have yet. After you do this, you should have references to all the branches from that remote, which you can merge in or inspect at any time.


> If you clone a repository, the command automatically adds that remote repository under the name “origin”. 

`git clone` 自动添加的 remote repository 名为 origin


> It’s important to note that the `git fetch` command only downloads the data to your local repository — it doesn’t automatically merge it with any of your work or modify what you’re currently working on. You have to merge it manually into your work when you’re ready.


> If your current branch is set up to track a remote branch (see the next section and Git Branching for more information), you can use the `git pull` command to automatically fetch and then merge that remote branch into your current branch.

如果当前 local branch 设置为 track a remote branch ，则可以用 `git pull` 命令自动做 fetch + merge


> by default, the `git clone` command automatically sets up your local master branch to track the remote master branch (or whatever the default branch is called) on the server you cloned from. Running `git pull` generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.

默认， `git clone` 自动设置本地 master branch track 服务器(remote)上的 master branch 。因此执行 `git pull` 会自动做 fetch + merge


## Pushing to Your Remotes
> If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their work first and incorporate it into yours before you’ll be allowed to push.


## Inspecting a Remote
> If you want to see more information about a particular remote, you can use the `git remote show <remote>` command.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    clear

执行

    git remote show origin

**执行结果**

    me@mypc:~/test/ticgit$ git remote show origin
    * remote origin
      Fetch URL: https://github.com/schacon/ticgit
      Push  URL: https://github.com/schacon/ticgit
      HEAD branch: master
      Remote branches:
        master tracked
        ticgit tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/ticgit$ 


## Renaming and Removing Remotes
### `git remote rename`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    git remote add pb https://github.com/paulboone/ticgit
    clear

执行

    git remote
    git remote rename pb paul
    git remote

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    pb
    me@mypc:~/test/ticgit$ git remote rename pb paul
    me@mypc:~/test/ticgit$ git remote
    origin
    paul
    me@mypc:~/test/ticgit$ 


> It’s worth mentioning that this changes all your remote-tracking branch names, too. What used to be referenced at `pb/master` is now at `paul/master`.


## `git remote remove`/`git remote rm`
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git clone https://github.com/schacon/ticgit
    cd ticgit/
    git remote add pb https://github.com/paulboone/ticgit
    clear

执行

    git remote
    git remote remove pb
    git remote

**执行结果**

    me@mypc:~/test/ticgit$ git remote
    origin
    pb
    me@mypc:~/test/ticgit$ git remote remove pb
    me@mypc:~/test/ticgit$ git remote
    origin
    me@mypc:~/test/ticgit$ 


> Once you delete the reference to a remote this way, all remote-tracking branches and configuration settings associated with that remote are also deleted.


# Tagging

- list the available tags
- create new tags
- different types of tags


## Listing Your Tags
Listing the available tags in Git is straightforward. Just type `git tag` (with optional `-l` or `--list`):

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    git tag
    git tag v1.3
    git tag v0.1
    git tag

**执行结果**

    me@mypc:~/test$ git tag
    me@mypc:~/test$ git tag v1.3
    me@mypc:~/test$ git tag v0.1
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    me@mypc:~/test$ 


> This command lists the tags in alphabetical order; the order in which they appear has no real importance.


### `git tag -l`
> You can also search for tags that match a particular pattern.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag
    git tag -l "v1.*"

**执行结果**

    me@mypc:~/test$ git tag
    v0.1
    v1.3
    me@mypc:~/test$ git tag -l "v1.*"
    v1.3
    me@mypc:~/test$ 

> Listing tag wildcards requires `-l` or `--list` option


## Creating Tags
tags types

- lightweight - very much like a branch that doesn't change — it's just a pointer to a specific commit.
- annotated

> Annotated tags, however, are stored as full objects in the Git database. They're checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG).


## Annotated Tags
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag -a v1.4 -m "my version 1.4"
    git tag
    git show v1.4

**执行结果**

    me@mypc:~/test$ git tag -a v1.4 -m "my version 1.4"
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    v1.4
    me@mypc:~/test$ git show v1.4
    tag v1.4
    Tagger: me <me@example.com>
    Date:   Sat Oct 27 13:44:01 2018 +0800

    my version 1.4

    commit 4f4de5f7c7310bf5bcb1b27aea294326292a9af6
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:43:52 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ 


## Lightweight Tags
> Another way to tag commits is with a lightweight tag. This is basically the commit checksum stored in a file — no other information is kept.

lightweight tag 只是个文件，其中只有 commit checksum

> To create a lightweight tag, don’t supply any of the -a, -s, or -m options, just provide a tag name

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v1.3
    clear

执行

    git tag v1.4-lw
    git tag
    git show v1.4-lw
    cat ~/test/.git/refs/tags/v1.4-lw

**执行结果**

    me@mypc:~/test$ git tag v1.4-lw
    me@mypc:~/test$ git tag
    v0.1
    v1.3
    v1.4-lw
    me@mypc:~/test$ git show v1.4-lw
    commit ba60ec05ae84634f29b1b21377780264b0ea6196
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:44:32 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ cat ~/test/.git/refs/tags/v1.4-lw
    ba60ec05ae84634f29b1b21377780264b0ea6196
    me@mypc:~/test$ 


## Tagging Later
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git add .
    git commit -m 'C1'
    git tag v0.2
    clear

执行

    git tag
    git log --pretty=oneline
    git tag -a v0.1 dbae2d -m 'my version 0.1'
    git tag
    git show v0.1

**执行结果**

    me@mypc:~/test$ git tag
    v0.2
    me@mypc:~/test$ git log --pretty=oneline
    13a69c42ece4f5f2010b8d33fac7dd7553af204f C1
    dbae2d40d93156fe731c9f821df985a991c4db1a C0
    me@mypc:~/test$ git tag -a v0.1 dbae2d -m 'my version 0.1'
    me@mypc:~/test$ git tag
    v0.1
    v0.2
    me@mypc:~/test$ git show v0.1
    tag v0.1
    Tagger: me <me@example.com>
    Date:   Sat Oct 27 13:47:39 2018 +0800

    my version 0.1

    commit dbae2d40d93156fe731c9f821df985a991c4db1a
    Author: me <me@example.com>
    Date:   Sat Oct 27 13:47:12 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ 


## Sharing Tags
> By default, the `git push` command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them. This process is just like sharing remote branches — you can run `git push origin <tagname>`.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone ~/test/repo/demo
    cd demo/
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git push origin
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ git push origin v0.1
    Total 0 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new tag]         v0.1 -> v0.1
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    d45f08c3fb1b689f4ae056a8553b949dc51570a2
    me@mypc:~/test/workspace/demo$ 


### `git push origin --tags`
> If you have a lot of tags that you want to push up at once, you can also use the `--tags` option to the `git push` command. This will transfer all of your tags to the remote server that are not already there.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone ~/test/repo/demo
    cd demo
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git tag v0.2
    git push origin
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2
    git push origin --tags
    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2

**执行结果**

    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.2
    cat: /home/me/test/repo/demo/refs/tags/v0.2: No such file or directory
    me@mypc:~/test/workspace/demo$ git push origin --tags
    Total 0 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new tag]         v0.1 -> v0.1
     * [new tag]         v0.2 -> v0.2
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    bf1022a27662771ed32c934c34b2e2abe50d4068
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.2
    bf1022a27662771ed32c934c34b2e2abe50d4068
    me@mypc:~/test/workspace/demo$ 


## Deleting Tags
> In order to update any remotes, you must use `git push <remote> :refs/tags/<tagname>`:

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone ~/test/repo/demo
    cd demo/
    touch README
    git add .
    git commit -m 'C0'
    git tag v0.1
    git push origin v0.1
    clear

执行

    git tag
    git tag -d v0.1
    git tag
    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin :refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

    me@mypc:~/test/workspace/demo$ git tag
    v0.1
    me@mypc:~/test/workspace/demo$ git tag -d v0.1
    Deleted tag 'v0.1' (was f3c3ab0)
    me@mypc:~/test/workspace/demo$ git tag
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    f3c3ab08fb68dea0b18c9f5233bf2f1355be1afe
    me@mypc:~/test/workspace/demo$ git push origin :refs/tags/v0.1
    To /home/me/test/repo/demo
     - [deleted]         v0.1
    me@mypc:~/test/workspace/demo$ cat ~/test/repo/demo/refs/tags/v0.1
    cat: /home/me/test/repo/demo/refs/tags/v0.1: No such file or directory
    me@mypc:~/test/workspace/demo$ 


## Checking out Tags
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'C0' > README
    git add .
    git commit -m 'C0'
    git tag v0.1
    echo 'C1' >> README
    git add .
    git commit -m 'C1'
    git tag v0.2
    clear

执行

    git checkout v0.1
    cat README
    git checkout v0.2
    cat README
    git checkout v0.1
    cat README
    git checkout -b v0.1.1 v0.1
    git branch
    cat README

**执行结果**

    me@mypc:~/test$ git checkout v0.1
    Note: checking out 'v0.1'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b <new-branch-name>

    HEAD is now at 4840396... C0
    me@mypc:~/test$ cat README
    C0
    me@mypc:~/test$ git checkout v0.2
    Previous HEAD position was 4840396... C0
    HEAD is now at 12cbbda... C1
    me@mypc:~/test$ cat README
    C0
    C1
    me@mypc:~/test$ git checkout v0.1
    Previous HEAD position was 12cbbda... C1
    HEAD is now at 4840396... C0
    me@mypc:~/test$ cat README
    C0
    me@mypc:~/test$ git checkout -b v0.1.1 v0.1
    Switched to a new branch 'v0.1.1'
    me@mypc:~/test$ git branch
      master
    * v0.1.1
    me@mypc:~/test$ cat README
    C0
    me@mypc:~/test$ 

> In “detached HEAD” state, if you make changes and then create a commit, the tag will stay the same, but your new commit won’t belong to any branch and will be unreachable, except by the exact commit hash. Thus, if you need to make changes — say you’re fixing a bug on an older version, for instance — you will generally want to create a branch


# Git Aliases
例如

    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status

This means that, for example, instead of typing `git commit`, you just need to type `git ci`

> However, maybe you want to run an external command, rather than a Git subcommand. In that case, you start the command with a `!` character. This is useful if you write your own tools that work with a Git repository. We can demonstrate by aliasing `git visual` to run `gitk`:
> 
>     $ git config --global alias.visual '!gitk'
