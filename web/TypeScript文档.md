# 变量声明

- var声明
- let 声明
- const声明
- 解构赋值
  - 解构数组
  - 对象解构

一、var声明



二、let声明



三、const声明



四、解构赋值

- 解构数组



- 解构对象

  - 普通解构

    ```typescript
    let o = {
        a: "foo",
        b: 12,
        c: "bar"
    };
    // 普通解构
    // let { a, b } = o;
    // 使用未声明变量解构，注意需要加括号将它括起来
    ({a, b} = o);
    // 使用...语法创建剩余变量
    let {a, ...manyParams} = o;
    console.log(a);
    console.log(b);
    ```

    

  - 属性重命名

    ```typescript
    let o = {
        a: "foo",
        b: 12,
        c: "bar"
    };
    let { a: name1, b: name2 } = o;
    //({a: newName1, b: newName2} = o);
    ```

    

  - 默认值

    

  - 函数声明





# 基础类型



# 接口



# 类