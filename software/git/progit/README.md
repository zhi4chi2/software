注：**文档中的示例默认是在 Linux 下运行的。只有当 Windows 下的操作或命令结果与 Linux 不一样时才特别列出。**


- [Getting Started](getting-started.md)
- [Git Basics](git-basics.md)
- [Git Branching](git-branching.md)
- [Git on the Server](git-server.md)
- [Distributed Git](distributed-git.md)
- [GitHub](github.md)
- [Git Tools](git-tools.md)
- [Customizing Git](customizing-git.md)
- [Git and Other Systems](git-and-other-scms.md)
- [Git Internals](git-internals.md)
- [Appendix A: Git in Other Environments](git-in-other-environments.md)
- [Appendix B: Embedding Git in your Applications](embedding-git.md)


# 术语
- VCS - Version Control System


- modified
- staged
- committed


- working tree/working directory/working copy/checkout - The working tree is a single checkout of one version of the project.
- staging area/index - The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit.
    Its technical name in Git parlance is the "index"
- Git directory - 即 .git directory(Repository), The Git directory is where Git stores the metadata and object database for your project.
- bare repository - a Git repository that has no working directory, is the contents of your project’s `.git` directory and nothing else.


- blob object - 文件内容实际存放在 blob objects 中
- tree object - lists the contents of the directory and specifies which file names are stored as which blobs
- commit object - with the pointer to that root tree and all the commit metadata
- merge commit - Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.

tree object 有多个，每个文件夹都有一个 tree object ，最顶级的文件夹对应的 tree object 叫 root tree object


- HEAD - a pointer to the local branch you're currently on(currently have checked out), 通过 `git checkout` 改变
- branch - a lightweight movable pointer to one of these commits. actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to
- master - not a special branch, exactly like any other branch, The only reason nearly every repository has one is that the `git init` command creates it by default


- remote references - references (pointers) in your remote repositories, including branches, tags, and so on.
- remote-tracking branches - references to the state of remote branches. They’re local references that you can’t move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository. 例如 `origin/master`
- origin - does not have any special meaning, “origin” is the default name for a remote when you run `git clone`. If you run `git clone -o booyah` instead, then you will have `booyah/master` as your default remote branch.
- tracking branch - local branches that have a direct relationship to a remote branch. If you’re on a tracking branch and type `git pull`, Git automatically knows which server to fetch from and which branch to merge in.
- upstream branch - Checking out a local branch from a remote-tracking branch automatically creates what is called a “tracking branch” (and the branch it tracks is called an “upstream branch”).


在 master branch 上执行 `git merge hotfix` 叫做

- merge hotfix branch
- merge hotfix branch into master branch
- merge master branch with hotfix branch

- you merged in - hotfix branch
- you're on - master branch


在 experiment branch 上执行 `git rebase master` 叫做

- you are rebasing onto - master branch
- you're on - experiment branch
- current branch - experiment branch


在 client branch 上执行 `git rebase --onto master server client`

- rebase target branch - server branch
- you are rebasing onto - master branch
- you're on - client branch


在 master branch 上执行 `git rebase master server`

- base branch - master branch


# 最佳实践
## 删除 tracked file
同时从 working tree 和 staging area 中删除

- unmodified - `git rm`
- modified - 先 `git checkout --` 再 `git rm`
- staged - `git rm -f`

如果仅从 staging area 删除，但在 working tree 中保留则使用 `git rm --cached`

应该不会需要只在 working tree 中删除！如果确实需要，使用 Linux 系统命令 `rm` 即可。


## 新建 tracking branch
例子

- `git checkout -b serverfix origin/serverfix`
- `git checkout -b sf origin/serverfix` - 指定分支名字为 sf
- `git checkout --track origin/serverfix`
- `git checkout serverfix` - 只有在 serverfix 分支当前不存在，且只有一个 remote 的分支名为 serverfix 时才可以
- `git checkout -b my-serverfix; git branch -u origin/serverfix` - 先建立分支，再设置 upstream branch


## push branch
例子

- `git push origin` - 只会 push 当前 branch ，且需要当前 branch 是 tracking branch
- `git push origin serverfix`
- `git push origin refs/heads/serverfix:refs/heads/serverfix`
- `git push origin serverfix:serverfix`
- `git push origin serverfix:awesomebranch`
- `git push --set-upstream origin serverfix` - 将 local branch push 到 remote 并设为 tracking branch ，相当于 `git push origin serverfix; git branch -u origin/serverfix`


# Reference
- https://git-scm.com/book/zh/v2 - 中文
- https://git-scm.com/book/en/v2 - 英文，英文版与中文版有些差别，应该是中文版不够新
- https://github.com/progit/progit2 - 源码
- https://github.com/progit/progit2-zh - 中文版源码
