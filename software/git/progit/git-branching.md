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
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    cat .git/refs/heads/testing
    git branch testing
    cat .git/refs/heads/testing

**执行结果**

    me@mypc:~/test$ cat .git/refs/heads/testing
    cat: .git/refs/heads/testing: No such file or directory
    me@mypc:~/test$ git branch testing
    me@mypc:~/test$ cat .git/refs/heads/testing
    a4724f7eb944c53f6401ae8e686b6210c1790b5c
    me@mypc:~/test$ 


> How does Git know what branch you’re currently on? It keeps a special pointer called `HEAD`. Note that this is a lot different than the concept of `HEAD` in other VCSs you may be used to, such as Subversion or CVS. In Git, this is a pointer to the local branch you’re currently on. 

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

    cat .git/HEAD
    cat .git/refs/heads/master

**执行结果**

    me@mypc:~/test$ cat .git/HEAD
    ref: refs/heads/master
    me@mypc:~/test$ cat .git/refs/heads/master
    d76330fe23a5e7d1592a84d143a3c2c0dae524e4
    me@mypc:~/test$ 


> The `git branch` command only created a new branch — it didn’t switch to that branch.

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

    git branch testing
    git log --oneline --decorate
    cat .git/HEAD

**执行结果**

    me@mypc:~/test$ git branch testing
    me@mypc:~/test$ git log --oneline --decorate
    86ac077 (HEAD -> master, testing) C0
    me@mypc:~/test$ cat .git/HEAD
    ref: refs/heads/master
    me@mypc:~/test$ 


## Switching Branches
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

    me@mypc:~/test$ git branch testing
    me@mypc:~/test$ cat .git/HEAD
    ref: refs/heads/master
    me@mypc:~/test$ cat .git/refs/heads/master
    0e6e227d7f465c0d20c593455e4346af76272ede
    me@mypc:~/test$ cat .git/refs/heads/testing
    0e6e227d7f465c0d20c593455e4346af76272ede
    me@mypc:~/test$ git checkout testing
    Switched to branch 'testing'
    me@mypc:~/test$ cat .git/HEAD
    ref: refs/heads/testing
    me@mypc:~/test$ cat .git/refs/heads/master
    0e6e227d7f465c0d20c593455e4346af76272ede
    me@mypc:~/test$ cat .git/refs/heads/testing
    0e6e227d7f465c0d20c593455e4346af76272ede
    me@mypc:~/test$ echo 'made a change' >> README
    me@mypc:~/test$ git commit -a -m 'made a change'
    [testing e4468a7] made a change
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ cat .git/HEAD
    ref: refs/heads/master
    me@mypc:~/test$ cat .git/refs/heads/master
    0e6e227d7f465c0d20c593455e4346af76272ede
    me@mypc:~/test$ cat .git/refs/heads/testing
    e4468a72ce9c238cbc0da161a318a5a59baddcfe
    me@mypc:~/test$ cat README
    me@mypc:~/test$ echo 'made other changes' >> README
    me@mypc:~/test$ git commit -a -m 'made other changes'
    [master ebcedcc] made other changes
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * ebcedcc (HEAD -> master) made other changes
    | * e4468a7 (testing) made a change
    |/  
    * 0e6e227 C0
    me@mypc:~/test$ 

> Because a branch in Git is actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. Creating a new branch is as quick and simple as writing 41 bytes to a file (40 characters and a newline).

> because we’re recording the parents when we commit, finding a proper merge base for merging is automatically done for us and is generally very easy to do.


# Basic Branching and Merging
## Basic Branching
> However, before you do that, note that if your working directory or staging area has uncommitted changes that conflict with the branch you’re checking out, Git won’t let you switch branches. It’s best to have a clean working state when you switch branches. There are ways to get around this (namely, stashing and commit amending) that we’ll cover later on

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git branch testing
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout testing
    echo 'something' >> README
    clear

执行

    git checkout master
    git status

**执行结果**

    me@mypc:~/test$ git checkout master
    error: Your local changes to the following files would be overwritten by checkout:
	    README
    Please, commit your changes or stash them before you can switch branches.
    Aborting
    me@mypc:~/test$ git status
    On branch testing
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   README

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ 

如果去掉 `echo 'C1' >> README`, `git commit -a -m 'C1'` 两行，则不再出错

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    git add .
    git commit -m 'C0'
    git branch testing
    git checkout testing
    echo 'something' >> README
    clear

执行

    git checkout master
    cat README

**执行结果**

    me@mypc:~/test$ git checkout master
    M	README
    Switched to branch 'master'
    me@mypc:~/test$ cat README
    something
    me@mypc:~/test$ 

这时虽然可以切换到 master 分支，但 README 的修改从 testing 分支移到 master 分支了。


## Basic Merging
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch index.html
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    echo 'C2' >> index.html
    git commit -a -m 'C2'
    clear

执行

    git checkout -b iss53
    echo 'C3' >> README
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo 'C4' >> index.html
    git commit -a -m 'C4'
    git log --oneline --decorate --graph --all
    git checkout master
    git merge hotfix
    git log --oneline --decorate --graph --all
    git branch -d hotfix
    git checkout iss53
    echo 'C5' >> README
    git commit -a -m 'C5'
    git log --oneline --decorate --graph --all
    git checkout master
    git merge iss53 -m 'C6'
    git log --oneline --decorate --graph --all
    git branch -d iss53

**执行结果**

    me@mypc:~/test$ git checkout -b iss53
    Switched to a new branch 'iss53'
    me@mypc:~/test$ echo 'C3' >> README
    me@mypc:~/test$ git commit -a -m 'C3'
    [iss53 20c7467] C3
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git checkout -b hotfix
    Switched to a new branch 'hotfix'
    me@mypc:~/test$ echo 'C4' >> index.html
    me@mypc:~/test$ git commit -a -m 'C4'
    [hotfix 63c9829] C4
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 63c9829 (HEAD -> hotfix) C4
    | * 20c7467 (iss53) C3
    |/  
    * 3193942 (master) C2
    * aa369f8 C1
    * 1bc22f8 C0
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge hotfix
    Updating 3193942..63c9829
    Fast-forward
     index.html | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 63c9829 (HEAD -> master, hotfix) C4
    | * 20c7467 (iss53) C3
    |/  
    * 3193942 C2
    * aa369f8 C1
    * 1bc22f8 C0
    me@mypc:~/test$ git branch -d hotfix
    Deleted branch hotfix (was 63c9829).
    me@mypc:~/test$ git checkout iss53
    Switched to branch 'iss53'
    me@mypc:~/test$ echo 'C5' >> README
    me@mypc:~/test$ git commit -a -m 'C5'
    [iss53 8cac3db] C5
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 8cac3db (HEAD -> iss53) C5
    * 20c7467 C3
    | * 63c9829 (master) C4
    |/  
    * 3193942 C2
    * aa369f8 C1
    * 1bc22f8 C0
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge iss53 -m 'C6'
    Merge made by the 'recursive' strategy.
     README | 2 ++
     1 file changed, 2 insertions(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    *   9d2a775 (HEAD -> master) C6
    |\  
    | * 8cac3db (iss53) C5
    | * 20c7467 C3
    * | 63c9829 C4
    |/  
    * 3193942 C2
    * aa369f8 C1
    * 1bc22f8 C0
    me@mypc:~/test$ git branch -d iss53
    Deleted branch iss53 (was 8cac3db).
    me@mypc:~/test$ 

`git checkout -b iss53` 是 shorthand for: `git branch iss53; git checkout iss53`

> Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.

在 C6 时， Git 自动创建了一个 merge commit


## Basic Merge Conflicts
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch index.html
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git commit -a -m 'C1'
    echo 'C2' >> index.html
    git commit -a -m 'C2'
    clear

执行

    git checkout -b iss53
    echo 'C3' >> index.html
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo 'C4' >> index.html
    git commit -a -m 'C4'
    git checkout master
    git merge hotfix
    git branch -d hotfix
    git checkout iss53
    echo 'C5' >> index.html
    git commit -a -m 'C5'
    cat index.html
    git checkout master
    cat index.html
    git merge iss53 -m 'C6'
    git status
    cat index.html

**执行结果**

    me@mypc:~/test$ git checkout -b iss53
    Switched to a new branch 'iss53'
    me@mypc:~/test$ echo 'C3' >> index.html
    me@mypc:~/test$ git commit -a -m 'C3'
    [iss53 e3890f6] C3
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git checkout -b hotfix
    Switched to a new branch 'hotfix'
    me@mypc:~/test$ echo 'C4' >> index.html
    me@mypc:~/test$ git commit -a -m 'C4'
    [hotfix b587e33] C4
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge hotfix
    Updating 104bc9d..b587e33
    Fast-forward
     index.html | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git branch -d hotfix
    Deleted branch hotfix (was b587e33).
    me@mypc:~/test$ git checkout iss53
    Switched to branch 'iss53'
    me@mypc:~/test$ echo 'C5' >> index.html
    me@mypc:~/test$ git commit -a -m 'C5'
    [iss53 f381948] C5
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ cat index.html
    C1
    C2
    C3
    C5
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ cat index.html
    C1
    C2
    C4
    me@mypc:~/test$ git merge iss53 -m 'C6'
    Auto-merging index.html
    CONFLICT (content): Merge conflict in index.html
    Automatic merge failed; fix conflicts and then commit the result.
    me@mypc:~/test$ git status
    On branch master
    You have unmerged paths.
      (fix conflicts and run "git commit")

    Unmerged paths:
      (use "git add <file>..." to mark resolution)

	    both modified:   index.html

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ cat index.html
    C1
    C2
    <<<<<<< HEAD
    C4
    =======
    C3
    C5
    >>>>>>> iss53
    me@mypc:~/test$ 


> Git hasn’t automatically created a new merge commit. It has paused the process while you resolve the conflict.

> Anything that has merge conflicts and hasn’t been resolved is listed as unmerged. Git adds standard conflict-resolution markers to the files that have conflicts, so you can open them manually and resolve those conflicts.

> This means the version in `HEAD` (your `master` branch, because that was what you had checked out when you ran your merge command) is the top part of that block (everything above the `=======`), while the version in your `iss53` branch looks like everything in the bottom part.

> In order to resolve the conflict, you have to either choose one side or the other or merge the contents yourself.

> After you’ve resolved each of these sections in each conflicted file, run `git add` on each file to mark it as resolved. Staging the file marks it as resolved in Git.

手动修改 index.html (`vim index.html`)后，执行

    git add index.html
    git status
    git commit -m 'C6'
    git log --oneline --decorate --graph --all

**执行结果**

    me@mypc:~/test$ git add index.html
    me@mypc:~/test$ git status
    On branch master
    All conflicts fixed but you are still merging.
      (use "git commit" to conclude merge)

    Changes to be committed:

	    modified:   index.html

    me@mypc:~/test$ git commit -m 'C6'
    [master 74a21d9] C6
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    *   74a21d9 (HEAD -> master) C6
    |\  
    | * f381948 (iss53) C5
    | * e3890f6 C3
    * | b587e33 C4
    |/  
    * 104bc9d C2
    * 6fc51ca C1
    * 24eed27 C0
    me@mypc:~/test$ 


### `git mergetool`
> If you want to use a graphical tool to resolve these issues, you can run `git mergetool`, which fires up an appropriate visual merge tool and walks you through the conflicts

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch index.html
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git commit -a -m 'C1'
    echo 'C2' >> index.html
    git commit -a -m 'C2'
    clear

执行

    git checkout -b iss53
    echo 'C3' >> index.html
    git commit -a -m 'C3'
    git checkout master
    git checkout -b hotfix
    echo 'C4' >> index.html
    git commit -a -m 'C4'
    git checkout master
    git merge hotfix
    git branch -d hotfix
    git checkout iss53
    echo 'C5' >> index.html
    git commit -a -m 'C5'
    cat index.html
    git checkout master
    cat index.html
    git merge iss53 -m 'C6'
    git status
    cat index.html
    git mergetool index.html

**执行结果**

    me@mypc:~/test$ git checkout -b iss53
    Switched to a new branch 'iss53'
    me@mypc:~/test$ echo 'C3' >> index.html
    me@mypc:~/test$ git commit -a -m 'C3'
    [iss53 a728105] C3
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git checkout -b hotfix
    Switched to a new branch 'hotfix'
    me@mypc:~/test$ echo 'C4' >> index.html
    me@mypc:~/test$ git commit -a -m 'C4'
    [hotfix 63b042f] C4
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge hotfix
    Updating ba0845c..63b042f
    Fast-forward
     index.html | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git branch -d hotfix
    Deleted branch hotfix (was 63b042f).
    me@mypc:~/test$ git checkout iss53
    Switched to branch 'iss53'
    me@mypc:~/test$ echo 'C5' >> index.html
    me@mypc:~/test$ git commit -a -m 'C5'
    [iss53 4303113] C5
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ cat index.html
    C1
    C2
    C3
    C5
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ cat index.html
    C1
    C2
    C4
    me@mypc:~/test$ git merge iss53 -m 'C6'
    Auto-merging index.html
    CONFLICT (content): Merge conflict in index.html
    Automatic merge failed; fix conflicts and then commit the result.
    me@mypc:~/test$ git status
    On branch master
    You have unmerged paths.
      (fix conflicts and run "git commit")

    Unmerged paths:
      (use "git add <file>..." to mark resolution)

	    both modified:   index.html

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ cat index.html
    C1
    C2
    <<<<<<< HEAD
    C4
    =======
    C3
    C5
    >>>>>>> iss53
    me@mypc:~/test$ git mergetool index.html

    This message is displayed because 'merge.tool' is not configured.
    See 'git mergetool --tool-help' or 'git help config' for more details.
    'git mergetool' will now attempt to use one of the following tools:
    meld opendiff kdiff3 tkdiff xxdiff tortoisemerge gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare emerge vimdiff
    Merging:
    index.html

    Normal merge conflict for 'index.html':
      {local}: modified file
      {remote}: modified file
    Hit return to start merge resolution tool (gvimdiff): 
    4 files to edit

    (gvim:6103): GLib-GObject-WARNING **: cannot retrieve class for invalid (unclassed) type '<invalid>'
    me@mypc:~/test$ 

`git mergetool` 修改保存之后，不需要如手动修改时再执行 `git add index.html` 。

然后执行

    rm index.html.orig
    git status
    git commit -m 'C6'
    git log --oneline --decorate --graph --all

**执行结果**

    me@mypc:~/test$ rm index.html.orig
    me@mypc:~/test$ git status
    On branch master
    All conflicts fixed but you are still merging.
      (use "git commit" to conclude merge)

    Changes to be committed:

	    modified:   index.html

    me@mypc:~/test$ git commit -m 'C6'
    [master 2d2a405] C6
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    *   2d2a405 (HEAD -> master) C6
    |\  
    | * 4303113 (iss53) C5
    | * a728105 C3
    * | 63b042f C4
    |/  
    * ba0845c C2
    * db65aaa C1
    * a279eb6 C0
    me@mypc:~/test$ 


# Branch Management
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch index.html
    git add .
    git commit -m 'C0'
    git checkout -b iss53
    echo 'C1' >> index.html
    git commit -a -m 'fix javascript issue'
    git checkout master
    echo 'C2' >> README
    git commit -a -m 'C2'
    git merge iss53 -m "Merge branch 'iss53'"
    git checkout -b testing
    echo 'C4' >> README
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

    me@mypc:~/test$ git branch
      iss53
    * master
      testing
    me@mypc:~/test$ git branch -v
      iss53   0c9bd56 fix javascript issue
    * master  d5d4327 Merge branch 'iss53'
      testing f6a52e6 add scott to the author list in the readmes
    me@mypc:~/test$ git branch --merged
      iss53
    * master
    me@mypc:~/test$ git branch --no-merged
      testing
    me@mypc:~/test$ git branch -d testing
    error: The branch 'testing' is not fully merged.
    If you are sure you want to delete it, run 'git branch -D testing'.
    me@mypc:~/test$ 

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

    me@mypc:~/test$ git checkout iss53
    Switched to branch 'iss53'
    me@mypc:~/test$ git branch --no-merged master
      testing
    me@mypc:~/test$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git ls-remote origin
    68b61778550f92895d4e44d189f9453d72b1fba7	HEAD
    68b61778550f92895d4e44d189f9453d72b1fba7	refs/heads/master
    49e1239fdb7da68f80e5d50681fd5f9a6d49cc2f	refs/heads/serverfix
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ 


> Remote-tracking branches are references to the state of remote branches. They’re local references that you can’t move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository. Think of them as bookmarks, to remind you where the branches in your remote repositories were the last time you connected to them.

> Remote-tracking branches take the form `<remote>/<branch>`. For instance, if you wanted to see what the `master` branch on your `origin` remote looked like as of the last time you communicated with it, you would check the `origin/master` branch.

## `git clone -o`
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

    me@mypc:~/test/workspace/demo$ git remote
    booyah
    me@mypc:~/test/workspace/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix
    git remote show origin

**执行结果**

    me@mypc:~/test/workspace/demo$ git push origin serverfix
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 225 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new branch]      serverfix -> serverfix
    me@mypc:~/test/workspace/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/workspace/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout master
    git push origin
    clear

执行

    git push origin refs/heads/serverfix:refs/heads/serverfix
    git remote show origin

**执行结果**

    me@mypc:~/test/workspace/demo$ git push origin refs/heads/serverfix:refs/heads/serverfix
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 225 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new branch]      serverfix -> serverfix
    me@mypc:~/test/workspace/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/workspace/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix:serverfix
    git remote show origin

**执行结果**

    me@mypc:~/test/workspace/demo$ git push origin serverfix:serverfix
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 224 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new branch]      serverfix -> serverfix
    me@mypc:~/test/workspace/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/workspace/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
    git checkout master
    git push origin
    clear

执行

    git push origin serverfix:awesomebranch
    git remote show origin

**执行结果**

    me@mypc:~/test/workspace/demo$ git push origin serverfix:awesomebranch
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 224 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
     * [new branch]      serverfix -> awesomebranch
    me@mypc:~/test/workspace/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        awesomebranch tracked
        master        tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/workspace/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git fetch origin
    me@mypc:~/test/worker2/demo$ git branch -vv
    * master a3000ec [origin/master] C0
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git checkout -b serverfix origin/serverfix
    Branch serverfix set up to track remote branch serverfix from origin.
    Switched to a new branch 'serverfix'
    me@mypc:~/test/worker2/demo$ git branch -vv
      master    a3000ec [origin/master] C0
    * serverfix 6f3ef14 [origin/serverfix] C1
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master    merges with remote master
        serverfix merges with remote serverfix
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch -vv
    * master 05fe296 [origin/master] C0
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git checkout --track origin/serverfix
    Branch serverfix set up to track remote branch serverfix from origin.
    Switched to a new branch 'serverfix'
    me@mypc:~/test/worker2/demo$ git branch -vv
      master    05fe296 [origin/master] C0
    * serverfix db226a9 [origin/serverfix] C1
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master    merges with remote master
        serverfix merges with remote serverfix
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch -vv
    * master 61a07b0 [origin/master] C0
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git checkout serverfix
    Branch serverfix set up to track remote branch serverfix from origin.
    Switched to a new branch 'serverfix'
    me@mypc:~/test/worker2/demo$ git branch -vv
      master    61a07b0 [origin/master] C0
    * serverfix 4c21fd3 [origin/serverfix] C1
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master    merges with remote master
        serverfix merges with remote serverfix
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch -vv
    * master 04fb0c4 [origin/master] C0
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git checkout -b sf origin/serverfix
    Branch sf set up to track remote branch serverfix from origin.
    Switched to a new branch 'sf'
    me@mypc:~/test/worker2/demo$ git branch -vv
      master 04fb0c4 [origin/master] C0
    * sf     47758a7 [origin/serverfix] C1
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master merges with remote master
        sf     merges with remote serverfix
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git push origin
    fatal: The upstream branch of your current branch does not match
    the name of your current branch.  To push to the upstream branch
    on the remote, use

        git push origin HEAD:serverfix

    To push to the branch of the same name on the remote, use

        git push origin sf

    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git checkout -b my-serverfix
    Switched to a new branch 'my-serverfix'
    me@mypc:~/test/worker2/demo$ git branch -u origin/serverfix
    Branch my-serverfix set up to track remote branch serverfix from origin.
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master       merges with remote master
        my-serverfix merges with remote serverfix
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git branch -vv
      master       4c0e39e [origin/master] C0
    * my-serverfix 4c0e39e [origin/serverfix: behind 1] C0
    me@mypc:~/test/worker2/demo$ git pull
    Updating 4c0e39e..a8db7ae
    Fast-forward
     README | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git checkout -b my-serverfix
    Switched to a new branch 'my-serverfix'
    me@mypc:~/test/worker2/demo$ git branch -u origin/serverfix
    Branch my-serverfix set up to track remote branch serverfix from origin.
    me@mypc:~/test/worker2/demo$ git merge @{u}
    Updating 7f58230..b78659e
    Fast-forward
     README | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch -vv
    * master b522c65 [origin/master] C0
    me@mypc:~/test/worker2/demo$ cd ~/test/worker1/demo
    me@mypc:~/test/worker1/demo$ git merge serverfix
    Updating b522c65..ac8cfaf
    Fast-forward
     README | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test/worker1/demo$ git push origin
    Total 0 (delta 0), reused 0 (delta 0)
    To /home/me/test/repo/demo
       b522c65..ac8cfaf  master -> master
    me@mypc:~/test/worker1/demo$ cd ~/test/worker2/demo
    me@mypc:~/test/worker2/demo$ git branch -vv
    * master b522c65 [origin/master] C0
    me@mypc:~/test/worker2/demo$ git fetch --all
    Fetching origin
    From /home/me/test/repo/demo
       b522c65..ac8cfaf  master     -> origin/master
    me@mypc:~/test/worker2/demo$ git branch -vv
    * master b522c65 [origin/master: behind 1] C0
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch --all
    * master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
      remotes/origin/serverfix
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git push origin --delete serverfix
    To /home/me/test/repo/demo
     - [deleted]         serverfix
    me@mypc:~/test/worker2/demo$ git branch --all
    * master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branch:
        master tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ 


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
    touch README
    git add .
    git commit -m 'C0'
    git checkout -b serverfix
    echo 'C1' >> README
    git commit -a -m 'C1'
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

    me@mypc:~/test/worker2/demo$ git branch --all
    * master
      serverfix
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
      remotes/origin/serverfix
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branches:
        master    tracked
        serverfix tracked
      Local branches configured for 'git pull':
        master    merges with remote master
        serverfix merges with remote serverfix
      Local refs configured for 'git push':
        master    pushes to master    (up to date)
        serverfix pushes to serverfix (up to date)
    me@mypc:~/test/worker2/demo$ git branch -vv
    * master    4adf702 [origin/master] C0
      serverfix c6d789c [origin/serverfix] C1
    me@mypc:~/test/worker2/demo$ git push origin --delete serverfix
    To /home/me/test/repo/demo
     - [deleted]         serverfix
    me@mypc:~/test/worker2/demo$ git branch --all
    * master
      serverfix
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    me@mypc:~/test/worker2/demo$ git remote show origin
    * remote origin
      Fetch URL: /home/me/test/repo/demo
      Push  URL: /home/me/test/repo/demo
      HEAD branch: master
      Remote branch:
        master tracked
      Local branches configured for 'git pull':
        master    merges with remote master
        serverfix merges with remote serverfix
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/worker2/demo$ git branch -vv
    * master    4adf702 [origin/master] C0
      serverfix c6d789c [origin/serverfix: gone] C1
    me@mypc:~/test/worker2/demo$ 

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
    touch README
    touch index.html
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    echo 'C2' >> index.html
    git commit -a -m 'C2'
    git branch experiment
    echo 'C3' >> README
    git commit -a -m 'C3'
    git checkout experiment
    echo 'C4' >> index.html
    git commit -a -m 'C4'
    clear

执行

    git log --oneline --decorate --graph --all
    git rebase master
    git log --oneline --decorate --graph --all
    git checkout master
    git merge experiment
    git log --oneline --decorate --graph --all

**执行结果**

    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 55609d7 (HEAD -> experiment) C4
    | * 2dd430c (master) C3
    |/  
    * fc962d0 C2
    * e7cdfe4 C1
    * 4971b97 C0
    me@mypc:~/test$ git rebase master
    First, rewinding head to replay your work on top of it...
    Applying: C4
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * a0bc37d (HEAD -> experiment) C4
    * 2dd430c (master) C3
    * fc962d0 C2
    * e7cdfe4 C1
    * 4971b97 C0
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge experiment
    Updating 2dd430c..a0bc37d
    Fast-forward
     index.html | 1 +
     1 file changed, 1 insertion(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * a0bc37d (HEAD -> master, experiment) C4
    * 2dd430c C3
    * fc962d0 C2
    * e7cdfe4 C1
    * 4971b97 C0
    me@mypc:~/test$ 


如果 rebase 分支上有多个 commit ：

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch index.html
    git add .
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    echo 'C2' >> index.html
    git commit -a -m 'C2'
    git branch experiment
    echo 'C3' >> README
    git commit -a -m 'C3'
    git checkout experiment
    echo 'C4' >> index.html
    git commit -a -m 'C4'
    echo 'C5' >> index.html
    git commit -a -m 'C5'
    clear

执行

    git log --oneline --decorate --graph --all
    git rebase master
    git log --oneline --decorate --graph --all
    git checkout master
    git merge experiment
    git log --oneline --decorate --graph --all

**执行结果**

    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 7846636 (HEAD -> experiment) C5
    * c08ba88 C4
    | * f26a02d (master) C3
    |/  
    * e510b0a C2
    * 89b4c9f C1
    * 516c07c C0
    me@mypc:~/test$ git rebase master
    First, rewinding head to replay your work on top of it...
    Applying: C4
    Applying: C5
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * a6552fb (HEAD -> experiment) C5
    * 7434e0f C4
    * f26a02d (master) C3
    * e510b0a C2
    * 89b4c9f C1
    * 516c07c C0
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge experiment
    Updating f26a02d..a6552fb
    Fast-forward
     index.html | 2 ++
     1 file changed, 2 insertions(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * a6552fb (HEAD -> master, experiment) C5
    * 7434e0f C4
    * f26a02d C3
    * e510b0a C2
    * 89b4c9f C1
    * 516c07c C0
    me@mypc:~/test$ 

> Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.


## More Interesting Rebases
预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch server
    touch client
    git add .
    git commit -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    git checkout -b server
    echo 'C3' >> server
    git commit -a -m 'C3'
    git branch client
    echo 'C4' >> server
    git commit -a -m 'C4'
    git checkout master
    echo 'C5' >> README
    git commit -a -m 'C5'
    echo 'C6' >> README
    git commit -a -m 'C6'
    git checkout client
    echo 'C8' >> client
    git commit -a -m 'C8'
    echo 'C9' >> client
    git commit -a -m 'C9'
    git checkout server
    echo 'C10' >> server
    git commit -a -m 'C10'
    git checkout client
    clear

执行

    git log --oneline --decorate --graph --all
    git rebase --onto master server client
    git log --oneline --decorate --graph --all
    git checkout master
    git merge client
    git log --oneline --decorate --graph --all
    git rebase master server
    git log --oneline --decorate --graph --all
    git checkout master
    git merge server
    git log --oneline --decorate --graph --all

**执行结果**

    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * cb8b852 (HEAD -> client) C9
    * 574dd7e C8
    | * ebed4c4 (master) C6
    | * 7979d29 C5
    | | * 2f98eb4 (server) C10
    | | * 3042c33 C4
    | |/  
    |/|   
    * | 852ab3c C3
    |/  
    * 17cd724 C2
    * c9a2d61 C1
    me@mypc:~/test$ git rebase --onto master server client
    First, rewinding head to replay your work on top of it...
    Applying: C8
    Applying: C9
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 1fe9488 (HEAD -> client) C9
    * f0d5f81 C8
    * ebed4c4 (master) C6
    * 7979d29 C5
    | * 2f98eb4 (server) C10
    | * 3042c33 C4
    | * 852ab3c C3
    |/  
    * 17cd724 C2
    * c9a2d61 C1
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge client
    Updating ebed4c4..1fe9488
    Fast-forward
     client | 2 ++
     1 file changed, 2 insertions(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * 1fe9488 (HEAD -> master, client) C9
    * f0d5f81 C8
    * ebed4c4 C6
    * 7979d29 C5
    | * 2f98eb4 (server) C10
    | * 3042c33 C4
    | * 852ab3c C3
    |/  
    * 17cd724 C2
    * c9a2d61 C1
    me@mypc:~/test$ git rebase master server
    First, rewinding head to replay your work on top of it...
    Applying: C3
    Applying: C4
    Applying: C10
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * d44ad96 (HEAD -> server) C10
    * 93400f0 C4
    * beec306 C3
    * 1fe9488 (master, client) C9
    * f0d5f81 C8
    * ebed4c4 C6
    * 7979d29 C5
    * 17cd724 C2
    * c9a2d61 C1
    me@mypc:~/test$ git checkout master
    Switched to branch 'master'
    me@mypc:~/test$ git merge server
    Updating 1fe9488..d44ad96
    Fast-forward
     server | 3 +++
     1 file changed, 3 insertions(+)
    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * d44ad96 (HEAD -> master, server) C10
    * 93400f0 C4
    * beec306 C3
    * 1fe9488 (client) C9
    * f0d5f81 C8
    * ebed4c4 C6
    * 7979d29 C5
    * 17cd724 C2
    * c9a2d61 C1
    me@mypc:~/test$ 

> You can rebase the server branch onto the `master` branch without having to check it out first by running `git rebase <basebranch> <topicbranch>` — which checks out the topic branch (in this case, `server`) for you and replays it onto the base branch (`master`):

在 master branch 上执行 `git rebase master server` 会自动 checkout 到 server branch


但这种方式很容易 rebase conflict

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    touch README
    touch server
    git add .
    git commit -m 'C1'
    echo 'C2' >> README
    git commit -a -m 'C2'
    git checkout -b server
    echo 'C3' >> server
    touch client
    git add .
    git commit -a -m 'C3'
    git branch client
    echo 'C4' >> server
    git commit -a -m 'C4'
    git checkout master
    echo 'C5' >> README
    git commit -a -m 'C5'
    echo 'C6' >> README
    git commit -a -m 'C6'
    git checkout client
    echo 'C8' >> client
    git commit -a -m 'C8'
    echo 'C9' >> client
    git commit -a -m 'C9'
    git checkout server
    echo 'C10' >> server
    git commit -a -m 'C10'
    git checkout client
    clear

执行

    git log --oneline --decorate --graph --all
    git rebase --onto master server client
    git status

**执行结果**

    me@mypc:~/test$ git log --oneline --decorate --graph --all
    * bc48051 (HEAD -> client) C9
    * e25dba5 C8
    | * bb3b03e (master) C6
    | * fe2b9e4 C5
    | | * 6eaadc3 (server) C10
    | | * 60cbaaa C4
    | |/  
    |/|   
    * | 3d139c3 C3
    |/  
    * 2d0ec03 C2
    * 4ab99eb C1
    me@mypc:~/test$ git rebase --onto master server client
    First, rewinding head to replay your work on top of it...
    Applying: C8
    Using index info to reconstruct a base tree...
    A	client
    Falling back to patching base and 3-way merge...
    CONFLICT (modify/delete): client deleted in bb3b03e0f7431d8679a9db7882d9b2f1b3abbbec and modified in C8. Version C8 of client left in tree.
    error: Failed to merge in the changes.
    Patch failed at 0001 C8
    The copy of the patch that failed is found in: .git/rebase-apply/patch

    When you have resolved this problem, run "git rebase --continue".
    If you prefer to skip this patch, run "git rebase --skip" instead.
    To check out the original branch and stop rebasing, run "git rebase --abort".

    me@mypc:~/test$ git status
    rebase in progress; onto bb3b03e
    You are currently rebasing branch 'client' on 'bb3b03e'.
      (fix conflicts and then run "git rebase --continue")
      (use "git rebase --skip" to skip this patch)
      (use "git rebase --abort" to check out the original branch)

    Unmerged paths:
      (use "git reset HEAD <file>..." to unstage)
      (use "git add/rm <file>..." as appropriate to mark resolution)

	    deleted by us:   client

    no changes added to commit (use "git add" and/or "git commit -a")
    me@mypc:~/test$ 


## The Perils of Rebasing
> Do not rebase commits that exist outside your repository

> When you rebase stuff, you’re abandoning existing commits and creating new ones that are similar but different. If you push commits somewhere and others pull them down and base work on them, and then you rewrite those commits with `git rebase` and push them up again, your collaborators will have to re-merge their work and things will get messy when you try to pull their work back into yours.


## Rebase When You Rebase
FIXME


## Rebase vs. Merge
> In general the way to get the best of both worlds is to rebase local changes you’ve made but haven’t shared yet before you push them in order to clean up your story, but never rebase anything you’ve pushed somewhere.

