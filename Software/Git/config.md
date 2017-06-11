几种使用方式
- git config name value
- git config -l/--list
- git config name


# git config name value
```bash
me@mypc:~$ git config --global user.name me
me@mypc:~$ git config --global user.email me@example.com
me@mypc:~$ 
```


# git config -l/--list
在 Linux 下
```bash
me@mypc:~$ git config --list
user.email=me@example.com
user.name=me
me@mypc:~$ 
```


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


Git 会从不同的文件中读取同一个配置，因此可能有重复的配置名，则将使用最后一个配置。


# git config name
可以使用 `git config name` 检查配置实际起作用的值。


```bash
me@mypc:~$ git config user.name
me
me@mypc:~$ git config user.email
me@example.com
me@mypc:~$ 
```


# file option
- --global
- --system
- --local
- -f/--file


`git config` 配置变量存储在
- /etc/gitconfig - 使用 --system 选项
- ~/.gitconfig 或 ~/.config/git/config - 使用 --global 选项
- .git/config - 默认


在 windows 下对应
- D:\Git\etc\gitconfig
- C:\Users\\$USER\.gitconfig
- .git/config


当使用 Git for Windows 2.x 时，在 Windows 下还有一个 system level config file 在 C:\ProgramData\Git\config 下，但只能通过 git config -f 修改。


# options
## --unset and --remove-section
```bash
me@mypc:~$ cat .gitconfig
[user]
	email = me@example.com
	name = me
me@mypc:~$ git config --global x.y xxyy
me@mypc:~$ cat .gitconfig
[user]
	email = me@example.com
	name = me
[x]
	y = xxyy
me@mypc:~$ git config --global --unset x.y
me@mypc:~$ cat .gitconfig
[user]
	email = me@example.com
	name = me
[x]
me@mypc:~$ git config --global --remove-section x
me@mypc:~$ cat .gitconfig
[user]
	email = me@example.com
	name = me
me@mypc:~$ 
```


# variables
Each variable must belong to some section
```bash
me@mypc:~$ git config --global x xx
error: key does not contain a section: x
```


可用的 variables
- user.name
- user.email


## core.editor
默认使用 vim ，可以修改为 emacs
```bash
git config --global core.editor emacs
```


在 Windows 下可以改为 Notepad++
```bash
git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```


# Reference
- https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup
