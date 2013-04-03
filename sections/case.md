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
			"name":"暨南大学教育管理项目",  
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
		"name":"暨南大学教育管理项目",  
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