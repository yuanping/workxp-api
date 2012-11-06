# Account data
`GET : /account.json` 账户信息和用户。

### Response
```json
	{
		"plan": "免费版",
		"expired_at": "yyyy-MM-dd HH:mm:ss +0800",
		"free_storage": 2000
	}
```

### 数据说明
`plan` 免费版、个人版、基础版、加强版、高级版、终极版、其它
`free_storage` 剩余空间数量，单位字节。(1024 = 1K)
`expired_at` 到期时间
