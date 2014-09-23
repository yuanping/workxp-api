# Users
用户是指使用WorkXP的人，一个公司帐号可能会有多个用户。

## Get user
`GET : /users/3.json`  返回指定的用户  
`GET : /users/me.json`  返回当前的用户

### Params
`group_id` 返回某个组的用户

### Response

```json
	{
		"id": 3, 
		"name": "YuanPing", 
		"email": "yuanping@workxp.info",
		"admin": true,
		"groups": [1, 3],
		"created_at": "YYYY-MM-DDTHH:MM:SSZ",
		"last_sign_in_at": "YYYY-MM-DDTHH:MM:SSZ",
		"avatar_url": "http://workxp.info/avatar.png"
	}
```

## Get users
`GET : /users.json`  一次取最多50条记录。如果取回来数据刚好是50条，客户端有责任检查是否有更多记录，`&page=2`取51-100条记录，`&page=3`以此类推。  
传`begin`参数取这个时间之后更新的记录。

### Response

```json
	[
		{
			"id": 3, 
			"name": "YuanPing", 
			"email": "yuanping@workxp.info",
			"admin": true,
      "groups": [1, 3],
			"created_at": "YYYY-MM-DDTHH:MM:SSZ",
			"last_sign_in_at": "YYYY-MM-DDTHH:MM:SSZ",
			"avatar_url": "http://workxp.info/avatar.png"
		}
	]
```
