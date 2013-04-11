# Tasks

## Get tasks

`GET /tasks.json` 得到所有访问权限能看见的任务（公开的或分配给我和我分配给别人的）.  
一页50条记录，如果要取更多记录，需要加参数`&page=2`，`&page=3`以此类推。如果没有新的数据，返回`[]`。

### Params
`collection`：如果为`incoming`表示待办任务，`completed`表示已完成的任务，`assigned`表示我分配给别人的。
### Response

```json
	[
		{
			"id":22,
			"content":"task content",
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
			"due_at":"YYYY-MM-DDTHH:MM:SSZ",
			"contact":{"id":66, "name":"汪练"},
			"deal":{"id":66, "name":"购买WorkXP基本版"},
			"case":{"id":66, "name":"销售案例"},
			"note":{"id":33, "content":"事件"},
			"category": {"id": 2, "name": "约见", "color": "#46647C"},
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"assigned_to":{
				"id": 21,
				"name": "汪练",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"completed_user":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"privacy":"public/private",
			"state":"pending/done"
		}
	]
```
### Description
一个任务可以关联多个对象（联系人，机会，项目，事件），也可以不关联任务对象。如果在一个联系人的事件上关联一个任务，则`contact`和`note`都有对应的值。

## Get task
`GET /tasks/22.json` 返回指定的任务

###Response
```json
	{
		"id":22,
		"content":"task content",
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"due_at":"YYYY-MM-DDTHH:MM:SSZ",
		"contact":{"id":66, "name":"汪练"},
		"deal":{"id":66, "name":"购买WorkXP基本版"},
		"case":{"id":66, "name":"销售案例"},
		"note":{"id":33, "content":"事件"},
		"category": {"id": 2, "name": "约见", "color": "#46647C"},
		"author":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"assigned_to":{
			"id": 21,
			"name": "汪练",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"completed_user":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"privacy":"public/private",
		"state":"pending/done"
	}
```

## Post task

`POST /tasks.json` `content`不能为空。

### Params

```json
	{
		"content":"task content",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"note_id":33,
		"due_at":"YYYY-MM-DDTHH:MM:SSZ",
		"category_id":2,
		"assigned_to_id":36,
		"privacy":"public/private",
		"state":"pending/done"
	}
```

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  

```json
	{"id": 83}
```

# Modify task

`PUT /tasks/37.json` 完成一个任务也用此接口，设置`state`为`done`。

### Params

```json
	{
		"content":"task content",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"note_id":33,
		"due_at":"YYYY-MM-DDTHH:MM:SSZ",
		"category_id":2,
		"assigned_to_id":36,
		"privacy":"public/private",
		"state":"pending/done"
	}
```

### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`

## Delete task
`DELETE /tasks/37.json`

### Response
删除成功返回`204 No Content`，如果用户没有权限修改返回`403 Forbidden`。
