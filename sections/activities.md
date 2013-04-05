# Activities
动态可以显示一个公司内所有员工的工作情况，包括事件、评论、任务的完成，机会状态变化等。

## Get global activities
`GET /activities.json` 一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`end`参数，取这个时间之前的历史记录，`begin`取这个时间之后的记录。
传`contact_id`参数，取与这个联系人相关的动态;`case_id`，取与这个项目相关的动态，`deal_id`，取与这个机会相关的动态。
一条动态可以同时关联到一个联系人和机会，即`contact`与`deal`都有值，也可以不关联到任何对象（联系人、机会、项目），即`contact`,`deal`,`case`都为`{}`。  
如果`author`的`type`值为`User`时，说明这条动态是由WorkXP的用户产生的，否则是外部的一个联系人添加的。

###Response

```json
	[
		{    
			"id":21,
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
			"occurred_at":"YYYY-MM-DDTHH:MM:SSZ",
			"author":{
				"id": 37,
				"type": "User/Person",
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"content":"Note content",
			"type":"Note/Comment/Schedule/Email/ChanceNote/KaseNote",
			"contact":{"id":66, "name":"汪练"},
			"deal":{"id":66, "name":"购买WorkXP基本版"},
			"case":{"id":66, "name":"销售案例"},
			"subject":"邮件主题",
			"email_from":{
				"id": 37,
				"type": "User/Person",
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"email_to":{
				"id": 37,
				"type": "User/Person",
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"category": {"id": 2, "name": "约见", "color": "#46647C"},
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
如果`type`为`ChanceNote`，表示这是机会状态改变的动态，`pending`,`won`,`lost`对应着机会状态变为跟踪、成功，失败, `''`表示新创建的机会。  
如果`type`为`KaseNote`，目前只有一种情况，表示新创建了项目。
`access_policy`：哪些人可以看见这条记录，`Everyone`所有人可见，`23,34,12`表示ID为23,34,12的用户可以看见。
`subject`,`email_to`和`email_from`只有在`type`为`Email`时有值，表示邮件的发件人与收件人。
`category`只有在`type`为`Schedule`时有值，表示任务的分类。

## Get activity
`GET /activities/3.json` 返回指定的动态

###Response

```json
	{    
		"id":3,
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"occurred_at":"YYYY-MM-DDTHH:MM:SSZ",
		"author":{
			"id": 37,
			"type": "User/Person",
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"content":"Note content",
		"type":"Note/Comment/Schedule/Email/ChanceNote/KaseNote",
		"contact":{"id":66, "name":"汪练"},
		"deal":{"id":66, "name":"购买WorkXP基本版"},
		"case":{"id":66, "name":"销售案例"},
		"subject":"邮件主题",
		"email_from":{
			"id": 37,
			"type": "User/Person",
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"email_to":{
			"id": 37,
			"type": "User/Person",
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"category": {"id": 2, "name": "约见", "color": "#46647C"},
		"parent_id":45,
		"external":false,
		"state":"done/pending/won/lost",
		"attachments":[
			{"name":"avatar.png", "url":"http://workxp.info/avatar.png"}
		],
		"access_policy": "Everyone/user_ids"
	}
```