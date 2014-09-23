# Contacts
联系人包括公司与个人。一个联系人可以有多个联系方式(`contact_methods`)。

## Get contacts
如果使用此接口取联系人，请确保通过`begin`参数来限制返回结果的数量，以联系人的`updated_at`时间，获取更新、或新增的联系人。如果没有新的数据，返回`[]`。  
`GET /contacts.json`  一页200条记录，如果要取更多记录，需要加`&page=2`参数，`&page=3`以此类推。

### Response

```json
	[
		{
			"id":56,
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
			"name":"汪练",  
			"title":"CEO",
			"type":"Company/Person",
			"company":{"id": 34, "name": "WorkXP"},
			"others":"background info",
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
			"contact_methods":[
				{
					"id":234,
					"type":"ContactPhone",
					"key":"office", 
					"value":"123123123321" 
				}
			],
			"tags":["VIP", "上海"],
			"access_policy": "Everyone/user_ids"
		}
	]
```

### Description
`contact_methods`的`type`取值：`ContactPhone/ContactEmail/ContactWebsite/ContactIm/ContactAddress`  
`contact_methods`的`key`取值：   
电话：office/公司  work/工作 mobile/手机  fax/传真  home/住宅  others/其它  
邮箱：work/工作  personal/个人  others/其它  
IM: gtalk/GTalk  msn/MSN  qq/QQ  others/其它  
网站: office/公司  personal/个人  others/其它 
地址: office/公司  home/住宅  others/其它  

`access_policy` 返回Everyone或以逗号分隔的用户ID字符串 `Everyone`是所有人可见，`1,3,5`表示ID为1，3和5的用户可以看见

## Get contacts count
`/cotnacts/count.json` 参数与取联系人相同，可以得到联系人的总数。

```json
	{"num": 1024}
```

## Get contact
`GET /activities/56.json` 返回指定的联系人

###Response
```json
	{
		"id":56,
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"name":"汪练",  
		"title":"CEO",
		"type":"Company/Person",
		"company":{"id": 34, "name": "WorkXP"},
		"others":"background info",
		"author":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
		"contact_methods":[
			{
				"id":234,
				"type":"ContactPhone",
				"key":"office", 
				"value":"123123123321" 
			}
		],
		"tags":["VIP", "上海"],
		"access_policy": "Everyone/user_ids"
	}
```

## Post contact
`POST /contacts.json` 上传或修改联系人头像需要头像文件的验证码(token)和文件名。验证码如何得到可以参考[Create attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)，
也就是说你要先上传图片，再把它关联到联系人上。没有头像，`avatar`设置为`{}`。

### Params

```json
	{
		"name": "汪练",  
		"title": "CEO",
		"company": "WorkXP",
		"others": "background info",
		"type":"Company/Person",
		"avatar_token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c",
		"tags":["VIP", "上海"],
		"contact_methods":[
			{
				"type":"ContactPhone",
				"key":"office", 
				"value":"123123123321" 
			}
		]
	}
```

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  

```json
	{
		"id":56,
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"name":"汪练",  
		"title":"CEO",
		"type":"Company/Person",
		"company":{"id": 34, "name": "WorkXP"},
		"others":"background info",
		"author":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
		"contact_methods":[
			{
				"id":234,
				"type":"ContactPhone",
				"key":"office", 
				"value":"123123123321" 
			}
		],
		"tags":["VIP", "上海"],
		"access_policy": "Everyone/user_ids"
	}
```

## Modify contact
`PUT /contacts/37.json`

### Params

```json
	{
		"name":"汪练",  
		"title":"CEO",
		"company":"WorkXP",
		"others":"background info",
		"avatar_token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c",
		"tags":["VIP", "上海"],
		"contact_methods":[ 
			 {
		 		"type":"ContactPhone",
		 		"key":"office", 
		 		"value":"123123123321" 
		 	}
		 ]
	}
```

### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`

## Delete contact
`DELETE /contacts/37.json`

### Response
删除成功返回`204 No Content`，如果用户没有权限修改返回`403 Forbidden`。