# HTML语义标签
## 字符实体
| 实体名称     | 显示结果 | 描述     |
| ------------ | -------- | -------- |
| ``&nbsp;``   | `` ``    | 空格     |
| ``&gt;``     | >        | 大于号   |
| ``&lt;``     | <        | 小于号   |
| ``&amp;``    | &        | 与       |
| ``&copy;``   | ©        | 版权     |
| ``&reg;``    | ®        | 注册商标 |
| ``&trade;``  | ™        | 商标     |
| ``&times;``  | ×        | 乘号     |
| ``&divide;`` | ÷        | 除号     |
| ``&iquest;`` | ¿        | 倒问号   |
## meta标签
- ``charset``：指定网页的字符集 
- ``name`` ：指定的数据的名称 
	- ``keywords``：表示网站的关键字，可以同时指定多个关键字，关键字间使用,隔开 
	- ``description``：表示网站的描述信息
	- ``content`` ：指定的数据的内容，会作为搜索结果的超链接上的文字显示 

```html
<!DOCTYPE html>

<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<!--这里使用了refresh，3秒钟后会跳转向百度-->
	<meta http-equiv="refresh" content="3;http://www.baidu.com">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta description="网站的描述">
	<meta keywords="搜索关键字">
	<title>登录</title>
</head>

<body>
</body>

</html>
```
如果设置了`http-equiv`属性，``<meta>``元素就是一个pragma指令，提供的信息相当于一个类似名称的HTTP头所能提供的信息。
-  `content-security-policy`：允许页面作者为当前页面定义一个内容策略。内容策略主要指定允许的服务器来源和脚本端点，这有助于防范跨站脚本攻击。
-  `content-type`：声明文档的MIME类型和字符编码。如果指定，content属性必须有 "text/html; charset=utf-8 "的值。这相当于一个指定了charset属性的<meta>元素，并对文档中的位置有同样的限制。注意：只能在使用text/html的文档中使用，不能在使用XML MIME类型的文档中使用。
-  `default-style`：设置默认的CSS样式表集的名称。
-  `x-ua-compatible`： 如果指定，内容属性必须有 "IE=edge"的值。用户代理被要求忽略这个pragma。
-  `refresh`：该指令指定页面重新加载及重定向的方式 
	- 直到页面应该被重新加载的秒数--只有当content属性包含一个正整数时。
	- 直到页面重定向到另一个页面的秒数--只有当内容属性包含一个正整数，后面跟着字符串';url='，以及一个有效的URL。

## 语义标签
1. 标题`h1`~`h6`，都是块元素
2. 标题组`hgroup`
3. 段落`p`
4. 长引文`blockquote`
5. 短引文`q`
6. 引文`cite`
7. 换行`br`
8. 强调`em`、`i`
9. 重要`strong`、`b`


标签	作用	描述
| 标签       | 作用 | 描述 |
| ---------- | ---- | ---- |
| h1-h6      |   标题   |      |
| hgroup     |    标题组  |   多层次的标题。它将一组h1～h6元素分组|
| p          |   段落   |页面中的一个段落。由空行或第一行缩进将相邻的文本块分开|
| blockquote |    长引用  |  用缩进表示所包含文本。可以用cite属性表示引文来源，用cite元素表示来源的文本表述|
| q          |     短引用 |用一个简短的内联引号包围文本。大多数浏览器通过在文本周围加上引号来实现。该元素用于不需要段落分隔的短引文；|
| br         |     换行 |      |
| em         |  强调    | 表示强调作用。em元素可以嵌套，每一级嵌套表示更高的强调程度i元素效果与它相同，不过i不属于语义标签|
| strong     |   重要   |表示重要性、严肃性或紧迫性。浏览器通常以粗体字呈现内容b元素效果与它相同，不过b不属于语义标签|
|header|页眉|介绍性的内容|
|footer|页脚|通常包含有关作者的信息、版权或文件链接|
|nav|导航链接|可以是当前文档内的，也可以是到其他文档的。常见例子是菜单、目录和索引|
|main|文档主内容|中心主题直接相关或扩展的内容|
|article>|文章|自成一体，独立分发，可重复使用|
|section|文档中的节|没有一个更具体的语义元素来代表|
|aside|页面内容以外的内容|其内容与文档的主要内容只有间接的关系。经常以边栏或呼出框的形式出现|
|mark|重要或强调的文本|为参考或记事目的而被标记或突出的文本，表明其相关性和重要性|
|summary|details标题|为details指定一个摘要、标题或图例。点击summary可以切换details打开和关闭|
|details|用户能够查看或隐藏的额外细节|其中的信息只有被切换到"打开"状态时才可见。必须使用summary提供一个摘要或标签|
|figure|自包含内容|独立的内容，用figcaption元素指定一个可选的标题。比如图示、图表、照片、代码清单等|
|figcaption|figure的标题|描述其父元素|
|time|定义日期/时间|可能包括datetime属性，将日期翻译成机器可读的格式，以便获得更好的搜索引擎结果或自定义功能。如提醒|
## 块元素和行内元素
在网页中一般使用块元素来网页布局，行内元素来包裹文字。
一般在块元素中放行内元素。
## 布局标签
![Pasted image 20230217160815](https://article.biliimg.com/bfs/article/0386fe4b456a841be7bed1471dd75da8b8956ff2.png)
- header表示网页的头部（页眉）
- main表示网页的主体部分（一个页面中只会有一个main） 
- footer表示网页的底部（页脚）
- nav表示网页中的导航
- aside和主体相关的其他内容（侧边栏）
- article表示一个独立的文章
- section表示一个独立的区块，上边的标签都不能表示时使用section
- div 块元素，没有任何的语义，就用来表示一个区块。目前来讲，div还是主要的布局元素
- span 行内元素，没有任何的语义，一般用于在网页中选中文字

## 列表
- 有序列表，使用`ol`标签来创建有序列表，使用`li`表示列表项
- 无序列表，使用`ul`标签来创建无序列表，使用`li`表示列表项
- 定义列表，使用`dl`标签来创建定义列表，使用`dt`表示定义的内容，使用`dd`来对内容进行解释说明 

## 超链接
超链接可以让我们从一个页面跳转到其他页面，或者是当前页面的其他的位置，使用`a`标签来定义超链接，`href`属性指定跳转的目标路径，值可以是一个外部网站的地址，也可以写一个内部页面的地址。超链接是也是一个行内元素，在`a`标签中可以嵌套除它自身外的任何元素。
`target`属性，用来指定超链接打开的位置可选值：
- self在当前页面中打开超链接，默认值
- blank在新建页面中打开超链接

## 锚点
可以使用`javascript:void(0);`来作为`href`的属性，此时点击这个超链接什么也不会发生。可以将`#`作为超链接的路径的占位符使用。
可以直接将超链接的`href`属性设置为`#`，这样点击超链接以后页面不会发生跳转，而是转到当前页面的顶部的位置，可以跳转到页面的指定位置（锚点），只需将`href`属性设置`#`目标元素的`id`属性值（唯一不重复）。

## 图片
图片标签用于向当前页面中引入一个外部图片。
`img`标签是一个自结束标签，这种元素属于替换元素（块和行内元素之间，具有两种元素的特点）
**属性**
- `src`：属性指定的是外部图片的路径（路径规则和超链接是一样的）
- `alt`：图片的描述，这个描述默认情况下不会显示，有些浏览器会在图片无法加载时显示，搜索引擎会根据`alt`中的内容来识别图片
- `width`：图片的宽度（单位是像素）
- `height` ：图片的高度（单位是像素）
- 宽度和高度中如果只修改了一个，则另一个会等比例缩放
**注意**
- 一般情况在pc端，不建议修改图片的大小，需要多大的图片就裁多大
- 但是在移动端，经常需要对图片进行缩放（大图缩小）

将图片使用`base64`编码，这样可以将图片转换为字符，通过字符的形式来引入图片。

## 内联格式
内联框架`iframe`，用于向当前页面中引入一个其他页面
- `src`指定要引入的网页的路径
- `frameborder`指定内联框架的边框

## 音频视频
`audio`标签用来向页面中引入一个外部的音频文件。音视频文件引入时，默认情况下不允许用户自己控制播放停止。
**属性**
`controls`是否允许用户控制播放。
`autoplay`音频文件是否自动播放，如果设置了`autoplay`，则音乐在打开页面时会自动播放，但是目前来讲大部分浏览器都不会自动对音乐进行播放。
`loop`音乐是否循环播放。

使用`video`标签来向网页中引入一个视频，使用方式和`audio`基本上是一样的。

# CSS语法
## 样式
- 内联样式
```html
<p style="color:red;font-size:60px;">内联样式（行内样式）</p>
```
- 内部样式
```html
<style>
p{
    color:green; 
    font-size:50px;
}
</style>
```
- 外部样式
```html
<link rel="stylesheet" href="./style.css">
```

## 声明块
基本格式如下。
```css
h1{
    color: green;
}
```

## 选择器
### 通配选择器
选中页面中的所有元素。如果后面有声明别的选择器，就会把这个通配的配置覆盖掉。
```css
*{
    color: red;
}
```
### 元素选择器
根据标签名来选中指定的元素。
```css
/* p标签 */
p{
    color: red; 
}

h1{
    color: green;
}
```
### 类选择器
根据元素的`class`属性值选中一组元素。
可以同时为一个元素指定多个`class`属性。
```css
.blue{
    color: blue;
}

.size{
    font-size: 20px;
}
```
### id选择器
根据元素的`id`属性值选中一个元素。
```css
#red{
    color: red;
}
```
### 属性选择器
根据元素的属性值选中一组元素。
- [属性名]选择含有指定属性的元素
- [属性名=属性值]选择含有指定属性和属性值的元素
- [属性名^=属性值]选择属性值以指定值开头的元素
- [属性名$=属性值]选择属性值以指定值结尾的元素
- [属性名*=属性值]选择属性值中含有某值的元素
```html
<style>
    input[type] {
        color: aqua;
    }
</style>

<body>
    <div>
        <form action="">
            <label>Login</label>
            <input type="text" value="用户名">
            <br>
            <label>Password</label>
            <input type="password" value="密码">
        </form>
    </div>
</body>
```
### 复合选择器
#### 交集选择器
选中同时复合多个条件的元素。
注意：交集选择器中如果有元素选择器，必须使用元素选择器开头。
```css
<style>
    p.two {
        color: red;
    }
</style>

<body>
    <div>
        <p class="one two">hhhhh </p> <!--这两个受到影响-->
        <p class="two">jjjjjj</p>     <!--这两个受到影响-->
        <p class="three">kkkkk</p>
    </div>
</body>
```
#### 并集选择器（选择器分组）
同时选择多个选择器对应的元素。
```css
<style>
    /* 只影响one、two两个 */
    .one,.two {
        color: red;
    }

    /* 下面的配置影响全部 */
    p,h1 {
        border: 2px;
        border-color: blue;
        border-style: dashed;
    }
</style>

<body>
    <div>
        <p class="one">hhhhh </p>
        <p class="two">jjjjjj</p>
        <p class="three">kkkkk</p>
        <h1 class="four">llllll</h1>
    </div>
</body>
```
### 关系选择器
- 父元素：直接包含子元素的元素叫做父元素
- 子元素：直接被父元素包含的元素是子元素
- 祖先元素：直接或间接包含后代元素的元素叫做祖先元素；一个元素的父元素也是它的祖先元素
- 后代元素：直接或间接被祖先元素包含的元素叫做后代元素；子元素也是后代元素
- 兄弟元素：拥有相同父元素的元素是兄弟元素
#### 子元素选择器（Child combinator）
选中指定父元素的指定子元素。
父元素 > 子元素。
```css
<style>
	/* 影响div下的p标签 */
    div>p {
        color: red;
    }
</style>

<body>
    <div>
        <p class="one">hhhhh </p>
        <p class="two">jjjjjj</p>
        <p class="three">kkkkk</p>
        <h1 class="four">llllll</h1>
    </div>
</body>
```
#### 后代元素选择器（Descendant combinator）
选中指定元素内的指定后代元。
祖先 后代。
```css
<style>
    div span {
        color: red;
    }
</style>

<body>
    <div>
        <p class="one">hhhhh </p>
        <p class="two">jjjjjj</p>
        <p class="three">kkkkk</p>
        <span>span</span>
    </div>
</body>
```
#### 兄弟元素选择器（Sibling combinator）
选择下一个兄弟。
前一个 + 下一个；前一个 + 下一组
```css
p + span{
    color: red;
}

p ~ span{
    color: red;
}
```
### 伪类选择器
```css
/* ul下所有li，黑色 */
ul>li {
    color: black;
}

/* ul下第偶数个li，黄色 */
ul>li:nth-child(2n) {
    color: yellow;
}

/* ul下第奇数个li，绿色 */
ul>li:nth-child(odd) {
    color: green;
}

/* ul下第一个li，红色 */
ul>li:first-child {
    color: red;
}

/* ul下最后一个li，黄色 */
ul>li:last-child {
    color: orange;
}
```
### 伪元素选择器

# 样式继承与其他概念
## 继承
样式的继承，我们为一个元素设置的样式，同时也会应用到它的后代元素上继承是发生在祖先后后代之间的，继承的设计是为了方便我们的开发。
利用继承，我们可以将一些通用的样式，统一设置到共同的祖先元素上。这样只需设置一次即可让所有的元素都具有该样式。
注意，并不是所有的样式都会被继承。

## 选择器的权重
| 选择器 | 权重 |
| ------ | ---- |
|内联样式|1, 0, 0, 0|
|ID选择器|0, 1, 0, 0|
|类和伪类选择器|0, 0, 1, 0|
|元素选择器|0, 0, 0, 1|
|通配选择器|0, 0, 0, 0|
|继承的样式|没有优先级|
可以在某一个样式的后边添加`!important`，则此时该样式会获取到最高的优先级，甚至超过内联样式，注意：在开发中一定要慎用！

## 长度单位
1. 像素
像素pixel，缩写成`px`。像素是指由图像的小方格组成的，这些小方块都有一个明确的位置和被分配的色彩数值，小方格颜色和位置就决定该图像所呈现出来的样子。
可以将像素视为整个图像中不可分割的单位或者是元素。不可分割的意思是它不能够再切割成更小单位抑或是元素，它是以一个单一颜色的小格存在。每一个点阵图像包含了一定量的像素，这些像素决定图像在屏幕上所呈现的大小。
`分辨率 = 水平方向像素 * 垂直方向像素`

2. 百分比
也可以将属性值设置为相对于其父元素属性的百分比，可以使子元素跟随父元素（暂且先理解成父元素，后面会详细说）的改变而改变。
- `em`：em是相对于元素的字体大小来计算的，`1em = <self>.font-size`，也就说em值会根据元素本身的字体大小的改变而改变。
- `rem`：rem是相对于根元素的字体大小来计算，`1em = <root>.font-size`，也就说em值会根据根元素的字体大小的改变而改变。

## 颜色单位
1. RGB：RGB通过三原色的不同浓度来调配出不同的颜色
- 语法：RGB(red, green, blue)
- 范围：每一种颜色的范围在0 ~ 255（0% ~ 100%）之间

2. RGBA：就是在rgb的基础上增加了一个a表示不透明度
- `·1`表示完全不透明
- `0`表示完全透明
- `.5`表示半透明

3. 十六进制的RGB值
- 语法：#RRGGBB
- 范围：每一种颜色的范围在00~ff之间

# 盒子模型
## 文档流（normalflow）
网页是一个多层的结构，一层摁着一层。
通过CSS可以分别为每一层来设置样式，作为用户来讲只能看到最顶上一层，这些层中，最底下的一层称为文档流，文档流是网页的基础我们所创建的元素默认都是在文档流中进行排列，对于我们来元素主要有两个状态：
- 在文档流中
- 不在文档流中（脱离文档流）

## 块元素
1. 块元素会在页面中独占一行
2. 默认宽度是父元素的全部（会把父元素撑满）
3. 默认高度是被内容撑开（子元素）

## 行内元素
1. 行内元素不会独占页面的一行，只占自身的大小
2. 行内元素在页面中左向右水平排列（书写习惯一致）
3. 如果一行之中不能容纳下所有的行内元素，则元素会换到第二行继续自左向右排列
4. 行内元素的默认宽度和高度都是被内容撑开

## 盒子模型
网页设计中常听的属性名：内容(content)、内边距(padding)、边框(border)、外边距(margin)， CSS盒子模型都具备这些属性。
这些属性我们可以用日常生活中的常见事物——盒子作一个比喻来理解，所以叫它盒子模型。
CSS盒子模型就是在网页设计中经常用到的CSS技术所使用的一种思维模型。
![Pasted image 20230220125442](https://article.biliimg.com/bfs/article/6c46ef541e2a149ed35e61fe2f43f2b4a5acf02f.png)

每一个盒子都由一下几个部分组成：
1. 内容区（content）
内容区是盒子模型的中心，它呈现了盒子的主要信息内容，这些内容可以是文本、图片等多种类型。
元素中的所有的子元素和文本内容都在内容区中：
- width和height 设置排列内容区的大小
- width 设置内容区的宽度
- height 设置内容区的高度

2. 内边距（padding）
内边距，也叫填充，是内容区和边框之间的空间。
padding内边距的简写属性，可以同时指定四个方向的内边距，规则和边框中属性值设置一样。

4.  边框（border）
边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部。
边框的大小会影响到整个盒子的大小。

3. 外边距（margin）
外边距，也叫空白边，位于盒子的最外围，是添加在边框外周围的空间。空白边使盒子之间不会紧凑地连接在一起，是CSS 布局的一个重要手段。
注意：外边距不会影响盒子可见框的大小，但是外边距会影响盒子的位置和占用空间。

## 水平方向布局
元素在其父元素中水平方向的位置由以下几个属性共同决定：
- margin-left
- border-left
- padding-left
- width
- padding-right
- border-right
- margin-right
一个元素在其父元素中，水平布局必须要满足以下的等式。
`margin-left + border-left + padding-left + width + padding-right + border-right + margin-right = 其父元素的宽度`
以上等式必须满足，如果相加结果使等式不成立，则称为`过渡约束`。

## 垂直方向布局
元素溢出：子元素是在父元素的内容区中排列的，如果子元素的大小超过了父元素，则子元素会从父元素中溢出。
使用`overflow/overflow-x/overflow-y`属性来设置父元素如何处理溢出的子元素
可选值：`visible/hidden/scroll/auto`
`visible`溢出内容会在父元素外部位置显示，默认值。

边距折叠
垂直外边距的重叠（折叠）：相邻的垂直方向外边距会发生重叠现象。

兄弟元素
兄弟元素间的相邻，垂直外边距会取两者之间的较大值（两者都是正值）。

特殊情况：
- 如果相邻的外边距一正一负，则取两者的和
- 如果相邻的外边距都是负值，则取两者中绝对值较大的




# 
