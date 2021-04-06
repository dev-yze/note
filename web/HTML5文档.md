### 一、H5开发和HTML5



### 二、html改变

#### 1、语法改变

##### 1）标记方法

- DOCTYPE声明

  改变，不用声明版本,不区分大小小，不区分单双引号

  ```html
  <!DOCTYPE html>
  ```

  使用工具时，也可以在DOCTYPE声明中加入SYSTEM识别符，声明如下：

  ```
  <!DOCTYPE HTML SYSTEM "about:legacy-compat">
  ```

  ​	识别符和html引用传统dtd差不多，legacy-compat表示传统的html文档类型定义

- 指定字符编码

  用meta元素指定字符编码

  ```html
  <!-- h4 -->
  <meta http-equiv="Content-Type" content="text/html;chartset=UTF-8">
  <!-- h5-->
  <meta chartset="UTF-8">
  ```

##### 2）确保兼容性

- 可以省略标记的元素

  - 不允许写结束标记

  area、base、br、col、command、embed、hr、img、input、keygen、link、meta、param、source、track、wbr

  - 可以省略结束标记

  li、dt、dd、p、rt、rp、optgroup、option、colgroup、thead、tbody、tfoot  、tr、td、th

  - 可以省略全部标记

  html head body colgroup tbody

- 具有boolean值的属性

  只写属性不写属性值时默认为true,将属性值设为true时，可以将属性名或空字符串设为属性值

- 省略引号

  当属性值不包括空字符串、“<”、">"、"="、单引号、双引号等字符时, 属性值两边的引号可以省略

#### 2、新增元素和废除元素

- 新增结构元素
  - section
  - article
  - aside
  - header
  - footer
  - nav
  - figure
  - main
  - 
- 新增的其它元素
  - video
  - audio
  - embed
  - mark
  - progress
  - meter
  - time
  - ruby
  - rt
  - rp
  - wbr
  - canvas
  - details
  - datalist
  - datagrid
  - output
  - source
  - dialog
- 新增的input元素的类型
  - email
  - url
  - number
  - range
  - Date Pickers
  - date
  - month
  - week
  - time
  - datetime
  - datetime-local
- 废除的元素

#### 3、新增属性和废除属性

- 表单相关属性
  - input
    - autofocus
    - placeholder
    - form
    - required
    - autocomplete
    - min
    - max
    - multiple
    - pattern
    - step
    - formaction
    - formenctype
    - formmethod
    - formnovalidate
    - formtarget
    - novalidate
    - labels
    - SelectionDirection
    - indeterminate
    - height、width
    - maxlength,wrap

#### 4、全局属性

#### 

# HTML头部

## (一) DOCTYPE声明

改变，不用声明版本,不区分大小小，不区分单双引号

```html
<!DOCTYPE html>
```

使用工具时，也可以在DOCTYPE声明中加入SYSTEM识别符，声明如下：

```
<!DOCTYPE HTML SYSTEM "about:legacy-compat">
```

​	识别符和html引用传统dtd差不多，legacy-compat表示传统的html文档类型定义

## (二) 指定字符编码

用meta元素指定字符编码

```html
<!-- h4 -->
<meta http-equiv="Content-Type" content="text/html;chartset=UTF-8">
<!-- h5-->
<meta chartset="UTF-8">
```

## (三) 引用style和js

```html
<script src='jsname.js'></script>
<link rel="stylesheet" href="cssFileName.css">
```



# 结构标签

## (1) div

## (2) article

## (3) section

## (4) nav

## (5) aside

## (6) time

## (7) pubdate

# 表单标签

# 文件

# 本地存储

# XMLHttpRequest及Fetch

# webWorkers处理线程

# ServiceWorker

# 通信API

# web组件

# 图形绘制

# 多媒体API

# 扩展











() 

() 

() 

() 

() 

() 

() 

() 

() 

() 



