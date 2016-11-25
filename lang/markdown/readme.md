### 0.前言

本文仅是我对markdown的学习心得笔记，会不定时间更新。个人习惯性的在系统学习前，先进行一些资料的学习整理和收集。

更新日志:

### 0.1相关资料

1. [Markdown(官方)文档][1] [中文翻译][2]
2. [GitHub的简明Markdown包含GFM的教程][3]
3. [CheatSheet][4]
4. [Wiki百科的介绍][5]


[1]: https://daringfireball.net/projects/markdown/syntax
[2]: http://wowubuntu.com/markdown/
[3]: https://guides.github.com/features/mastering-markdown/
[4]: https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf
[5]: https://zh.wikipedia.org/wiki/Markdown
[6]: https://daringfireball.net/projects/markdown/

### 1.什么是Markdown

Markdown发明者的设计思想

> ​	The overriding design goal for Markdown’s formatting syntax is to make it as readable as possible. The idea is that a Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions. While Markdown’s syntax has been influenced by several existing text-to-HTML filters, the single biggest source of inspiration for Markdown’s syntax is the format of plain text email.

1. Markdown是一种轻量级的、可读性强的文本标记语言，适合编写文档，并且通过Markdown程序转换成对应的HTML脚本（本质上是把MD标记翻译成HTML标签，所以HTML标签也可以在MD文档中使用）。

2. Markdown的语法简单，只需要用到几种简单的标记即可完成。

github的简单描述:


###2.什么是GFM/gfm?
​	GFM即*GitHub-Flavored-Markdown*。是github所支持的md标记,在普通md标记的基础上又增加了（为什么说是普通的而不是标准的，目前看来还没有标准的MD语法定义）一些扩展，例如emoji表情支持、TaskList支持等。

###3.Markdown语法整理

其实官方的文档说明已经很详实了，这里仅记录一些要点。

#### 3.1标签们

MD中的标签元素分为下面三大类

#####3.1.1区块元素

+ 标题(`#`)

  1. 标题对应HTML中的H标签，故只有H1-H6级标签，另外一级和二级标签可以通过(`-------`)和(`=========`)表示。

  2. 如果使用`#`标记，那么不需要进行闭合。例如（`###三级标题`）就表示是H3了，后面不需要闭合。

+ 区块引用 (`>`)

  1. 一个段落一般只要在行首插入区块引用元素即可。

  2. 区块引用可以嵌套，多级引用。

  3. 区块引用中可以嵌套其它的MD标记。

+ 代码片段
  1. 代码片段跟段落一样，没有可见的标记。通过四个空格或者一个TAB的缩进来表示后续代码片段的开始。如果后续行没有缩进，表示代码区段的结束。

+ 段落和换行
  1. 注意段落没有任何可见的元素，段落由一行或者多行文本构成，MD中通过一个前置空行表示一个段落的开始。
  2. 因为MD最终转换为HTML，所以一般不要自行换行，浏览器会自动布局。
  3. 换行可以通过插入<br>标签或者，后面跟两个以上空格外加回车实现。
+ 列表
  1. MD中的列表分为有序列表和无序列表。

  2. 无序列表以`+`、`-`、`*`  开头表示。

  3. 有序列表以数字.的形式表示例如

     > 	1. 列表1
     > 	2. 列表2

  4. 有序列表前面的数字并不表示真实的列表顺序，只是符合文法，建议按照顺序填写(万一后面MD支持根据数字排序的功能了):

     >	1. 列表1
     >	1. 列表2

     最终呈现的结果和3中的一样。  
+ 分割线(`*-`)
  1. 分割线通过使用`*`、`-`描述，一行内有三个重复的符号即可形成分割线，注意行内不能有其它字符。

#####3.1.2区段元素

+ 超链接
  1. 超链接可以有参考式`[name][id] --> [id]: url "title"`、内联形式 `[name](url "title")`、隐式链接`[name][]  --> [name]: url "title"`（类似于参考式）。这里的title是<A>中的title属性可以省略,而name则是锚文本字面。
  2. 参考式和隐式链接其实分为两个步骤：第一，文字编写中插入标记。第二个步骤是对所插入的链接进行定义（有点像写论文中的资料引用，这个定义可以放到MD文档任何地方）。注意一点：这种链接的定义如果没有被上面两种标记引用到就不会出现在最终的文档中（MD转换成HTML）。
+ 图片
  1. 图片也有参考式`![name][id] --> [id]: url "title"` (和超链接的参考式很像很像)和内联式`![name](imgurl "title")`两种。
  2. MD目前无法支持指定图片的尺寸，所以有的时候在MD编写中插入图片就比较麻烦，没有传统编辑器一样可以调整大小，不过可以用`<IMG>`标签。
+ 代码
  1. 使用`` ` ``标记这里有别于代码区段，只是用于行内的代码插入。
  2. 注意点如果 代码中要插入反引号（反引号是代码标记），则需要通过两个反引号开始和结束。

#####3.1.3其他标签

###关于编辑器

目前生活工作基本是linux desktop和osx。自己使用的是emacs markdown-mode 外挂markdown可以perview。
近期也开始尝试bear,mou,macdown等工具，等体验之后再分享。

知乎讨论:https://www.zhihu.com/question/22700184