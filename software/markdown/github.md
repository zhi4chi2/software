GitHub 使用 GitHub Flavored Markdown


GitHub Flavored Markdown 在 markdown 上添加了
- @mentions
- links to issues and pull requests
- emoji


# Basic writing and formatting syntax
https://help.github.com/articles/basic-writing-and-formatting-syntax/


使用 \~\~ 表示删除，例如 `~~This was mistaken text~~` 显示为 ~~This was mistaken text~~


如果在 comment 中包含 URL 则 GitHub 会自动创建 links 。


You can create nested ordered and unordered combination lists by indenting lines by four spaces.


在行前缩进**四**个空白创建**混合 ordered and unordered** 的嵌套列表
```markdown
1. Make my changes
    * Fix bug
    - Improve formatting
```


实际效果
1. Make my changes
    * Fix bug
    - Improve formatting


注意，如果 parent list 是 unordered 的嵌套列表，可以只缩进两个空格。
```markdown
- x
  1. y
  1. z
```


实际效果
- x
  1. y
  1. z


只有 parent list 是 ordered 的嵌套列表，才必须缩进四个空格。
```markdown
1. x
    1. y
```


实际效果
1. x
    1. y


与 - / * 一起使用 [ ] 创建 task list ，使用 [x] 表示 task 已完成
```markdown
- [x] Finish my changes
- [ ] Push my commits to GitHub
```


实际效果
- [x] Finish my changes
- [ ] Push my commits to GitHub


如果某个 task 以 () 开头，则需要用 \ escape
```markdown
- [ ] \(Optional) Open a followup issue
- [ ] (Optional) Open a followup issue
```


实际效果
- [ ] \(Optional) Open a followup issue
- [ ] (Optional) Open a followup issue


早期第二行显示不正确， \[ \] \(Optional\) 都不显示，可能是与 link 语法冲突的原因。如今两行都可以正确显示！


在 issue, pull request, comment 中通过 @ 会给某人或某个 team (包括 child teams)全体成员发 notification
```markdown
@github/support What do you think about these updates?
```


实际效果参见 https://github.com/zhi4chi2/software/issues/1


在 issue, pull request, comment 中通过 # 加 issue or PR number or title 引用 issues and pull requests ，参见 https://github.com/zhi4chi2/software/pull/2


使用 :EMOJICODE: 添加 emoji 参见 http://emoji-cheat-sheet.com/
```markdown
@octocat :+1: This PR looks great - it's ready to merge! :shipit:
```


实际效果 @octocat :+1: This PR looks great - it's ready to merge! :shipit:


# Working with advanced formatting
https://help.github.com/articles/working-with-advanced-formatting/


## Organizing information with tables
https://help.github.com/articles/organizing-information-with-tables/


例子
```markdown
| Command | Description |
| --- | --- |
| git status | List all new or modified files |
| git diff | Show file differences that haven't been staged |
```


实际效果

| Command | Description |
| --- | --- |
| git status | List all new or modified files |
| git diff | Show file differences that haven't been staged |


注意
- \- 分隔 header ，至少要有三个 \-
- 两边的 | 可以省略
- 列宽不需要一样


使用 : 表示左对齐、右对齐或中间对齐
```markdown
| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |
```


实际效果

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |


如果单元格内容中有 | 则使用 \ escape


## Creating and highlighting code blocks
https://help.github.com/articles/creating-and-highlighting-code-blocks/


GitHub 使用 Linguist(https://github.com/github/linguist) 探测语言并语法高亮。


支持的语言参见 https://github.com/github/linguist/blob/master/lib/linguist/languages.yml


其中的 key 是 language name, 对应的 value 中的 aliases 是别名(隐式包含 name.downcase)。例如第 2024 行
```yml
Java:
  type: programming
  ace_mode: java
  codemirror_mode: clike
  codemirror_mime_type: text/x-java
  color: "#b07219"
  extensions:
  - ".java"
language_id: 181
```
则 name 是 Java, aliases 隐式包含 java 。即用 Java/java 都可以


常用的有：
- java
- jsp
- html
- javascript/js
- json
- bat - dos cmd/bat
- shell/bash
- yaml/yml


## Autolinked references and URLs
https://help.github.com/articles/autolinked-references-and-urls/


在 issue, pr, comment 中指向 issues and pull requests 的引用会被转为短 link ，参见 https://github.com/zhi4chi2/software/pull/2
- https://github.com/zhi4chi2/software/issues/1 - 转为 #1 并自动加链接
- #1 - 自动加链接
- GH-1 - 自动加链接
- zhi4chi2/software#1 - 自动加链接


在 issue, pr, comment 中指向某个提交的 SHA hash 会自动转为短链接，参见 https://github.com/zhi4chi2/software/issues/1
- https://github.com/zhi4chi2/software/commit/9759c4cbe4110a7d3ed0d092b63c94f96df66939 - 转为 9759c4c 加链接
- 9759c4cbe4110a7d3ed0d092b63c94f96df66939 - 转为 9759c4c 加链接
- zhi4chi2@9759c4cbe4110a7d3ed0d092b63c94f96df66939 - 转为 9759c4c 加链接
- zhi4chi2/software@9759c4cbe4110a7d3ed0d092b63c94f96df66939 - 转为 9759c4c 加链接


# Mastering Markdown
https://guides.github.com/features/mastering-markdown/


GitHub Flavored Markdown 的某些特性仅用于 descriptions and comments of Issues and Pull Requests ，这包括
- @mentions
- references to SHA-1 hashes, Issues, and Pull Requests


Task Lists are also available in Gist comments and in Gist Markdown files.


GitHub Flavored Markdown 增加的特性
- Syntax highlighting
- Task Lists
- Tables
- SHA references
- Issue references within a repository
- Username @mentions
- Automatic linking for URLs - Any URL (like http://www.github.com/) will be automatically converted into a clickable link.
- Strikethrough
- Emoji


支持的 emoji 列表在 http://www.emoji-cheat-sheet.com/


# About task lists
https://help.github.com/articles/about-task-lists/


comments 中的 task list 可以点选。 Markdown 文件中的 task list 只读。


You can view task list summary information in issue and pull request lists, when the task list is in the initial comment.


在 comment 中，点击 task checkbox 左边可以拖动 task 以 reorder task lists


# Reference
- https://help.github.com/articles/about-writing-and-formatting-on-github
