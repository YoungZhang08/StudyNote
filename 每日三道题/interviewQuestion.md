## 2019/09/20

### [html] bdo 标签
- 用于覆盖默认文本方向，属性 dir 有两个值，ltr（从左往右写，与现代汉语的书写习惯相同） & rtl（从右往左写，与古代汉语书写习惯相同）
### [css] BFC
- Block Formatting Context（块级格式化上下文），是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。块容器，用于管理块级元素。
- 创建块级格式化上下文：
  
  1. html（根元素）
  2. 浮动（float: left | right|）
  3. 绝对定位（position: absolute | fixed）
  4. 行内块元素（display: inline-block）
  5. overflow: auto | hidden
  6. contain: layout | content | paint
  7. 弹性元素（display 为 flex | inline-flex 元素的直接子元素）
  8. 网格元素（display 为 grid | inline-grid 元素的直接子元素）
  9. 多列容器（column-count | column-width 不为 auto，包括 column-count 为 1）
  10. column-span: all
  11. 表格表单元素（display: table-cell）
  12. 表格标题(display: table-caption)
  13. 匿名表格单元格元素(display: table(table) | table-row(row) | table-row-group(tbody) | table-header-group(thead) | table-footer-group(tfoot) | inline-table)

- BFC 特性

  1. 属于同一个 BFC 的两个块元素如同时设置了 margin-top（下面的）和 margin-bottom（上面的）会发生重叠，重叠结果为两个外边距取最大值。可使其分属于两个不同的 BFC 来放置外边距重叠。
  2. 包含浮动元素。给浮动元素的父元素设置 overflow: hidden 可以清除浮动。
  3. BFC 区域不与 float box 重叠。属于同一父元素下的 float box 和正常文档流的 normal box，触发 normal box 的 BFC 即可。（自适应两栏布局）
  4. 每个元素的 margin box 的左边与包含块 context box 的左边相接触，浮动元素也是如此，如果不清楚浮动，父元素高度会塌陷，但是浮动元素仍然属于其父元素的范围。
  5. 计算 BFC 高度时，浮动元素也计算在内。

- BFC in IE（使用 zoom:1 触发 IE 的 Layout） 

### [js] js 拖拽用到的事件
- drag（onDrag，当拖动元素或选中文本时触发）
- dragend（ondragend，当拖拽操作结束时触发。比如：松开鼠标按键或者敲 "ESC"）
- dragenter（ondragenter，当拖拽元素或选中的文本到一个可释放目标时触发）
- dragexit（ondragexit，当元素变得不再是拖动操作的选中目标时触发）
- dragleave（ondragleave，当拖动元素或选中的文本离开一个可释放目标时触发）
- dragover（ondragover，当元素或选中的文本被拖到一个可释放目标上时触发[100ms 触发一次]）
- dragstart（ondragstart，当用户开始拖动一个元素或选中文本时触发）
- drop（ondrop，当元素或选中的文本在可释放目标上被释放时触发）

## 2019/09/21

### [html] figure 标签
- 规定独立的流内容（图像、图表、照片和代码等等）
- figure 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响
- \<figcaption> 标签定义 figure 元素的标题（caption）
### [css] 弹性布局
https://youngzhang08.github.io/2018/08/17/Flex%E5%B8%83%E5%B1%80%E7%AC%94%E8%AE%B0/
### [js] 数组排序方法


## 2019/09/22

### [html] 纯 html 怎么实现下拉提示
- input & datalist & option
```
<label for="myBrowser">Choose a browser from this list:</label>
<input list="browsers" id="myBrowser" name="myBrowser" />
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Internet Explorer">
  <option value="Opera">
  <option value="Safari">
  <option value="Microsoft Edge">
</datalist>
```
### [css] css 实现两端对齐
```
text-align-last: justify;
```

### [js] js 中 attribute 和 property 的区别
- attribute 是属于 property 的一个子集，它保存了 html 标签上定义的属性。它的值只能够是字符串，并且会始终保持 html 代码中的初始值
- property 是 DOM 中的属性，是 JavaScript 里的对象，在其生命周期中是可变的
- DOM 节点在初始化的时候会将 html 规范中定义的 attribute 赋值到 property 上, 而自定义的 attribute 并不属于这个氛围内, 自然生成的 DOM 节点就没有这个 property