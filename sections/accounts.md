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
		"name": "容平志远科技（北京）有限公司", 
		"domain": "rongping",
		"plan": "免费版",
		"expire_on": "YYYY-MM-DD",
		"free_storage": 2000,
		"dropbox_email": "box.workxp@workxp.info"
	}
```
### Description
`plan` 免费版、个人版、基础版、加强版、高级版、终极版、其它  
`free_storage` 剩余空间数量，单位字节。(1024 = 1K)  
`expire_on` 到期时间  

## Get Accounts
登录成功后可以通过此接口得到用户所有的帐户信息。其中域名`domain`会以Request的HEAD请求得到此帐户的数据。
### Request
`GET : /accounts.json`  

### Response

```json
	[
		{
			"id": 3, 
			"name": "容平志远科技（北京）有限公司", 
			"domain": "rongping",
			"plan": "免费版",
			"expire_on": "YYYY-MM-DD",
			"free_storage": 2000
		}
	]
```

## Register
注册WorkXP账号

### Request
'POST : /accounts.json'

### Params
```json
	{
		"email": "yuanping@workxp.info",  
		"password": "Password",
		"name": "user's name",
		"company":"Company or Team Name",
		"plan": "free/solo/basic/plus/advance/max"
	}
```

### Response
创建成功返回`201 Created`，如果用户已注册返回`409 Conflict`，用户注册但没激活返回`403 Forbidden`。 

## Update Company name
修改当前账号信息，公司名称和自己的姓名，只用传需要修改的参数，此接口在请求的Head里要有二级域名。
### Request
`PUT : /accounts/3.json`  

### Params
```json
	{
		"company_name": "团队名称",
		"user_name": "用户的姓名"
	}
```

### Response
创建成功返回`200 OK`

## Reset Password
通过Email重置密码

### Request
'POST : /accounts/password.json'

### Params
```json
	{
		"email": "yuanping@workxp.info"
	}
```

### Response
创建成功返回`200 OK`，如果这个Email没有注册返回`403 Forbidden`。 
