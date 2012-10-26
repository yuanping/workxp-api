# Account data
`GET : /account.json` 账户信息和用户、分类数据。传`begin`参数，返回users/categories这个时间之后更新的数据。

```json
	[
		"plan":"免费版",
		"expired":true,
		"free_storage":2000,
		"users":[
							{"id":user_id, "name":"user1", "avatar_url": "http://workxp.info/avatar.png"},
							{"id":user_id, "name":"user2", "avatar_url": "http://workxp.info/avatar.png"}
	   				],
		"categories":[
									{"id":category_id, "name":"email",  "color":"#46647C", "type":"TaskCategory/ChanceCategory"}
								 ]
	]
```

### 数据说明
`plan` 免费版、个人版、基础版、加强版、高级版、终极版、其它
`free_storage` 剩余空间数量，单位字节。(1024 = 1K)
`expired` 是否已过期
