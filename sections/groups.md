# Groups
用户（同事）组。一个用户可以在多个组中。

## Get groups
`GET : /groups.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`begin`参数取这个时间之后更新的记录。

### Response

```json
	[
		{
			"id":5, 
			"name":"销售部",
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ"
		},
		{
			"id":6, 
			"name":"市场部",  
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ"
		}
	]
```
