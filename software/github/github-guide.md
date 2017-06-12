# Understanding the GitHub Flow
https://guides.github.com/introduction/flow/ 中有个 Deploy 不明白何意。

Once your pull request has been reviewed and the branch passes your tests, you can deploy your changes to verify them in production. If your branch causes issues, you can roll it back by deploying the existing master into production.


# Hello World
https://guides.github.com/activities/hello-world/


# Getting Started with GitHub Pages
https://guides.github.com/features/pages/

- repository 名字必须是 username.github.io
- 在 repository 的 Settings 下在 GitHub Pages 区域选择 Theme
- https://username.github.io/ 默认显示 README.md 如果有 index.md 则显示 index.md


# Getting your project on GitHub
https://guides.github.com/introduction/getting-your-project-on-github/


# Forking Projects
https://guides.github.com/activities/forking/


# Be Social
https://guides.github.com/activities/socialize/

在 https://github.com/stars 中可以看到 friend(following) star 的 projects


# Making Your Code Citable
https://guides.github.com/activities/citable-code/


# Mastering Issues
https://guides.github.com/features/issues/

在 https://github.com/notifications 按 ? 显示可用的快捷键。

建议使用 "/cc @kneath @jresig" 方式通知某人。

使用 # 关联 issue ，例如 "Hey @kneath, I think the problem started in #42" 这会在 issue #42 上创建 event

还可以关联其它 repository 的 issue 例如 "kneath/example-project#42"

在 commit message 中使用 "Fixes", "Fixed", "Fix", "Closes", "Closed", or "Close" 加上 #issue ，会在 commit merged into master 时自动关闭 issue 。例如 "Fixed #19"

search issue 的方式参见 https://help.github.com/articles/using-search-to-filter-issues-and-pull-requests


# Mastering Markdown
https://guides.github.com/features/mastering-markdown/


# Documenting your projects on GitHub
https://guides.github.com/features/wikis/

README.md 可以包含
- Project name
- Description
- Table of Contents
- Installation
- Usage
- Contributing
- Credits
- License

选择 license 参见 http://choosealicense.com/

GitHub Wiki 支持很多种 markup format(http://github.com/github/markup)

名叫 Home 的页面，会作为 wiki 的入口。如果没有这个页面，则默认是 table of contents

参见 https://help.github.com/articles/adding-and-editing-wiki-pages-locally

# Reference
- https://guides.github.com/