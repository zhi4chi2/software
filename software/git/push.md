默认不会 push local branches 到 remote 。需要显式 push

    FIXME
    git push origin serverfix
    git push origin serverfix:serverfix
    git push origin serverfix:awesomebranch


默认不会 push tags 到 remote

    FIXME
    git push origin v1.0
    git push origin --tags


# --delete

    FIXME
    git push origin --delete serverfix


# -u/--set-upstream

    FIXME
    git push -u origin next


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes
- https://git-scm.com/book/en/v2/Git-Basics-Tagging
- https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches