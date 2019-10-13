- json数组追加对象：`a.objectName = objectVal;`

- Uint8Array转字符串
```javascript
for (var i = 0; i < array.length; i++) {
    resultStr += String.fromCharCode(array[i]);
}
```
- 批量替换
```javascript
//替换str字符串中的所有a，/g是全文匹配标识
var str2 = str.replace(/a/g, str); 
```
- 获取cookie：`document.cookie`

- 获取User-Agent：`navigator.userAgent`

- input 限制只能输入正整数：`<input onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}" onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}">`
- ajax访问跨域请求
```javascript
$.ajax({
    type: "GET",
    async:false,
    url: loginUrl,
    dataType: "jsonp",
    cache: false,
    success : function(data) {
        window.open(biddingUrl);
    },
    error : function(data) {
        window.open(biddingUrl);
    }
});
```

- js包转ts：`npm install --save @types/xxxxx`，`xxxxx`为js包的名称