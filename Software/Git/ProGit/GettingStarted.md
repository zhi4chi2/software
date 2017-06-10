# Git 基础

## 直接记录快照，而非差异比较
每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。
 
为了高效，如果文件没有修改， Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个快照流。

## 近乎所有操作都是本地执行

## Git 保证完整性

Git 中所有数据在存储前都计算校验和，然后以校验和来引用。

这意味着不可能在 Git 不知情时更改任何文件内容或目录内容。

这个功能建构在 Git 底层，是构成 Git 哲学不可或缺的部分。

若你在传送过程中丢失信息或损坏文件， Git 就能发现。

Git 用以计算校验和的机制叫做 SHA-1 散列，这是一个由 40 个十六进制字符（ 0-9 和 a-f ）组成字符串，基于 Git 中文件的内容或目录结构计算出来。

Git 数据库中保存的信息都是以文件内容的哈希值来索引，而不是文件名。

## Git 一般只添加数据

## 三种状态

文件有三种状态
- 已提交(committed) - 数据已经安全的保存在本地数据库中
- 已修改(modified) - 修改了文件，但还没保存到数据库中
- 已暂存(staged) - 对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中

三个工作区域
- Git 仓库
- 暂存区域(staging area) - 是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。有时候也被称作索引(index)
- 工作目录


# 命令行


# 安装 Git
本书写作时使用的 Git 版本为 2.0.0

Linux 下安装 `apt-get install git` 。英文文档中的安装方法是 `apt-get install git-all`

Windows 下的官方版本是一个名为 Git for Windows 的项目（也叫做 msysGit ），和 Git 是分别独立的项目；更多信息请访问 http://msysgit.github.io/ 。

英文文档中给的地址是 https://git-for-windows.github.io/

另一个简单的方法是安装 GitHub for Windows 。该安装程序包含图形化和命令行版本的 Git 。 它也能支持 Powershell ，提供了稳定的凭证缓存和健全的 CRLF 设置。

安装过程参见 [Git](/Software/Git/README.md)


# 初次运行 Git 前的配置

`git config` 配置变量存储在
- /etc/gitconfig - 使用 --system 选项
- ~/.gitconfig 或 ~/.config/git/config - 使用 --global 选项
- .git/config - 默认

在 windows 下对应
- D:\Git\etc\gitconfig
- C:\Users\\$USER\.gitconfig
- .git/config

当使用 Git for Windows 2.x 时，在 Windows 下还有一个 system level config file 在 C:\ProgramData\Git\config 下，但只能通过 git config -f 修改。


## 用户

在 windows 下
```bash
bruce@bruce-PC MINGW64 ~
$ git config --global user.name "me"

bruce@bruce-PC MINGW64 ~
$ git config --global user.email me@example.com

bruce@bruce-PC MINGW64 ~
$
```

在 Linux 下
```bash
me@mypc:~$ git config --global user.name me
me@mypc:~$ git config --global user.email me@example.com
me@mypc:~$ 
```

## 文本编辑器

默认使用 vim ，可以修改为 emacs

```bash
git config --global core.editor emacs
```

在 Windows 下可以改为 Notepad++
```bash
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```


## 检查配置信息

在 windows 下
```bash
bruce@bruce-PC MINGW64 ~
$ git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
rebase.autosquash=true
http.sslcainfo=D:/Git/mingw64/ssl/certs/ca-bundle.crt
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.required=true
filter.lfs.process=git-lfs filter-process
credential.helper=manager
user.name=me
user.email=me@example.com

bruce@bruce-PC MINGW64 ~
$
```


在 Linux 下
```bash
me@mypc:~$ git config --list
user.email=me@example.com
user.name=me
me@mypc:~$ 
```

Git 会从不同的文件中读取同一个配置，因此可能有重复的配置名，则将使用最后一个配置。可以使用 `git config key` 检查配置

在 windows 下
```bash
bruce@bruce-PC MINGW64 ~
$ git config user.name
me

bruce@bruce-PC MINGW64 ~
$
```

在 Linux 下
```bash
me@mypc:~$ git config user.name
me
me@mypc:~$ git config user.email
me@example.com
me@mypc:~$ 
```

# 获取帮助

有三种方式
- `git help <verb>` - 例如 `git help config` 在 windows 下打开 file:///D:/Git/mingw64/share/doc/git-doc/git-config.html
- `git <verb> --help` - 例如 `git config --help` 在 windows 下打开 file:///D:/Git/mingw64/share/doc/git-doc/git-config.html
- `man git-<verb>`

在 windows 下
```bash
bruce@bruce-PC MINGW64 ~
$ git help config

bruce@bruce-PC MINGW64 ~
$ git config --help

bruce@bruce-PC MINGW64 ~
$ man git-config
bash: man: command not found

bruce@bruce-PC MINGW64 ~
$
```

在 Linux 下
```bash
me@mypc:~$ git help config
me@mypc:~$ git config --help
me@mypc:~$ man git-config
me@mypc:~$ 
```
三种方式得到的帮助是一样的。

