# Notes
增加、修改事件(Note)或评论(Comment)，一次只能增加一个事件。

## Post note
`POST /notes.json` 添加一个事件或评论.  
把文件关联到事件或评论上需要验证码(token)和文件名。验证码如何得到可以参考[Create attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)，
也就是说你要先上传文件，再把它关联到事件或评论上。

### Params

```json
	{    
		"author_id": 37,
		"content":"Note content",
		"type":"Note/Comment",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"parent_id":9,
		"external":false,
		"attachments": [
	    {
	      "token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c",
	      "name": "final_mockup.png"
	    }
	  ]
	}	
```

### 数据说明
`name`参数*必须*是一个有效的文件名并且有后缀名。一次可以关联多个附件。
如果没有附件上传，`attachments`参数设置为`[]`。

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。

```json
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
		"type":"Note/Comment",
		"contact":{"id":66, "name":"汪练"},
		"deal":{"id":66, "name":"购买WorkXP基本版"},
		"case":{"id":66, "name":"销售案例"},
		"occurred_at":"yyyy-MM-dd HH:mm:ss +0800",
		"parent_id":45,
		"external":false,
		"state":"done",
		"attachments":[
			{"name":"final_mockup.png", "url":"http://workxp.info/avatar.png"}
		],
		"access_policy": "Everyone/user_ids"
	}
```

## Modify note
`PUT /notes/37.json`

### Params

```json
	{
		"content":"Note content"
	}
```


### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`。



