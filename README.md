# WorkXP接口文档
这是一个REST形式的API，使用JSON序列化和OAuth2认证。

## Request

所有的请求都以`https://<:domain>.workxp.info/api/v3/`开始。 **使用SSL**。请求的地址包括二级域名和版本号。

要请求取你帐户上所有的联系人，在上面的地址后面加上联系的Path，比如 https://<:domain>.workxp.info/api/v3/contacts.json. 可以用curl来测试:

```shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' https://demo.workxp.info/api/v3/contacts.json
```

要创建的话也是一样的，只不过请求的head必须加上`Content-Type: application/json`：

```shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ "name": "My new note!" }' \
  https://demo.workxp.info/api/v3/notes.json
```


## 通用参数说明

* 所有时间格式都为`yyyy-MM-dd HH:mm:ss +0800`  
* `begin` 取这个时间之后的记录，`end` 取这个时间之前的记录，同时传两个参数取这两个时间之间的记录。  
* `page` 取更多数据，比如一页为50条记录，则`&page=2`取51-100条记录


## Response

* `200` OK 修改成功
* `201` Created 保存成功
* `203` Non-Authoritative Information 认证失败
* `401` 请求处理失败
* `403` Forbidden 没有权限

If WorkXP is having trouble, you might see a 5xx error. 500 means that the app is entirely down, but you might also see 502 Bad Gateway, 503 Service Unavailable, or 504 Gateway Timeout. It's your responsibility in all of these cases to retry your request later. 

## Identify your app
You must include a `User-Agent` header with the name of your application and a link to it or your email address so we can get in touch in case you're doing something wrong (so we may warn you before you're blacklisted) or something awesome (so we may congratulate you). Here's an example:

    User-Agent: Freshbooks (http://freshbooks.com)

If you don't supply this header, you will get a `400 Bad Request`.

## No XML, just JSON
We only support JSON for serialization of data. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Basecamp. **All API URLs end in .json to indicate that they accept and return JSON.**

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the `Content-Type` header.

# Authentication
`POST /users/sign_in`

### Params

* `user[email]` 用户名
* `user[password]` 密码
* `from` mobile

### Response

```json
	{
		"auth_token":"value",
		"user_id":"current_user_id",
		"products":[{"company":"Rongping","domain":"rongping"}]
	}
```

## 数据接口

* [Account](https://github.com/yuanping/workxp-api/blob/master/sections/account.md)
* [Contacts](https://github.com/yuanping/workxp-api/blob/master/sections/contacts.md)
* [Activities](https://github.com/yuanping/workxp-api/blob/master/sections/activities.md)
* [Notes](https://github.com/yuanping/workxp-api/blob/master/sections/notes.md)
* [Tasks](https://github.com/yuanping/workxp-api/blob/master/sections/tasks.md)
* [Attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)
* [Deletions](https://github.com/yuanping/workxp-api/blob/master/sections/deletions.md)
* [Feedback](https://github.com/yuanping/workxp-api/blob/master/sections/feedback.md)

## 帮助我们使之更好
如果有可以让API更好的想法请告诉我们。如果你有一个特定的功能需求，或者你发现了一个bug，请使用GitHub的issues功能。Fork这个文档然后发一个改进的pull request。  