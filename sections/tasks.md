# Tasks

## Get tasks

`GET /tasks.json` 得到所有自己的待办任务.一页100条记录，如果要取更多记录，需要加参数`&page=2`，`&page=3`以此类推。如果没有新的数据，返回`[]`。

### Response

```json
	[
		{
			"id":22,
			"content":"task content",
			"target_id": 26,
			"target_type": "Contact/Deal/Case/Note",
			"target_name": "袁平",
			"due_at":"YYYY-MM-DDTHH:MM:SSZ",
			"category": {"id": 2, "name": "约见"},
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
			"privacy":"public/private",
			"state":"pending/done"
		}
	]
```


## Post task

`POST /tasks.json`

### Params

```json
	{
		"content":"task content",
		"target_id": 26,
		"target_type": "Contact/Deal/Case/Note",
		"due_at":"YYYY-MM-DDTHH:MM:SSZ",
		"category_id":2,
		"owner_id":37,
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
		"due_at":"YYYY-MM-DDTHH:MM:SSZ",
		"category_id":2,
		"assigned_to_id":36,
		"privacy":"public/private",
		"state":"pending/done"
	}
```

### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`


