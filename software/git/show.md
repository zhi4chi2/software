
    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git init
    Initialized empty Git repository in /home/me/test/workspace/.git/
    me@mypc:~/test/workspace$ touch README
    me@mypc:~/test/workspace$ git add README
    me@mypc:~/test/workspace$ git commit -m 'init commit'
    [master (root-commit) b650122] init commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README
    me@mypc:~/test/workspace$ git tag v1.0
    me@mypc:~/test/workspace$ git show v1.0
    commit b6501223db962b660529f41a82fa81b3ed9162c1
    Author: me <me@example.com>
    Date:   Sun Jun 11 16:43:23 2017 +0800
    
        init commit
    
    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test/workspace$ git tag -a atag -m 'an annotated tag'
    me@mypc:~/test/workspace$ git show atag
    tag atag
    Tagger: me <me@example.com>
    Date:   Sun Jun 11 16:44:57 2017 +0800
    
    an annotated tag
    
    commit b6501223db962b660529f41a82fa81b3ed9162c1
    Author: me <me@example.com>
    Date:   Sun Jun 11 16:43:23 2017 +0800
    
        init commit
    
    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Tagging
