https://www.runoob.com/css/css-border.html



# `CSS`单位

## 绝对单位

​	cm、mm、in、pt、 pc等，很少使用

## 相对单位

常见相对单位有：像素px、百分比%、当前元素字体大小em、根元素字体大小rem,其它还有ex、vw和vh

- 像素px

  px，像素，指一张图片中最小的点或计算机屏幕中最小的点

  各种系统分辨率也不同,window系统的分辨率为每英寸96px，osx为每英寸72px

- 百分比%

  1)width、height、font-size

  2) line-height

  3)vertical-align

- 当前元素字体大小em

  当前元素字体大小指的是以px为单位的font-size值，font-size为10px，1em即为10px

  当前元素字体大小未定义，则继承父元素大小，所有祖先元素都未定义，继承浏览器默认的16px

  技巧

  - 首行缩进使用text-indent:2em实现
  - 使用em为统一单位 `body{font-size: 62.5%;}`

- 相对于根元素的字体大小rem

  相对于根元素html的font-size而言

- ex

- `vw`

- `vh`



# `CSS`特性

## 继承性

部分样式能够被子标签继承

主要是和文本相关

## 层叠性

## 优先级

### `CSS`优先级规则

- ID选择器 > 类选择器 > 标签选择器
- ID选择器数量更多， 则优先级更高
- ID选择器数量相同，则拥有最多类的选择器优先级更高
- 如果ID选择器和类选择器数量都相同，则标签选择器多的优先级更高
- 优先级相同，后面的样式会覆盖前面的样式
- !import 将优先级提升到最高

### `css`优先级案例

```css
// 四个标签选择器，优先级最低
html body header h1 {  
	color: blue;
}
// 三个标签一个类,优先级较低
body header.page-header h1 {
    color: orange
}
// 二个类选择器，优先级一般
.page-header .title {
    color: green
}
// 一个ID选择器，优先级最高
#page-title {
    color: red
}
```



### 优先级标记计算

用数值来计算: 

​	ID选择器数量,类选择器数量,标签选择器数量

或

​	行内样式标签,ID选择器数量,类选择器数量,标签选择器数量

上面的表示分别为:

```
0,0,4
0,1,3
0,2,0
1,0,0

行内样式标签：1-代表有，优先级最高;0-代表无
```



### 关键字

#### inherit继承

#### initial重置

# `CSS`规范

## 命名规范

### 文件命名

|    文件名     |   说明   |
| :-----------: | :------: |
|  `reset.css`  | 重置样式 |
| `global.css`  | 全局样式 |
| `themes.css`  | 主题样式 |
| `module.css`  | 模块样式 |
| `master.csss` | 母版样式 |
| `columns.css` | 专栏样式 |
|  `forms.css`  | 表单样式 |
|  `mend.css`   | 补丁样式 |
|  `print.css`  | 打印样式 |



### id命名和class命名

- 命名方法

  - 驼峰命名
  - 中划线命名
  - 下划线命名

- 命名规范

  - 网页主题部分

    | 网页部分 |   命名    |
    | :------: | :-------: |
    |  最外层  |  wrapper  |
    |   头部   |  header   |
    |   内容   |  content  |
    |   侧栏   |  sidebar  |
    |   栏目   |  column   |
    |   热点   |    hot    |
    |   新闻   |   news    |
    |   下载   | download  |
    |   标志   |   logo    |
    |  导航条  |    nav    |
    |   主体   |   main    |
    |   左侧   | main-left |

  - 网页细节部分

    | 网页部分 | 命名          |
    | -------- | ------------- |
    | 主导航   | main-nav      |
    | 子导航   | sub-nav       |
    | 边导航   | side-nav      |
    | 左导航   | leftside-nav  |
    | 右导航   | rightside-nav |


## 书写规范

书写顺序

- 布局属性 display position float clear
- 盒模型 margin、padding
- 文本性属性 text font
- 装饰性属性 color backgroud-colr opacity cursor
- 其它属性 content list-style quotes

## 注释规范

- 顶部注释

- 模块注释

- 简单注释

- 发布保留注释

  ```
  /*! 保留注释内容 */
  ```

## `CSS` reset

​	重置样式，去除浏览器默认样式



# 文字和字体

### 文本属性

| 属性             | 描述                                                         |
| ---------------  | ------------------------------------------------------------ |
| color           | 设置文本颜色                                                 |
| direction       | 设置文本方向 { ltr: “左到右”, rtl: “右到左”, inherit: “继承父元素” } |
| letter-spacing  | 设置字符间距                                                 |
| line-height     | 设置行高，一行的高度，一般浏览器默认为110%-120%              |
| text-align      | 对齐元素中的文本 { left: “”, right: “”, center: “”, justify: “两端对齐”, inherit: “”} |
| text-decoration | 向文本添加修饰 {none: “”, underline: “下划线”, overline: “文本上线”,<br /> line-through: “穿过文本线”, blink: “定义闪烁的文本”, inherit: “继承”} |
| text-indent     | 缩进元素中文本的首行                                         |
| text-shadow     | 设置文本阴影                                                 |
| text-transform  | 控制元素中的字母 { none: “默认大小写”,  capitalize: “每个单词大写字母开头”,<br /> uppercase:  “仅有大写字母“, lowercase: “”仅有小写字母, inherit} |
| unicode-bidi    | 设置或返回文本是否重写                                       |
| vertical-align  | 设置元素的垂直对齐                                           |
| white-space     | 设置元素中空白的处理方式                                     |
| word-spacing    | 设置字间距                                                   |

#### 1、`color`

常用颜色有：

#### 2、`letter-spacing`与`word-spacing`

letter-spacing: 字符间距,单词字母之间的距离,中文汉字之间的距离 ,可为负值，重叠

word-spacing: 字间距, 单词与单词之间的距离

#### 3、`text-align`

justify: 文本两端对齐，使文本更加工整，建议文章使用

#### 4、text-decoration

blink: 

可以定义多个样式

```css
/*
dotted:虚线
wavy: 波浪线
*/
p.underover {
    text-decoration: underline overline dotted red;
}
```



#### 5、`text-indent`

```
使用em进行文本首行缩进
text-indent: 2em;
text-align: justify
logo搜索引擎优化
text-indent: -9999px
```



#### 6、text-shadow 

```css
/*
 h-shadow: 水平阴影，距离左上角水平距离，必须，允许负值
 v-shadow: 垂直阴影, 距离左上角垂直距离，必须，允许负值
 blur: 模糊的距离, 可选
 color: 阴影颜色，可选
*/
text-shadow: h-shadow, v-shadow, blur, color

h1 {text-shadow:1px 1px #FF0000;}


/* 白字阴影效果 */
h1
{
	color:white;
	text-shadow:2px 2px 4px #000000;
}
/* 氖辉光文字阴 */
h1
{
	text-shadow:0 0 3px #FF0000;
}
```

#### 7、unicode-bidi



#### 8、vertical-align



| baseline    | 默认。元素放置在父元素的基线上。                             |
| ----------- | ------------------------------------------------------------ |
| sub         | 垂直对齐文本的下标。                                         |
| super       | 垂直对齐文本的上标                                           |
| top         | 把元素的顶端与行中最高元素的顶端对齐                         |
| text-top    | 把元素的顶端与父元素字体的顶端对齐                           |
| middle      | 把此元素放置在父元素的中部。                                 |
| bottom      | 使元素及其后代元素的底部与整行的底部对齐。                   |
| text-bottom | 把元素的底端与父元素字体的底端对齐。                         |
| length      | 将元素升高或降低指定的高度，可以是负数。                     |
| %           | 使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。 |
| inherit     | 规定应该从父元素继承 vertical-align 属性的值。               |

#### 9、white-space

| normal   | 默认。空白会被浏览器忽略。                                   |
| -------- | ------------------------------------------------------------ |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。    |
| nowrap   | 文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |



### 字体

| Property     | 描述                                 |
| :----------- | :----------------------------------- |
| font         | 在一个声明中设置所有的字体属性       |
| font-family  | 指定文本的字体系列                   |
| font-size    | 指定文本的字体大小                   |
| font-style   | 指定文本的字体样式                   |
| font-variant | 以小型大写字体或者正常字体显示文本。 |
| font-weight  | 指定字体的粗细。                     |



# 链接



# 列表



# 表格



# 盒模型

盒模型指的是网页元素的结构。当指定一个元素的宽度或高度时，便设置了元素内容的尺寸

- 内边距  `padding`
- 边框 `border`
- 外边距 `margin`

border-box

作用：

1) 让内容居中

2) 创建等高列

3) 控制元素的间距



# 背景



# 边框

```css
border: border-width borderstyle border-color
```

#### 1、border-style

![image-20201127083547132](F:\note\web\css3\image-20201127083547132.png)



#### 2、border-width

- px、em、pt、cm登单位
- thick、medium、thin

#### 3、border-color

- name ,如‘red’
- rgb, 如‘rgb(255, 0, 0)’
- Hex，如“#ff00000”

#### 4、边框-单独设置各边

- border-top-style
- border-right-style
- border-bottom-style
- border-left-style

#### 5、边框角度

border-radius

```css
div {
	border:2px solid #a1a1a1;
	padding:10px 40px; 
	background:#dddddd;
	width:300px;
	border-radius:25px;
}
```

#### 6、盒阴影

```css
box-shadow: x y len color
```



# 轮廓

**轮廓：**outline绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用，outline属性规定元素轮廓的样式、颜色和深度

```css
outline: outline-color outline-style outline-width inherit
```



#### 1、outline-color



#### 2、outline-style



#### 3、outline-width



# 变形



# 动画



# 布局

布局一般是指对标题、导航栏、主要内容、脚注、表单等各构成要素进行合理编排，在CSS3之前主要是使用float属性或position属性进行页面的简单布局，CSS3加入了新的布局方式，可以进行更为便捷、复杂的页面布局

## 多栏布局



```css
	<style type="text/css">
        #container {
            /* width: 50em; */
        }
        div#div1 {
            width: 100em;
            /* 
                column-count: 规定分栏数量
                column-width:   规定每栏的宽度
                width: 每栏宽度之和/总宽度,规定了width后column-width失效，等分
                column-gap: 分栏之间的间隔
                column-rule: 栏与栏之间增加间隔线，设定间隔线的宽度、样式、颜色
             */
            column-count: 2;                
            -moz-column-count: 2;
            -webkit-column-count: 2;
            column-width: 10em;     
            -moz-column-width: 10em;
            -webkit-column-width: 10em;
            column-gap: 3em;
            -moz-column-gap: 3em;
            -webkit-column-gap: 3em;
            column-rule: 1px solid red;
            -moz-column-rule: 1px solid red;
            -webkit-column-rule: 1px solid red;
        }
        div#div2 {
            width: 100%;
            background-color: yellow;
            height: 200px;
        }
    </style>
```



## 盒布局



```css
<style type="text/css">
        #container {
            /* 
                盒布局
                父元素使用盒布局，子元素会自动调整对其高度
             */
            display: -moz-box;
            display: -webkit-box;
        }
        #left-sidebar {
            width: 200px;
            padding: 20px;
            background-color: orange;
        }
        #contents {
            width: 300px;
            padding: 20px;
            background-color: yellow;
        }
        #right-sidebar {
            width: 200px;
            padding: 20px;
            background-color: limegreen;
        
        }
        #left-sidebar, #contents, #right-sidebar {
            box-sizing: border-box;
        }
    </style>
```

​	多栏布局和盒布局区别、用法

- ​	多栏布局每栏宽度相等，不能指定某栏显示什么内容，适合显示文章内容时，不适合用于安排整个网页中由各元素组成的网页结构的时候
- 盒布局可以用来安排网页的结构,左中右，保持高度一致



## 弹性盒布局

适应窗口的变化，随着浏览器的高度宽度而改变

参考：

[阮一峰Flex布局]: http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html

#### 设置弹性盒布局

```css
#div {
	display: flex;
}
#div {
	display: inline-flex;
}
```

#### flex六大要素：

- flex-direction	指定弹性容器中子元素的排列方式

  ![img](https://upload-images.jianshu.io/upload_images/2326131-bbd36877856086ff.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp) 



​		属性值：

​		

| 值             | 描述                                 |
| -------------- | ------------------------------------ |
| row            | 默认值，元素将水平显示，沿主轴方向上 |
| row-reverse    | 与row相同，但以相反的顺序显示        |
| column         | 元素将垂直显示，沿侧轴方向上         |
| column-reverse | 与column相同，但是以相反的顺序       |



- flex-wrap          设置弹性盒子的子元素超出父容器是否换行

  flex-wrap属性规定flex容器是单行还是多行

  | 值           | 描述 |
  | ------------ | ---- |
  | nowrap       |      |
  | wrap         |      |
  | wrap-reverse |      |

  

- flex-flow           flex-direction 和 flex-wrap 的简写

- justify-content    设置弹性盒子元素在主轴（横轴）方向上的对齐方式

  | 值            | 描述                         |
  | ------------- | ---------------------------- |
  | flex-start    | 默认值，位于容器横轴开始位置 |
  | flex-end      | 位于容器横轴的结尾           |
  | center        | 位于容器横轴的中心           |
  | space-between | 子元素之间间距相等           |
  | space-around  | 子元素左右边距相等           |

  

- align-items          设置弹性盒子元素在侧轴（纵轴）方向上的对齐方式

- align-content     有多行时，设置行对齐，类似align-items

弹性布局子元素属性

- order	用整数值来定义排列顺序，数值小的排在前面

- flex-grow     一个数字，规定项目将相对于其他灵活的项目进行扩展的量，默认值是0

- flex-shrink    一个数字，规定项目相对于其它灵活项目进行伸缩的量

- flex-basis   一个长度单位或者一个百分比，规定元素的初始长度

- flex       用于设置或检索弹性盒模型对象的子元素如何分配空间

  flex属性是flex-grow、flex-shrink、flex-basis属性的简写

- align-self     允许单个项目与其它项目不一样的对齐方式，可以覆盖align-items属性，默认auto



## 网格布局

​	概述：新增的网格布局由一些不可见的垂直线以及水平线组成，这些垂直线和水平线之间划分了许多单元格，可以在其中放置页面内容，类似表格

- 线：垂直线和水平线
- 轨道：轨道为两根线之间的间隔
- 单元格：垂直线和水平线之间的交错部分
- 区域：一个区域可以由开发者指定的单元格组成的矩形，与线一样，可以给区域指定名称

​	

# `calc`()方法

​		calc()函数： 通过该方法来自动计算元素的宽度，高度等数值

```css
#foo {
	width: calc(50% - 10px);
}
```

​		calc函数还可以混合不同单位进行运算

```css
#container {
	height: calc(10em + 3px);
}
```

# 查询表达式

## （一）媒体查询表达式



## （二）特性查询表达式



# 其他重要样式和属性

#### （一）颜色相关样式

css3之前：

- 指定颜色的值只能为RGB颜色值
- 只能通过opacity来设置元素的透明度

css3增加了3种颜色值

- RGBA颜色值、HSL颜色值、HSLA颜色值
- 允许通过对RGBA颜色值和HSLA颜色值设定alpha通道的方法来更加容易地实现将半透明文字与图像互相重叠的效果

####  1、使用alpah通道来设定颜色

- 通过对rgb颜色设定alpha通道的方法来定义RGBA颜色

  RGBA颜色是指利用红色值(R)、绿色值(G)、蓝色值(B)、alpha通道值(A)来定义颜色,其中alpha通道值的范围是0-1.0,0表示完全透明，1表示完全不透明。

- 对HSL颜色设定alpha通道

  HSL颜色是指使用色调(H)、饱和度(S)、亮度(L)来定义颜色，其中色调值中用0或360表示红色，120表示绿色，240表示蓝色，当取值大于360时，实际的值等于该值除以360之后的余数。饱和度和亮度的取值范围均为0%到100%

  HSLA颜色是在HSL颜色上利用alpha通道的方法来定义，A即指通道透明度

#### 2、alpha通道与opacity属性的区别

​	opacity属性可以直接来设置颜色透明度，取值范围为0-1，0表示完全透明，1表示不透明

#### 3、指定颜色值为transparent

​	如果将颜色值指定为transparent，则会将背景、文字或边框等的颜色设定为完全透明，相当于使用了值为0的alpah通道



#### （二）用户界面相关样式



#### （三）使用initial属性值取消对元素的样式指定

1. 取消对元素样式的指定方法
   - 删除该样式代码
   - 删除元素class属性值
   - 使用initial属性值
2. initial属性值的作用是让各种属性使用默认值
3. 使用initial属性值并不等于取消样式设定的特例，如h1-h6



#### （四）用于控制鼠标事件的pointer-events属性

css3新增控制鼠标事件的pointer-events属性，如果将属性值指定为none,则不会出发鼠标事件

#### （五）实现CSS 3中滤镜特效

### 十三、常用布局案例

### 十四、其他

一、clientHeight、offsetHeight、scrollHeight、offsetTop、scrollTop区别

- clientHeight	网页可见区域高
- 网页正文全文高
- 网页可见区域高（包含边线的高）
- 网页被卷去的高
- 屏幕分辨率





