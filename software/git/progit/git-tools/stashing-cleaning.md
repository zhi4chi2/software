> Stashing takes the dirty state of your working directory — that is, your modified tracked files and staged changes — and saves it on a stack of unfinished changes that you can reapply at any time (even on a different branch).

> As of late October 2017, there has been extensive discussion on the Git mailing list, wherein the command `git stash save` is being deprecated in favour of the existing alternative `git stash push`. The main reason for this is that `git stash push` introduces the option of stashing selected *pathspecs*, something `git stash save` does not support.

# Stashing Your Work
> Having a clean working directory and applying it on the same branch aren’t necessary to successfully apply a stash. You can save a stash on one branch, switch to another branch later, and try to reapply the changes. You can also have modified and uncommitted files in your working directory when you apply a stash — Git gives you merge conflicts if anything no longer applies cleanly.


预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    clear

执行

    git status
    git stash
    git status
    git checkout -b testing
    echo 'something' >> index.html
    git stash list
    git stash apply
    cat index.html

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash
    Saved working directory and index state WIP on master: ad8b108 C0
    HEAD is now at ad8b108 C0
    me@mypc:~/test$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ git checkout -b testing
    Switched to a new branch 'testing'
    me@mypc:~/test$ echo 'something' >> index.html
    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: ad8b108 C0
    me@mypc:~/test$ git stash apply
    error: Your local changes to the following files would be overwritten by merge:
	    index.html
    Please, commit your changes or stash them before you can merge.
    Aborting
    me@mypc:~/test$ cat index.html
    something
    me@mypc:~/test$ 

会报错 `Your local changes to the following files would be overwritten by merge`

在 `git stash apply` 前添加 `git add index.html` 之后就不报错了！而是自动 merge 然后出现 merge conflict

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    clear

执行

    git status
    git stash
    git status
    git checkout -b testing
    echo 'something' >> index.html
    git add index.html
    git stash list
    git stash apply
    git status
    cat index.html
    git add index.html
    git status

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash
    Saved working directory and index state WIP on master: 358b15d C0
    HEAD is now at 358b15d C0
    me@mypc:~/test$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ git checkout -b testing
    Switched to a new branch 'testing'
    me@mypc:~/test$ echo 'something' >> index.html
    me@mypc:~/test$ git add index.html
    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: 358b15d C0
    me@mypc:~/test$ git stash apply
    Auto-merging index.html
    CONFLICT (content): Merge conflict in index.html
    me@mypc:~/test$ git status
    On branch testing
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   lib/simplegit.rb

    Unmerged paths:
      (use "git reset HEAD <file>..." to unstage)
      (use "git add <file>..." to mark resolution)

	    both modified:   index.html

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ cat index.html
    <<<<<<< Updated upstream
    something
    =======
    C1
    >>>>>>> Stashed changes
    me@mypc:~/test$ git add index.html
    me@mypc:~/test$ git status
    On branch testing
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html
	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ 


> you must run the `git stash apply` command with a `--index` option to tell the command to try to reapply the staged changes.

> The apply option only tries to apply the stashed work — you continue to have it on your stack. To remove it, you can run `git stash drop` with the name of the stash to remove

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    git stash
    clear

执行

    git stash apply --index
    git status
    git stash list
    git stash drop
    git stash list

**执行结果**

    me@mypc:~/test$ git stash apply --index
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: c01d8d7 C0
    me@mypc:~/test$ git stash drop
    Dropped refs/stash@{0} (b4016c68df8f4bcb02e983356d8bf8cba745337d)
    me@mypc:~/test$ git stash list
    me@mypc:~/test$ 


> You can also run `git stash pop` to apply the stash and then immediately drop it from your stack.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    git stash
    clear

执行

    git status
    git stash pop --index
    git status
    git stash list

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    nothing added to commit but untracked files present (use "git add" to track)
    me@mypc:~/test$ git stash pop --index
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    Dropped refs/stash@{0} (101a17b86144b219e4743b58d5ec15c8e818e58d)
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash list
    me@mypc:~/test$ 


# Creative Stashing
> `--keep-index` option to the `stash save` command. This tells Git to not only include all staged content in the stash being created, but simultaneously leave it in the index.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    clear

执行

    git status
    git stash --keep-index
    git status
    git stash list

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash --keep-index
    Saved working directory and index state WIP on master: 0360549 C0
    HEAD is now at 0360549 C0
    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: 0360549 C0
    me@mypc:~/test$ 


> By default, `git stash` will stash only modified and staged tracked files. If you specify `--include-untracked` or `-u`, Git will include untracked files in the stash being created.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    clear

执行

    git status
    git stash -u
    git status
    git stash list

**执行结果**

    me@mypc:~/test$ git status
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

	    README

    me@mypc:~/test$ git stash -u
    Saved working directory and index state WIP on master: 153e196 C0
    HEAD is now at 153e196 C0
    me@mypc:~/test$ git status
    On branch master
    nothing to commit, working directory clean
    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: 153e196 C0
    me@mypc:~/test$ 


> if you specify the `--patch` flag, Git will not stash everything that is modified but will instead prompt you interactively which of the changes you would like to stash and which you would like to keep in your working directory.

FIXME


# Creating a Branch from a Stash
> If you stash some work, leave it there for a while, and continue on the branch from which you stashed the work, you may have a problem reapplying the work. If the apply tries to modify a file that you’ve since modified, you’ll get a merge conflict and will have to try to resolve it. If you want an easier way to test the stashed changes again, you can run `git stash branch <branch>`, which creates a new branch for you with your selected branch name, checks out the commit you were on when you stashed your work, reapplies your work there, and then drops the stash if it applies successfully

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    mkdir lib
    touch index.html
    touch lib/simplegit.rb
    git add .
    git commit -m 'C0'
    echo 'C1' >> index.html
    git add index.html
    echo 'C1' >> lib/simplegit.rb
    echo 'C1' > README
    git stash
    git add README
    git commit -m 'C1'
    clear

执行

    git log -2
    git status
    git stash list
    git stash branch testchanges
    git status
    git stash list
    git log -1
    ls README

**执行结果**

    me@mypc:~/test$ git log -2
    commit 9df902a04f490a20d985616436c6ea5dc37afd92
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:57:29 2018 +0800

        C1

    commit 024222a6bdfe764ed1340fb0f7fc3f722adcf4cb
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:57:29 2018 +0800

        C0
    me@mypc:~/test$ git status
    On branch master
    nothing to commit, working directory clean
    me@mypc:~/test$ git stash list
    stash@{0}: WIP on master: 024222a C0
    me@mypc:~/test$ git stash branch testchanges
    Switched to a new branch 'testchanges'
    On branch testchanges
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    Dropped refs/stash@{0} (e6e38b59d0e6c863a31960f37287a3f1f72b5340)
    me@mypc:~/test$ git status
    On branch testchanges
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

	    modified:   index.html

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

	    modified:   lib/simplegit.rb

    me@mypc:~/test$ git stash list
    me@mypc:~/test$ git log -1
    commit 024222a6bdfe764ed1340fb0f7fc3f722adcf4cb
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:57:29 2018 +0800

        C0
    me@mypc:~/test$ ls README
    ls: cannot access 'README': No such file or directory
    me@mypc:~/test$ 


# Cleaning your Working Directory
FIXME

