# Notes
增加、修改事件(Note)或评论(Comment)，一次只能增加一个事件。

## Post note
`POST /notes.json` 添加一个事件,评论或签到.  
把文件关联到事件或评论上需要验证码(token)和文件名。验证码如何得到可以参考[Create attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)，
也就是说你要先上传文件，再把它关联到事件或评论上。  
`type`为`CustomNote`时，Note的content字段在WorkXP上显示时，支持Markdown的语法。即`content`字段可以传入Markdown格式的字符串，
可以实现从WorkXP到其它系统的链接。
### Params

```json
	{    
		"content":"Note content",
		"type":"CustomNote/Note/Comment/CheckIn",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"parent_id":9,
		"longitude": 32.233,
		"latitude": 123.222,
		"external":false,
		"attachments": ["4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c"]
	}	
```

### CustomNote Params

```json
	{    
		"content":"Note content",
		"type":"CustomNote",
		"contact_id":66,
		"deal_id":77,
		"case_id":77,
		"parent_id":9,
		"longitude": 32.233,
		"latitude": 123.222,
		"external":false,
		"attachments": ["4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c"],
		"link_name": "任务关联时显示的名称",
		"link_url": "任务关联时的链接",
		"can_edit": true/false,
		"can_delete": true/false,
		"can_archive": true/false
	}	
```

### Description
当`type`为`CustomNote`时，多了`link_name`, `link_url`, `can_edit`, `can_delete`, `can_archive`五个字段，可以设置CustomNote到外部系统的链接，是否可编辑、删除，归档等。

`attachments`类型是数组，一次可以关联多个附件。
如果没有附件上传，`attachments`参数设置为`[]`。

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  
返回的数据结构与`Get activity`接口返回的内容一致。

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

## Delete note
`DELETE /notes/37.json`

### Response
删除成功返回`204 No Content`，如果用户没有权限修改返回`403 Forbidden`。

