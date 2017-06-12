```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) e9270f4] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ git mv README README.txt
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    README -> README.txt

me@mypc:~/test/workspace$ git commit -m 'rename README to README.txt'
[master b77d5c6] rename README to README.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename README => README.txt (100%)
me@mypc:~/test/workspace$ 
```


`git mv` 相当于运行了三条命令
1. mv README README.txt
1. git rm README
1. git add README.txt


如此分开操作， Git 也会意识到这是一次改名，所以不管何种方式结果都一样。
```bash
me@mypc:~/test$ mkdir workspace
me@mypc:~/test$ cd workspace
me@mypc:~/test/workspace$ git init
Initialized empty Git repository in /home/me/test/workspace/.git/
me@mypc:~/test/workspace$ touch README
me@mypc:~/test/workspace$ git add README
me@mypc:~/test/workspace$ git commit -m 'init commit'
[master (root-commit) efbd51c] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
me@mypc:~/test/workspace$ mv README README.txt
me@mypc:~/test/workspace$ git rm README
rm 'README'
me@mypc:~/test/workspace$ git add README.txt
me@mypc:~/test/workspace$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    README -> README.txt

me@mypc:~/test/workspace$ git commit -m 'rename README to README.txt'
[master 930ecf1] rename README to README.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename README => README.txt (100%)
me@mypc:~/test/workspace$ 
```


# Reference
- https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
