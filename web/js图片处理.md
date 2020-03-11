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

