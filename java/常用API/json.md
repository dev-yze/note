一、JSON语法

http://kimmking.github.io/2017/06/06/json-best-practice/

1、概念

​		Json是一种轻量级的数据交换格式，采用一种“键：值”对的文本格式来存储和表示数据，在系统交换数据过程中常常被使用，是一种理想的数据交换语言

2、语法

- JSON对象

```json
{
	"id": 101,
	"name": "张三",
	"age": 24
}
```

​	json对象特征:

		1.  数据在花括号中
  		2.  数据以键值对形式出现
  		3.  每个键值对以逗号分隔，最后一个键省略

- JSON数组

```
[
	{"ID": 1001, "name": "张三", "age": 24},
	{"ID": 1002, "name": "李四", "age": 25},
	{"ID": 1003, "name": "王五", "age": 22}
]
```

​	json对象数组特征:

	1. 数组在方括号内
 	2. 方括号中每个数据以json对象形式出现
 	3. 每两个数据以逗号分隔（最后一个无需逗号）

- JSON字符串

  json字符串特征:

  1、它必须是一个字符串，由" "或者' '包裹数据，支持字符串的各种操作

  2、里面的数据格式应该要满足其中一个格式，可以是json对象，也可以是json对象数组或者是两种基本形式的组合变形。

- 组合

  ​        json可以简单的分为基本形式：json对象，json对象数组。两种基本格式组合变形出其他的形式，但本质还是json对象或者json对象数组中的一种。json对象或对象数组可以转化为json字符串，使用于不同的场合

二、`FastJson`

1、概述

​	     `fastjson`是阿里巴巴的开源`JSON`解析库，它可以解析`JSON`格式的字符串，支持将Java Bean序列化为`JSON`字符串，也可以从`JSON`字符串反序列化到`JavaBean`。

2、常用Class介绍和使用

- `JSON`
  - `toJSONString`
  - `toJSON`
  - `toJavaObject`
  - `parse`
  - `parseObject`
- `JSONObject`
- `JSONArray`

```
public static void test01() {
        List<Student> list = new ArrayList<Student>();
        Student stu1 = new Student("张一", 23, 3, 1);
        Student stu2 = new Student("张二", 22, 3, 3);
        list.add(stu1);
        list.add(stu2);
        System.out.println("************javaBean to JsonString******");
        String stu1String = JSON.toJSONString(stu1);
        String stu2String = JSON.toJSONString(stu2);
        System.out.println(stu1String);
        System.out.println(stu2String);
        System.out.println("************JsonString to javaBean******");
        Student parseStu1 = JSON.parseObject(stu1String, Student.class);
        Student parseStu2 = JSON.parseObject(stu2String, Student.class);
        System.out.println(parseStu1);
        System.out.println(parseStu2);
        System.out.println("************javaBean to JSONObject******");
        JSONObject jsonObject = (JSONObject) JSON.toJSON(stu1);
        System.out.println(jsonObject);
        System.out.println(jsonObject.get("name"));
        System.out.println(jsonObject.getInteger("age"));
        System.out.println("************JSONObject to javaBean******");
        Student studentBean = JSON.toJavaObject(jsonObject, Student.class);
        System.out.println(studentBean);
        System.out.println("************JSONString to JSONObject******");
        JSONObject jsonObject1 = (JSONObject) JSON.parse(stu1String);
        System.out.println(jsonObject1);
        System.out.println("************JSONObject to JSONString******");
        String s = JSON.toJSONString(jsonObject1);
        System.out.println(s);

        System.out.println("************javaBean to JSONArray******");
        List<Student> studentList = new ArrayList<Student>();
        for (int i = 0; i < 5; i++) {
            studentList.add(new Student("李", Integer.parseInt("2" + i), i, i));
        }
        JSONArray jsonArray = (JSONArray) JSON.toJSON(studentList);
        for (int i = 0; i < jsonArray.size(); i++) {
            System.out.println(jsonArray.get(i));
            System.out.println(jsonArray.getJSONObject(i));
        }
        System.out.println("************JSONArray to javaBean******");
        List<Student> studentList1 = new ArrayList<Student>();
        for (int i = 0; i < jsonArray.size(); i++) {
            studentList1.add(JSON.toJavaObject(jsonArray.getJSONObject(i), Student.class));
        }
        studentList1.stream().forEach(System.out::println);

    }
```

三、GJSON





四、比较