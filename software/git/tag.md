tag 有两种

- lightweight tag
- annotated tag


    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) b6dfcc8] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ git tag v0.1
    me@mypc:~/test/workspace$ echo hello > README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'change README'
    [master c546305] change README
     1 file changed, 1 insertion(+)
    me@mypc:~/test/workspace$ git tag v0.2
    me@mypc:~/test/workspace$ git tag
    v0.1
    v0.2
    me@mypc:~/test/workspace$ git tag -l "v*"
    v0.1
    v0.2
    me@mypc:~/test/workspace$ git tag -l "*.2"
    v0.2
    me@mypc:~/test/workspace$ 


# git tag tagname commit

    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) 5fc65c3] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ echo hello > README
    me@mypc:~/test/workspace$ git commit -a -m 'modify README'
    [master 23775ca] modify README
     1 file changed, 1 insertion(+)
    me@mypc:~/test/workspace$ echo world >> README
    me@mypc:~/test/workspace$ git commit -a -m 'modify README again'
    [master db6ec50] modify README again
     1 file changed, 1 insertion(+)
    me@mypc:~/test/workspace$ git log --pretty=oneline
    db6ec5099ca3ac8f60083dc6a75460f59f701cd8 modify README again
    23775ca349a300cd2a7af9b732afb92c7c0770a8 modify README
    5fc65c3ab076fa7098f65c57f6774c11bcf6dc01 init commit
    me@mypc:~/test/workspace$ git tag v0.1 5fc65c3
    me@mypc:~/test/workspace$ git tag -a -m 'test annotated tag' v0.2 23775ca
    me@mypc:~/test/workspace$ git tag
    v0.1
    v0.2
    me@mypc:~/test/workspace$ 


# -a

    me@mypc:~/test/workspace$ git tag -a atag -m 'an annotated tag'
    me@mypc:~/test/workspace$ git tag
    atag
    v0.1
    v0.2
    me@mypc:~/test/workspace$ 


# -l

    me@mypc:~/test/workspace$ git tag -l "*.2"
    v0.2
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Tagging
- [git show](/Software/Git/show.md)
