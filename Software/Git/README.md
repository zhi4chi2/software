# 安装

```bash
me@mypc:~$ sudo apt-get install git
[sudo] password for me: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-4.4.0-21 linux-headers-4.4.0-21-generic linux-headers-4.4.0-31
  linux-headers-4.4.0-31-generic linux-headers-4.4.0-34
  linux-headers-4.4.0-34-generic linux-headers-4.4.0-36
  linux-headers-4.4.0-36-generic linux-headers-4.4.0-43
  linux-headers-4.4.0-43-generic linux-headers-4.4.0-62
  linux-headers-4.4.0-62-generic linux-headers-4.4.0-64
  linux-headers-4.4.0-64-generic linux-headers-4.4.0-66
  linux-headers-4.4.0-66-generic linux-headers-4.4.0-71
  linux-headers-4.4.0-71-generic linux-headers-4.4.0-72
  linux-headers-4.4.0-72-generic linux-image-4.4.0-21-generic
  linux-image-4.4.0-31-generic linux-image-4.4.0-34-generic
  linux-image-4.4.0-36-generic linux-image-4.4.0-43-generic
  linux-image-4.4.0-62-generic linux-image-4.4.0-64-generic
  linux-image-4.4.0-66-generic linux-image-4.4.0-71-generic
  linux-image-4.4.0-72-generic linux-image-extra-4.4.0-21-generic
  linux-image-extra-4.4.0-31-generic linux-image-extra-4.4.0-34-generic
  linux-image-extra-4.4.0-36-generic linux-image-extra-4.4.0-43-generic
  linux-image-extra-4.4.0-62-generic linux-image-extra-4.4.0-64-generic
  linux-image-extra-4.4.0-66-generic linux-image-extra-4.4.0-71-generic
  linux-image-extra-4.4.0-72-generic ubuntu-core-launcher
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  git-man liberror-perl
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk
  gitweb git-arch git-cvs git-mediawiki git-svn
The following NEW packages will be installed:
  git git-man liberror-perl
0 upgraded, 3 newly installed, 0 to remove and 51 not upgraded.
Need to get 3,823 kB of archives.
After this operation, 25.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 liberror-perl all 0.17-1.2 [19.6 kB]
Get:2 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 git-man all 1:2.7.4-0ubuntu1.1 [735 kB]
Get:3 http://cn.archive.ubuntu.com/ubuntu xenial-updates/main amd64 git amd64 1:2.7.4-0ubuntu1.1 [3,068 kB]
Fetched 3,823 kB in 42s (90.2 kB/s)                                            
Selecting previously unselected package liberror-perl.
(Reading database ... 536483 files and directories currently installed.)
Preparing to unpack .../liberror-perl_0.17-1.2_all.deb ...
Unpacking liberror-perl (0.17-1.2) ...
Selecting previously unselected package git-man.
Preparing to unpack .../git-man_1%3a2.7.4-0ubuntu1.1_all.deb ...
Unpacking git-man (1:2.7.4-0ubuntu1.1) ...
Selecting previously unselected package git.
Preparing to unpack .../git_1%3a2.7.4-0ubuntu1.1_amd64.deb ...
Unpacking git (1:2.7.4-0ubuntu1.1) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up liberror-perl (0.17-1.2) ...
Setting up git-man (1:2.7.4-0ubuntu1.1) ...
Setting up git (1:2.7.4-0ubuntu1.1) ...
me@mypc:~$ git --version
git version 2.7.4
me@mypc:~$ 
```


# Reference

- https://git-scm.com/