# Deletions
服务器端删除的数据，包括事件、评论，用户，分类，联系等。

## Get deletions
`GET /deletions.json` 得到服务器端删除的所有数据。一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`begin`参数取这个时间之后删除的记录。

### Response

```json
	[
		{
		"id":"34,35,36",  
		"type":"Note/User/Catetory/Contact/Schedule",
		"created_at":"YYYY-MM-DDTHH:MM:SSZ"
		}
	]
```