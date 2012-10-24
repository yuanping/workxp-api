# Feeds
`GET /activities.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录。
传`end`参数，取这个时间之前的历史记录，`begin`取这个时间之后的记录。同时传两个参数，取这两个时间之间的记录。

###Response

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
			"type":"Note/Task/Email/ChanceNote",
			"contact":{"id":66, "name":"汪练"},
			"deal":{"id":66, "name":"购买WorkXP基本版"},
			"case":{"id":66, "name":"销售案例"},
			"occurred_at":"yyyy-MM-dd HH:mm:ss +0800",
			"parent_id":"note_parent_id",
			"external":false,
			"completed_user_id":0,
			"state":"done/pending",
			"attachments":[
				{"name":"avatar.png", "url":"http://workxp.info/avatar.png"}
			]
		}
	]

## Get contact feeds
`GET /people/56/activities.json` 一次取最多50条记录。同取Feeds

## Post note
`POST /people.json`

	{    
		"cid":"client id",
		"subject":"subject",
		"author_id": 37,
		"content":"Note content",
		"type":"Note/Task/Email/ChanceNote/Comment",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"parent_id":"note_parent_id",
		"external":false,
		"completed_user_id":0,
		"state":"done/pending"
	}	


###Response
`201 Created` 

## Modify note
`PUT `

	{"cid": "client id", "id": 83}

