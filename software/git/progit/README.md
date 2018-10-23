注：**文档中的示例默认是在 Linux 下运行的。只有当 Windows 下的操作或命令结果与 Linux 不一样时才特别列出。**


- [Getting Started](getting-started.md)
- [Git Basics](git-basics.md)
- [Git Branching](git-branching.md)


# 术语
- VCS - Version Control System


- modified
- staged
- committed


- working tree/working directory/working copy/checkout - The working tree is a single checkout of one version of the project.
- staging area/index - The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit.
    Its technical name in Git parlance is the "index"
- Git directory - 即 .git directory(Repository), The Git directory is where Git stores the metadata and object database for your project.


# 最佳实践
## 删除 tracked file
同时从 working tree 和 staging area 中删除

- unmodified - `git rm`
- modified - 先 `git checkout --` 再 `git rm`
- staged - `git rm -f`

如果仅从 staging area 删除，但在 working tree 中保留则使用 `git rm --cached`

应该不会需要只在 working tree 中删除！如果确实需要，使用 Linux 系统命令 `rm` 即可。


# Reference
- https://git-scm.com/book/zh/v2 - 中文
- https://git-scm.com/book/en/v2 - 英文，英文版与中文版有些差别，应该是中文版不够新
- https://github.com/progit/progit2 - 源码
- https://github.com/progit/progit2-zh - 中文版源码
