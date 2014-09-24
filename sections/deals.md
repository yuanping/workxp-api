# Deal
商业机会

## Get deals
如果使用此接口取机会，请确保通过`begin`参数来限制返回结果的数量，以机会的`updated_at`时间,获取更新、或新增的机会。如果没有新的数据，返回`[]`。  
`GET /deals.json`  一页200条记录，如果要取更多记录，需要加`&page=2`参数，`&page=3`以此类推。

### Response

```json
	[
		{
			"id":56,
			"created_at":"YYYY-MM-DDTHH:MM:SSZ",
			"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
			"name":"WorkXP基础版",  
			"state":"pending/won/lost",
			"expected_contact_amount":300,
			"price":30,
			"price_type": "fixed/hour/month/year",
			"duration": 5,
			"contact":{"id":66, "name":"汪练"},
			"description":"description",
			"author":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"assigned_user":{
				"id": 37,
				"name": "袁平",
				"avatar_url":"http://workxp.info/avatar.png"
			},
			"category": {"id": 2, "name": "外包", "color": "#46647C"},
			"access_policy": "Everyone/user_ids"
		}
	]
```

### Description
`access_policy` 返回Everyone或以逗号分隔的用户ID字符串 `Everyone`是所有人可见，`1,3,5`表示ID为1，3和5的用户可以看见  
`price_type` 计费的类型：固定价/每小时/每月/每年   
`duration` 如果`price_type`为每月时，表示收费几个月  
`price` 每月多少钱  
`expected_contact_amount` 为总金额  

## Get contacts count
`/deals/count.json` 参数与取机会相同，可以得到机会的总数。

```json
	{"num": 1024}
```

## Get deal
`GET /deals/3.json` 返回指定的机会

###Response

```json
	{
		"id":56,
		"created_at":"YYYY-MM-DDTHH:MM:SSZ",
		"updated_at":"YYYY-MM-DDTHH:MM:SSZ",
		"name":"WorkXP基础版",  
		"state":"pending/won/lost",
		"expected_contact_amount":300,
		"price":30,
		"price_type": "fixed/hour/month/year",
		"duration": 5,
		"contact":{"id":66, "name":"汪练"},
		"description":"description",
		"author":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"assigned_user":{
			"id": 37,
			"name": "袁平",
			"avatar_url":"http://workxp.info/avatar.png"
		},
		"category": {"id": 2, "name": "外包", "color": "#46647C"},
		"access_policy": "Everyone/user_ids"
	}
```

## Post deal
`POST /deals.json` 上传或修改机会图标需要文件的验证码(token)和文件名。验证码如何得到可以参考[Create attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)，
也就是说你要先上传图片，再把它关联到机会。不设置图标，`avatar_token`设置为`{}`。

### Params

```json
	{
		"name":"WorkXP基础版",  
		"state":"pending/won/lost",
		"expected_contact_amount":300,
		"price":30,
		"price_type": "fixed/hour/month/year",
		"duration": 5,
		"contact_id": 66,
		"description":"description",
		"avatar_token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c",
		"assigned_user_id":36,
    "category_id":2
	}
```

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。  
返回的数据结构与`Get deal`接口返回的内容一致。

## Modify deal
`PUT /deals/37.json`

### Params

与Post deal参数一致。

### Response
如果更新成功返回`200 OK`，如果用户没有权限修改返回`403 Forbidden`

## Delete deal
`DELETE /deals/37.json`

### Response
删除成功返回`204 No Content`，如果用户没有权限修改返回`403 Forbidden`。