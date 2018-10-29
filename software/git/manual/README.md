# 术语
- refspec - 例如 `refs/heads/serverfix:refs/heads/serverfix` 参见 [git push](push.md)
- refname - 例如 `refs/heads/serverfix` 参见 [git push](push.md)
- start-point - a branch name, a commit-id, or a tag. 例如 `origin/master` 参见 [git branch](branch.md)


## upstream
注意：设置 upstream 只影响 pull 不影响 push ！ push 的默认行为由 `push.default` 决定。


branch 在本地新建，希望 push 到 remote ，并设置 upstream

- `git push -u/--set-upstream`
- `git push` 后再执行 `git branch -u/--set-upstream-to`


从 remote branch 建立 local branch

- `git branch branchname remote/branch`
- `git checkout --track remote/branch`


# Reference
- file:///D:/Git/mingw64/share/doc/git-doc/index.html
