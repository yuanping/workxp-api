# 认证
如果你需要一个自己企业使用的应用，用基于HTTP的认证方式就可以了，但如果你要做一个公开的应用，让别人来使用，那就要用OAuth2认证方式。
你可以用自己的用户名、密码访问自己的帐户测试API，OAuth2是一个简单的认证协议，你也可以很快的了解并使用它。  
如果想得到当前用户的信息，可以通过[Get myself](https://github.com/yuanping/workxp-api/blob/master/sections/users.md#get-user)接口得到。

## HTTP认证

`POST /sign_in` 认证后会返回一个Token，之后每个数据接口请求都要加上`auth_token`参数来验证身份。  
Token就像你的用户名和密码，任何人知道了你的Token就可以访问修改你的数据。  
当你修改了密码后，认证的Token也会改变，这时需要重新认证取得新的Token。

### Params

```json
	{
		"email": "yuanping@workxp.info",  
		"password": "test"
	}
```

### Response
如果认证成功，返回`200` OK，认证失败返回`203` Non-Authoritative Information。

```json
	{
		"auth_token":"jWu7aUYpFmNMevnTaKx0"
	}
```

## OAuth2认证