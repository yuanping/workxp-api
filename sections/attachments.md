# Attachments

文件上传

## Create attachment
`POST /attachments.json` 上传Note/Comment的附件，一次只能上传一个附件。别忘记了设置`Content-Type`参数。

###Params

`id`: `Note/Comment`的`ID`
`type`: `Note/Comment`
`file`: 要上传的文件

###Response

上传成功返回`200 OK`，如果用户没有权限或空间已满返回`403 Forbidden`。


```json
{
  "can_upload": true
}
```




