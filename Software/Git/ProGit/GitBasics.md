# 获取 Git 仓库
## 在现有目录中初始化仓库
参见 [git init](/Software/Git/init.md)


## 克隆现有的仓库
参见 [git clone](/Software/Git/clone.md)


# 记录每次更新到仓库
## 检查当前文件状态
参见 [git status](/Software/Git/status.md)


## 跟踪新文件
参见 [git status](/Software/Git/status.md)


## 暂存已修改文件
参见 [git status](/Software/Git/status.md)


## 状态简览
参见 [git status](/Software/Git/status.md)


## 忽略文件
文件 .gitignore 的格式规范如下
- 所有空行或者以 # 开头的行都会被 Git 忽略。
- 可以使用标准的 glob 模式匹配
- 匹配模式可以以 / 开头防止递归
- 匹配模式可以以 / 结尾指定目录。
- 不忽略指定模式的文件或目录，可以在模式前加上 ! 取反。


glob 模式是指 shell 所使用的简化了的正则表达式。
- \* 匹配零个或多个任意字符；
- \[abc\] 匹配任何一个列在方括号中的字符；
- ? 只匹配一个任意字符；
- 如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。
- 使用两个星号 \*\* 表示匹配任意中间目录，比如 `a/**/z` 可以匹配 a/z, a/b/z 或 a/b/c/z 等。


GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 https://github.com/github/gitignore 找到它


例子
```
# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```


## 查看已暂存和未暂存的修改
在本书中，我们使用 git diff 来分析文件差异。但是，如果你喜欢通过图形化的方式或其它格式输出方式的话，可以使用 git difftool 命令来用 Araxis, ecmerge 或 vimdiff 等软件输出 diff 分析结果。使用 git difftool --tool-help 命令来看你的系统支持哪些 Git Diff 插件。


参见 [git diff](/Software/Git/diff.md), [git difftool](/Software/Git/difftool.md)


## 提交更新
参见 [git commit](/Software/Git/commit.md)


## 跳过使用暂存区域
参见 [git commit](/Software/Git/commit.md)


## 移除文件
参见 [git rm](/Software/Git/rm.md)


## 移动文件
参见 [git mv](/Software/Git/mv.md)


# 查看提交历史
参见 [git log](/Software/Git/log.md)


# 撤消操作
注意，有些撤消操作是不可逆的。这是在使用 Git 的过程中，会因为操作失误而导致之前的工作丢失的少有的几个地方之一。


参见 [git commit](/Software/Git/commit.md), [git reset](/Software/Git/reset.md), [git checkout](/Software/Git/checkout.md)


# Working with Remotes
参见 [git remote](/Software/Git/remote.md), [git fetch](/Software/Git/fetch.md), [git push](/Software/Git/push.md)
