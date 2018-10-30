术语

- repository - remote, destination of a push operation, either a URL or the name of a remote
- refspec - specify what destination ref to update with what source object

refspec 的格式：

    +<src>:<dst>

其中

- \+
- src - often the name of the branch, but it can be any arbitrary "SHA-1 expression", such as `master~4` or `HEAD`
- dst


# Synopsis


# Description


# Options
## repository
> When the command line does not specify where to push with the `<repository>` argument, `branch.*.remote` configuration for the current branch is consulted to determine where to push. If the configuration is missing, it defaults to `origin`.

预处理

    cd
    rm -rf test
    mkdir test
    cd test/
    mkdir -p repo1/demo
    cd ~/test/repo1/demo
    git init --bare
    cd ~/test
    mkdir repo2
    cp -r repo1/demo repo2
    cd ~/test
    mkdir workspace
    cd workspace/
    git clone -o repo1 ~/test/repo1/demo
    cd demo/
    git remote add repo2 ~/test/repo2/demo
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    git config branch.master.remote
    git push
    git config branch.master.remote repo2
    git push

**执行结果**

FIXME


## refspec
### 默认值
> When the command line does not specify what to push with `<refspec>...` arguments or `--all`, `--mirror`, `--tags` options, the command finds the default `<refspec>` by consulting `remote.*.push` configuration, and if it is not found, honors `push.default` configuration to decide what to push

> When neither the command-line nor the configuration specify what to push, the default behavior is used, which corresponds to the `simple` value for `push.default`: the current branch is pushed to the corresponding upstream branch, but as a safety measure, the push is aborted if the upstream branch does not have the same name as the local one.


#### `push.default=simple`(default)
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
    clear

执行

    git config remote.origin.push
    git config push.default
    git push origin

**执行结果**

FIXME


如果 upstream branch does not have the same name as the local one

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
    git checkout -b testing
    touch README
    git add .
    git commit -m 'C0'
    clear

执行

    git config remote.origin.push
    git config push.default
    git push origin

**执行结果**

FIXME


#### 使用 `remote.*.push`
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
    git branch testing
    clear

执行

    git config remote.origin.push
    git config push.default
    git remote show origin
    git config remote.origin.push testing
    git remote show origin
    git push origin

**执行结果**

FIXME


### refspec 的各种形式
#### tagname
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
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

FIXME


#### `:branch`
> Pushing an empty `<src>` allows you to delete the `<dst>` ref from the remote repository.

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
    git branch testing
    git push -u --all origin
    clear

执行

    git branch -vv
    git remote show origin
    cat ~/test/repo/demo/refs/heads/testing
    git push origin :testing
    git branch -vv
    git remote show origin
    cat ~/test/repo/demo/refs/heads/testing

**执行结果**

FIXME


#### `:refs/tags/<tagname>`
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

    cat ~/test/repo/demo/refs/tags/v0.1
    git push origin :refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

FIXME


# Examples


# Demo
## `git push --tags`
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
    clear

执行

    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2
    git push origin --tags
    cat ~/test/repo/demo/refs/tags/v0.1
    cat ~/test/repo/demo/refs/tags/v0.2

**执行结果**

FIXME


## `git push --all`
> Push all branches (i.e. refs under `refs/heads/`);

注意不包括 tags 


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
    git branch testing
    clear

执行

    git push --all origin
    cat ~/test/repo/demo/refs/tags/v0.1
    git push --tags origin
    cat ~/test/repo/demo/refs/tags/v0.1

**执行结果**

FIXME


## `git push -u/--set-upstream`
> For every branch that is up to date or successfully pushed, add upstream (tracking) reference

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
    git branch testing
    clear

执行

    git branch -vv
    git remote show origin
    git push -u origin testing
    git branch -vv
    git remote show origin

**执行结果**

FIXME


## `git push --delete`
> All listed refs are deleted from the remote repository. This is the same as prefixing all refs with a colon.

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
    git branch testing
    git push -u --all origin
    clear

执行

    git branch -vv
    git remote show origin
    cat ~/test/repo/demo/refs/heads/testing
    git push --delete origin testing
    git branch -vv
    git remote show origin
    cat ~/test/repo/demo/refs/heads/testing

**执行结果**

FIXME


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/git-push.html
