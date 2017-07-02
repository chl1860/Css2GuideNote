## 改变元素显示
可以为属性 diplay 设置值，来影响用户代理显示方式\
display
- 值 none | inline | block | inline-block | list-item | run-in | table | inline-table | table-row-group | table-header-group | table-footer-group | table-row | table-column-group | table-column | table-cell | table-caption | inherit

- 初始值: inline
- 应用于：所有元素
- 继承性： 无
- 计算值：对于浮动、定位和根元素，计算值可变；否则根据指定去顶

### 改变元素的显示角色
改变的只是元素的显示角色，而不是元素的本质。例如：让一个段落生成行内框，并不会把这个段落真正变成一个行内元素。行内元素可能是一个块级元素的后代，反过来却不行。例如：
```html
    <!--以下标记是不合法的-->
    <a href = "www.example.net" style="display:block;">
        <p style="display:inline;">this is wrong</p>
    </a>
```

### 行内块元素

*inline-block* 属性值是块级元素与行内元素的混合\
行内元素作为替换元素放在行中\
行内块元素的底端默认地位于文本行基线上，而且内部没有行分隔符\
行内块元素内部会像块元素一样设置内容的格式

### run-in 元素
如果一个元素生成 run-in 框，而且该框后面是一个块级框，那么该 run-in 元素会成为块级元素框开始处的一个行内框

run-in 框格式化为另一个元素的行内框，它们仍从文档中的父元素继承属性，而不是说它们放在哪个元素中就从哪个元素继承属性

只有当 run-in 框后面是一个块级元素时 run-in 框才起作用。如果不是这样 run-in 框本身将成为块级元素 

### 计算值
对于浮动元素和绝对定位元素，计算值由声明确定
对于根元素，如果声明为值 inline-table 或 table，都会得到计算值table，声明为 none 则会得到 none。 所有其他 display 值 都计算为 block
