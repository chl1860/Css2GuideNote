## 表单元格边框
CSS中有两种边框模型
- 分隔边框模型: 单元格之间的边框是分隔的

- 合并边框模型: 单元格间没有可见的间隔

前者是默认模型，可以使用border-collapse 在这两种模型中做出选择

**border-collapse**
- 值: collapse | separate | inherit

- 初始值: sparate
- 应用于：display 值为 table 或者 inline-table的元素
- 继承性: 有
- 计算值: 根据指定值确定

#### 分隔单元格边框
采用这种模型，表中的每个单元格都与其他单元格分开一定距离,而且单元格的边框彼此不会合并

- 边框间隔 **border-spacing**
    - 值：\<length> \<length>? | inherit
    - 初始值：0
    - 应用于：display 值为 table 或 inline-table 的元素
    - 继承性: 有
    - 计算值: 两个绝对长度
    - 说明：除非 border-collapse 为 separate 否则忽略该属性

    border-spacing 应用于表本身而不是单个单元格

    在分隔边框模型中，为行、行组、列和列组设置的边框会被忽略

- 使用 empty-cells 属性处理空单元格
    - show： 会画出空单元格的边框和背景
    - hide: 不会画出单元格的任何部分，就好像单元格被设置为 visibility: hidden
    - **empty-cells**
        - 值：show | hide | inherit
        - 初始值：show
        - 应用于：display值为 table-cell 的元素
        - 继承性：有
        - 计算值：根据指定确定
        - 说明：除非 border-collapse 为 separate， 否则忽略该属性 

    如果一个单元格含有内容，则不能为空。这里的 “内容” 不仅包括文本、图像、表单元素等等，还包括不可分空间实体(&nbsp;)和除 CR（回车）, LF(换行)、tab和空格符以外所有其他空白字符。如果一行中所有单元格都为空， 而且 empty-cells 值都是hide，则整行都将处理为好像这个行元素设置为 display:none

    **注意：IE 不一定支持该属性**

#### 合并单元格边框

- display 值为 table 或 inline-table 的元素不能有任何内比那家，不过它们可以有外边距。因此，表的外围边框与其最外单元格的边界之间不会有任何间隔

- 边框可以应用到单元格、行、行组、列和列组。表元素本身通常都有一个边框
- 单元格边框之间不会有任何间隔
- 一旦合并，单元格之间的边框会在单元格间的假想表格线上居中

###### 合并边框布局

在开始建立一个合并边框布局时，设置初始左右边框宽度的步骤：
- 检查第一行第一个单元格的左边框并取边框宽度的一半作为表的初始左边框宽度
- 检查第一行最后一个单元格有边框并取边框宽度的一半作为表的初始右边框宽度
- 对于第一行之后的其他行，如果其左右边框宽度比初始边框宽度更宽，则会延伸到表的外边距区中

###### 边框合并
规则：
- 如果合并边框的 border-style 为 hidden， 它会优于所有其他合并边框。这个位置的所有边框都隐藏

- 如果合并边框的 border-style 为 none，它的优先级最低。这个位置上不会画出该边框，除非其他合并边框的 border-style 为 none
- 如果至少有一个合并框的 border-style 值不是 none， 而且所有合并边框的 border-style 值都不是hidden，则窄边框不敌宽边框。如果多个合并边框有相同的宽度，则会考虑边框样式，根据以下优先级进行合并：
double > solid > dashed > dotted > ridge > outset > groove > inset
- 如果合并边框的样式和宽度都一样，但颜色不同，按以下优先级使用颜色： cell > row > row group > column > column group  > table
