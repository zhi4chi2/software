# Single Revisions
> You can obviously refer to any single commit by its full, 40-character SHA-1 hash


# Short SHA-1
> Git is smart enough to figure out what commit you’re referring to if you provide the first few characters of the SHA-1 hash, as long as that partial hash is at least four characters long and unambiguous; that is, no other object in the object database can have a hash that begins with the same prefix.

至少要 4 个字符

> If you pass `--abbrev-commit` to the `git log` command, the output will use shorter values but keep them unique; it defaults to using seven characters but makes them longer if necessary to keep the SHA-1 unambiguous

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
    git commit -a -m 'C1'
    clear

执行

    git log
    git show f5a3dabe1974c23fe51375db6985fd42539d6807
    git show f5a3dabe1974c23
    git show f5a3
    git log --abbrev-commit --pretty=oneline

**执行结果**

    me@mypc:~/test$ git log
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    commit 8b4f2ec68d38a68dd462be873e1dcef98b337d47
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C0
    me@mypc:~/test$ git show f5a3dabe1974c23fe51375db6985fd42539d6807
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show f5a3dabe1974c23
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show f5a3
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git log --abbrev-commit --pretty=oneline
    f5a3dab C1
    8b4f2ec C0
    me@mypc:~/test$ 

> Generally, eight to ten characters are more than enough to be unique within a project.

> If you do happen to commit an object that hashes to the same SHA-1 value as a previous different object in your repository, Git will see the previous object already in your Git database, assume it was already written and simply reuse it. If you try to check out that object again at some point, you’ll always get the data of the first object.

但这个几率非常小，小到可以忽略不计


# Branch References
> One straightforward way to refer to a particular commit is if it’s the commit at the tip of a branch; in that case, you can simply use the branch name in any Git command that expects a reference to a commit.

> If you want to see which specific SHA-1 a branch points to, or if you want to see what any of these examples boils down to in terms of SHA-1s, you can use a Git plumbing tool called `rev-parse`.

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
    git commit -a -m 'C1'
    clear

执行

    git log -1
    git show c818631a50200a9297a347739f24000fbf9c821b
    git show master
    git rev-parse master

**执行结果**

    me@mypc:~/test$ git log -1
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1
    me@mypc:~/test$ git show c818631a50200a9297a347739f24000fbf9c821b
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show master
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git rev-parse master
    c818631a50200a9297a347739f24000fbf9c821b
    me@mypc:~/test$ 


# RefLog Shortnames
> One of the things Git does in the background while you’re working away is keep a “reflog” — a log of where your HEAD and branch references have been for the last few months.

> Every time your branch tip is updated for any reason, Git stores that information for you in this temporary history. You can use your reflog data to refer to older commits as well.

> You can also use this syntax to see where a branch was some specific amount of time ago.

> This technique only works for data that’s still in your reflog, so you can’t use it to look for commits older than a few months.

> To see reflog information formatted like the `git log` output, you can run `git log -g`

> It’s important to note that reflog information is strictly local — it’s a log only of what you’ve done in your repository. The references won’t be the same on someone else’s copy of the repository; also, right after you initially clone a repository, you’ll have an empty reflog, as no activity has occurred yet in your repository.

> **Think of the reflog as Git’s version of shell history**

> what’s there is clearly relevant only for you and your “session”, and has nothing to do with anyone else who might be working on the same machine.

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
    git commit -a -m 'C1'
    clear

执行

    git reflog
    git show HEAD@{1}
    git show master@{yesterday}
    git show HEAD@{2.months.ago}
    git log -g master

**执行结果**

    me@mypc:~/test$ git reflog
    b63728e HEAD@{0}: commit: C1
    5ddb924 HEAD@{1}: commit (initial): C0
    me@mypc:~/test$ git show HEAD@{1}
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git show master@{yesterday}
    warning: Log for 'master' only goes back to Sat, 27 Oct 2018 14:34:24 +0800.
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git show HEAD@{2.months.ago}
    warning: Log for 'HEAD' only goes back to Sat, 27 Oct 2018 14:34:24 +0800.
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git log -g master
    commit b63728eaf51934e7d1de3b1a82d12f9e2715ba08
    Reflog: master@{0} (me <me@example.com>)
    Reflog message: commit: C1
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C1

    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Reflog: master@{1} (me <me@example.com>)
    Reflog message: commit (initial): C0
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0
    me@mypc:~/test$ 


# Ancestry References
> The other main way to specify a commit is via its ancestry. If you place a `^` (caret) at the end of a reference, Git resolves it to mean the parent of that commit.

> Then, you can see the previous commit by specifying `HEAD^`, which means “the parent of HEAD”:

> On Windows in `cmd.exe`, `^` is a special character and needs to be treated differently. You can either double it or put the commit reference in quotes
>     $ git show HEAD^     # will NOT work on Windows
>     $ git show HEAD^^    # OK
>     $ git show "HEAD^"   # OK

> You can also specify a number after the `^` – for example, `d921970^2` means “the second parent of d921970.” This syntax is useful only for merge commits, which have more than one parent. The first parent is the branch you were on when you merged, and the second is the commit on the branch that you merged in:

> The other main ancestry specification is the `~` (tilde). This also refers to the first parent, so `HEAD~` and `HEAD^` are equivalent. The difference becomes apparent when you specify a number. `HEAD~2` means “the first parent of the first parent,” or “the grandparent” — it traverses the first parents the number of times you specify.

> This can also be written `HEAD~~~`, which again is the first parent of the first parent of the first parent

> You can also combine these syntaxes — you can get the second parent of the previous reference (assuming it was a merge commit) by using `HEAD~3^2`, and so on.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'add open3_detach to gemspec file list'
    echo 'C1' >> README
    git commit -a -m 'ignore *.gem'
    git checkout -b rdocs
    echo 'C2' > rdoc
    git add .
    git commit -m 'Some rdoc changes'
    git checkout master
    echo 'C3' >> README
    git commit -a -m 'added some blame and merge stuff'
    git merge rdocs -m "Merge commit 'phedders/rdocs'"
    echo 'C4' >> README
    git commit -a -m 'fixed refs handling, added gc auto, updated tests'
    clear

执行

    git log --pretty=format:'%h %s' --graph
    git rev-parse HEAD^
    git rev-parse HEAD~3
    git rev-parse HEAD~~~
    git rev-parse HEAD~^2

**执行结果**

    me@mypc:~/test$ git log --pretty=format:'%h %s' --graph
    * 20fccdf fixed refs handling, added gc auto, updated tests
    *   1f767b4 Merge commit 'phedders/rdocs'
    |\  
    | * 226dc8e Some rdoc changes
    * | cf08d76 added some blame and merge stuff
    |/  
    * 562db1c ignore *.gem
    * c0c1a96 add open3_detach to gemspec file list
    me@mypc:~/test$ git rev-parse HEAD^
    1f767b409976e910fb95d50a0853e824623e76c3
    me@mypc:~/test$ git rev-parse HEAD~3
    562db1cd2f325b44646a7d2df4ea1bbeb7499707
    me@mypc:~/test$ git rev-parse HEAD~~~
    562db1cd2f325b44646a7d2df4ea1bbeb7499707
    me@mypc:~/test$ git rev-parse HEAD~^2
    226dc8eb06990e291867a6039aee54437eb09fdc
    me@mypc:~/test$ 


# Commit Ranges
## Double Dot
> `master..experiment` — that means “all commits reachable from experiment that aren’t reachable from master.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'A' > README
    git add .
    git commit -m 'A'
    echo 'B' >> README
    git commit -a -m 'B'
    git checkout -b experiment
    echo 'C' >> README
    git commit -a -m 'C'
    echo 'D' >> README
    git commit -a -m 'D'
    git checkout master
    echo 'E' >> README
    git commit -a -m 'E'
    echo 'F' >> README
    git commit -a -m 'F'
    clear

执行

    git log --oneline --graph --all --decorate
    git log master..experiment
    git log experiment..master

**执行结果**

FIXME

    me@mypc:~/test$ git log --oneline --graph --all
    * 92036ce D
    * 26dfd83 C
    | * 5a43578 F
    | * abfd124 E
    |/  
    * 3443d85 B
    * 93730c2 A
    me@mypc:~/test$ git log master..experiment
    commit 92036ce6ae3a3d7ce6e9a4a4d3517f5deb43336c
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        D

    commit 26dfd83c0ac523ad0669b5db169aa55af3e7152d
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        C
    me@mypc:~/test$ git log experiment..master
    commit 5a43578295bea6e4c6c3f8712ff80fb2ba507197
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        F

    commit abfd1247ba782f79edd51221e8a1e15ef986a3f2
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        E
    me@mypc:~/test$ 


> If you run a `git push` and your current branch is tracking `origin/master`, the commits listed by `git log origin/master..HEAD` are the commits that will be transferred to the server. You can also leave off one side of the syntax to have Git assume `HEAD`. For example, you can get the same results as in the previous example by typing `git log origin/master..` — Git substitutes `HEAD` if one side is missing.


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
    git push origin
    echo 'C1' >> README
    git commit -a -m 'C1'
    clear

执行

    git log --oneline --graph --all --decorate
    git log origin/master..HEAD
    git log origin/master..

**执行结果**

FIXME

    me@mypc:~/test/workspace/demo$ git log --oneline --graph --all
    * 2023e76 C1
    * 715ad3c C0
    me@mypc:~/test/workspace/demo$ git log origin/master..HEAD
    commit 2023e76754c461b166d3a9404417aff4db11c194
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:01 2018 +0800

        C1
    me@mypc:~/test/workspace/demo$ git log origin/master..
    commit 2023e76754c461b166d3a9404417aff4db11c194
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:01 2018 +0800

        C1
    me@mypc:~/test/workspace/demo$ 


## Multiple Points
FIXME


## Triple Dot
> triple-dot syntax, which specifies all the commits that are reachable by either of two references but not by both of them.

> A common switch to use with the `log` command in this case is `--left-right`, which shows you which side of the range each commit is in.


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'A' > README
    git add .
    git commit -m 'A'
    echo 'B' >> README
    git commit -a -m 'B'
    git checkout -b experiment
    echo 'C' >> README
    git commit -a -m 'C'
    echo 'D' >> README
    git commit -a -m 'D'
    git checkout master
    echo 'E' >> README
    git commit -a -m 'E'
    echo 'F' >> README
    git commit -a -m 'F'
    clear

执行

    git log --oneline --graph --all --decorate
    git log master...experiment
    git log --left-right master...experiment

**执行结果**

FIXME

    me@mypc:~/test$ git log --oneline --graph --all
    * 3f4a997 D
    * a34f23d C
    | * 7d30ec3 F
    | * db4577b E
    |/  
    * 1dbda29 B
    * 82cb477 A
    me@mypc:~/test$ git log master...experiment
    commit 7d30ec3a692afdfba5ae0fd3c39c7d9609b611ec
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        F

    commit 3f4a9973314ae872c671f6d80f9d456f9f64efce
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        D

    commit db4577b8791917d059a8ba00b493a77d53e7f7f4
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        E

    commit a34f23d63d16a905139f6434f87c21a8919dc5c3
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        C
    me@mypc:~/test$ git log --left-right master...experiment
    commit < 7d30ec3a692afdfba5ae0fd3c39c7d9609b611ec
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        F

    commit > 3f4a9973314ae872c671f6d80f9d456f9f64efce
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        D

    commit < db4577b8791917d059a8ba00b493a77d53e7f7f4
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        E

    commit > a34f23d63d16a905139f6434f87c21a8919dc5c3
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        C
    me@mypc:~/test$ 


