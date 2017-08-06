术语
- block-level HTML tags - div, table, p, pre, etc.
- span-level HTML tags - span, cite, del, a, img
- hard-wrapped/hard breaks - Markdown supports hard-wrapped text paragraphs, 即将连续的多行视为一行，不会将每行的换行视为 br tag


# Overview
## Inline HTML
markdown 文档中可以使用 HTML tag ，但是 block-level HTML elements(div, table, p, pre, etc.) 需要在前后加上空行，并且 the start and end tags 前后不能有 tabs or spaces 。


block-level HTML tags 中不能使用 markdow 语法。


Span-level HTML tags(span, cite, del, a, img)可以与 markdown 一起使用。即 can be used anywhere in a Markdown paragraph, list item, or header. 并且 Markdown syntax is processed within span-level tags.


## Automatic Escaping for Special Characters
Markdown 文档中可以使用 &, < 字符，不需要 escape 。即可以在 markdown 文档中
```
&copy;
AT&T
4 < 5
<a>
```


结果
- &copy;
- AT&T
- 4 < 5
- <a>xx</a>


但是，在 Markdown code spans and blocks 中， &, < 字符将总是被 encoded 。这方便 markdown 写 HTML code


# Block Elements
## Paragraphs and Line Breaks
段落不能用 spaces or tabs 缩进。段落用空行分隔。只包含 spaces or tabs 的行认为是空行。


markdown 不会将换行转为 &lt;br> ，如果确实需要 br 则要在行尾加上两个以上的空格，然后再换行。


## Headers
有两种 header 样式：
*Setext - =/- 的数目无所谓
*atx - 可以 close header


Setext 例子
```markdown
This is an H1
=============

This is an H2
-------------
```


atx close header 的例子
```markdown
# This is an H1 #

## This is an H2 ##

### This is an H3 ######
```


如果 close 和 open 的 # 的数目不一致，以 open 的 # 的数目为准。


## Blockquotes
Blockquotes 可以只在 hard-wrapped 段落的第一行加 > 标记
```markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```


嵌套 Blockquotes
```markdown
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```


Blockquotes 中可以包含 markdown elements, including headers, lists, and code blocks:
```markdown
> ## This is a header.
> 
> 1.   This is the first list item.
> 2.   This is the second list item.
> 
> Here's some example code:
> 
>     return shell_exec("echo $input | $markdown_script");
```


## Lists
列表可以使用 *, +, -
```markdown
+   Red
+   Green
+   Blue
```


List markers typically start at the left margin, but may be indented by up to three spaces. List markers must be followed by one or more spaces or a tab.


如果列表项间有空行
```markdown
*   Bird

*   Magic
```


将生成
<syntaxhighlight lang="html5" line="GESHI_NORMAL_LINE_NUMBERS">
<ul>
<li><p>Bird</p></li>
<li><p>Magic</p></li>
</ul>
```


如果列表中某项有多个段落，则第二个及以后的段落要缩进 4 spaces or one tab
```markdown
1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

    > This is a blockquote
    > inside a list item.
2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```


如果列表中某项有 code block 则 code block 要缩进两次，即 8 spaces or two tabs
```markdown
*   A list item with a code block:

        <code goes here>
```


## Code Blocks
code blocks 中不能使用 markdown syntax


## Horizontal Rules
在一行中使用三个以上的 *, -, _  制造横线(hr), If you wish, you may use spaces between the hyphens or asterisks.
```markdown
*****

- - -

---------------------------------------
```


# Span Elements
## Links
inline link
```markdown
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

See my [About](/about/) page for details.
```


Reference-style links
```markdown
This is [an example][id] reference-style link.
```


You can optionally use a space to separate the sets of brackets, 即 an example 和 id 的 bracket 之间可以有空格。


然后在文档中某处
```markdown
[id]: http://example.com/  "Optional Title Here"

[id]: <http://example.com/>  "Optional Title Here"

[foo]: http://example.com/  "Optional Title Here"
[foo]: http://example.com/  'Optional Title Here'
[foo]: http://example.com/  (Optional Title Here)

[id]: http://example.com/longish/path/to/resource/here
    "Optional Title Here"
```


注意
- Square brackets containing the link identifier (optionally indented from the left margin using up to three spaces);
- : 后面 followed by one or more spaces (or tabs);
- url 可以用尖括号括起来
- title 可以用单引号，双引号或者圆括号括起来。
- title 可以在另一行使用 spaces or tabs for padding


link definition name(例子中的 id)不区分大小写


Link definitions are only used for creating links during Markdown processing, and are stripped from your document in the HTML output.


implicit link name 使用 link text 作为 link name
```markdown
Visit [Daring Fireball][] for more information.
[Daring Fireball]: http://daringfireball.net/
```


使用 reference-style links 文档更可读。


## Emphasis
如果 * or _ 两侧是空白，则认为是字面量，而不是表示加粗或斜体。


## Code
如果要在 code span 中使用 \` 则可以用两个 \` 包围 code span
```markdown
``There is a literal backtick (`) here.``
```


code span 两侧的 ` 需要与 code span 之间有空格。这样可以在 code span 的最开始和最后有 ` 字符。
```markdown
A single backtick in a code span: `` ` ``

A backtick-delimited string in a code span: `` `foo` ``
```


code span 中可以使用 &, < 不需要转义
```markdown
Please don't use any `<blink>` tags.
```


## Images
Inline image syntax
```markdown
![Alt text](/path/to/img.jpg)

![Alt text](/path/to/img.jpg "Optional title")
```


Reference-style image syntax
```markdown
![Alt text][id]
[id]: url/to/image  "Optional title attribute"
```


Markdown 不支持指定 image 的大小(dimensions)。可以改用 html img tag


# Miscellaneous
## Automatic Links
automatic links
```markdown
<http://example.com/>
```


Automatic links for email addresses
```markdown
<address@example.com>
```
会生成
```html
<a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>
```
即
```html
<a href="mailto:address@example.com">address@example.com</a>
```
这可以逃避垃圾邮件检查。


## Backslash Escapes
Markdown 可以使用 \ escape
```markdown
\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark
```


其中 {} 好像没有在 markdown 中用到。


# Reference
- https://daringfireball.net/projects/markdown/syntax