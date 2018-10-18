# About Version Control
术语

- VCS - Version Control System


## Local Version Control Systems
## Centralized Version Control Systems

- CVS
- Subversion
- Perforce


## Distributed Version Control Systems

- Git
- Mercurial
- Bazaar
- Darcs


# A Short History of Git
# Git Basics
## Snapshots, Not Differences
> These other systems (CVS, Subversion, Perforce, Bazaar, and so on) think of the information they store as a set of files and the changes made to each file over time (this is commonly described as delta-based version control).

CVS, Subversion 等等 Storing data as changes to a base version of each file.


> Git thinks of its data more like a series of snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git doesn't store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.

Git Storing data as snapshots of the project over time.

每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。
 
为了高效，如果文件没有修改， Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个快照流(stream of snapshots, a series of snapshots of a miniature filesystem)。


## Nearly Every Operation Is Local
## Git Has Integrity
> Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it's impossible to change the contents of any file or directory without Git knowing about it. This functionality is built into Git at the lowest levels and is integral to its philosophy. You can't lose information in transit or get file corruption without Git being able to detect it.

Git 中所有数据在存储前都计算校验和，然后以校验和来引用。


这意味着不可能在 Git 不知情时更改任何文件内容或目录内容。


这个功能建构在 Git 底层，是构成 Git 哲学不可或缺的部分。


若你在传送过程中丢失信息或损坏文件， Git 就能发现。


> The mechanism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git.

Git 用以计算校验和的机制叫做 SHA-1 散列，这是一个由 40 个十六进制字符（ 0-9 和 a-f ）组成字符串，基于 Git 中文件的内容或目录结构计算出来。


> Git stores everything in its database not by file name but by the hash value of its contents.

Git 数据库中保存的信息都是以文件内容的哈希值来索引，而不是文件名。


## Git Generally Only Adds Data
## The Three States
文件有三种状态

- 已提交(committed) - 数据已经安全的保存在本地数据库中
- 已修改(modified) - 修改了文件，但还没保存到数据库中
- 已暂存(staged) - 对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中


三个工作区域

- Git 仓库(Git directory)
- 暂存区域(staging area) - 是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。有时候也被称作索引(index)
- 工作目录(working tree)


# The Command Line
# Installing Git
本书写作时使用的 Git 版本为 2.0.0


## Installing on Linux
Linux 下安装 `apt-get install git` 。英文文档中的安装方法是 `apt-get install git-all`


## Installing on Mac
## Installing on Windows
> The most official build is available for download on the Git website. Just go to <http://git-scm.com/download/win> and the download will start automatically. Note that this is a project called Git for Windows, which is separate from Git itself; for more information on it, go to <https://git-for-windows.github.io/>.

Windows 下的官方版本是一个名为 Git for Windows 的项目，和 Git 是分别独立的项目

- http://git-scm.com/download/win - 下载地址
- https://git-for-windows.github.io/

中文版文档称为 msysGit ，网址为 <http://msysgit.github.io/>


英文版文档中还有一个(community maintained automated installation) <https://chocolatey.org/packages/git>


> Another easy way to get Git installed is by installing GitHub Desktop. The installer includes a command line version of Git as well as the GUI. It also works well with Powershell, and sets up solid credential caching and sane CRLF settings.

另一个简单的方法是安装 GitHub Desktop 。该安装程序包含图形化和命令行版本的 Git 。 它也能支持 Powershell ，提供了稳定的凭证缓存和健全的 CRLF 设置。


实际安装过程参见 [Git](/software/git/README.md)


## Installing from Source


# First-Time Git Setup
`git config` 配置变量存储在

- /etc/gitconfig - 使用 --system 选项， applied to every user on the system and all their repositories.
- ~/.gitconfig 或 ~/.config/git/config - 使用 --global 选项， affects all of the repositories you work with on your system.
- .git/config - **默认**，使用 --local 选项， specific to that single repository


local 优先级最高， system 最低

在 windows 下对应

- `D:\Git\etc\gitconfig`
- `C:\Users\$USER\.gitconfig`
- `.git\config`


> If you are using version 2.x or later of Git for Windows, there is also a system-level config file at `C:\Documents and Settings\All Users\Application Data\Git\config` on Windows XP, and in `C:\ProgramData\Git\config` on Windows Vista and newer. This config file can only be changed by `git config -f <file>` as an admin.

当使用 Git for Windows 2.x 时，在 Windows 下还有一个 system level config file 在 C:\ProgramData\Git\config 下，但只能通过 git config -f 修改。


## Your Identity

    me@mypc:~$ git config --global user.name me
    me@mypc:~$ git config --global user.email me@example.com
    me@mypc:~$ 


## Your Editor
默认使用 vim ，可以修改为 emacs

    git config --global core.editor emacs


在 Windows 下可以改为 Notepad++

    git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"


## Checking Your Settings
在 Linux 下

    me@mypc:~$ git config --list
    user.email=me@example.com
    user.name=me
    me@mypc:~$ 


在 windows 下

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


> You may see keys more than once, because Git reads the same key from different files (`/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

Git 会从不同的文件中读取同一个配置，因此可能有重复的配置名，则将使用最后一个配置。


可以使用 `git config <key>` 检查配置实际起作用的值。

    me@mypc:~$ git config user.name
    me
    me@mypc:~$ git config user.email
    me@example.com
    me@mypc:~$ 

使用 `git config --show-origin` 得到配置值的 origin(which configuration file)

    git config --show-origin user.name


# Getting Help
参见 [git help](/software/git/help.md)


# Summary
