# Contacts

## Get contacts

如果使用此接口取联系人，请确保传`begin`参数来限制返回结果的数量，以联系人的`updated_at`时间,获取更新、或新增的联系人。如果没有新的数据，返回`[]`。  
`GET /contacts.json`  一页500条记录，如果要取更多记录，需要加`&page=2`参数，`&page=3`以此类推。

### Response

```json
	[
		{
			"id":56,
			"created_at":"yyyy-MM-dd HH:mm:ss +0800",
			"updated_at":"yyyy-MM-dd HH:mm:ss +0800",
			"name":"汪练",  
			"title":"CEO",
			"type":"Company/Person",
			"company":{"id": 34, "name": "WorkXP"},
			"other":"background info",
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
			"access_policy": "Everyone/user_ids"
		}
	]
```

### 数据说明
`contact_methods`的`type`取值：`ContactPhone/ContactEmail/ContactWebsite/ContactIm/ContactAddress`  
`contact_methods`的`key`取值：   
电话：office/公司  work/工作 mobile/手机  fax/传真  home/住宅  other/其它  
邮箱：work/工作  personal/个人  other/其它  
IM: gtalk/GTalk  msn/MSN  qq/QQ  other/其它  
网站: office/公司  personal/个人  other/其它 
地址: office/公司  home/住宅  other/其它  

## Post contact
`POST /contacts.json`

###Params
`avatar`: 头像  
`data`:

```json
	{
		"name":"汪练",  
		"title":"CEO",
		"company":"WorkXP",
		"other":"background info",
		"contact_methods":[
			{
				"id":234,
					"type":"ContactPhone",
					"key":"office", 
					"value":"123123123321" 
				}
			]
	}
```

###Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  

```json
	{"cid": "client id", "id": 83}
```
## Modify contact
`PUT /contacts/37.json`

###Params
`avatar`: 头像  
`data`:

```json
	{
		"name":"汪练",  
		"title":"CEO",
		"company":"WorkXP",
		"other":"background info",
		"contact_methods":[ 
			 {
		 		"id":234,
		 		"type":"ContactPhone",
		 		"key":"office", 
		 		"value":"123123123321" 
		 	}
		 ]
	}
```

###Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`