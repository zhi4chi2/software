
    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo
    Cloning into 'demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  demo/
    me@mypc:~/test$ cd demo
    me@mypc:~/test/demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/demo$ 


clone 到了 /home/me/test/demo 目录下（自动创建此目录），库在 /home/me/test/demo/.git


GitHub 的 git clone url 可以加 .git 也可以省略。

    me@mypc:~/test$ ls -aF
    ./  ../
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo.git my-demo
    Cloning into 'my-demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ ls -aF
    ./  ../  my-demo/
    me@mypc:~/test$ cd my-demo
    me@mypc:~/test/my-demo$ ls -aF
    ./  ../  .git/  README.md
    me@mypc:~/test/my-demo$ 


除了 https:// 协议外还可以使用 git:// 或者使用 SSH 传输协议。


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


# -o

    FIXME
    git clone -o not-origin
    git remote


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository
- https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches