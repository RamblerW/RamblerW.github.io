- 初始化表格的当前页为第1页

```javascript
//初始化后台数据为第1页
$('#dgOrderDetails').datagrid('options').pageNumber = 1;
//初始化前台显示为第1页
var p = $('#dgOrderDetails').datagrid('getPager');
p.pagination("refresh",{pageNumber:1});
```