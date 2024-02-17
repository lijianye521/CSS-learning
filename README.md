# 精通CSS

> caiye个人学习精通CSS：高级Web标准解决方案（第三版）一书中的读书笔记，网上的教程千奇百怪，还是自己读读书看看文档练习练习来的方便。
>
> 本读书笔记代码仓库：https://github.com/lijianye521/CSS-learning.git

## 第一章 基础知识

HTML5新增的一些元素

section header footer nav article aside main

## 第二章 添加样式

### 2.1CSS选择器

类型选择符用于选择特定类型的元素，比如段落或标题

```css
p{
color:black;
}
```

后代选择符用于选择某个或某组元素的后代‘

```css
blockquote p{
    padding-left:2em;
}
```

为了更精确的选择目标元素，可以使用ID选择符和类选择符

```css
#intro{
font-weight:bold;
}
.date-posted{
color:#ccc;
}
```

此外id和类选择符可以混合使用 不必为所有元素都添加ID和类选择符

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
#latest h1 {
font-size:1.8em;
}
#latest .date-posted{
font-weight:bold;
color: blueviolet;
}

    </style>
</head>
<body>
    <!-- <i>caiye</i><p>caiye</p> -->
<article id="latest">
    <h1>Happy Birthday,Andy</h1>
    <p class="date-posted">
        <time datetime="2013-01-20">
            20/1/2013
        </time>
    </p>
</article>
</body>
</html>
```

#### 2.1.1子选择器与同辈选择器

子选择符只选择一个元素的直接后代，也就是子元素。

此例子为外部列表项nav的子元素li都会有自定义标签，其他的子元素没有 并且li标签下嵌套的li标签也没有这个样式。（也就是只给列表的子元素添加样式 ，孙子元素不受影响）

```css
#nav > li{
background:url(folder.png) no-repeat left top;
    padding-left:20px;
}
```

![image-20240211151120007](./assets/image-20240211151120007.png)

相邻同辈选择器可以用于选择位于某个元素后面，并与该元素拥有共同父元素的元素。

```css
h2 + p {
    font-size:1.4em;
    font-weight:bold;
    colorl:#777;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        h2 + p {
    font-size:1.4em;
    font-weight:bold;
    color:#777;
}
    </style>
</head>
<body>
    <h2>
        我是h2标签
    </h2>
    <p>
        我是紧跟h2后面的p标签 ，是相邻同辈
    </p>

</body>
</html>
```

![image-20240211151655139](./assets/image-20240211151655139-1707635933269-6.png)

\>和+在这里为组合子，/>子组合子和+相邻同辈组合子 实际上还存在一般同辈组合子：~。使用一般同辈选择符可以选择h2元素后面的所有段落

```css
h2 ~ p {
	font-size:1.4em;
    font-weight:bold;
    color:#777;
}
```

#### 2.1.2 通用选择器

通用选择符可以匹配任何元素。通用选择符使用星号*来表示，我们可以使用通用选择符来删除所有元素默认的内外边距。

```css
* {
	padding: 0;
    margin: 0;
}
```

#### 2.1.3属性选择器

属性选择器基于元素是否有某个属性或者是否有某个值来选择元素。

#### 2.1.4伪元素

我们想选择的页面区域不是通过元素来表示的，而我们也不想为此给页面添加额外标记。css为这种情况提供了一种特殊选择器，伪元素。

::first-letter 选择一段文本的第一个字符

::first-line 选择一段文本的第一行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .chapter::before{
            content:'”';
            font-size:3em;
        }
        .chapter p::first-letter{
            float: left;
            font-size: 3em;
            font-family: Georgia, 'Times New Roman', Times, serif;
        }
        .chapter::first-line{
            font-family: Georgia, 'Times New Roman', Times, serif;
            text-transform: uppercase;
        }

    </style>
</head>
<body>
    <h1>A Study In Scarlet</h1>
    <section class="chapter">
        <p>
            In the year 1878 I took my degree of Doctor of Medicine of the University of London,and proceeded 
            to Netley to go throuogh thr course prescribed for surgeons in the army.Having completed
            my studies there, I was duly attached to the Fifth Northumberland Fusiliers as Assistant Surgeon.
        </p>
    </section>
</body>
</html>
```

![image-20240216205833455](./assets/image-20240216205833455-1708088316692-3-1708088317818-5.png)

#### 2.1.5伪类

伪类选择器的语法是以一个冒号开头，用于选择元素的特定状态或关系。

```css
   /* 未访问的链接为蓝色 */
        a:link{
            color:blue;
        }
        /* 访问过的为绿色 */
        a:visited{
            color: green;
        }
        /* 悬停及获取键盘焦点时为红色 */
        a:hover,a:focus{
            color:red;
        }
        /* 活动状态时为紫色 */
        a:active{
            color: purple;
        }
```

#### 2.1.6结构化伪类

:nth-child选择器可以用来交替为表格行应用样式。

:nth-child可以像函数一样接受参数如odd和even

```css
tr:nth-child(odd){
background:yellow;
}
/*表格从第一行开始，在后面每隔一行变成黄色背景。就是奇数行变为黄色*/
```

:nth-last-child 与:nth-child相似，只不过倒着计算

:last-child对应于:nth-last-child(1) 选择最后一个子元素

:nth-of-type(N)会选择特定类型的唯一子元素

#### 2.1.7表单伪类

:required必填 :optional可选

```css
input[type="email"]:valid{
    border-color:green;
}
input[type="email"]:invalid{
    border-color:red;
}
```

此外针对type值为number的含有:in-range、:out-of-range伪类，针对readonly有read-only伪类。

### 2.2层叠

稍微复杂的样式表可能存在两条甚至多条规则选择一个元素的情况。CSS通过一种叫做层叠的机制来处理这种冲突。

为给用户更高的优先权，CSS允许用户使用!important覆盖任何规则，包括网站作者使用!important标注的规则。!important要放在属性声明的后面。

```css
p{
font-size: 1.5em !important;
color:#666 !important;  
}
```

层叠机制的重要性级别从高到低分别为

> 标注为!important的用户样式；
>
> 标注为!important的作者样式；
>
> 作者样式；
>
> 用户样式；LO
>
> 
>
> 浏览器（或用户代码）的默认样式。

在此基础上，规则再按照选择器的特殊性排序。特殊性高的选择器覆盖特殊性低的选择器。如果两条规则的特殊性相等，则后定义的规则优先。

### 2.3特殊性（也就是选择器的权重）

### 特殊性的权重

1. **内联样式**：具有最高的特殊性，记作（1,0,0,0）。
2. **ID选择器**：特殊性次之，记作（0,1,0,0）。
3. **类选择器、属性选择器和伪类**：特殊性更低，记作（0,0,1,0）。
4. **类型选择器和伪元素**：具有最低的特殊性，记作（0,0,0,1）。

![image-20240216221108159](./assets/image-20240216221108159-1708092669514-7.png)

向量中的四个数字从高位开始比较 如果相同则比较下一位。

本质上而言，如果样式被写在了元素的style属性里的特殊性>写在id属性应用的规则>类选择器，属性选择器和伪类>类型选择器和伪元素

如果真要比较某个相同等级选择器的优先级，需要计算特殊性，此外，如果权重相同，那么以定义顺序靠后的选择器优先，或者有**!important**标记优先。理论上行内样式就是最高的优先级，但是可能会被!important覆盖。

#### 控制特殊性

尽量的采用低特殊性的选择器，对于伪类的顺序应该是:link,:visited,:hover,:focus和:active

> 记住这个就行了
>
> Lord Vader Hates Furry Animals

### 2.4继承

有些属性，像颜色或字体大小，会被应用于它们的元素的后代所继承。

继承的属性没有任何特殊性 连0都算不上。

通用选择符的特殊性为0，但是仍优先于继承的属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=!, initial-scale=1.0">
    <title>Document</title>
    <style>
    .father{
        color:green;
    }
    *{
        color:black;
    }
    h2{
        color:red;
    }</style>
</head>
<body>

    <p>我是黑色</p>
    <h2>我h2的特殊性高
    </h2>
    <div class="father">
        <p>我本来能继承father的green 但是通用选择符让我是黑色</p>
    </div>
</body>
</html>
```

### 2.5为文档应用样式

#### 2.5.1 link与style元素

```html
<!--可以直接写在style标签中-->

<style>
        h2 + p {
    font-size:1.4em;
    font-weight:bold;
    color:#777;
}
    </style>
<!--从外部文件引用  增加了css样式的复用-->
<link href="/c/base.css" ref="stylesheet" />
<!--除了link元素以外，还可以使用@import指令加载外部css文件 但是link更推荐  后序会讲-->
<style>
@import url("/c/modules.css");
</style>
```

 使用lnik或style在html中添加多个样式表或者样式块时，他们声明的次序就是他们在html源代码中出现的次序。

```html
<link ref="stylesheet" href="css/sheet1.css">
<style>
@import url("/c/sheet2.css");
    h1{
		color:red;
    }
</style>
<link ref="stylesheet" href="css/sheet3.css">

```

最后sheet3.css中的h2样式胜出，因为他是最后一个。

#### 2.5.2性能

度量web性能的一个重要指标就是网页内容实际显示在屏幕上需要多久。这个指标有时也叫“渲染时间”或“上屏时间”

不要把CSS放到body里或者放到页面底部。

**1.减少HTTP请求**

在链接外部样式表时，保证链接的文件数量最少至关重要。线上网页最好把需要加载的CSS文件控制在一个或者两个。此外线上网页尽量也不要使用@import 因为一个请求下载链接受的文件还要额外发送请求取得所有导入的文件。

**2.压缩和缓存内容**

使用gzip压缩线上资源，CSS压缩的比率很高。一般来说CSS文件压缩后会减少70%-80%。

类似的，让Web服务器帮你设置一定的CSS文件缓存时间也很重要。理想情况 下，浏览器只下载一次CSS文件。除非线上文件有变化。方法就是通过HTTP首部来告诉浏览器，把文件缓存较长的一段时间，如果文件有修改，则通过文件名来“清楚缓存”。

> 通过HTTP首部控制浏览器缓存是优化网页加载速度和减少服务器负担的有效方法。以下是实现此目的的常见方法：
>
> ### 1. 缓存控制 HTTP 首部
>
> - **Cache-Control**：这个HTTP首部字段可以用来定义资源的缓存策略。常用的值包括`max-age`（资源可以被缓存并且被重用的最大时间，单位是秒），`no-cache`（强制每次请求都去服务器验证），`no-store`（完全不缓存此资源），等等。例如，`Cache-Control: max-age=31536000`告诉浏览器，资源可以在本地缓存并且在接下来的一年内使用，不需要再去服务器请求。
>
> ### 2. ETag 和 If-None-Match
>
> - **ETag**：是资源的唯一标识符，服务器使用它来识别资源状态是否有变化。
> - 当浏览器第一次请求资源时，服务器在响应中包含一个`ETag`值。当浏览器再次请求该资源时，会发送一个`If-None-Match`请求头，其值为之前收到的`ETag`值。如果`ETag`未改变，服务器返回304状态码，表示内容未修改，浏览器可以从缓存加载资源。如果`ETag`值有变化，则服务器会发送新的资源和`ETag`。
>
> ### 3. 使用文件名版本控制清除缓存
>
> - **文件名版本控制**：当你想强制浏览器清除缓存并获取最新版本的文件时，可以通过更改文件名来实现。这种方法常见于对静态资源如CSS和JavaScript文件的管理。例如，如果你有一个`style.css`文件，可以将其重命名为`style.v2.css`来指示这是一个新版本的文件。通过更改文件名，你实际上改变了资源的URL，因此浏览器会认为这是一个全新的资源并发起新的请求。
>
> ### 实现示例
>
> 假设你有一个CSS文件，名称为`style.css`。在对其进行更新后，你想确保所有用户都能获取到最新版本。你可以这样操作：
>
> 1. 在服务器配置中设置`Cache-Control`首部，为CSS文件指定一个长时间的缓存周期，比如一年（`Cache-Control: max-age=31536000`）。
> 2. 更新CSS文件后，更改其名称，比如从`style.css`更改为`style.v2.css`。
> 3. 更新所有引用该CSS文件的HTML或其他文件，确保它们指向新的文件名。
>
> 这样，即使旧的CSS文件被缓存了很长时间，更改文件名也能保证用户访问时获取的是最新版本的文件。

**3.不让浏览器渲染阻塞javascript**

渲染阻塞会拖慢网站下载速度。为此，主流的做法是在HTML页面底部的结束标签</body>之前加载javascript。

比较现代的方式是在head中使用<script>标签，但是添加async和defer属性。

asycn属性会异步加载脚本，不阻塞HTML解析，但会在脚本加载完毕执行时阻断HTML解析。

defer属性同样是异步加载脚本，不同的是会在HTML解析完毕后在执行加载的脚本。

## 第三章 可见格式化模型

### 3.1盒模型

盒模型是CSS的核心概念，描述了元素如何显示，以及（在一定程度上）如何相互作用，相互影响。outline这个属性（轮廓线）可以在盒子外围画出一条线

![image-20240217191109352](./assets/image-20240217191109352-1708168270407-1.png)

#### 3.1.1盒子大小

默认情况下，元素盒子的width和height属性是指内容盒子，也就是元素可渲染内容区域的宽度和高度。这个时候添加边框和内边距不会影响盒子的大小，但是会让盒子变大。

```css
    .mybox{
            width: 80px;
            padding:5px;
            border:5px solid;
            margin:10px;
            background-color: bisque;
        }
```

![image-20240217191516214](./assets/image-20240217191516214-1708168518020-3.png)

box-sizing属性可以改变计算盒子大小的方式。box-sizing的默认值为content-box。（对应着标准盒模型）

可以修改box-sizing的值来将width和height属性的值付给内边距和边框。

```css
    .mybox{
          box-sizing:border-box;
            width: 80px;
            padding:5px;
            border:5px solid;
            margin:10px;
            background-color: bisque;
        }
```

![image-20240217191938018](./assets/image-20240217191938018-1708168779087-5.png)

内边距和外边距的值可以是CSS规范中规定的任意长度单位px，em，百分比之类。

```css
.block{
    margin-left:5%;
}
```

这里的百分之5是指父元素.group的百分之5。如果.group的宽度是100像素，那么这里左边距就是5像素。

因元素的高度常常不被声明，因内容多少而差异很大，所以CSS规定，上下方位的内外边距，仍然基于包含块来计算。这里，包含块就是父元素，但是有时候规则不一定。具体后序再讲。

#### 3.1.2最大值和最小值

max-width和min-width

max-height和min-height(max-height慎用 容易让内容跑到固定高度之外去)

### 3.2课件格式化模型

p，h1和article都是block box 块级盒子

strong，span 和time 都是inline box 行内盒子

可以使用display属性改变生成的盒子模型。比如把span的display改为block，让span变成块级元素。如果把display改为none，还可以让浏览器不为相应元素生成盒子。

CSS中有几种不同的定位模型，包括浮动、绝对定位和相对定位。

由一行文本形成的水平盒子叫做行盒子，而行盒子的高度由所包含的行内盒子决定，修改行盒子大小的唯一途径就是修改行高 line-height。

![image-20240217194455888](./assets/image-20240217194455888.png)

#### 3.2.1匿名盒子

不明确定义的元素也会生成块级盒子，也就是**匿名块盒子**。

```css
<section>
some text
<p>
Some more text</p>
</section>
```

"some text"就算没有定义为块级元素 也会生成块级盒子。因为这个盒子不与任何特定元素相关。此外还会存在**匿名行盒子**，比如一个段落包含三段文本，那么每一个文本都是一个**匿名行盒子**。

#### 3.2.2外边距折叠

垂直方向上的两个外边距相遇时，会折叠成一个外边距，折叠后外边距的高度等于两者中较大的那一个高度。

![image-20240217195326851](./assets/image-20240217195326851.png)

![image-20240217195342959](./assets/image-20240217195342959.png)

![image-20240217195352397](./assets/image-20240217195352397.png)

![image-20240217195403134](./assets/image-20240217195403134.png)

外边距折叠只发生在文档常规文本流中会计盒子的垂直方向上。行内盒子、浮动盒子或绝对定位盒子的外边距不会折叠。

#### 3.2.3包含块

确定元素的包含块，要看元素是如何定位的，如果元素的定位方式为静态定位（即不指定position属性的值）或相对定位，则其包含块的边界就计算到最近的父元素，该元素的display属性必须能够提供类似的块级上下文（如block、inline-block、table-cell、list-item）。如果当前元素的定位模型改成了absolute或者fixed，那么计算依据就会发生变化。
