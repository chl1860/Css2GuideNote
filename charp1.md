#### 1.  **替换元素**： 是指用来替换元素内容的部分并非由文档内容直接显示。如 *img，input* 元素

#### 2. **非替换元素**： 其内容由用户代理（通常是一个浏览器）在元素本身生成的框中显示

#### 3. **元素显示角色**： 除替换和非替换元素，CSS2.1 还使用另外两种基本元素类型：**块级元素** 和 **行内元素**

- **块级元素**：生成一个元素框，（默认地）它会填充其父元素的内容区，旁边不能有其他元素。换句话说，它在元素框之前和之后都生成了“分隔符”。

&emsp;&emsp;&emsp;&emsp;a. 替换元素可以是块级元素，不过一般都不是。\
&emsp;&emsp;&emsp;&emsp;b. 列表项是块级元素的一个特例

- **行内元素**： 在一个文本行内生成元素框，而不会打断这行文本。例如 *a，strong，em* 都属于行内元素。这些元素不会在它本身之前或之后生成“分隔符”，所以可以出现中另一个元素的内容中，而不会破会其显示。在 HTML 中块级元素不能继承自行内元素（即不能嵌套在行内元素中），但在CSS中对于显示角色如何嵌套不存在任何限制。

#### 4. 结合CSS和XHTML
&emsp;&emsp;HTML 和 XHTML 都有一个固有的结构。页面应当包含有某种结构含义的信息

#### 5. Link标记
&emsp;&emsp; Link标记的基本目的是允许 HTML 创作人员将含有Link标记的文档与其他文档关联起来
样式表不能包含XHTML或其他任何标记语言，只能有样式规则属性：\
- rel代表关系，关系为stylesheet
- type总是设置为 text/css，这个值描述了使用 Link 标记加载的数据的类型
- href 表示样式表的 URL 可以是决定 URL 也可以是相对 URL 
- media\
&emsp;&emsp;*all* 表示样式表用于所有表现媒体\
&emsp;&emsp;*aural* 用于语音合成器、屏幕阅读器和文档的其他声音表现\
&emsp;&emsp;*braille* 用Braille设备表现文档时使用\
&emsp;&emsp;*embossed* 用Braille打印设备打印时使用\
&emsp;&emsp;*handled* 用于手持设备\
&emsp;&emsp;*print* 用于打印文档时使用\
&emsp;&emsp;*projection* 用于投影仪\
&emsp;&emsp;*screen* 屏幕媒体（Web浏览器都是屏幕媒体用户代理）\
&emsp;&emsp;*tty* 在固定间距中显示文档时使用\
&emsp;&emsp;*tv* 电视上显示文档时使用\
&emsp;&emsp;Web浏览器支持最广的是： all、 screen、 print\
&emsp;&emsp;Web可以在多个媒体中使用同一个样式表，为此要提供此样式的媒体列表，各媒体用逗号分隔。例如：
```html
   <link rel='stylesheet' type='text/css' href = '' media = 'screen, projection'/>         
```

#### 6. 候选样式表
- 将 **rel** 属性设置为  *alternate stylesheet* 就可以定影候选样式表，只有在用户选择这个样式表时才会用于文档表现

- 如果浏览器能使用候选样式表， 它会使用 **link** 元素的 *title* 属性生成一个候选样式列表

- 候选样式表在大多数基于 Gecko 的浏览器中得到了支持

- 如果为一个**rel** 为 stylesheet 的 link指定了标题（title），也就指定了该样式为首选样式，显示时首先使用首选样式。不过，一旦选择了候选样式，就不会使用首选样式表了。

- 此外如果指定了一组首选样式表，则只会使用其中的一个，而HTML 和 XHTML中没有提供任何方法确定哪些首选样式会被忽略

- 如果，没有为样式表指定 title， 那么它将是个永久样式表，始终用于文档的显示

#### 7. style 元素
- 可以用style元素包含样式表，它在文档中单独出现：
```html
 <style type='text/css'>
    ....
 </style>
 ```
- style 一定要使用type属性， 对于CSS 文档，正确的type属性是 text/css
- style 元素还可以指定 media属性， 属性值与 Link中相同

#### 8. @import 指令
- @import 指令可以包含多个外部样式表链接，例如：@import url(sheet2.css)
- @import 必须放在其他 CSS 规则之前，否则将不起作用
- 一个文档中可以有多个 @import标记
- 用 @import 标记无法指定候选样式表
##### Tips: 
&emsp;&emsp;有些老旧浏览器无法处理不同形式的 @import 指令，可以适当利用这一点，对这些浏览器隐藏样式\

&emsp;&emsp;可以限制所导入的样式表应用于一种或多种媒体，可以在url之后列出要应用此样式的媒体。例如：
```CSS
    @import url(eet2.css) all;
    @import url(blueworld.css) screen;
    @import url(zany.css) projection, print;
```

&emsp;&emsp; @import 指令可以用于外部样式表中，引入需要使用的其他样式表中的样式，例如：
```CSS
    @import url(http://...);
    @import url(basic-text.css);
    @import url(printer.css) print;
    
    body{color:red;}
    h1{color:blue;}    
```
    CSS 要求 @import指令出现在样式表中其他规则之前，否则兼容代理会将其忽略（IE除外）

#### 9. 向后可访问性
&emsp;&emsp; 将style标记的内容包含在注释标记中
```html
<style type='text/css'><!-- your style --></style>
```
&emsp;&emsp;这样防止老旧浏览器无法忽略声明的问题。与此同时，能理解 CSS的浏览器仍能正常读取样式

#### 10. CSS 注释
    CSS 注释不允许嵌套， 嵌套注释中，外部注释会中内部注释的结束处结束

#### 11. 内联样式
    内联样式中不能使用 @import 指令，也不能包含完整规则，通常并不推荐使用内联样式，内联样式会抵消 CSS 的重要优点