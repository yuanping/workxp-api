# WorkXP接口文档
这是一个REST形式的API，使用JSON序列化和OAuth2认证。

## Request

所有的请求都以`https://<:domain>.workxp.info/api/v3/`开始。 **使用SSL**。请求的地址包括二级域名。

通过请求得到你帐户上所有的联系人，在上面的地址后面加上联系的Path，比如 https://<:domain>.workxp.info/api/v3/contacts.json. 可以用curl来测试:

```shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' https://demo.workxp.info/api/v3/contacts.json
```

要创建一个事件也是一样的，只不过请求的head必须加上`Content-Type: application/json`：

```shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ "name": "My new note!" }' \
  https://demo.workxp.info/api/v3/notes.json
```

## Response

* `200` OK 修改成功
* `201` Created 保存成功
* `203` Non-Authoritative Information 认证失败
* `401` 请求处理失败
* `403` Forbidden 没有权限

If WorkXP is having trouble, you might see a 5xx error. 500 means that the app is entirely down, but you might also see 502 Bad Gateway, 503 Service Unavailable, or 504 Gateway Timeout. It's your responsibility in all of these cases to retry your request later. 

## 通用参数说明

* 所有时间格式都为`yyyy-MM-dd HH:mm:ss +0800`  
* `begin` 取这个时间之后的记录，`end` 取这个时间之前的记录，同时传两个参数取这两个时间之间的记录。  
* `page` 取更多数据，比如一页为50条记录，则`&page=2`取51-100条记录

## 标识你的应用
你必须包含一个`User-Agent`的header来标识你的应用。`User-Agent`包括你应用的名称与Email，这样如果我们发现有错误或问题时，我们可以及时联系你。下面是一个例子：

    User-Agent: Freshbooks (http://freshbooks.com)

如果你不提供这个头信息，我们会返回 `400 Bad Request`。

## No XML, just JSON
We only support JSON for serialization of data. Our format is to have no root element and we use snake\_case to describe attribute keys. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Basecamp. **All API URLs end in .json to indicate that they accept and return JSON.**

You'll receive a `415 Unsupported Media Type` response code if you attempt to use a different URL suffix or leave out the `Content-Type` header.

# 认证
WorkXP提供了两种认证方式，基于HTTP与OAuth2认证。  
如果你需要一个自己企业使用的应用，用HTTP认证方式就可以了，但如果你要做一个公开的应用，让别人来使用，那就要用OAuth2认证方式。


## 数据接口
* [Authentication](https://github.com/yuanping/workxp-api/blob/master/sections/authentication.md)
* [Account](https://github.com/yuanping/workxp-api/blob/master/sections/account.md)
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