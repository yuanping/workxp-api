# Activities

动态可以理解为用户在WorkXP工作的日志，包括事件、评论、任务的完成，机会状态变化等。

## Get global activities
`GET /activities.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`end`参数，取这个时间之前的历史记录，`begin`取这个时间之后的记录。同时传两个参数，取这两个时间之间的记录。

###Response

```json
	[
		{    
			"id":21,
			"created_at":"yyyy-MM-dd HH:mm:ss +0800",
			"updated_at":"yyyy-MM-dd HH:mm:ss +0800",
			"subject":"Contact name or Chance name or Task...",
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"content":"Note content",
			"type":"Note/Comment/DoneTask/Email/ChanceNote",
			"contact":{"id":66, "name":"汪练"},
			"deal":{"id":66, "name":"购买WorkXP基本版"},
			"case":{"id":66, "name":"销售案例"},
			"occurred_at":"yyyy-MM-dd HH:mm:ss +0800",
			"parent_id":45,
			"external":false,
			"state":"done/pending/won/lost",
			"attachments":[
				{"name":"avatar.png", "url":"http://workxp.info/avatar.png"}
			],
			"access_policy": "Everyone/user_ids"
		}
	]
```

### 数据说明
如果`type`为`Comment`，表示这条记录是评论，`parent_id`表示这条评论属于哪个事件。
如果`type`为`ChanceNote`，表示这是机会状态改变的动态，`pending`,`won`,`lost`对应着机会状态变为跟踪、成功，失败。
`access_policy`：哪些人可以看见这条记录，`Everyone`所有人可见，`23,34,12`表示ID为23,34,12的用户可以看见。

## Get contact activities
`GET /contacts/56/activities.json` 一次取最多50条记录。同取Feeds  

###Response

```json
	[
		{    
			"id":21,
			"created_at":"yyyy-MM-dd HH:mm:ss +0800",
			"updated_at":"yyyy-MM-dd HH:mm:ss +0800",
			"subject":"Contact name or Chance name or Task...",
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"content":"Note content",
			"type":"Note/Comment/DoneTask/Email/ChanceNote",
			"contact":{"id":66, "name":"汪练"},
			"deal":{"id":66, "name":"购买WorkXP基本版"},
			"case":{"id":66, "name":"销售案例"},
			"occurred_at":"yyyy-MM-dd HH:mm:ss +0800",
			"parent_id":45,
			"external":false,
			"state":"done/pending/won/lost",
			"attachments":[
				{"name":"avatar.png", "url":"http://workxp.info/avatar.png"}
			]	,
			"access_policy": "Everyone/user_ids"
		}
	]
```