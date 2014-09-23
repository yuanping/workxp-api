# Case
项目

## Get Cases
如果使用此接口取项目，请确保通过`begin`参数来限制返回结果的数量，以项目的`updated_at`时间,获取更新、或新增的项目。如果没有新的数据，返回`[]`。  
`GET /cases.json`  一页200条记录，如果要取更多记录，需要加`&page=2`参数，`&page=3`以此类推。

### Response

```json
	[
		{
			"id":56,
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
			"closed_at":"YYYY-MM-DDTHH:MM:SSZ",
			"name":"WorkXP iOS开发",  
			"description":"description",
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
			"access_policy": "Everyone/user_ids"
		}
	]
```

### Description
`closed_at` 关闭时间

## Get Cases count
`/cases/count.json` 参数与取项目相同，可以得到项目的总数。

```json
	{"num": 1024}
```

## Get Case
`GET /cases/3.json` 返回指定的项目

###Response

```json
	{
		"id":56,
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"closed_at":"YYYY-MM-DDTHH:MM:SSZ",
		"name":"WorkXP iOS开发",  
		"description":"description",
		"author":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
		"access_policy": "Everyone/user_ids"
	}
	
```

## Post case
`POST /cases.json` 上传或修改项目图标需要文件的验证码(token)和文件名。验证码如何得到可以参考[Create attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)，
也就是说你要先上传图片，再把它关联到项目。不设置图标，`avatar_token`设置为`{}`。

### Params

```json
	{
		"name":"WorkXP基础版",  
		"description":"description",
		"closed_at":"YYYY-MM-DDTHH:MM:SSZ",
		"avatar_token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c"
	}
```

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  
返回结果与Get case一致。

## Modify case
`PUT /cases/37.json`

### Params

与Post case参数一致。

### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`

## Delete case
`DELETE /cases/37.json`

### Response
删除成功返回`204 No Content`，如果用户没有权限修改返回`403 Forbidden`。