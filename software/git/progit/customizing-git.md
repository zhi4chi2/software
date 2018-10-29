# Git Configuration
## Basic Client Configuration
> The configuration options recognized by Git fall into two categories: client-side and server-side.

### core.editor
> By default, Git uses whatever you’ve set as your default text editor via one of the shell environment variables `VISUAL` or `EDITOR`, or else falls back to the `vi` editor to create and edit your commit and tag messages. To change that default to something else, you can use the `core.editor` setting


### commit.template
> The value in creating a custom commit template is that you can use it to remind yourself (or others) of the proper format and style when creating a commit message.

预处理

`~/.gitmessage.txt`

    Subject line (try to keep under 50 characters)
    
    Multi-line description of commit,
    feel free to be detailed.
    
    [Ticket: X]

预执行

    cd
    rm -rf test
    mkdir test
    cd test/
    git init
    git config commit.template ~/.gitmessage.txt
    touch README
    git add .
    clear

执行

    git commit

**执行结果**

FIXME


### core.pager
> This setting determines which pager is used when Git pages output such as `log` and `diff`. You can set it to `more` or to your favorite pager (by default, it’s `less`)


### user.signingkey
FIXME


### core.excludesfile
FIXME


### help.autocorrect
FIXME


### Colors in Git
FIXME


### External Merge and Diff Tools
FIXME


### Formatting and Whitespace
#### core.autocrlf
> many editors on Windows silently replace existing LF-style line endings with CRLF

- CR - carriage-return
- LF - linefeed

> Git can handle this by auto-converting CRLF line endings into LF when you add a file to the index, and vice versa when it checks out code onto your filesystem. You can turn on this functionality with the `core.autocrlf` setting. If you’re on a Windows machine, set it to `true` — this converts LF endings into CRLF when you check out code:
> 
>     $ git config --global core.autocrlf true

> If you’re on a Linux or Mac system that uses LF line endings, then you don’t want Git to automatically convert them when you check out files; however, if a file with CRLF endings accidentally gets introduced, then you may want Git to fix it. You can tell Git to convert CRLF to LF on commit but not the other way around by setting core.autocrlf to input:
> 
>     $ git config --global core.autocrlf input
> 
> This setup should leave you with CRLF endings in Windows checkouts, but LF endings on Mac and Linux systems and in the repository.


#### core.whitespace
> It can look for six primary whitespace issues — three are enabled by default and can be turned off, and three are disabled by default but can be activated.

three that are turned on by default

- blank-at-eol - looks for spaces at the end of a line
- blank-at-eof - notices blank lines at the end of a file
- space-before-tab - looks for spaces before tabs at the beginning of a line


three that are disabled by default

- indent-with-non-tab - looks for lines that begin with spaces instead of tabs (and is controlled by the `tabwidth` option);
- tab-in-indent - watches for tabs in the indentation portion of a line
- cr-at-eol - tells Git that carriage returns at the end of lines are OK

> You can tell Git which of these you want enabled by setting `core.whitespace` to the values you want on or off, separated by commas. You can disable an option by prepending a `-` in front of its name, or use the default value by leaving it out of the setting string entirely.

> For example, if you want all but `space-before-tab` to be set, you can do this (with `trailing-space` being a short-hand to cover both `blank-at-eol` and `blank-at-eof`):
> 
>     $ git config --global core.whitespace trailing-space,-space-before-tab,indent-with-non-tab,tab-in-indent,cr-at-eol

实际可以只设置 customizing part only

>     $ git config --global core.whitespace -space-before-tab,indent-with-non-tab,tab-in-indent,cr-at-eol

> Git will detect these issues when you run a `git diff` command and try to color them so you can possibly fix them before you commit.


> It will also use these values to help you when you apply patches with `git apply`. When you’re applying patches, you can ask Git to warn you if it’s applying patches with the specified whitespace issues:
> 
>     $ git apply --whitespace=warn <patch>
> 
> Or you can have Git try to automatically fix the issue before applying the patch:
> 
>     $ git apply --whitespace=fix <patch>

> These options apply to the `git rebase` command as well. If you’ve committed whitespace issues but haven’t yet pushed upstream, you can run `git rebase --whitespace=fix` to have Git automatically fix whitespace issues as it’s rewriting the patches.


### Server Configuration
FIXME


# Git Attributes
