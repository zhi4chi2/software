# Branches in a Nutshell
> When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author’s name and email address, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.

commit object 包含

- a pointer to the snapshot of the content you staged(root tree object)
- author's name and email address
- the message that you typed(commit message)
- pointers to the commit or commits that directly came before this commit (its parent or parents)


> Staging the files computes a checksum for each one (the SHA-1 hash we mentioned in Getting Started), stores that version of the file in the Git repository (Git refers to them as blobs), and adds that checksum to the staging area

stage files(git add)会

- computes a checksum for each one
- stores that version of the file in the Git repository(保存 blobs)
- adds that checksum to the staging area(index)


> When you create the commit by running git commit, Git checksums each subdirectory (in this case, just the root project directory) and stores those tree objects in the Git repository. Git then creates a commit object that has the metadata and a pointer to the root project tree so it can re-create that snapshot when needed.

git commit 会

- 计算每个子文件夹的 checksum 在 Git repository 中保存为 tree objects
- 创建 commit object


术语

- blob object - 文件内容实际存放在 blob objects 中
- tree object - lists the contents of the directory and specifies which file names are stored as which blobs
- commit object - with the pointer to that root tree and all the commit metadata

tree object 包含该目录下每个文件的 checksum(指向每个文件的 blob 对象)，并将文件名和 checksum 对应。

tree object 有多个，每个文件夹都有一个 tree object ，最顶级的文件夹对应的 tree object 叫 root tree object


> A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is `master`. As you start making commits, you’re given a `master` branch that points to the last commit you made. Every time you commit, the `master` branch pointer moves forward automatically.

在 Git 中， branch 就是一个可以移动的 pointer ，指向不同的 commit object

每次提交时，都会自动移动 master branch pointer 指向最新的 commit object

> The “master” branch in Git is not a special branch. It is exactly like any other branch. The only reason nearly every repository has one is that the `git init` command creates it by default and most people don’t bother to change it.

参见原文档 Figure 11. A branch and its commit history


## Creating a New Branch
> What happens if you create a new branch? Well, doing so creates a new pointer for you to move around.

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

    cat .git/refs/heads/testing
    git branch testing
    cat .git/refs/heads/testing

**执行结果**

FIXME


> How does Git know what branch you’re currently on? It keeps a special pointer called `HEAD`. Note that this is a lot different than the concept of `HEAD` in other VCSs you may be used to, such as Subversion or CVS. In Git, this is a pointer to the local branch you’re currently on. 

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

    cat .git/HEAD
    cat .git/refs/heads/master

**执行结果**

FIXME


> The `git branch` command only created a new branch — it didn’t switch to that branch.

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

    git branch testing
    git log --oneline --decorate
    cat .git/HEAD

**执行结果**

FIXME


## Switching Branches
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

    git branch testing
    cat .git/HEAD
    cat .git/refs/heads/master
    cat .git/refs/heads/testing
    git checkout testing
    cat .git/HEAD
    cat .git/refs/heads/master
    cat .git/refs/heads/testing
    echo 'made a change' >> README
    git commit -a -m 'made a change'
    git checkout master
    cat .git/HEAD
    cat .git/refs/heads/master
    cat .git/refs/heads/testing
    cat README
    echo 'made other changes' >> README
    git commit -a -m 'made other changes'
    git log --oneline --decorate --graph --all

**执行结果**

FIXME

> Because a branch in Git is actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. Creating a new branch is as quick and simple as writing 41 bytes to a file (40 characters and a newline).

> because we’re recording the parents when we commit, finding a proper merge base for merging is automatically done for us and is generally very easy to do.


# Basic Branching and Merging
## Basic Branching
## Basic Merging
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'C0'
    echo 'modify Readme' >> README
    git commit -a -m 'C1'
    echo '<html>' > index.html
    git add .
    git commit -m 'C2'
    clear

执行

    git checkout -b iss53
    echo '# modify something' >> README
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo '</html>' >> index.html
    git commit -a -m 'C4'
    git log --oneline --graph --all
    git checkout master
    git merge hotfix
    git log --oneline --graph --all
    git branch -d hotfix
    git checkout iss53
    echo 'modified' >> README
    git commit -a -m 'C5'
    git log --oneline --graph --all
    git checkout master
    git merge iss53 -m 'C6'
    git log --oneline --graph --all
    git branch -d iss53

**执行结果**

FIXME


`git checkout -b` 是 shorthand for: `git branch iss53; git checkout iss53`

> Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.

在 C6 时， Git 自动创建了一个 merge commit


## Basic Merge Conflicts
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'C0'
    echo 'modify Readme' >> README
    git commit -a -m 'C1'
    echo '<html>' > index.html
    git add .
    git commit -m 'C2'
    clear

执行

    git checkout -b iss53
    echo '<body>' >> index.html
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo '</html>' >> index.html
    git commit -a -m 'C4'
    git checkout master
    git merge hotfix
    git branch -d hotfix
    git checkout iss53
    echo '</body>' >> index.html
    git commit -a -m 'C5'
    git checkout master
    git merge iss53 -m 'C6'
    git status
    cat index.html

**执行结果**

FIXME


> Git hasn’t automatically created a new merge commit. It has paused the process while you resolve the conflict.

> Anything that has merge conflicts and hasn’t been resolved is listed as unmerged. Git adds standard conflict-resolution markers to the files that have conflicts, so you can open them manually and resolve those conflicts.

> This means the version in `HEAD` (your `master` branch, because that was what you had checked out when you ran your merge command) is the top part of that block (everything above the `=======`), while the version in your `iss53` branch looks like everything in the bottom part.

> In order to resolve the conflict, you have to either choose one side or the other or merge the contents yourself.

> After you’ve resolved each of these sections in each conflicted file, run `git add` on each file to mark it as resolved. Staging the file marks it as resolved in Git.

手动修改 index.html (`vim index.html`)后，执行

    git add index.html
    git status
    git commit -m 'C6'
    git log --oneline --graph --all

**执行结果**

FIXME


### `git mergetool`
> If you want to use a graphical tool to resolve these issues, you can run `git mergetool`, which fires up an appropriate visual merge tool and walks you through the conflicts

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'C0'
    echo 'modify Readme' >> README
    git commit -a -m 'C1'
    echo '<html>' > index.html
    git add .
    git commit -m 'C2'
    clear

执行

    git checkout -b iss53
    echo '<body>' >> index.html
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo '</html>' >> index.html
    git commit -a -m 'C4'
    git checkout master
    git merge hotfix
    git branch -d hotfix
    git checkout iss53
    echo '</body>' >> index.html
    git commit -a -m 'C5'
    git checkout master
    git merge iss53 -m 'C6'
    git status
    cat index.html
    git mergetool index.html

**执行结果**

FIXME


`git mergetool` 修改保存之后，不需要如手动修改时再执行 `git add index.html` 。

然后执行

    rm index.html.orig
    git status
    git commit -m 'C6'
    git log --oneline --graph --all

**执行结果**

FIXME


# Branch Management
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b iss53
    echo '<html>' > index.html
    echo '</html>' >> index.html
    git add .
    git commit -m 'fix javascript issue'
    git checkout master
    echo 'modify Readme' >> README
    git commit -a -m 'modify Readme'
    git merge iss53 -m "Merge branch 'iss53'"
    git checkout -b testing
    echo 'add scott to the author list in the readmes' >> README
    git commit -a -m 'add scott to the author list in the readmes'
    git checkout master
    clear

执行

    git branch
    git branch -v
    git branch --merged
    git branch --no-merged
    git branch -d testing

**执行结果**

FIXME

> Notice the `*` character that prefixes the `master` branch: it indicates the branch that you currently have checked out (i.e., the branch that `HEAD` points to). This means that if you commit at this point, the `master` branch will be moved forward with your new work.

> To see the last commit on each branch, you can run `git branch -v`

> To see which branches are already merged into the branch you’re on, you can run `git branch --merged`

> Branches on this list without the `*` in front of them are generally fine to delete with `git branch -d`; you’ve already incorporated their work into another branch, so you’re not going to lose anything.

> To see all the branches that contain work you haven’t yet merged in, you can run `git branch --no-merged`

> Because it contains work that isn’t merged in yet, trying to delete it with `git branch -d` will fail

> You can always provide an additional argument to ask about the merge state with respect to some other branch without checking that other branch out first, as in, what is not merged into the `master` branch?

执行

    git checkout iss53
    git branch --no-merged master

**执行结果**

FIXME


# Branching Workflows
common workflows(branching scheme)

- Long-Running Branches - 在很长一段时间里，从一个分支多次 merge 到另一个分支。前一个分支(develop / next)用于开发，后一个分支(master)用于发布
- Topic Branches - topic branch is a short-lived branch that you create and use for a single particular feature or related work


## Long-Running Branches
> you can have several branches that are always open and that you use for different stages of your development cycle; you can merge regularly from some of them into others.

> having only code that is entirely stable in their master branch — possibly only code that has been or will be released

> have another parallel branch named develop or next that they work from or use to test stability — it isn’t necessarily always stable, but whenever it gets to a stable state, it can be merged into master. It’s used to pull in topic branches (short-lived branches, like your earlier iss53 branch) when they’re ready, to make sure they pass all the tests and don’t introduce bugs.

有至少两个 branch

- master - 通过测试的代码
- develop or next - 从 topic branches 中 pull 代码，测试，当测试通过时， merge into master

master 和 develop or next 分支实际是在一个 commit line 中， merge 时会是 Fast-forward

develop or next 和 topic branches 可能需要 three-way merge

> You can keep doing this for several levels of stability. Some larger projects also have a `proposed` or `pu` (proposed updates) branch that has integrated branches that may not be ready to go into the `next` or `master` branch.

除了 master 和 develop or next 之外，还可以有其它分支，以提供 several levels of stability 。比如 proposed or pu 分支

> The idea is that your branches are at various levels of stability; when they reach a more stable level, they’re merged into the branch above them.


## Topic Branches
> You can keep the changes there for minutes, days, or months, and merge them in when they’re ready, regardless of the order in which they were created or worked on.


# Remote Branches
术语

- remote references - references (pointers) in your remote repositories, including branches, tags, and so on.
- remote-tracking branches - references to the state of remote branches. They’re local references that you can’t move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository. 例如 `origin/master`
- origin - does not have any special meaning, “origin” is the default name for a remote when you run `git clone`. If you run `git clone -o booyah` instead, then you will have `booyah/master` as your default remote branch.
- tracking branch - local branches that have a direct relationship to a remote branch. If you’re on a tracking branch and type `git pull`, Git automatically knows which server to fetch from and which branch to merge in.
- upstream branch - Checking out a local branch from a remote-tracking branch automatically creates what is called a “tracking branch” (and the branch it tracks is called an “upstream branch”).


> You can get a full list of remote references explicitly with `git ls-remote [remote]`, or `git remote show [remote]` for remote branches as well as more information.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git ls-remote origin
    git remote show origin

**执行结果**

FIXME


> Remote-tracking branches are references to the state of remote branches. They’re local references that you can’t move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository. Think of them as bookmarks, to remind you where the branches in your remote repositories were the last time you connected to them.

> Remote-tracking branches take the form `<remote>/<branch>`. For instance, if you wanted to see what the `master` branch on your `origin` remote looked like as of the last time you communicated with it, you would check the `origin/master` branch.


> “origin” is the default name for a remote when you run `git clone`. If you run `git clone -o booyah` instead, then you will have `booyah/master` as your default remote branch.

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
    git clone -o booyah ~/test/repo/demo
    cd demo
    clear

执行

    git remote

**执行结果**

FIXME


## Pushing
> Your local branches aren’t automatically synchronized to the remotes you write to — you have to explicitly push the branches you want to share.


> This is a bit of a shortcut. Git automatically expands the `serverfix` branchname out to `refs/heads/serverfix:refs/heads/serverfix`, which means, “Take my serverfix local branch and push it to update the remote’s serverfix branch.”

> You can also do `git push origin serverfix:serverfix`, which does the same thing — it says, “Take my serverfix and make it the remote’s serverfix.” You can use this format to push a local branch into a remote branch that is named differently. If you didn’t want it to be called `serverfix` on the remote, you could instead run `git push origin serverfix:awesomebranch` to push your local `serverfix` branch to the `awesomebranch` branch on the remote project.


### `git push origin serverfix`
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
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix
    git remote show origin

**执行结果**

FIXME


### `git push origin refs/heads/serverfix:refs/heads/serverfix`
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
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    clear

执行

    git push origin refs/heads/serverfix:refs/heads/serverfix
    git remote show origin

**执行结果**

FIXME


### `git push origin serverfix:serverfix`
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
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix:serverfix
    git remote show origin

**执行结果**

FIXME


### `git push origin serverfix:awesomebranch`
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
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix:awesomebranch
    git remote show origin

**执行结果**

FIXME


### `git checkout -b`
> It’s important to note that when you do a fetch that brings down new remote-tracking branches, you don’t automatically have local, editable copies of them. In other words, in this case, you don’t have a new `serverfix` branch — you only have an `origin/serverfix` pointer that you can’t modify.

> If you want your own `serverfix` branch that you can work on, you can base it off your remote-tracking branch:

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git fetch origin
    git branch -vv
    git remote show origin
    git checkout -b serverfix origin/serverfix
    git branch -vv
    git remote show origin

**执行结果**

FIXME


## Tracking Branches
> Checking out a local branch from a remote-tracking branch automatically creates what is called a “tracking branch” (and the branch it tracks is called an “upstream branch”). Tracking branches are local branches that have a direct relationship to a remote branch. If you’re on a tracking branch and type `git pull`, Git automatically knows which server to fetch from and which branch to merge in.

> When you clone a repository, it generally automatically creates a `master` branch that tracks `origin/master`.


### `git checkout --track`
> This is a common enough operation that Git provides the `--track` shorthand

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch -vv
    git remote show origin
    git checkout --track origin/serverfix
    git branch -vv
    git remote show origin

**执行结果**

FIXME


### `git checkout`
> this is so common that there’s even a shortcut for that shortcut. If the branch name you’re trying to checkout (a) doesn’t exist and (b) exactly matches a name on only one remote, Git will create a tracking branch for you:

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch -vv
    git remote show origin
    git checkout serverfix
    git branch -vv
    git remote show origin

**执行结果**

FIXME


### `git checkout -b`
> To set up a local branch with a different name than the remote branch, you can easily use the first version with a different local branch name

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch -vv
    git remote show origin
    git checkout -b sf origin/serverfix
    git branch -vv
    git remote show origin
    git push origin

**执行结果**

FIXME


### `git branch -u`
> If you already have a local branch and want to set it to a remote branch you just pulled down, or want to change the upstream branch you’re tracking, you can use the `-u` or `--set-upstream-to` option to `git branch` to explicitly set it at any time.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git checkout -b my-serverfix
    git branch -u origin/serverfix
    git remote show origin
    git branch -vv
    git pull

**执行结果**

FIXME


### `git merge @{u}`
> When you have a tracking branch set up, you can reference its upstream branch with the `@{upstream}` or `@{u}` shorthand. So if you’re on the `master` branch and it’s tracking `origin/master`, you can say something like `git merge @{u}` instead of `git merge origin/master` if you wish.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git checkout -b my-serverfix
    git branch -u origin/serverfix
    git merge @{u}

**执行结果**

FIXME


### `git branch -vv`
> If you want to see what tracking branches you have set up, you can use the `-vv` option to `git branch`. This will list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both.

> It’s important to note that these numbers are only since the last time you fetched from each server. This command does not reach out to the servers, it’s telling you about what it has cached from these servers locally. If you want totally up to date ahead and behind numbers, you’ll need to fetch from all your remotes right before running this.


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch -vv
    cd ~/test/worker1/demo
    git merge serverfix
    git push origin
    cd ~/test/worker2/demo
    git branch -vv
    git fetch --all
    git branch -vv

**执行结果**

FIXME


## Pulling
> While the `git fetch` command will fetch down all the changes on the server that you don’t have yet, it will not modify your working directory at all. It will simply get the data for you and let you merge it yourself. However, there is a command called `git pull` which is essentially a `git fetch` immediately followed by a `git merge` in most cases.

> If you have a tracking branch set up as demonstrated in the last section, either by explicitly setting it or by having it created for you by the `clone` or `checkout` commands, `git pull` will look up what server and branch your current branch is tracking, fetch from that server and then try to merge in that remote branch.

> Generally it’s better to simply use the `fetch` and `merge` commands explicitly as the magic of `git pull` can often be confusing.


## Deleting Remote Branches
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    clear

执行

    git branch --all
    git remote show origin
    git push origin --delete serverfix
    git branch --all
    git remote show origin

**执行结果**

FIXME


如果 Remote Branches 在本地有 tracking branch, `git push origin --delete` 会导致状态不一致！

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo/demo
    cd ~/test/repo/demo
    git init --bare
    cd ~/test
    mkdir worker1
    cd worker1/
    git clone ~/test/repo/demo
    cd demo
    echo 'My Project' > README
    git add .
    git commit -m 'Initial Commit'
    git checkout -b serverfix
    echo '<html>' > index.html
    git add .
    git commit -m 'add index.html'
    git checkout master
    git push origin
    git push origin serverfix
    cd ~/test
    mkdir worker2
    cd worker2/
    git clone ~/test/repo/demo
    cd demo
    git checkout -b serverfix origin/serverfix
    git checkout master
    clear

执行

    git branch --all
    git remote show origin
    git branch -vv
    git push origin --delete serverfix
    git branch --all
    git remote show origin
    git branch -vv

**执行结果**

FIXME

`git remote show origin` 中还显示 `serverfix merges with remote serverfix`

`git branch -vv` 中显示 `origin/serverfix: gone`

在 `git push origin --delete serverfix` 之前先执行 `git branch -d serverfix` 即可


# Rebasing
## The Basic Rebase
> It works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.

> rebasing makes for a cleaner history. If you examine the log of a rebased branch, it looks like a linear history: it appears that all the work happened in series, even when it originally happened in parallel.


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'C0'
    echo 'modify Readme' >> README
    git commit -a -m 'C1'
    echo '<html>' > index.html
    git add .
    git commit -m 'C2'
    git branch experiment
    echo '# modify something' >> README
    git commit -a -m 'C3'
    git checkout experiment
    echo '</html>' >> index.html
    git commit -a -m 'C4'
    clear

执行

    git log --oneline --graph --all
    git rebase master
    git log --oneline --graph --all
    git checkout master
    git merge experiment
    git log --oneline --graph --all

**执行结果**

FIXME


如果 rebase 分支上有多个 commit ：

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    git add .
    git commit -m 'C0'
    echo 'modify Readme' >> README
    git commit -a -m 'C1'
    echo '<html>' > index.html
    git add .
    git commit -m 'C2'
    git branch experiment
    echo '# modify something' >> README
    git commit -a -m 'C3'
    git checkout experiment
    echo '<body></body>' >> index.html
    git commit -a -m 'C4'
    echo '</html>' >> index.html
    git commit -a -m 'C5'
    clear

执行

    git log --oneline --graph --all
    git rebase master
    git log --oneline --graph --all
    git checkout master
    git merge experiment
    git log --oneline --graph --all

**执行结果**

FIXME


> Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.


## More Interesting Rebases
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    echo '# server' > server
    echo '# client' > client
    git add .
    git commit -m 'C1'
    echo '# in C2' >> README
    git commit -a -m 'C2'
    git checkout -b server
    echo '# in C3' >> server
    git commit -a -m 'C3'
    git branch client
    echo '# in C4' >> server
    git commit -a -m 'C4'
    git checkout master
    echo '# In C5' >> README
    git commit -a -m 'C5'
    echo '# In C6' >> README
    git commit -a -m 'C6'
    git checkout client
    echo '# In C8' >> client
    git commit -a -m 'C8'
    echo '# In C9' >> client
    git commit -a -m 'C9'
    git checkout server
    echo '# In C10' >> server
    git commit -a -m 'C10'
    git checkout client
    clear

执行

    git log --oneline --graph --all
    git rebase --onto master server client
    git log --oneline --graph --all
    git checkout master
    git merge client
    git log --oneline --graph --all
    git rebase master server
    git log --oneline --graph --all
    git checkout master
    git merge server
    git log --oneline --graph --all

**执行结果**

FIXME


> You can rebase the server branch onto the `master` branch without having to check it out first by running `git rebase <basebranch> <topicbranch>` — which checks out the topic branch (in this case, `server`) for you and replays it onto the base branch (`master`):

在 master branch 上执行 `git rebase master server` 会自动 checkout 到 server branch


但这种方式很容易 rebase conflict

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    echo 'My Project' > README
    echo '# server' > server
    git add .
    git commit -m 'C1'
    echo '# in C2' >> README
    git commit -a -m 'C2'
    git checkout -b server
    echo '# in C3' >> server
    echo '# client' > client
    git add .
    git commit -a -m 'C3'
    git branch client
    echo '# in C4' >> server
    git commit -a -m 'C4'
    git checkout master
    echo '# In C5' >> README
    git commit -a -m 'C5'
    echo '# In C6' >> README
    git commit -a -m 'C6'
    git checkout client
    echo '# In C8' >> client
    git commit -a -m 'C8'
    echo '# In C9' >> client
    git commit -a -m 'C9'
    git checkout server
    echo '# In C10' >> server
    git commit -a -m 'C10'
    git checkout client
    clear

执行

    git log --oneline --graph --all
    git rebase --onto master server client
    git status

**执行结果**

FIXME


## The Perils of Rebasing
> Do not rebase commits that exist outside your repository

> When you rebase stuff, you’re abandoning existing commits and creating new ones that are similar but different. If you push commits somewhere and others pull them down and base work on them, and then you rewrite those commits with `git rebase` and push them up again, your collaborators will have to re-merge their work and things will get messy when you try to pull their work back into yours.


## Rebase When You Rebase
FIXME


## Rebase vs. Merge
> In general the way to get the best of both worlds is to rebase local changes you’ve made but haven’t shared yet before you push them in order to clean up your story, but never rebase anything you’ve pushed somewhere.

