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
    git clone https://github.com/zhi4chi2/demo
    ls -aF
    cd demo
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo
    Cloning into 'demo'...
    remote: Enumerating objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  demo/
    me@mypc:~/test$ cd demo
    me@mypc:~/test/demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/demo$ 

clone 到了 `/home/me/test/demo` 目录下（自动创建此目录），库在 `/home/me/test/demo/.git`


GitHub 的 git clone url 可以加 .git 也可以省略。


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    clear

执行

    ls -aF
    git clone https://github.com/zhi4chi2/demo.git my-demo
    ls -aF
    cd my-demo
    ls -aF

**执行结果**

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo.git my-demo
    Cloning into 'my-demo'...
    remote: Enumerating objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  my-demo/
    me@mypc:~/test$ cd my-demo
    me@mypc:~/test/my-demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/my-demo$ 

除了 https:// 协议外还可以使用 git:// 或者使用 SSH 传输协议（例如 `user@server:path/to/repo.git` ）。


# Recording Changes to the Repository
working directory 中文件的状态(<https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository>)

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


## Staging Modified Files
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'Initial CONTRIBUTING.md' > CONTRIBUTING.md
    git add CONTRIBUTING.md
    git commit -m 'Initial Commit'
    echo 'My Project' > README
    git add README
    echo '# first time modified' >> CONTRIBUTING.md
    clear

执行

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

    me@mypc:~/test$ 

执行

    echo '# second time modified' >> CONTRIBUTING.md
    git status

**执行结果**

    me@mypc:~/test$ echo '# second time modified' >> CONTRIBUTING.md
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

    me@mypc:~/test$ 

执行

    git add CONTRIBUTING.md
    git status

**执行结果**

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
    echo 'My Project' > README
    echo 'Initial Rakefile' > Rakefile
    mkdir lib
    touch lib/simplegit.rb
    git add .
    git commit -m 'Initial Commit'
    echo '# first time modified' >> Rakefile
    echo '# modified' >> lib/simplegit.rb
    touch lib/git.rb
    git add .
    echo '# first time modified' >> README
    echo '# second time modified' >> Rakefile
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
    echo 'Initial CONTRIBUTING.md' > CONTRIBUTING.md
    git add .
    git commit -m 'Initial Commit'
    echo 'My Project' > README
    git add README
    echo '# first time modified CONTRIBUTING.md' >> CONTRIBUTING.md
    echo 'modify something in CONTRIBUTING.md' >> CONTRIBUTING.md
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
    index 2d02d7c..a907480 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1 +1,3 @@
     Initial CONTRIBUTING.md
    +# first time modified CONTRIBUTING.md
    +modify something in CONTRIBUTING.md
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
    index 0000000..56266d3
    --- /dev/null
    +++ b/README
    @@ -0,0 +1 @@
    +My Project
    me@mypc:~/test$ 

执行

    git add CONTRIBUTING.md
    echo '# test line' >> CONTRIBUTING.md
    git status
    git diff
    git diff --staged

**执行结果**

    me@mypc:~/test$ git add CONTRIBUTING.md
    me@mypc:~/test$ echo '# test line' >> CONTRIBUTING.md
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

    me@mypc:~/test$ git diff
    diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
    index a907480..6321bd6 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1,3 +1,4 @@
     Initial CONTRIBUTING.md
     # first time modified CONTRIBUTING.md
     modify something in CONTRIBUTING.md
    +# test line
    me@mypc:~/test$ git diff --cached
    diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
    index 2d02d7c..a907480 100644
    --- a/CONTRIBUTING.md
    +++ b/CONTRIBUTING.md
    @@ -1 +1,3 @@
     Initial CONTRIBUTING.md
    +# first time modified CONTRIBUTING.md
    +modify something in CONTRIBUTING.md
    diff --git a/README b/README
    new file mode 100644
    index 0000000..56266d3
    --- /dev/null
    +++ b/README
    @@ -0,0 +1 @@
    +My Project
    me@mypc:~/test$ 


> There is another way to look at these diffs if you prefer a graphical or external diff viewing program instead. If you run `git difftool` instead of `git diff`, you can view any of these diffs in software like emerge, vimdiff and many more (including commercial products). Run `git difftool --tool-help` to see what is available on your system.


### git difftool
执行

    git difftool

**执行结果**

    me@mypc:~/test$ git difftool

    This message is displayed because 'diff.tool' is not configured.
    See 'git difftool --tool-help' or 'git help config' for more details.
    'git difftool' will now attempt to use one of the following tools:
    meld opendiff kdiff3 tkdiff xxdiff kompare gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare emerge vimdiff

    Viewing (1/1): 'CONTRIBUTING.md'
    Launch 'gvimdiff' [Y/n]: y
    2 files to edit

    (gvim:8235): GLib-GObject-WARNING **: cannot retrieve class for invalid (unclassed) type '<invalid>'
    me@mypc:~/test$ 


### `git difftool --tool-help`
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

FIXME

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
    echo 'Initial CONTRIBUTING.md' > CONTRIBUTING.md
    git add .
    git commit -m 'Initial Commit'
    echo 'My Project' > README
    echo '# first time modified CONTRIBUTING.md' >> CONTRIBUTING.md
    echo 'modify something in CONTRIBUTING.md' >> CONTRIBUTING.md
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

> For an even more explicit reminder of what you’ve modified, you can pass the -v option to `git commit`. Doing so also puts the diff of your change in the editor so you can see exactly what changes you’re committing.


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
     13 index 2d02d7c..a907480 100644
     14 --- a/CONTRIBUTING.md
     15 +++ b/CONTRIBUTING.md
     16 @@ -1 +1,3 @@
     17  Initial CONTRIBUTING.md
     18 +# first time modified CONTRIBUTING.md
     19 +modify something in CONTRIBUTING.md
     20 diff --git a/README b/README
     21 new file mode 100644
     22 index 0000000..56266d3
     23 --- /dev/null
     24 +++ b/README
     25 @@ -0,0 +1 @@
     26 +My Project
    ~                                                                               
    ~                                                                               
    ~                                                                               
    "~/test/.git/COMMIT_EDITMSG" 26L, 719C                        1,0-1         All

执行

    git commit -m 'modified CONTRIBUTING.md, add README'

**执行结果**

    me@mypc:~/test$ git commit -m 'modified CONTRIBUTING.md, add README'
    [master d6d6248] modified CONTRIBUTING.md, add README
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
    echo 'Initial CONTRIBUTING.md' > CONTRIBUTING.md
    git add .
    git commit -m 'Initial Commit'
    echo 'My Project' > README
    echo '# first time modified CONTRIBUTING.md' >> CONTRIBUTING.md
    echo 'modify something in CONTRIBUTING.md' >> CONTRIBUTING.md
    clear

执行

    git status
    git commit -a -m 'modified CONTRIBUTING.md'
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
    me@mypc:~/test$ git commit -a -m 'modified CONTRIBUTING.md'
    [master 4f47390] modified CONTRIBUTING.md
     1 file changed, 2 insertions(+)
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
    echo 'My Project' > PROJECTS.md
    git add .
    git commit -m 'Initial Commit'
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
    echo 'My Project' > PROJECTS.md
    git add .
    git commit -m 'Initial Commit'
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


> If you modified the file and added it to the staging area already, you must force the removal with the `-f` option. This is a safety feature to prevent accidental removal of data that hasn’t yet been recorded in a snapshot and that can’t be recovered from Git.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > PROJECTS.md
    git add .
    git commit -m 'Initial Commit'
    echo 'modified something' >> PROJECTS.md
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


> Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore` file and accidentally staged it, like a large log file or a bunch of `.a` compiled files. To do this, use the `--cached` option

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
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


## Moving Files
> Unlike many other VCS systems, Git doesn’t explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. However, Git is pretty smart about figuring that out after the fact


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README.md
    git add .
    git commit -m 'Initial Commit'
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
    echo 'My Project' > README.md
    git add .
    git commit -m 'Initial Commit'
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



# 撤消操作
注意，有些撤消操作是不可逆的。这是在使用 Git 的过程中，会因为操作失误而导致之前的工作丢失的少有的几个地方之一。


参见 [git commit](/Software/Git/commit.md), [git reset](/Software/Git/reset.md), [git checkout](/Software/Git/checkout.md)


# Working with Remotes
参见 [git remote](/Software/Git/remote.md), [git fetch](/Software/Git/fetch.md), [git push](/Software/Git/push.md), [git pull](/Software/Git/pull.md)


# Tagging
参见 [git tag](/Software/Git/tag.md), [git show](/Software/Git/show.md), [git push](/Software/Git/push.md), [git checkout](/Software/Git/checkout.md)


# Git Aliases
参见 [git config](/Software/Git/config.md)

