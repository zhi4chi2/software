# 安装
```bash
me@mypc:~$ sudo apt-get install passwordsafe
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-4.4.0-75 linux-headers-4.4.0-75-generic
  linux-image-4.4.0-75-generic linux-image-extra-4.4.0-75-generic snap-confine
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  passwordsafe-common
The following NEW packages will be installed:
  passwordsafe passwordsafe-common
0 upgraded, 2 newly installed, 0 to remove and 5 not upgraded.
Need to get 9,366 kB of archives.
After this operation, 13.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://cn.archive.ubuntu.com/ubuntu xenial/universe amd64 passwordsafe-common all 0.98.1+dfsg-3 [8,432 kB]
Get:2 http://cn.archive.ubuntu.com/ubuntu xenial/universe amd64 passwordsafe amd64 0.98.1+dfsg-3 [934 kB]
Fetched 9,366 kB in 9s (1,005 kB/s)                                            
Selecting previously unselected package passwordsafe-common.
(Reading database ... 247485 files and directories currently installed.)
Preparing to unpack .../passwordsafe-common_0.98.1+dfsg-3_all.deb ...
Unpacking passwordsafe-common (0.98.1+dfsg-3) ...
Selecting previously unselected package passwordsafe.
Preparing to unpack .../passwordsafe_0.98.1+dfsg-3_amd64.deb ...
Unpacking passwordsafe (0.98.1+dfsg-3) ...
Processing triggers for hicolor-icon-theme (0.15-0ubuntu1) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for desktop-file-utils (0.22-1ubuntu5.1) ...
Processing triggers for bamfdaemon (0.5.3~bzr0+16.04.20160824-0ubuntu1) ...
Rebuilding /usr/share/applications/bamf-2.index...
Processing triggers for gnome-menus (3.13.3-6ubuntu3.1) ...
Processing triggers for mime-support (3.59ubuntu1) ...
Setting up passwordsafe-common (0.98.1+dfsg-3) ...
Setting up passwordsafe (0.98.1+dfsg-3) ...
me@mypc:~$ 
```


# bugs
- 在 Ubuntu 下输入主密码的特殊字符的键盘打不开
- 在 Ubuntu 下显示密码的对话框不会在几分钟后自动隐藏，而是一直显示！而应用的主界面虽然不隐藏但变为空白。

