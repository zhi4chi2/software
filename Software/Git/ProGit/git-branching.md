# Branches in a Nutshell
commit object 包含
- author’s name and email
- commit message
- pointers to the parents commits
- pointer to the snapshot of the content(root tree object)


stage file(git add)会
- computes a checksum(SHA-1) for each file
- stores that version of the file in the Git repository
- adds that checksum to the staging area(index)


tree object 有多个，每个文件夹都有一个 tree object ，最顶级的叫 root tree object


git commit 会
- 计算每个文件夹的 checksum 在 Git repository 中保存为 tree objects
- 创建 commit object


tree object 包含该目录下每个文件的 checksum(指向每个文件的 blob 对象)，并将文件名和 checksum 对应。


## Creating a New Branch
参见 [git branch](/Software/Git/branch.md)


HEAD 指向当前所在的分支。


## Switching Branches
参见 [git checkout](/Software/Git/checkout.md), [git log](/Software/Git/log.md)


# Basic Branching and Merging
参见 [git merge](/Software/Git/merge.md), [git mergetool](/Software/Git/mergetool.md)


# Branch Management
参见 [git branch](/Software/Git/branch.md)


# Branching Workflows
common workflows(branching scheme)
- Long-Running Branches - 在很长一段时间里，从一个分支多次 merge 到另一个分支。前一个分支(develop / next)用于开发，后一个分支(master)用于发布
- Topic Branches - topic branch is a short-lived branch, use for a single particular feature


# Remote Branches
Remote-tracking branches 形如 (remote)/(branch) 例如 origin/master


参见 [git clone](/Software/Git/clone.md), [git fetch](/Software/Git/fetch.md), [git push](/Software/Git/push.md), [git merge](/Software/Git/merge.md), [git checkout](/Software/Git/checkout.md)


# Rebasing
参见 [git rebase](/Software/Git/rebase.md)