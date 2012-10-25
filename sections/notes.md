# Notes
增加、修改事件

## Post note
`POST /notes.json`

```json
	{    
		"cid":"client id",
		"subject":"subject",
		"author_id": 37,
		"content":"Note content",
		"type":"Note/Comment",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"parent_id":"note_parent_id",
		"external":false
	}	
```

###Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。

```json
	{"cid": "client id", "id": 83}
```

## Modify note
`PUT /notes/37.json`

###Params
`data`:

```json
	{
		"content":"Note content"
	}
```


###Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`



