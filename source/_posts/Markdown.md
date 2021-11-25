---
title: Markdown 语法手册
date: 2021-11-24 09:27:14
tags: Markdown语法
categories: 教程
cover: /img/markdown-guide-og.jpg
---

# 总览

几乎所有 Markdown 应用程序都支持 John Gruber 原始设计文档中列出的 Markdown 基本语法。但是，Markdown 处理程序之间存在着细微的变化和差异，我们都会尽可能标记出来。

# 标题（Headings）

要创建标题，请在单词或短语前面添加井号 (#) 。井号的数量代表了标题的级别。例如，添加三个井号即创建一个三级标题 (&lt;h3&gt;) (例如：### My Header)。

{% tabs test1 %}
<!-- tab 样式预览 -->
# 我是一级标题
## 我是二级标题
### 我是三级标题
#### 我是四级标题
##### 我是五级标题
###### 我是六级标题
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
# 我是一级标题
## 我是二级标题
### 我是三级标题
#### 我是四级标题
##### 我是五级标题
###### 我是六级标题
```
<!-- endtab -->
{% endtabs %}

# 段落（Paragraphs）

要创建段落，请使用空白行将一行或多行文本进行分隔。
段落（Paragraph）用法的最佳实践：除非 段落在列表中，否则不要用空格（spaces）或制表符（ tabs）缩进段落。

{% tabs test1 %}
<!-- tab 样式预览 -->
我是第一行，我喜欢Markdown

我是第二行，我喜欢Markdown
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
我是第一行，我喜欢Markdown

我是第二行，我喜欢Markdown
```
<!-- endtab -->
{% endtabs %}

# 换行（Line Breaks）

在一行的末尾添加两个或多个空格，然后按回车键，即可创建一个换行。

## 换行（Line Break）用法的最佳实践
几乎每个 Markdown 应用程序都支持两个或多个空格进行换行 (称为 “结尾空格（trailing whitespace）”) 的方式，但这是有争议的，因为很难在编辑器中直接看到空格，并且很多人在每个句子后面都会有意或无意地添加两个空格。由于这个原因，你可能需要使用除结尾空格以外的其它方式来进行换行。幸运的是，几乎每个 Markdown 应用程序都支持另一种换行方式：HTML 的 &lt;br&gt; 标签。

为了兼容性，请在行尾添加“结尾空格”或 HTML 的 &lt;br&gt; 标签来实现换行。

还有两种其他方式我并不推荐使用。CommonMark 和其它几种轻量级标记语言支持在行尾添加反斜杠 (\\) 的方式实现换行，但是并非所有 Markdown 应用程序都支持此种方式，因此从兼容性的角度来看，不推荐使用。并且至少有两种轻量级标记语言支持无须在行尾添加任何内容，只须键入回车键（ return）即可实现换行。

# 文本样式强调（Emphasis）

{% tabs test1 %}
<!-- tab 样式预览 -->
1. 我的名字叫**白月紫罗** &nbsp;&nbsp;&nbsp;&nbsp;//粗体
2. 我的名字叫*白月紫罗* &nbsp;&nbsp;&nbsp;&nbsp;//斜体
3. 我的名字叫***白月紫罗*** &nbsp;&nbsp;&nbsp;&nbsp;//粗体加斜体
4. 我的名字叫~~白月紫罗~~&nbsp;&nbsp;&nbsp;&nbsp;//删除线
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
我的名字叫**白月紫罗**  //粗体
我的名字叫*白月紫罗*  //斜体
我的名字叫***白月紫罗***  //粗体加斜体
我的名字叫~~白月紫罗~~  //删除线
```
<!-- endtab -->
{% endtabs %}

# 块引用（Blockquotes）

要创建块引用，请在段落前添加一个 > 符号。

    > Dorothy followed her through many of the beautiful rooms in her castle.

渲染效果如下所示：

> Dorothy followed her through many of the beautiful rooms in her castle.

## 多个段落的块引用（Blockquotes）

块引用可以包含多个段落。为段落之间的空白行各添加一个 > 符号。

    > Dorothy followed her through many of the beautiful rooms in her castle.
    >
    > The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

渲染效果如下：

> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

## 嵌套块引用（Nested Blockquotes）

块引用可以嵌套。在要嵌套的段落前添加一个 >> 符号。

    > Dorothy followed her through many of the beautiful rooms in her castle.
    >
    >> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

渲染效果如下：

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

## 带有其它元素的块引用（Blockquotes with Other Elements）

块引用可以包含其他 Markdown 格式的元素。并非所有元素都可以使用，你需要进行实验以查看哪些元素有效。

    > #### The quarterly results look great!
    >
    > - Revenue was off the chart.
    > - Profits were higher than ever.
    >
    >  *Everything* is going according to **plan**.

渲染效果如下：

> #### The quarterly results look great!
>
> - Revenue was off the chart.
> - Profits were higher than ever.
>
>  *Everything* is going according to **plan**.

# 列表（Lists）

你可以将多个条目组织成有序或无序列表。

## 有序列表（Ordered Lists）

要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。

{% tabs test1 %}
<!-- tab 样式预览 -->
1. First item
2. Second item
3. Third item
  1. First item
  2. Second item
  3. Third item
  4. Fourth item
4. Fourth item
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
1. First item
2. Second item
3. Third item
  1. First item
  2. Second item
  3. Third item
  4. Fourth item
4. Fourth item
```
<!-- endtab -->
{% endtabs %}

## 无序列表（Unordered Lists）

要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。

{% tabs test1 %}
<!-- tab 样式预览 -->
- First item
- Second item
- Third item
  - First item
  - Second item
  - Third item
  - Fourth item
- Fourth item
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
- First item
- Second item
- Third item
  - First item
  - Second item
  - Third item
  - Fourth item
- Fourth item
```
<!-- endtab -->
{% endtabs %}

# 代码

要将单词或短语表示为代码，请将其包裹在反引号 (`) 中。

{% tabs test1 %}
<!-- tab 样式预览 -->
At the command prompt, type `nano`.
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
At the command prompt, type `nano`.
```
<!-- endtab -->
{% endtabs %}

## 转义反引号

如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号(``)中。

{% tabs test1 %}
<!-- tab 样式预览 -->
``Use `code` in your Markdown file.``
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
``Use `code` in your Markdown file.``
```
<!-- endtab -->
{% endtabs %}

## 代码块（Code Blocks）

要创建代码块，请将代码块的每一行缩进至少四个空格或两个制表符。

{% tabs test1 %}
<!-- tab 样式预览 -->
    <html>
      <head>
      </head>
    </html>
<!-- endtab -->

<!-- tab 示例源码 -->
        <html>
          <head>
          </head>
        </html>
<!-- endtab -->
{% endtabs %}

## 围栏代码块（Fenced Code Blocks）

Markdown 的基本语法允许你通过缩进四个空格或一个制表符来创建 代码块 。如果你觉得不方便，可以试试围栏代码块（fenced code blocks）。根据 Markdown 解析器或编辑器的不同，代码块的前后可以使用三个反引号（```）或三个波浪号（~~~）来标记围栏代码块。这有什么优势吗？你不必费力缩进任何行了！

{% tabs test1 %}
<!-- tab 样式预览 -->
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
<!-- endtab -->

<!-- tab 示例源码 -->
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
<!-- endtab -->
{% endtabs %}

{% note info no-icon %}注意：因为本主题对围栏代码块进行了js美化，示例代码用的也是围栏代码块，所以“样式预览”和“示例源码”一样{% endnote %}

## 语法高亮

许多 Markdown 解析器都支持围栏代码块的语法高亮功能。此功能允许你为编写代码所用的编程语言添加带颜色的语法高亮显示。如需添加语法高亮，请在围栏代码块前的反引号旁指定所用的编程语言。

{% tabs test1 %}
<!-- tab 样式预览 -->
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
<!-- endtab -->

<!-- tab 示例源码 -->
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
<!-- endtab -->
{% endtabs %}

# 分隔线（Horizontal Rules）

要创建分隔线，请在单独一行上使用三个或多个星号 (***)、破折号 (---) 或下划线 (___) ，并且不能包含其他内容。

{% tabs test1 %}
<!-- tab 样式预览 -->
***

请叫我白月紫罗

---

请叫我白月紫罗

_________________
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
***

请叫我白月紫罗

---

请叫我白月紫罗

_________________
```
<!-- endtab -->
{% endtabs %}

# 链接（Links）

要创建链接，请将链接文本括在方括号（例如 [Duck Duck Go]）中，后面紧跟着括在圆括号中的 URL（例如 (https://duckduckgo.com) ）。

{% tabs test1 %}
<!-- tab 样式预览 -->
这个是我的[GitHub](https://github.com/BaitianXI).
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
这个是我的[GitHub](https://github.com/BaitianXI).
```
<!-- endtab -->
{% endtabs %}

## 添加标题

你可以选择为链接添加标题（即 title 属性）。当用户将鼠标悬停在链接上时，将显示一个提示。要添加标题，请将其放在 URL 后面。

{% tabs test1 %}
<!-- tab 样式预览 -->
这个是我的[GitHub](https://github.com/BaitianXI "你好呀，我是title提示属性").悬浮上面有惊喜哦
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
这个是我的[GitHub](https://github.com/BaitianXI "你好呀，我是title提示属性").悬浮上面有惊喜哦
```
<!-- endtab -->
{% endtabs %}

## 网址和电子邮件地址

要将 URL 或电子邮件地址快速转换为链接，请将其括在尖括号中。

{% tabs test1 %}
<!-- tab 样式预览 -->
<https://github.com/BaitianXI>
<zixuan030426@gmail.com>
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
<https://github.com/BaitianXI>
<zixuan030426@gmail.com>
```
<!-- endtab -->
{% endtabs %}

## 格式化链接

如需 强调（emphasize） 某个链接, 请在方括号前及圆括号后添加星号。要将链接表示为 代码（code） ，请在方括号内添加反引号。

{% tabs test1 %}
<!-- tab 样式预览 -->
I love supporting the **[EFF](https://eff.org)**.
This is the *[Markdown Guide](https://www.markdownguide.org)*.
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
I love supporting the **[EFF](https://eff.org)**.
This is the *[Markdown Guide](https://www.markdownguide.org)*.
```
<!-- endtab -->
{% endtabs %}

## 引用式链接

引用式（Reference-style）链接是一种特殊类型的链接，它使得 URL 在 Markdown 中更易于显示和阅读。引用式链接由两部分组成：一部分被放置在正文文本中；另一部分被放置在文档中的其它地方，以便于阅读。

{% tabs test1 %}
<!-- tab 样式预览 -->
这个是我的[GitHub][1].悬浮上面有惊喜哦
点击我进入[百度][2]

[1]:<https://github.com/BaitianXI> "你好呀，我是title提示属性"
[2]:<https://www.baidu.com> "点击进入搜素页面"
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
这个是我的[GitHub][1].悬浮上面有惊喜哦
点击我进入[百度][2]

[1]:<https://github.com/BaitianXI> "你好呀，我是title提示属性"
[2]:<https://www.baidu.com> "点击进入搜素页面"
```
<!-- endtab -->
{% endtabs %}

# 图片（Images）

要添加图片，首先请添加感叹号（!），然后紧跟着是方括号，方括号中可添加替代文本（alt text，即图片显示失败后显示此文本），最后跟着圆括号，圆括号中添加图片资源的路径或 URL。你可以选择在圆括号中的 URL 之后添加标题（即 title 属性）。

{% tabs test1 %}
<!-- tab 样式预览 -->
![此图片是Markdown图标](/img/markdown-guide-og.jpg "Markdown很棒")
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
![此图片是Markdown图标](/img/markdown-guide-og.jpg "Markdown很棒")
```
<!-- endtab -->
{% endtabs %}

## 带链接的图片

要为图片添加链接，请先为图片的 Markdown 标记添加一个方括号，然后紧跟着一个圆括号，并在圆括号中添加链接地址。

{% tabs test1 %}
<!-- tab 样式预览 -->
[![此图片是Markdown图标](/img/markdown-guide-og.jpg "Markdown很棒")](https://www.markdown.xyz/)
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
[![此图片是Markdown图标](/img/markdown-guide-og.jpg "Markdown很棒")](https://www.markdown.xyz/)
```
<!-- endtab -->
{% endtabs %}

# 转义字符（Escaping Characters）

要显示原本用于格式化 Markdown 文档的字符，请在字符前面添加反斜杠字符 (\\) 。

{% tabs test1 %}
<!-- tab 样式预览 -->
\* 如果没有开头的反斜杠字符的话，这一行将显示为无序列表。
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
\* 如果没有开头的反斜杠字符的话，这一行将显示为无序列表。
```
<!-- endtab -->
{% endtabs %}

## 可做转义的（英文）字符

以下列出的字符都可以通过使用反斜杠字符从而达到转义目的。

|**字符**|**名称**|
|:------:|------|
|\|反斜杠（backslash）|
|`|backtick (另请参见 在代码中转义反引号)|
|*|星号（asterisk）|
|_|下划线（underscore）|
|{ }|花括号（curly braces）|
|[ ]|方括号（brackets）|
|< >|angle brackets|
|( )|圆括号或括号（parentheses）|
|#|井号（pound sign）|
|+|加号（plus sign）|
|-|减号（minus sign） (也叫连字符 hyphen)|
|.|句点（dot）|
|!|感叹号（exclamation mark）|
|&#124;|管道符（pipe） (另请参见 在表格中转义管道符)|

{% note primary flat %}特殊情况，在表格里输入|时：竖线用 &\#124; 或者 &\#x7C; 来代替{% endnote %}

# HTML 标签

大多 Markdown 应用程序允许你在 Markdown 格式文本中添加 HTML 标签。如果你喜欢某些 HTML 标签胜于 Markdown 语法的话，这将何有帮助。例如，某些人发现通过 HTML 标签添加图像更加容易。当你需要更改元素的属性时（例如为文本指定颜色或更改图像的宽度），使用 HTML 标签更方便些。

如需使用 HTML，请将 HTML 标签添加到 Markdown 格式文本中即可。

{% tabs test1 %}
<!-- tab 样式预览 -->
This **word** is bold. This <em>word</em> is italic.
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
This **word** is bold. This <em>word</em> is italic.
```
<!-- endtab -->
{% endtabs %}

# 表格（Tables）

如需添加表格，请使用三个或更多个连字符（---）来为每个列创建表头，并使用管道符（|）来分隔每个列。你还可以在表格的任意一侧添加管道符。

{% tabs test1 %}
<!-- tab 样式预览 -->
| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |
<!-- endtab -->

<!-- tab 示例源码 -->
```Markdown
| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |
```
<!-- endtab -->
{% endtabs %}

{% note info no-icon %}提示：使用连字符（hyphens）和管道符（pipes）创建表格会很乏味。若要加快进度，请试一试 [Markdown 表格生成器](https://www.tablesgenerator.com/markdown_tables)。使用图形界面生成表格，然后将生成的 Markdown 格式的文本复制粘贴到文件中即可。{% endnote %}

# 自定义标题的 ID

许多 Markdown 解析器都支持为 标题（headings） 自定义 ID，某些 Markdown 解析器会自动为标题添加 ID。通过添加自定义 ID， 能够让你直接链接到这个标题，并且还能使用 CSS 修改其样式。如需为标题添加自定义 ID，请将自定义 ID 用花括号括起来并与标题一起放在同一行。

    ### My Great Heading {#custom-id}

输出的 HTML 如下所示：

    <h3 id="custom-id">My Great Heading</h3>
