# WorkXP接口文档
这是一个REST形式的API，使用JSON序列化和OAuth2认证。

## Request

所有的请求（除Accounts接口）都以`https://<:domain>.workxp.info/api/`开始。 **使用SSL**。请求的地址包括二级域名。
二级域名可以通过[Accounts](https://github.com/yuanping/workxp-api/blob/master/sections/accounts.md)接口得到。
Accounts接口不需要二级域名，以`https://workxp.info/api/`开始。

通过请求得到你帐户上所有的联系人，在上面的地址后面加上联系的Path，比如 https://<:domain>.workxp.info/api/contacts.json. 可以用curl来测试:

```shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' https://demo.workxp.info/api/contacts.json
```

要创建一个事件也是一样的，只不过请求的head必须加上`Content-Type: application/json`：

```shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ "name": "My new note!" }' \
  https://demo.workxp.info/api/notes.json
```

## Response

* `200 OK` 修改成功
* `201 Created` 保存成功
* `203 Non-Authoritative Information` 非认证的信息
* `401 Unauthorized` 认证失败
* `403 Forbidden` 没有权限

If WorkXP is having trouble, you might see a 5xx error. 500 means that the app is entirely down, but you might also see 502 Bad Gateway, 503 Service Unavailable, or 504 Gateway Timeout. It's your responsibility in all of these cases to retry your request later. 

## 通用参数说明

* 所有时间格式都以ISO 8601标准 `YYYY-MM-DDTHH:MM:SSZ` (eg. 2012-05-03T18:01:29+08:00)  
* `begin` 取这个时间之后的记录，`end` 取这个时间之前的记录，同时传两个参数取这两个时间之间的记录。  
* `page` 取更多数据，比如一页为50条记录，则`&page=2`取51-100条记录

## 版本
要使用指定版本的接口，需要在请求上Head上设置`Accept`的值为：`application/vnd.workxp.v3`。  
如果不指定`Accept`，则默认使用最新版本的API
```shell
curl -u user:pass -H 'Accept: application/vnd.workxp.v3' https://demo.workxp.info/api/contacts.json
```

## 标识你的应用
你必须包含一个`User-Agent`的header来标识你的应用。`User-Agent`包括你应用的名称与Email，这样如果我们发现有错误或问题时，我们可以及时联系你。下面是一个例子：

    User-Agent: Freshbooks (http://freshbooks.com)

如果你不提供这个头信息，我们会返回 `400 Bad Request`。

## 使用 JSON格式
我们目前只支持JSON格式来序列话数据。我们的格式没有根节点，属性使用下划线的命名方式。
这意味着当你要发起`POST`或`PUT`请求时，必须要设置`Content-Type: application/json; charset=utf-8`。
我们返回的所有的数据都是以JSON格式，所以API URL都以.json结尾。  
如果你忘记了设置`Content-Type`，会收到`415 Unsupported Media Type`的返回代码。

# 认证
WorkXP提供了两种认证方式，基于HTTP与OAuth2认证。  
如果你需要一个自己企业使用的应用，用HTTP认证方式就可以了，但如果你要做一个公开的应用，让别人来使用，那就要用OAuth2认证方式。  
Basic HTTP Authentication  

	curl -u user:pass https://demo.workxp.info/api/users.json
	
OAuth2 token认证方式  

	curl -H "Authorization: Bearer OAUTH-TOKEN" https://demo.workxp.info/api/users.json

## 数据接口
目前只实现了下面的接口，如果你需要更多的接口，可以和我们联系:yuanping@workxp.info
* [Authentication](https://github.com/yuanping/workxp-api/blob/master/sections/authentication.md)
* [Accounts](https://github.com/yuanping/workxp-api/blob/master/sections/accounts.md)
* [Users](https://github.com/yuanping/workxp-api/blob/master/sections/users.md)
* [Contacts](https://github.com/yuanping/workxp-api/blob/master/sections/contacts.md)
* [Activities](https://github.com/yuanping/workxp-api/blob/master/sections/activities.md)
* [Notes](https://github.com/yuanping/workxp-api/blob/master/sections/notes.md)
* [Tasks](https://github.com/yuanping/workxp-api/blob/master/sections/tasks.md)
* [Attachments](https://github.com/yuanping/workxp-api/blob/master/sections/attachments.md)
* [Categories](https://github.com/yuanping/workxp-api/blob/master/sections/categories.md)
* [Deletions](https://github.com/yuanping/workxp-api/blob/master/sections/deletions.md)
* [Feedback](https://github.com/yuanping/workxp-api/blob/master/sections/feedback.md)

## 帮助我们使之更好
如果有可以让API更好的想法请告诉我们。如果你有一个特定的功能需求，或者你发现了一个bug，请使用GitHub的issues功能。Fork这个文档然后发一个改进的pull request。  