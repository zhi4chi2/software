
    me@mypc:~/test$ mkdir workspace
    me@mypc:~/test$ git clone https://github.com/zhi4chi2/demo.git workspace
    Cloning into 'workspace'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ cd workspace
    me@mypc:~/test/workspace$ git remote
    origin
    me@mypc:~/test/workspace$ git remote -v
    origin	https://github.com/zhi4chi2/demo.git (fetch)
    origin	https://github.com/zhi4chi2/demo.git (push)
    me@mypc:~/test/workspace$ 


# add

    me@mypc:~/test/workspace$ cd ..
    me@mypc:~/test$ git clone --bare https://github.com/zhi4chi2/demo.git demo
    Cloning into bare repository 'demo'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    me@mypc:~/test$ cd workspace/
    me@mypc:~/test/workspace$ git remote add mypc file:///home/me/test/demo
    me@mypc:~/test/workspace$ git remote -v
    mypc	file:///home/me/test/demo (fetch)
    mypc	file:///home/me/test/demo (push)
    origin	https://github.com/zhi4chi2/demo.git (fetch)
    origin	https://github.com/zhi4chi2/demo.git (push)
    me@mypc:~/test/workspace$ git fetch mypc
    From file:///home/me/test/demo
     * [new branch]      master     -> mypc/master
    me@mypc:~/test/workspace$ 


# show

    me@mypc:~/test/workspace$ git remote show mypc
    * remote mypc
      Fetch URL: file:///home/me/test/demo
      Push  URL: file:///home/me/test/demo
      HEAD branch: master
      Remote branch:
        master tracked
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/workspace$ git remote show origin
    * remote origin
      Fetch URL: https://github.com/zhi4chi2/demo.git
      Push  URL: https://github.com/zhi4chi2/demo.git
      HEAD branch: master
      Remote branch:
        master tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local ref configured for 'git push':
        master pushes to master (up to date)
    me@mypc:~/test/workspace$ 


# rename

    me@mypc:~/test/workspace$ git remote rename mypc me
    me@mypc:~/test/workspace$ git remote -v
    me	file:///home/me/test/demo (fetch)
    me	file:///home/me/test/demo (push)
    origin	https://github.com/zhi4chi2/demo.git (fetch)
    origin	https://github.com/zhi4chi2/demo.git (push)
    me@mypc:~/test/workspace$ 


# remove

    me@mypc:~/test/workspace$ git remote remove me
    me@mypc:~/test/workspace$ git remote -v
    origin	https://github.com/zhi4chi2/demo.git (fetch)
    origin	https://github.com/zhi4chi2/demo.git (push)
    me@mypc:~/test/workspace$ 


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes
