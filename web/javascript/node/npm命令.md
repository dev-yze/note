1、添加ES6支持

```javascript
// 1、初始化npm工作目录，生成package.json文件
npm init -y
// 2、安装babel-cli
npm install babel-cli --save 或 npm install babel-cli --g
// 3、安装babel-preset-es2015支持ES6的语法
npm install babel-preset-es2015 --save
// 添加名为.babelrc的配置文件
{
    "presets": [
        "es2015"
    ],
    "plugins": []
}
```

2、