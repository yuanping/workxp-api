# Activities
动态可以理解为用户在WorkXP工作的日志，包括事件、评论、任务的完成，机会状态变化等。

## Get global activities
`GET /activities.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`end`参数，取这个时间之前的历史记录，`begin`取这个时间之后的记录。同时传两个参数，取这两个时间之间的记录。
一条动态可以同时关联到某个联系人和机会，即`contact`与`deal`都有值，也可以不关联到任何对象（联系人、机会、项目），即`contact`,`deal`,`case`都为`{}`。  
如果`author`的`id`为`0`，说明这条动态不是由WorkXP的用户产生的，是外部的一个联系人添加的，这时`author`的`name`为联系人姓名，`avatar_url`为联系人的头像。

###Response

```json
	[
		{    
			"id":21,
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
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
			"occurred_at":"YYYY-MM-DDTHH:MM:SSZ",
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

### Description
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
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
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
			"occurred_at":"YYYY-MM-DDTHH:MM:SSZ",
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