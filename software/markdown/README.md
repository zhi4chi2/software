术语
- block-level HTML tags - div, table, p, pre, etc.
- span-level HTML tags - span, cite, del, a, img
- hard-wrapped/hard breaks - Markdown supports hard-wrapped text paragraphs, 即将连续的多行视为一行，不会将每行的换行视为 br tag 。副作用是对于 block-level elements 需要在后面都加上空行。
- code block - 用 4 spaces or one tab 缩进的代码块，会解释为 &lt;pre> and &lt;code> tag
- code span - 用一个 \` 包含的代码，会解释为 &lt;code> tag
- 4 spaces or one tab - markdown 中大量使用 4 spaces or one tab 表示一层缩进。例如表示 code block, 或者表示 list item 中的 subsequent paragraph


Block Elements
- Paragraphs and Line Breaks
- Headers
- Blockquotes
- Lists
- Code Blocks
- Horizontal Rules


Span Elements
- Links
- Emphasis
- Code
- Images


# Overview
## Inline HTML
markdown 文档中可以使用 HTML tag ，但是 block-level HTML elements(div, table, p, pre, etc.) 需要在前后加上空行，并且 the start and end tags 前后不能有 tabs or spaces 。


The only restrictions are that block-level HTML elements — e.g. &lt;div>, &lt;table>, &lt;pre>, &lt;p>, etc. — must be separated from surrounding content by blank lines, and the start and end tags of the block should not be indented with tabs or spaces.


block-level HTML tags 中不能使用 markdow 语法。


Span-level HTML tags(span, cite, del, a, img)可以与 markdown 一起使用。即 can be used anywhere in a Markdown paragraph, list item, or header. 并且 Markdown syntax is processed within span-level tags.


## Automatic Escaping for Special Characters
Markdown 文档中可以使用 &, < 字符，不需要 escape 。即可以在 markdown 文档中
```markdown
- &copy;
- AT&T
- 4 < 5
- <a id="xx">xx</a>
```


实际效果
- &copy;
- AT&T
- 4 < 5
- <a id="xx">xx</a>


规则是：
- If you use an ampersand(&) as part of an HTML entity, it remains unchanged; otherwise it will be translated into &amp;amp;.
- if you use angle brackets(<) as delimiters for HTML tags, Markdown will treat them as such. otherwise it will be translated into &amp;lt;.


但是，在 Markdown code spans and blocks 中， &, < 字符将总是被 encoded 。这方便 markdown 写 HTML code


Block Elements
=
## Paragraphs and Line Breaks
段落不能用 spaces or tabs 缩进（否则可能认为是 code block ）。段落用空行分隔。只包含 spaces or tabs 的行认为是空行。


Normal paragraphs should not be indented with spaces or tabs.


markdown 不会将换行转为 &lt;br> ，如果确实需要 br 则要在行尾加上两个以上的空格，然后再换行。


markdown 的这种(hard-wrapped)方式，使得 blockquoting and multi-paragraph list items work best — and look better


Headers
-

有两种 header 样式：
- Setext - =/- 的数目无所谓。但 = 只能表示 h1 ，相当于 #。 - 只能表示 h2 ，相当于 ##
- atx - 可以(Optionally) close header


Setext 例子参见上面的 [Block Elements](#block-elements), [Headers](#headers)


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


实际效果
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.


但在每一行都加 > 标记会比较好看(looks best)。


嵌套 Blockquotes
```markdown
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```


实际效果
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.


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


实际效果
> ## This is a header.
> 
> 1.   This is the first list item.
> 2.   This is the second list item.
> 
> Here's some example code:
> 
>     return shell_exec("echo $input | $markdown_script");


## Lists
列表可以使用 *, +, -


在每行前加数字（还要有个 "." ）创建有序列表
```markdown
1. James Madison
2. James Monroe
4. John Quincy Adams
```


实际效果
1. James Madison
2. James Monroe
4. John Quincy Adams


实际显示为 1,2,3 即 `4. John Quincy Adams` 显示为 `3. John Quincy Adams` 。这是因为实际转为 html ol tag 因此值由 html 重新计算。但是注意第一项必须从 1 开始！


If you do use lazy list numbering, however, you should still start the list with the number 1.


List markers typically start at the left margin, but may be indented by up to three spaces(因为 4 个空格就认为是 code block 了). List markers must be followed by one or more spaces or a tab.


```markdown
   +     Red
 +   Green
 +   Blue
```


实际效果
   +     Red
 +   Green
 +   Blue


注意，如果 list markers 后面有 4 个以上(>4, 因为 list marker 后需要至少一个空格才能接 item 值)空格，则认为是 code block ，如例子中(5 个空格)的 Red


如果列表项间有空行
```markdown
*   Bird

*   Magic
```


将生成
```html
<ul>
<li><p>Bird</p></li>
<li><p>Magic</p></li>
</ul>
```


实际效果
*   Bird

*   Magic


如果列表中某项有多个段落(即 li 中有多个 p)，则第二个及以后的段落要缩进 4 spaces or one tab
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


实际效果
1.  This is a list item with two paragraphs. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit. Aliquam hendrerit
mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
sit amet velit.

    > This is a blockquote
    > inside a list item.
2.  Suspendisse id sem consectetuer libero luctus adipiscing.


每一行都 hanging indents 会比较好看(look nice)，即
1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.



如果列表中某项有 code block 则 code block 要缩进两次，即 8 spaces or two tabs
```markdown
*   A list item with a code block:

        function test(){
        }
```


实际效果
*   A list item with a code block:

        function test(){
        }


## Code Blocks
One level of indentation — 4 spaces or 1 tab — is removed from each line of the code block. 即 code block 用 4 spaces or 1 tab 缩进。


A code block continues until it reaches a line that is not indented (or the end of the article).


code blocks 中不能使用 markdown syntax


## Horizontal Rules
在一行中使用三个以上的 \*, -, _  制造横线(hr), If you wish, you may use spaces between the hyphens or asterisks.
```markdown
*****

- - -

---------------------------------------
```


实际效果
*****

- - -

---------------------------------------


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


例子
```markdown
This is [an example] [id] reference-style link.

some other text

[ID]: http://example.com/longish/path/to/resource/here
    "Optional Title Here"
```


实际效果

This is [an example] [id] reference-style link.

some other text

[ID]: http://example.com/longish/path/to/resource/here
    "Optional Title Here"


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

some other text

[Daring Fireball]: http://daringfireball.net/
```


实际效果

Visit [Daring Fireball][] for more information.

some other text

[Daring Fireball]: http://daringfireball.net/


使用 reference-style links 文档更可读。


## Emphasis
如果 * or _ 两侧是空白，则认为是字面量，而不是表示加粗或斜体。


- 使用 \*\* / \_\_ 表示加粗
- 使用 \* / \_ 表示斜体
- 使用 \*\*, \_ 表示加粗斜体


```markdown
- **This is bold text**
- __This is bold text also__
- *This text is italicized*
- _This text is italicized also_
- **This text is _extremely_ important**
- ** 第二个星号不紧邻文字，而是之间有空格间隔，则视为字面量，只显示为斜体 **
```


实际效果
- **This is bold text**
- __This is bold text also__
- *This text is italicized*
- _This text is italicized also_
- **This text is _extremely_ important**
- ** 第二个星号不紧邻文字，而是之间有空格间隔，则视为字面量，只显示为斜体 **


## Code
如果要在 code span 中使用 \` 则可以用两个 \` 包围 code span
```markdown
``There is a literal backtick (`) here.``
```


实际效果

``There is a literal backtick (`) here.``


code span 两侧的 \` 可以与 code span 之间有空格。这样可以在 code span 的最开始和最后有 \` 字符。
```markdown
A single backtick in a code span: `` ` ``

A backtick-delimited string in a code span: `` `foo` ``
```


实际效果

A single backtick in a code span: `` ` ``

A backtick-delimited string in a code span: `` `foo` ``


code span 中可以使用 &, < 不需要转义
```markdown
Please don't use any `<blink>` tags.

`&#8212;` is the decimal-encoded equivalent of `&mdash;`.
```


实际效果

Please don't use any `<blink>` tags.

`&#8212;` is the decimal-encoded equivalent of `&mdash;`.


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


实际效果
<http://example.com/>


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


实际效果
<address@example.com>


## Backslash Escapes
Markdown 可以使用 \ escape
```markdown
\   escape
`   code span
*   lists, hr, emphasis
_   hr, emphasis
{}
[]  links, images
()  links, images
#   headers
+   lists
-   lists, hr, headers
.   order lists
!   images
```


有些特殊字符重复了，可以只使用 - 表示 list, _ 表示 hr, * 表示 emphasis 避免歧义。


其中 \{\} 好像没有在 markdown 中用到。


另外还有特殊字符没有说能不能 escape
- = - header
- > - block quote


# 最佳实践
- 可以只使用 - 表示 list, _ 表示 hr, * 表示 emphasis 避免歧义。
- 对 Block Elements 前后都加上空行！！！
- 如果 Blockquotes 有多行，可以在每行前加 > ，会比较好看(looks best)。英文单词间本就有空格，但中文的话会导致添加额外的空格
- 如果 List item 有多行，可以悬挂缩进，会 look nice 。英文单词间本就有空格，但中文的话会导致添加额外的空格
- 如果 List item 有多个段落，可以每行都缩进， looks nice 。英文单词间本就有空格，但中文的话会导致添加额外的空格
- 尽量使用 Reference-style links 而不是 inline link


# 不足
Markdown's formatting syntax only addresses issues that can be conveyed in plain text.

Markdown 只做可以用纯字符表达的格式。


可能有些插件能办到
- 不能表示嵌套列表(GitHub Flavored Markdown 可以)
- 没有 TOC
- 显示代码无法显示行号，无法高亮某行
- 没有定义引用列表(du/dl)的方式


bug
- 不能在 markdown 文档中用 `<span id="list-item-problem"></span>` 方式插入锚点，生成的 HTML 会把 id 去除。用 a 标签也不行， a 标签的 id 会被替换。


# 测试
## Block Elements 前后的空行
**最佳实践：对 Block Elements 前后都加上空行！！！**


当前测试结果
- Paragraphs 前后都需要空行
- Headers 前后都不需要空行。前不需要空行是因为它们都由特定的字符开头。 Setext 风格的 Header 前也不需要空行。后不需要空行，是因为它们不会跨行。
- Blockquotes **后需要有空行**。前不需要空行是因为它们都由特定的字符开头。
- Lists **后需要有空行，且下一行要从行首开始，不然仍认为是 list item 的一部分**，参见 [list item 空行问题](#list-item-problem)。前不需要空行是因为它们都由特定的字符开头。
- Code Blocks **前需要有空行**，否则成为前一个段落的一部分。后不需要空行，是因为 code block 每行都必须以 4 spaces or one tab 开头。
- Horizontal Rules 前后都不需要空行。前不需要空行是因为它们都由特定的字符开头。后不需要空行，是因为它们不会跨行。如果使用 - 表示 Horizontal Rules 则前需要空行，否则将表示 Setext 风格的 Header ！


测试在 https://daringfireball.net/projects/markdown/dingus 中 Lists 前需要空行！在 GitHub Flavored Markdown 中前面可以不需要空行。


```markdown
some text
# header
some text
> blockquotes

some text
- x
- y

some text

    function(){
    }
some text
***
some text

---
```


实际效果

some text
# header
some text
> blockquotes

some text
- x
- y

some text

    function(){
    }
some text
***
some text

---


### list item problem
如果 list item 后不是新的段落的开始，将始终认为是 list item 的一部分，例如
```markdown
- x


    function(){
    }
```


实际效果为
- x


    function(){
    }

本意是希望 function 是 code block ，但实际显示为 list item 的一部分。 list item 直到遇到新的段落开始（前一行是空白，本行从行开头就有字符）才结束。


# Reference
- https://daringfireball.net/projects/markdown/syntax
- https://daringfireball.net/projects/markdown/dingus 试验语法效果
