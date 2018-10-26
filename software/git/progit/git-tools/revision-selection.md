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
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    echo '# modify README' >> README
    git commit -a -m 'modify README'
    clear

执行

    git log
    git show
    git show
    git show
    git log --abbrev-commit --pretty=oneline

**执行结果**

FIXME

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
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    echo '# modify README' >> README
    git commit -a -m 'modify README'
    clear

执行

    git log -1
    git show
    git show master
    git rev-parse master

**执行结果**

FIXME


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
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    echo '# modify README' >> README
    git commit -a -m 'modify README'
    clear

执行

    git reflog
    git show HEAD@{1}
    git show master@{yesterday}
    git show HEAD@{2.months.ago}
    git log -g master

**执行结果**

FIXME


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
    echo 'add open3_detach to gemspec file list' > README
    git add .
    git commit -m 'add open3_detach to gemspec file list'
    echo 'ignore *.gem' >> README
    git commit -a -m 'ignore *.gem'
    git checkout -b rdocs
    echo 'Some rdoc changes' > rdoc
    git add .
    git commit -m 'Some rdoc changes'
    git checkout master
    echo 'added some blame and merge stuff' >> README
    git commit -a -m 'added some blame and merge stuff'
    git merge rdocs -m "Merge commit 'phedders/rdocs'"
    echo 'fixed refs handling, added gc auto, updated tests' >> README
    git commit -a -m 'fixed refs handling, added gc auto, updated tests'
    clear

执行

    git log --pretty=format:'%h %s' --graph
    git show HEAD^
    git show
    git show
    git show HEAD~3
    git show HEAD~~~
    git show HEAD~^2

**执行结果**

FIXME


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
    echo 'C' > experiment
    git add .
    git commit -m 'C'
    echo 'D' >> experiment
    git commit -a -m 'D'
    git checkout master
    echo 'E' >> README
    git commit -a -m 'E'
    echo 'F' >> README
    git commit -a -m 'F'
    clear

执行

    git log --oneline --graph --all
    git log master..experiment
    git log experiment..master


**执行结果**

FIXME


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
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git push origin
    echo 'modify README' >> README
    git commit -a -m 'modify README'
    clear

执行

    git log --oneline --graph --all
    git log origin/master..HEAD
    git log origin/master..

**执行结果**

FIXME


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
    echo 'C' > experiment
    git add .
    git commit -m 'C'
    echo 'D' >> experiment
    git commit -a -m 'D'
    git checkout master
    echo 'E' >> README
    git commit -a -m 'E'
    echo 'F' >> README
    git commit -a -m 'F'
    clear

执行

    git log --oneline --graph --all
    git log master...experiment
    git log --left-right master...experiment

**执行结果**

FIXME

