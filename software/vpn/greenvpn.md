版本： 1.1.4(Green_Win_V114.zip)


发任意邮件至 GreenDiZhi@gmail.com 可以获得最新网址


# 安装
Windows 下
- 需要先安装 .NET Framework 4.6(NDP46-KB3045557-x86-x64-AllOS-ENU.exe)
- 解压即可


# bug
- 密码不能有特殊字符，应使用 simple 密码策略，否则登录不了。


# Linux 下配置 OpenVPN
```bash
me@mypc:~$ sudo apt-get install network-manager-gnome network-manager-pptp network-manager-openvpn
sudo: unable to resolve host mypc
[sudo] password for me: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
network-manager-pptp is already the newest version (1.1.93-1ubuntu1).
network-manager-pptp set to manually installed.
network-manager-gnome is already the newest version (1.2.6-0ubuntu0.16.04.2).
network-manager-gnome set to manually installed.
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
Suggested packages:
  easy-rsa
The following NEW packages will be installed:
  libpkcs11-helper1 network-manager-openvpn openvpn
0 upgraded, 3 newly installed, 0 to remove and 51 not upgraded.
Need to get 489 kB of archives.
After this operation, 1,265 kB of additional disk space will be used.
Get:1 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 libpkcs11-helper1 amd64 1.11-5 [44.0 kB]
Get:2 http://cn.archive.ubuntu.com/ubuntu xenial/main amd64 openvpn amd64 2.3.10-1ubuntu2 [418 kB]
Get:3 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 network-manager-openvpn amd64 1.1.93-1ubuntu1.1 [26.5 kB]
Fetched 489 kB in 0s (740 kB/s)                    
Preconfiguring packages ...
Selecting previously unselected package libpkcs11-helper1:amd64.
(Reading database ... 536319 files and directories currently installed.)
Preparing to unpack .../libpkcs11-helper1_1.11-5_amd64.deb ...
Unpacking libpkcs11-helper1:amd64 (1.11-5) ...
Selecting previously unselected package openvpn.
Preparing to unpack .../openvpn_2.3.10-1ubuntu2_amd64.deb ...
Unpacking openvpn (2.3.10-1ubuntu2) ...
Selecting previously unselected package network-manager-openvpn.
Preparing to unpack .../network-manager-openvpn_1.1.93-1ubuntu1.1_amd64.deb ...
Unpacking network-manager-openvpn (1.1.93-1ubuntu1.1) ...
Processing triggers for libc-bin (2.23-0ubuntu7) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for systemd (229-4ubuntu16) ...
Processing triggers for ureadahead (0.100.0-19) ...
ureadahead will be reprofiled on next reboot
Processing triggers for dbus (1.10.6-1ubuntu3.3) ...
Setting up libpkcs11-helper1:amd64 (1.11-5) ...
Setting up openvpn (2.3.10-1ubuntu2) ...
 * Restarting virtual private network daemon(s)...                               *   No VPN is running.
Setting up network-manager-openvpn (1.1.93-1ubuntu1.1) ...
Processing triggers for libc-bin (2.23-0ubuntu7) ...
Processing triggers for systemd (229-4ubuntu16) ...
Processing triggers for ureadahead (0.100.0-19) ...
Processing triggers for dbus (1.10.6-1ubuntu3.3) ...
me@mypc:~$ sudo apt-get install -y network-manager-openvpn network-manager-openvpn-gnome
sudo: unable to resolve host mypc
Reading package lists... Done
Building dependency tree       
Reading state information... Done
network-manager-openvpn is already the newest version (1.1.93-1ubuntu1.1).
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
The following NEW packages will be installed:
  network-manager-openvpn-gnome
0 upgraded, 1 newly installed, 0 to remove and 51 not upgraded.
Need to get 180 kB of archives.
After this operation, 1,235 kB of additional disk space will be used.
Get:1 http://cn.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 network-manager-openvpn-gnome amd64 1.1.93-1ubuntu1.1 [180 kB]
Fetched 180 kB in 0s (641 kB/s)                       
Selecting previously unselected package network-manager-openvpn-gnome.
(Reading database ... 536417 files and directories currently installed.)
Preparing to unpack .../network-manager-openvpn-gnome_1.1.93-1ubuntu1.1_amd64.deb ...
Unpacking network-manager-openvpn-gnome (1.1.93-1ubuntu1.1) ...
Setting up network-manager-openvpn-gnome (1.1.93-1ubuntu1.1) ...
me@mypc:~$ sudo /etc/init.d/network-manager restart
sudo: unable to resolve host mypc
[ ok ] Restarting network-manager (via systemctl): network-manager.service.
me@mypc:~$ 
```


# Reference
- https://www.greenjsq.me/index.php
- https://www.greenjsq.me/client/Green_Win_V114.zip - 下载地址
- https://www.greenjsq.me/user-xianlu.html
- https://www.greenjsq.me/shiyong/88.html - PPTP 测试不成功
- https://www.greenjsq.me/shiyong/67.html - OpenVPN 最后不应该使用 ca.crt 而是使用默认的与连接名同名的 pem 文件才成功。例如 /home/me/.cert/nm-openvpn/UnitedStates-05-ca.pem

