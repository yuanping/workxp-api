# Attachments

上传文件到WorkXP需要两个步骤：  
1.  上传文件，当上传成功后会收到一个验证码。  
2.  把这个文件与事件或评论关联，可以参考[添加事件](https://github.com/yuanping/workxp-api/blob/master/sections/notes.md)

## Create attachment

`POST /attachments.json` 一次只能上传一个附件,请求的参数`file`是这个文件的二进制流。请确保正确设置了`Content-Type` `Content-Length`头。  
一旦上传成功，你会收到`200 OK`的响应和一个验证码(token)，你要保存好这个验证码，之后会用到关联事件上。  
### Params
`file`:上传的文件

### Response
创建成功返回`201 Created`，如果用户没有存储空间或权限返回`403 Forbidden`。

```json
{
  "token": "4f71ea23-134660425d1818169ecfdbaa43cfc07f4e33ef4c"
}
```

### Ruby Example

```ruby
conn = Faraday.new(:url => 'https://workxp.info') do |builder|
  # POST/PUT params encoders:
  builder.request  :multipart
  builder.request  :url_encoded
  builder.request  :json

  builder.adapter  :net_http
end

# uploading a file:
payload = { :profile_pic => Faraday::UploadIO.new('avatar.jpg', 'image/jpeg') }

# "Multipart" middleware detects files and encodes with "multipart/form-data":
conn.post '/attachments.json', payload, :'Sub-Domain' => 'your_domain'
```


