# 认证
如果你需要一个自己企业使用的应用，用基于HTTP的认证方式就可以了，但如果你要做一个公开的应用，让别人来使用，那就要用OAuth2认证方式。
你可以用自己的用户名、密码访问自己的帐户测试API，OAuth2是一个简单的认证协议，你也可以很快的了解并使用它。  
如果想得到当前用户的信息，可以通过[Get myself](https://github.com/yuanping/workxp-api/blob/master/sections/users.md#get-user)接口得到。

## HTTP认证
快速的使用起WorkXP API 可以通过基本的HTTP认证方式。
```shell
curl -u user:pass -H 'User-Agent: MyApp (yourname@example.com)' https://workxp.info/api/accounts.json
```

要创建一个事件也是一样的，只不过请求的head必须加上`Content-Type: application/json`：  

```shell
curl -u username:password \
  -H 'Content-Type: application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ "name": "My new note!" }' \
  https://workxp.info/api/notes.json
```

## OAuth2认证
要做一个完整的公开的应用，你不能向你的客户要他们的用户名和密码进行认证，更不能保存客户的密码！  
OAuth2是一种标准的认证方式，提供了一种简单的方式来让用户访问他的帐户。你会得到一个API的token而不用向用户要他们的密码。

1. [OAuth2的客户端](http://oauth.net/code/).
2. 在WorkXP上注册你的应用 [workxp.info/integrate](https://workxp.info/integrate)（目前还未开放自助注册，可以通过邮件联系我们）。注册完成后你会分配到`client_id`和`client_secret`。
你需要要提供一个`redirect_uri`:我们会把验证的`code`发到这个URL。如果你还没准备好，可以先提供一个测试的，比如说 `http://myapp.com/oauth`。
3. 配置你的OAuth2 library，设置`client_id`, `client_secret`, 和 `redirect_uri`。请求`https://workxp.info/oauth/authorize`认证并通过 `https://workxp.info/oauth/token`(POST请求)得到访问token。
4. 试着发起一个请求`https://workxp.info/api/authorization.json`测试一下。


## 认证信息
`GET /authorization.json` 返回当前登录用户的基本信息和产品列表，如果想了解某个产品下用户的信息（比如是否是管理员等）通过[Users](https://github.com/yuanping/workxp-api/blob/master/sections/users.md)接口获得。

```json
	{
		"identity": {
			"id": 12,
			"name": "袁平",
			"email": "yuanping@workxp.info",
			"avatar_url": "http://workxp.info/avatar.png"
		},
		"accounts": {
			"company": "容平志远科技（北京）有限公司", 
			"domain": "rongping"
		}
	}
```