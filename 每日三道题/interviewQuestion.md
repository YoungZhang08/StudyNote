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
- property 是 DOM 中的属性，是 JavaScript 里的对象，在其生命周期中是可变的
- DOM 节点在初始化的时候会将 html 规范中定义的 attribute 赋值到 property 上, 而自定义的 attribute 并不属于这个范围内, 生成的 DOM 节点就没有这个 property
- attribute 是属于 property 的一个子集，它保存了 html 标签上定义的属性。它的值只能够是字符串，并且会始终保持 html 代码中的初始值

## 2019/09/23

### [html] 怎么检测浏览器是否支持HTML5特性？
- 在浏览器中使用 h5 标签。
```

```
### [css]  判断第一行和第二行的颜色分别是什么？并解释为什么？[代码]
```
<style>
.red {color:red;}
.green {color:green;}
</style>

<div class="red green">第一行：颜色是什么？</div>
<div class="green red">第二行：颜色是什么？</div>

```
- 对于相同类型选择器指定的样式，在样式表文件中，越靠后的优先级越高。
- 注意：这里是样式表文件中越靠后的优先级越高，而不是在元素 class 出现的顺序。

### [js] 有些 js 库习惯在代码开头处添加分号有什么作用呢？除了分号还可以换成别的吗？
- js 文件结束处是没有分号的。若几个 js 连在一起时，2个 js 连接处会发生语法上的混淆。开头加 ; 用于分隔，可以避免多文件压缩在一起时引起的错误。分号和分号放在一起也没问题，相当于 “空语句”。

## 2019/09/24

### [html] HTML5 如何调用摄像头
- window.navigator.getUserMedia()（这个已废弃，仅为了向后兼容而存在，已更名为MediaDevices.getUserMedia()）
```
navigator.getUserMedia( constraints, successCallback, errorCallback );
// MediaStreamConstaints 对象指定了请求使用媒体的类型，还有每个类型的所需要的参数。
// 当调用成功后，successCallback 中指定的函数就被调用，包含了媒体流的MediaStream对象作为它的参数，你可以把媒体流对象赋值给合适的元素，然后使用它。
// 当调用失败，errorCallback 中指定的函数就会被调用。
// eg:
navigator.getUserMedia = navigator.getUserMedia ||
                         navigator.webkitGetUserMedia ||
                         navigator.mozGetUserMedia;

if (navigator.getUserMedia) {
  navigator.getUserMedia(
    { audio: true, video: { width: 1280, height: 720 } }, 
    (stream) => {
      var video = document.querySelector('video');
      video.src = window.URL.createObjectURL(stream);
      video.onloadedmetadata = (e) => { // 在视频的元数据加载后执行 JavaScript
        video.play();
      };
    },
    (err) => {
      console.log("The following error occurred: " + err.name);
    }
  );
} else {
  console.log("getUserMedia not supported");
}
```
- navigator.mediaDevices.getUserMedia()
> MediaDevices.getUserMedia() 会提示用户给予使用媒体输入的许可，媒体输入会产生一个MediaStream，里面包含了请求的媒体类型的轨道。此流可以包含一个视频轨道（来自硬件或者虚拟视频源，比如相机、视频采集设备和屏幕共享服务等等）、一个音频轨道（同样来自硬件或虚拟音频源，比如麦克风、A/D转换器等等），也可能是其它轨道类型。

> 它返回一个 Promise 对象，成功后会 resolve 回调一个 MediaStream 对象。若用户拒绝了使用权限，或者需要的媒体源不可用，promise 会 reject，回调一个  PermissionDeniedError 或者 NotFoundError 。
```
/** 
constraints 参数是一个包含了 video 和 audio 两个成员的 MediaStreamConstraints 对象，用于说明请求的媒体类型。
必须至少一个类型或者两个同时可以被指定。
如果浏览器无法找到指定的媒体类型或者无法满足相对应的参数要求，那么返回的 Promise 对象就会处于 rejected［失败］状态，NotFoundError 作为 rejected［失败］回调的参数。
*/

// 想要获取一个最接近 1280x720 的相机分辨率
var constraints = { audio: true, video: { width: 1280, height: 720 } }; 

navigator.mediaDevices.getUserMedia(constraints)
.then((mediaStream) => {
  var video = document.querySelector('video');
  video.srcObject = mediaStream;
  video.onloadedmetadata = (e) => {
    video.play();
  };
})
.catch((err) => { 
  console.log(err.name + ": " + err.message); 
}); // 总是在最后检查错误
```

### [css]  CSS3 有哪些新增的特性
#### 边框（border）
- border-radius 圆角  如果你在 border-radius 属性中指定

1. 四个值： 第一个值为左上角，第二个值为右上角，第三个值为右下角，第四个值为左下角。
2. 三个值： 第一个值为左上角, 第二个值为右上角和左下角，第三个值为右下角
3. 两个值： 第一个值为左上角与右下角，第二个值为右上角与左下角
4. 一个值： 四个圆角值相同
- box-shadow 盒阴影
- border-image 边框图像

#### 背景
- background-position 背景图位置
- background-size 背景图大小
- background-origin 定位(content-box, padding-box 和 border-box)区域内可以放置背景图像
- background-clip 背景剪裁属性是从指定位置开始绘制

#### 渐变
- linear-gradient 线性渐变（向下/向上/向左/向右/对角方向）
- radial-gradient 径向渐变（由它们的中心定义）

#### 文本效果
- text-shadow 文本阴影
- text-overflow 如何显示溢出内容
- word-wrap 自动换行（break-word/no-wrap）
- word-break 单词拆分换行（keep-all/break-all）
- text-wrap 文本换行
- text-outline 文本轮廓
- text-justify 规定当 text-align 设置为 "justify" 时所使用的对齐方法

#### 字体
- @font-face

#### 2D 转换
- 2D 转换属性
  - transform
  - trnasform-origin 更改转换元素的位置
- 2D 转换方法
  - translate() 平移
  - rotate() 旋转
  - scale() 缩放
  - skew() 倾斜
  - matrix() matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能

#### 3D 转换
- 3D 转换属性
  - transform
  - trnasform-origin 更改转换元素的位置
  - transform-style
- 3D 转换方法
  - translate3d(x, y, z)
  - rotate3d(x, y, z)
  - scale3d(x, y, z)

#### 过渡
- transtion

#### 动画
- animation
- @keyframes 规则

#### 媒介查询
- @media

### [js] 写一个方法去掉字符串中的空格
```
(str) => {
  return str.replace(/\s/g, '');
}

(str) => {
  return str.split(' ').join('');
}
```