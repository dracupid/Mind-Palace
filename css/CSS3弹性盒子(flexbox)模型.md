CSS 3 弹性盒子模型
=======================
#### Zhao Jingchen
#### 2015.01.01
---------------

弹性盒子（flexbox）模型是CSS 3引入的新布局模式（[最新标准请戳](http://www.w3.org/TR/css3-flexbox/)），可以让开发者更容易、更可控地完成自适应的布局。无论从易用性和实现的效果而言，弹性盒子模型都堪称是目前最强大的布局方式。

## 1. 弹性盒子的主要功能
- 更简单的使单个或一组元素居中（垂直或水平）
- 更容易的改变元素的排布顺序、方向和对齐方式，减少破坏布局流的float的使用。
- 通过扩张或收缩元素来利用可用空间，“弹性”的控制元素的排布。

## 2. 弹性盒子标准的变迁
在了解弹性盒子模型之前，有必要先了解一下弹性盒子标准的变迁。Flexbox规范的制定工作从2009年至今，前后历经三个大的版本：

- `display: box/inline-box`
    - 2009年7月[工作草案](http://www.w3.org/TR/2009/WD-css3-flexbox-20090723/)提出
    - 支持最广泛：除IE 9- 和 部分opera浏览器外均支持。
- `display: flexbox/inline-flexbox`
    - 2011年3月[工作草案](http://www.w3.org/TR/2011/WD-css3-flexbox-20110322/)提出
    - 只有IE 10支持。
- `display: flex/inline-flex`
    - 2012年6月[工作草案](http://www.w3.org/TR/2012/WD-css3-flexbox-20120612/)提出
    - 2012年9月成为[候选推荐](http://www.w3.org/TR/2012/CR-css3-flexbox-20120918/)
    - 2014年9月成为[最终征求意见稿](http://www.w3.org/TR/2014/WD-css-flexbox-1-20140925/)。基本可以确定未来成为最终标准。
    - 现在已被广泛支持：Chrome 21+, Safari 6.1+, Firefox 22+, Opera (& Opera Mobile) 12.1+, IE 11+, and Blackberry 10+.

详细的兼容性列表请参见[Can I Use](http://caniuse.com/#feat=flexbox)。

之后的浏览器版本很大可能会停止对旧版本标准的支持，比如最新的firefox浏览器。在今后的编程中，应该完全使用最新的flex标准（后文也已最新标准为准），并使用[autoprefixer](https://github.com/postcss/autoprefixer)添加不同版本的属性值和浏览器前缀，以保障向后兼容。

> autoprefixer[只会处理](https://github.com/postcss/autoprefixer#why-doesnt-autoprefixer-support-display-box-box-align-etc)使用最新flex标准的css语句，为其添加浏览器前缀和旧版本的shim。


## 3. 相关术语
- 伸缩容器：一个设有 `display:flex` 或 `display:inline-flex` 的元素。
- 伸缩项目：伸缩容器的子元素。
- 主轴(main axis)：浏览器沿一个伸缩容器的主轴排布伸缩项目，是一个向量。
- 侧轴(cross axis)：与主轴垂直的轴称作侧轴，是侧轴方向的延伸。
- 轴起点、轴终点：伸缩项目的排布从容器的主起点边开始，到轴终点边结束。
- 轴长度：伸缩项目的在轴方向的宽度或高度
- 轴长度属性：width或height属性，由哪一个对着轴方向决定。

以行方向排布的盒子为例

![](http://www.w3.org/html/ig/zh/wiki/images/b/bf/Flex-direction-terms-new.zh-hans.png)

## 4. 相关属性（第一个值为默认值）

###应用于伸缩容器：

#### flex-flow
两个属性的简写
- flex-direction: 指定主轴和主轴方向 `row | row-reverse | column | column-reverse`
- flex-wrap: 规定伸缩容器是单行还是多行，以及侧轴方向新行的堆放方向。 `nowrap | wrap | wrap-reverse`

####align-items
伸缩项目在侧轴的对齐方式 `stretch | flex-start | flex-end | center | baseline`

![](http://www.w3.org/html/ig/zh/wiki/images/5/59/Flex-align.png)

#### justify-content
伸缩项目在主轴的对齐方式 `flex-start | flex-end | center | space-between | space-around`

![](http://www.w3.org/html/ig/zh/wiki/images/1/1b/Flex-pack-new.png)

####align-content
伸缩行（多行）在伸缩容器里的对齐方式 `flex-start | flex-end | center | space-between | space-around`

> 该属性会更改 flex-wrap 的行为

![](http://www.w3.org/html/ig/zh/wiki/images/9/97/Align-content-example.png)

###应用于伸缩元素：

####order
指定元素在容器中的位置。 `integer`

####margin
若伸缩元素的margin为auto，则容器中所有的空余空间都会成为该元素的外边距。

####flex
三个属性的简写
- flex-grow: 元素未填满容器时扩张各元素的的比例因子 `0 number`
- flex-shrink: 元素溢出容器后收缩各元素的比例因子 `1 | number`
- flex-basis: 元素进行收缩和扩张的基础宽度 `auto | content | <'width'>`

####align-self
元素在侧轴的对齐方式 `auto | flex-start | flex-end | center | baseline | stretch`

>会覆盖容器的align-items

## 5. 各版本属性的对应关系

|版本|属性|
| ----- | ------ |
|flex   |justify-content|flex-start|center|flex-end|space-between|space-around|
|flexbox|flex-pack|start|同上|end|justify|distribute|
|box    |box-pack|同上|同上|同上|同上|N/A|

|版本|属性|
| ----- | ------ |
|flex   |align-items|flex-start|center|flex-end|baseline|stretch|
|flexbox|flex-align|start|同上|end|同上|同上|
|box    |box-align|同上|同上|同上|同上|同上|同上|

|版本|属性|
| ----- | ------ |
|flex   |align-self|auto|flex-start|center|flex-end|baseline|stretch|
|flexbox|flex-item-align|同上|start|同上|end|同上|同上|
|box    |N/A|同上|同上|同上|同上|同上|同上|

|版本|属性|
| ----- | ------ |
|flex   |align-content|flex-start|center|flex-end|space-between|space-around|stretch|
|flexbox|flex-line-pack|start|同上|end|justify|distribute|stretch|
|box    |N/A|同上|同上|同上|同上|同上|同上|

|版本|属性|
| ----- | ------ |
|flex   |order|
|flexbox|flex-order|
|box    |box-ordinal-group|

|版本|属性|
| ----- | ------ |
|flex   |flex|flex-grow flex-shrink? or flex-basis
|flexbox|flex|pos-flex neg-flex? or preferred-size
|box    |box-flex| number

|版本|属性|
| ----- | ------ |
|flex   |flex-direction|row|row-reverse|column|column-reverse|
|flexbox|flex-direction|同上|同上|同上|同上|
|box    |box-orient|horizontal|horizontal|vertical|vertical|
||box-direction|normal|reverse|normal|reverse|

|版本|属性|
| ----- | ------ |
|flex   |flex-wrap|nowrap|wrap|wrap-reverse|
|flexbox|flex-wrap|同上|同上|同上|
|box    |box-lines|single|multiple|N/A|

## 相关阅读
1. [W3C 标准](http://www.w3.org/TR/css3-flexbox/)
2. [Designing CSS Layouts With Flexbox Is As Easy As Pie - David Storey](http://www.smashingmagazine.com/2013/05/22/centering-elements-with-flexbox/) | [译文](http://www.w3cplus.com/css3/designing-css-layout-with-flexbox.html)
3. [Flexbox — Fast Track to Layout Nirvana?](http://dev.opera.com/articles/view/flexbox-basics/) | [译文](http://www.w3cplus.com/css3/flexbox-basics.html)
4. [Dive into Flexbox](http://bocoup.com/weblog/dive-into-flexbox/) | [译文](http://www.w3cplus.com/blog/666.html)
5. [W3C Wiki](http://www.w3.org/html/ig/zh/wiki/Css3-flexbox/zh-hans)