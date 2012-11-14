# Categories
任务或机会的分类。

## Get categories
`GET : /categories.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`begin`参数取这个时间之后更新的记录。

### Response

```json
	[
		{"id":5, "name":"email",  "color":"#46647C", "type":"TaskCategory"},
		{"id":6, "name":"Call",  "color":"#4664CC", "type":"ChanceCategory"}
	]
```

### Description
`type`区分是任务分类还是机会分类 `TaskCategory/ChanceCategory`