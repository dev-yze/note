canvas与svg区别

- 位图和矢量图
- 创建方式

```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="100%" height="100%" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>
</svg>
```

引入svg方法

- 使用`<embed>`标签
- 使用`<object>`标签
- 使用`<iframe>`标签
- `<img>`
- 使用css中`background: url(filename)`属性
- html中使用

基本图形

- `<cicle>`标签
  - cx、cy、r
  - fill、stroke、stroke-width
  - style
- `<react>`标签
  - x、y
  - width、height
  - rx、ry 
- `<line>`标签
  - x1、y1
  - x2、y2
  - stroke、stroke-width、stroke-opacity
- `<ellipse>`
- `<polyine>`
- `<ploygon>`
- `<path>`