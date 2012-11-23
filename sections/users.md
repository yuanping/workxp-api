# Users
用户是指使用WorkXP的人，一个公司帐号可能会有多个用户。

## Get user
`GET : /users/3.json`  返回指定的用户  
`GET : /users/me.json`  返回当前的用户

### Response

```json
	{
		"id": 3, 
		"name": "YuanPing", 
		"email": "yuanping@workxp.info",
		"admin": true,
		"created_at": "YYYY-MM-DDTHH:MM:SSZ",
		"last_sign_in_at": "YYYY-MM-DDTHH:MM:SSZ",
		"avatar_url": "http://workxp.info/avatar.png"
	}
```

## Get users
`GET : /users.json`  

### Response

```json
	[
		{
			"id": 3, 
			"name": "YuanPing", 
			"email": "yuanping@workxp.info",
			"admin": true,
			"created_at": "YYYY-MM-DDTHH:MM:SSZ",
			"last_sign_in_at": "YYYY-MM-DDTHH:MM:SSZ",
			"avatar_url": "http://workxp.info/avatar.png"
		}
	]
```
