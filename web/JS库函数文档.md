# Axios

一、基础了解

- 名称解释

  - 拦截器 interceptors
  - 数据转换器
  - http请求适配器
  - config配置项

- 工具方法

  - bind
  - forEach
  - merge
  - extend

- axios使用方式

  - `axios(option)`

    ```javascript
    axios({url, method, headers})
    ```

  - `axios(url[,options])`

    ```javascript
    axios(url, {method, headers,})
    ```

  - `axios[method](url[,option])`

  - `axios[method](url[,data[,option]])`

  - `axios.request(option)`

    ```javascript
    axios.request({
    	url,
    	method,
    	headers,
    })
    ```



使用axios中post方法传值接收为空

解决办法：

- 设置config中`'Content-Type': 'application/x-www-form-urlencoded'`
- 引用qs模块，系列化表单

demo:

```
axios.post(url, qs.stringify(form), { 'Content-Type': 'application/x-www-form-urlencoded' })
```

二、工具方法

- 

1、FormData





2、XMLHttpRequest



3、ajax



4、axios



# 图片处理

1、将base64通过blob转为file

```javascript
// 将base64转换为blob 
    dataURLtoBlob: function(dataurl) {
      let arr = dataurl.split(','),
        mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]),
        n = bstr.length,
        u8arr = new Uint8Array(n);
      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }
      return new Blob([u8arr], { type: mime });
    }
// 将blob转换为file文件
    blobToFile: function(theBlob, fileName){
      return new File([theBlob], fileName);
    }
```

2、将base64直接转为file

```javascript
// 将base64直接转为file    
    dataURLtoFile: function(dataurl, filename) { 
	    var arr = dataurl.split(','),
	        mime = arr[0].match(/:(.*?);/)[1],
	        bstr = atob(arr[1]),
	        n = bstr.length,
	        u8arr = new Uint8Array(n);
	    while (n--) {
	        u8arr[n] = bstr.charCodeAt(n);
	    }
	    return new File([u8arr], filename, { type: mime });
	}
```

