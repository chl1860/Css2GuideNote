## 表大小
确定表宽度的两种方法：
- 固定宽度布局
- 自动宽度布局

不论使用哪种宽度计算方法，高度都会自动计算

#### 宽度
可以使用 table-layout 来选择采用哪种方法计算表的宽度

**table-layout**
- 值: auto | fixed | inherit

- 初始值: auto
- 应用于：display 值为 table 或 inline-table 的元素
- 继承性: 有
- 计算值：根据指定确定

固定宽度布局比自动宽度布局速度更快

##### 固定布局
布局不依赖表单元格的内容。其布局是根据该表以及表中列和单元格的 width 值决定

固定布局工作的步骤：
- width 属性值不是 auto 的所有列元素会根据 width 值设置该列的宽度

- 如果其中一个列的宽度为 auto， 不过表首行该列的单元格 width 不是 auto，则根据该单元格宽度设置此列的宽度。如果这个单元格跨多列，则宽度在这些列上平均分配
- 以上两步之后，如果列的宽度仍为 auto， 会自动确定其大小，使其宽度尽可能相等

此时，表的宽度设置为表的 width 值或列宽之和(取其中较大者)。 如果表宽度大于其列宽总和，将二者之差除以列数，再把得到的这个宽度加到每一列上

这种方法的速度很快，因为所有列宽都由表的第一行定义。

如果一个单元格的内容无法放下，该单元格overflow值将决定单元格内容是剪裁还是生成滚动条

使用固定宽度布局模型时，没有必要非得为表指定一个显式宽度，不过如果指定一个宽度确实有帮助

```css
/**
* 以下样式用户代理可能计算出表的宽度比父元素的 width 窄 50px。固定布局算法中会使用计算得到的这个宽度
*/
table {
    table-layout: fixed;
     margin: 0 25px;
    width: auto;
  }
```
#### 自动布局
P377