

# --bare

    me@mypc:~$ git clone --bare https://github.com/zhi4chi2/demo.git demo
    Cloning into bare repository 'demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~$ ls
    1.txt  demo  Desktop  Documents  Downloads  examples.desktop  GitBook  GitHub  Music  Pictures  Public  Templates  test  Videos
    me@mypc:~$ cd demo
    me@mypc:~/demo$ ls -aF
    ./  ../  branches/  config  description  HEAD  hooks/  info/  objects/  packed-refs  refs/
    me@mypc:~/demo$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository
- https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches