## 表格式化
 - 表是如何组成的
 - 表中各元素之间如何关联

#### 表的视觉编排
- CSS 如何定义表的编排？\
    CSS 对于表元素<sup>[1]</sup> 和表内元素<sup>[2]</sup>做了明确的区分。在CSS 中， 表内元素会生成带有内容(content), 内边距(padding) 和边框(border)，但没有外边距(margin) 的矩形框。这意味着，不能通过外边距 (margin) 来定义表内元素(table internal element) 间的间隔。CSS标准流览器(A CSS-conformant browser) 会忽略掉任何企图对单元格 (cell), 行(row)或者其他任何(除 caption 外)表内元素应用外边距(margin)的行为。 

- 表编排的 6 条规则：
    - 这些规则的基础，表单元格<sup>[3]</sup>规则。表单元格是指表格所绘制的表格线之间的区域。

    - 每个行框<sup>[4]</sup> 包含一整行单独的表单元格。所有的行框会按照它们在原文档中出现的顺序，从上至下地填充表。因此表格有多少行元素，就有多少行
    - 一个行组，包含其成员行框所包含的单元格<sup>[5]</sup>

    - 一个列框包含已列或多列表单元格。所有列框都按照其出现顺序依次摆放。在从左往右阅读的语言中，先出现的在后出现的列框走遍，在从右往左阅读的语言中则相反
    - 一个列组，包含其成员列框所有的表单元格
    - CSS 并没有就单元格跨行和跨列的行为给出具体定义。相反，将这种行为 由文档语言来控制。每一个跨行(或列)单元格都是一个具有一个或多个表单元宽高的矩形框。这个矩形框的顶行位于其单元格的父行中。在从左往右阅读的语言中，矩形框会尽可能向左包含，但不会覆盖矩形框外的其他元素，它也必须包含稍早出现在原文档的其同行所有元素的右边部分。在从右往左阅读的语言中则与之相反
    - 一个单元框不能超出一个表或者行组的最后一个行框。如果一个表结构存在超出的情况，那么这个单元格会被缩小至这个表或者行组可以包住它为止
    
    **CSS 不鼓励但也不禁止对表元素的定位行为。定位一个包含跨行单元格的行会因为从改行被从表中移除而改变表的布局，也因此造成其他行布局会忽略跨行单元格造成的布局影响**

    通过定义，表单元格都是矩形，但它们并不总有相同尺寸。所有的在同一表列中的单元格都具有相同宽度，所有位于同一表行中的单元格具有相同高度，但不同的表行之间可以有不同的高度。与之相似，不同的表列之间可以有不同的宽度

#### 表显示值
- **display**
    - 值：none | inline | block | inline-block | list-item | run-in | table | inline-table | table-row-group | table-header-group | table-footer-group | table-row | table-column-group | table-column | table-cell | table-caption | inherit

    - 初始值：inline
    - 应用于：所有元素
    - 继承性：无
    - 计算值：对于浮动元素，定位元素和根元素，计算值可变；否则根据指定确定

        - table: 使用这个display 值的元素，定义了一个块级表。因此，定义了一个生成块框的矩形块。与之相近的 HTML 元素是 table

        - inline-table: 使用这个display 值的元素，定义了一个行内表。这意味着该元素定义了一个生成行内框的矩形块。与之相近的非表格值是 inline-block.与之最相近的 HTML 元素是table,尽管默认情况下 HTML table 不是行内元素

        - table-row: 强调该元素是一行单元格. 相似HTML元素为 tr
        - table-row-group: 强调该元素为一个行组.相近 HTML 元素未 tbody
        - table-header-group: 这个值于 table-row-group非常像，只是显示格式不同,表头行组,总是显示在其他行、行组或者其他任何顶部内容之前。打印时，用户代理会在每页的顶端重复显示行组元素的内容. 这个值并没有对为个元素赋 table-row-group 值将会发生行为进行定义。一个头组会可以包含多行. HTML 中等效元素为 thaed
        - table-footer-group： 与 table-header-group 类似，除了它是出现在所有行、行组或者任何其他顶部内容之后。等效 HTML 元素未 tfoot
        - table-column: 这个值声明该元素用于描述列单元格.在CSS术语中，使用该值的元素并不会被实际渲染出来，于使用none差不多。之所以存在这个值是为了帮助定义列中单元格的表现形式. 相应 HTML 元素未 col
        - table-column-group: 声明列组,类似于 table-column 元素， table-column-group元素也不会显示, 不过有助于定义列组中元素的表示. 相应的 HTML 元素是 colgroup
        - table-cell:指定一个元素表示为表中的单元格。HTML 中等效元素为 td 和 th
        - table-caption: 这个值定义了表的标题. CSS 并没有定义如果多个元素都设置为 table-caption 会发生什么，除了给一个显示的警告:"...authors should not put more than one element with `display: caption' inside a table or inline-table element."
        
        **注意：IE7之前以上display值都无效**

#### 以行为组
- 列：
    CSS模型是面向行的.虽然单元格在文档源中是行元素的后代,但它们可能同时属于两个上下文(行和列).不过 CSS 中列和列组只能接受 4 种样式: *border*, *background*, *width* 和 *visibility*\
    这 4 个属性只能应用于列上下文的特殊规则:

    - border: 只有当 border-collapse 属性值为 collapse 时才能为列和列组设置边框。在这种情况下列和列组边框会参与设置各单元格边界边框样式的合并算法

    - background: 只有当单元格与其行有透明背景时,列或列组的背景才可见
    - width: 定义了列或列组的最小宽度.列（或列组）的背景可能要求列更宽
    - visibility:如果一个列或列组的visibility 为 collapse 则该列(或列组)中所有单元格都不显示。从合并列跨到其他列的单元格会被剪裁,类似于从其他列跨到隐藏列中的单元格。另外表的总宽度会减去已合并列的宽度

- 匿名表对象:
    CSS 中定义了一种机制,可以将“遗漏”组件作为匿名对象插入。

    CSS 中可能出现 7 种不同的匿名对象插入
    - 如果一个 table-cell 元素的父元素不是 table-row 元素,则会在该 table-cell 元素及其父元素之间插入一个匿名 table-row 对象

    - 如果一个 table-row 元素的父元素不是 table, inline-table 或者 table-row-group 元素，则会在该 table-row 元素及父元素之间插入一个匿名 table 元素 
    - 如果一个 table-column 元素的父元素不是 table, inline-table 或者 table-cloumn-group 元素，则会在该 table-column 元素及父元素之间插入一个匿名 table 元素
    - 如果一个 table-row-group, table-header-group, table-footer-group, table-column-group 或者 table-caption 的父元素不是 table 元素，则会在该元素及其父元素间插入一个匿名 table 元素       
    - 如果一个 table 或者 inline-table 元素的子元素不是 table-row-group, table-header-group， table-footer-group， table-column-group, table-row 或者 table-captiony元素,则会在该table 元素及其子元素间插入一个匿名 table-row 对象
    - 如果一个 table-row-group, table-header-group， table-footer-group 元素的子元素不是 table-row 对象，则会在该元素及其子元素间插入一个匿名 table-row 对象
    - 如果一个 table-row 元素的子元素不是 table-cell 对象，则在该元素及其子元素间插入一个匿名 table-cell对象

- #### 表层
    CSS 定义了6 个不同的层， 从上往下依次为:单元格，行，行组，列，列组, 表
        
    对应表各个方面的样式都是在其各自的层上绘制

- #### 表标题
    表标题是一小段文字，描述了表内容的本质. 利用 caption-side属性可以把这个元素放置table之上或底下。(HTML 中, caption 元素只能出现在开始table元素的后面)

    表标题格式化为就好像它是直接放在表框之前(或之后)的块框。只有两个不同
    - 表标题仍能从表继承
    - 如果一个 run-in 元素在表之前，它不会进入表的上标题，也不会进入表中,而是处理为好像其 display 值为 block

    **caption-side**
    - 值：top|bottom
    - 初始值: top
    - 应用于: display值为table-caption的元素
    - 继承性: 有
    - 计算值: 根据指定确定

    caption 元素宽度要基于 table 内容宽度
    大多数情况下，caption 应用样式非常类似于块级元素
    
----
[1] 原文: table elements\
[2] 原文: table internal elements\
[3] 原文：grid cell\
[4] 原文: row box\
[5] 原文: A row group's box encompasses the same grid cells as the row boxes it contains.


