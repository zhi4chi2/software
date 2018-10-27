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

**执行结果**

FIXME

会报错


添加 `git add index.html` 之后：

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

FIXME


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

FIXME


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

    git stash pop --index
    git status
    git stash list

**执行结果**

FIXME


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

FIXME


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

FIXME


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

FIXME


# Cleaning your Working Directory
FIXME

