# Attachments

上传文件到WorkXP需要两个步骤：
1. 上传文件，当上传成功后会收到一个验证码。
2. 把这个文件与事件或评论关联，可以参考[添加事件](https://github.com/yuanping/workxp-api/blob/master/sections/notes.md)

## Create attachment

`POST /attachments.json` 一次只能上传一个附件,请求的body应该是这个文件的二进制流。请确保正确设置了`Content-Type` `Content-Length`头。  
一旦上传成功，你会收到`200 OK`的响应和一个验证码(token)，你要保存好这个验证码，之后会用到关联事件上。  

下面是使用`curl`请求的例子：

```
curl --data-binary @logo.png \
       -u user:pass \
       -H 'Content-Type: image/png' \
       -H 'User-Agent: Demo (yuanping@workxp.info)' \
       https://demo.workxp.info/api/v3/attachments.json
```

### Response
创建成功返回`201 Created`，如果用户没有存储空间或权限返回`403 Forbidden`。

```json
{
  "token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c"
}
```





