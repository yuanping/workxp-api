# WorkXP移动终端接口文档

# 通用参数说明
所有请求协议都使用http，除sign\_in以外每个请求都要有二级域名和 auth\_token参数。
接口URL:http://<:domain>.api3.workxp.info  
所有时间格式都为`yyyy-MM-dd HH:mm:ss +0800`  
`begin` 取这个时间之后的记录，`end` 取这个时间之前的记录，同时传两个参数取之间的记录。  
所有的`POST`请求，`JSON`数据放到`data`参数里

## Request
* `auth_token` 在认证成功后返回，客户端应保存此token，作为每次请求的参数
* `domain` 二级域名
* `page` 取更多数据，比如一页为50条记录，则`&page=2`取51-100条记录

## Response
* `200` OK 修改成功
* `201` Created 保存成功
* `203` Non-Authoritative Information 认证失败
* `401` 请求处理失败
* `403` Forbidden 没有权限

If WorkXP is having trouble, you might see a 5xx error. 500 means that the app is entirely down, but you might also see 502 Bad Gateway, 503 Service Unavailable, or 504 Gateway Timeout. It's your responsibility in all of these cases to retry your request later. 

## No XML, just JSON
We only support JSON for serialization of data. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Basecamp. **All API URLs end in .json to indicate that they accept and return JSON.**

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the `Content-Type` header.

## 数据接口

* [Contacts](https://github.com/yuanping/workxp-api/blob/master/sections/contacts.md)
* [Activities](https://github.com/yuanping/workxp-api/blob/master/sections/notes.md)

# Sign in
`POST /users/sign_in`
###Params
* `user[email]` 用户名
* `user[password]` 密码
* `from` mobile

###Response

	{
		"auth_token":"value",
		"user_id":"current_user_id",
		"products":[{"company":"Rongping","domain":"rongping"}]
	}

# Account data
`GET : /account.json` 账户信息和用户、分类数据。传`begin`参数，返回users/categories这个时间之后更新的数据。

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

### 数据说明
`plan` 免费版、个人版、基础版、加强版、高级版、终极版、其它
`free_storage` 剩余空间数量，单位字节。(1024 = 1K)
`expired` 是否已过期

