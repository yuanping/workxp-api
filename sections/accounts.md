# Accounts
用户注册WorkXP后，会给用户分配一个帐户，用户可以可以邀请更多的同事来一起使用这个帐户。用户也可以注册多个帐户（公司）。

## Get Account
通过此接口可以得到帐户的过期时间，可用的存储空间，付费计划等。
### Request
`GET : /accounts/3.json`  

### Response

```json
	{
		"id": 3, 
		"name": "容平志远（北京）科技有限公司", 
		"domain": "rongping",
		"plan": "免费版",
		"expired_at": "YYYY-MM-DDTHH:MM:SSZ",
		"free_storage": 2000
	}
```
### Description
`plan` 免费版、个人版、基础版、加强版、高级版、终极版、其它
`free_storage` 剩余空间数量，单位字节。(1024 = 1K)
`expired_at` 到期时间

## Get Accounts
登录成功后可以通过此接口得到用户所有的帐户信息。其中域名`domain`作为URL的二级域名请求得到此帐户的数据。
### Request
`GET : /accounts.json`  

### Response

```json
	[
		{
			"id": 3, 
			"name": "容平志远（北京）科技有限公司", 
			"domain": "rongping",
			"plan": "免费版",
			"expired_at": "YYYY-MM-DDTHH:MM:SSZ",
			"free_storage": 2000
		}
	]
```

