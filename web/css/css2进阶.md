### 一、css单位

#### 1、绝对单位

​	cm、mm、in、pt、 pc等，很少使用

#### 2、相对单位

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

### 二、CSS特性

- 继承性
- 层叠性
- 优先级

### 三、CSS规范

#### 1、命名规范

- 文件命名

  |   文件名    |   说明   |
  | :---------: | :------: |
  |  reset.css  | 重置样式 |
  | global.css  | 全局样式 |
  | themes.css  | 主题样式 |
  | module.css  | 模块样式 |
  | master.csss | 母版样式 |
  | columns.css | 专栏样式 |
  |  forms.css  | 表单样式 |
  |  mend.css   | 补丁样式 |
  |  print.css  | 打印样式 |

  

- id命名和class命名

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
      |   主题   |   main    |
      |   左侧   | main-left |

    - 网页细节部分

      | 网页部分 | 命名          |
      | -------- | ------------- |
      | 主导航   | main-nav      |
      | 子导航   | sub-nav       |
      | 边导航   | side-nav      |
      | 左导航   | leftside-nav  |
      | 右导航   | rightside-nav |
      |          |               |
      |          |               |
      |          |               |
      |          |               |

      - 菜单
      - 其它

#### 2、书写规范

书写顺序

- 布局属性 display position float clear
- 盒模型 margin、padding
- 文本性属性 text font
- 装饰性属性 color backgroud-colr opacity cursor
- 其它属性 content list-style quotes

#### 3、注释规范

- 顶部注释

- 模块注释

- 简单注释

- 发布保留注释

  ```
  /*! 保留注释内容 */
  ```

  

#### 4、CSS reset

​	重置样式，去除浏览器默认样式

### 四、盒子模型

#### 1、CSS盒子模型

