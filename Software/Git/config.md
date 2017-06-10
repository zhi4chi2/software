```bash
me@mypc:~$ git config --global user.name me
me@mypc:~$ git config --global user.email me@example.com
me@mypc:~$ 
```


# 选项
- --global
- --system


## --list
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


# key
可以使用 `git config key` 检查配置实际起作用的值。


```bash
me@mypc:~$ git config user.name
me
me@mypc:~$ git config user.email
me@example.com
me@mypc:~$ 
```


可用的 key
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


