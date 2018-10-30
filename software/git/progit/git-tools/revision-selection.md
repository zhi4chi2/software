    touch README
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    git show f5a3dabe1974c23fe51375db6985fd42539d6807
    git show f5a3dabe1974c23
    git show f5a3
    me@mypc:~/test$ git log
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    commit 8b4f2ec68d38a68dd462be873e1dcef98b337d47
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C0
    me@mypc:~/test$ git show f5a3dabe1974c23fe51375db6985fd42539d6807
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show f5a3dabe1974c23
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show f5a3
    commit f5a3dabe1974c23fe51375db6985fd42539d6807
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:29:09 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git log --abbrev-commit --pretty=oneline
    f5a3dab C1
    8b4f2ec C0
    me@mypc:~/test$ 
    touch README
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    git show c818631a50200a9297a347739f24000fbf9c821b
    me@mypc:~/test$ git log -1
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1
    me@mypc:~/test$ git show c818631a50200a9297a347739f24000fbf9c821b
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git show master
    commit c818631a50200a9297a347739f24000fbf9c821b
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:32:42 2018 +0800

        C1

    diff --git a/README b/README
    index e69de29..e2cf5e7 100644
    --- a/README
    +++ b/README
    @@ -0,0 +1 @@
    +C1
    me@mypc:~/test$ git rev-parse master
    c818631a50200a9297a347739f24000fbf9c821b
    me@mypc:~/test$ 
    touch README
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    me@mypc:~/test$ git reflog
    b63728e HEAD@{0}: commit: C1
    5ddb924 HEAD@{1}: commit (initial): C0
    me@mypc:~/test$ git show HEAD@{1}
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git show master@{yesterday}
    warning: Log for 'master' only goes back to Sat, 27 Oct 2018 14:34:24 +0800.
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git show HEAD@{2.months.ago}
    warning: Log for 'HEAD' only goes back to Sat, 27 Oct 2018 14:34:24 +0800.
    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0

    diff --git a/README b/README
    new file mode 100644
    index 0000000..e69de29
    me@mypc:~/test$ git log -g master
    commit b63728eaf51934e7d1de3b1a82d12f9e2715ba08
    Reflog: master@{0} (me <me@example.com>)
    Reflog message: commit: C1
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C1

    commit 5ddb9240a514d366497b3d07a636e679865d28d9
    Reflog: master@{1} (me <me@example.com>)
    Reflog message: commit (initial): C0
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:34:24 2018 +0800

        C0
    me@mypc:~/test$ 
    touch README
    echo 'C1' >> README
    echo 'C2' > rdoc
    echo 'C3' >> README
    echo 'C4' >> README
    git rev-parse HEAD^
    git rev-parse HEAD~3
    git rev-parse HEAD~~~
    git rev-parse HEAD~^2
    me@mypc:~/test$ git log --pretty=format:'%h %s' --graph
    * 20fccdf fixed refs handling, added gc auto, updated tests
    *   1f767b4 Merge commit 'phedders/rdocs'
    |\  
    | * 226dc8e Some rdoc changes
    * | cf08d76 added some blame and merge stuff
    |/  
    * 562db1c ignore *.gem
    * c0c1a96 add open3_detach to gemspec file list
    me@mypc:~/test$ git rev-parse HEAD^
    1f767b409976e910fb95d50a0853e824623e76c3
    me@mypc:~/test$ git rev-parse HEAD~3
    562db1cd2f325b44646a7d2df4ea1bbeb7499707
    me@mypc:~/test$ git rev-parse HEAD~~~
    562db1cd2f325b44646a7d2df4ea1bbeb7499707
    me@mypc:~/test$ git rev-parse HEAD~^2
    226dc8eb06990e291867a6039aee54437eb09fdc
    me@mypc:~/test$ 
    echo 'C' >> README
    git commit -a -m 'C'
    echo 'D' >> README
    me@mypc:~/test$ git log --oneline --graph --all
    * 92036ce D
    * 26dfd83 C
    | * 5a43578 F
    | * abfd124 E
    |/  
    * 3443d85 B
    * 93730c2 A
    me@mypc:~/test$ git log master..experiment
    commit 92036ce6ae3a3d7ce6e9a4a4d3517f5deb43336c
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        D

    commit 26dfd83c0ac523ad0669b5db169aa55af3e7152d
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        C
    me@mypc:~/test$ git log experiment..master
    commit 5a43578295bea6e4c6c3f8712ff80fb2ba507197
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        F

    commit abfd1247ba782f79edd51221e8a1e15ef986a3f2
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:39:23 2018 +0800

        E
    me@mypc:~/test$ 
    touch README
    git commit -m 'C0'
    echo 'C1' >> README
    git commit -a -m 'C1'
    me@mypc:~/test/workspace/demo$ git log --oneline --graph --all
    * 2023e76 C1
    * 715ad3c C0
    me@mypc:~/test/workspace/demo$ git log origin/master..HEAD
    commit 2023e76754c461b166d3a9404417aff4db11c194
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:01 2018 +0800

        C1
    me@mypc:~/test/workspace/demo$ git log origin/master..
    commit 2023e76754c461b166d3a9404417aff4db11c194
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:01 2018 +0800

        C1
    me@mypc:~/test/workspace/demo$ 
    echo 'C' >> README
    git commit -a -m 'C'
    echo 'D' >> README
    me@mypc:~/test$ git log --oneline --graph --all
    * 3f4a997 D
    * a34f23d C
    | * 7d30ec3 F
    | * db4577b E
    |/  
    * 1dbda29 B
    * 82cb477 A
    me@mypc:~/test$ git log master...experiment
    commit 7d30ec3a692afdfba5ae0fd3c39c7d9609b611ec
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        F

    commit 3f4a9973314ae872c671f6d80f9d456f9f64efce
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        D

    commit db4577b8791917d059a8ba00b493a77d53e7f7f4
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        E

    commit a34f23d63d16a905139f6434f87c21a8919dc5c3
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        C
    me@mypc:~/test$ git log --left-right master...experiment
    commit < 7d30ec3a692afdfba5ae0fd3c39c7d9609b611ec
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        F

    commit > 3f4a9973314ae872c671f6d80f9d456f9f64efce
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        D

    commit < db4577b8791917d059a8ba00b493a77d53e7f7f4
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        E

    commit > a34f23d63d16a905139f6434f87c21a8919dc5c3
    Author: me <me@example.com>
    Date:   Sat Oct 27 14:40:52 2018 +0800

        C
    me@mypc:~/test$ 
