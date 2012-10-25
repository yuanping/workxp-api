# Feedback

用户可以通过此接口反馈问题和意见。

## Post note
`POST /feedback.json`

###Params

`content`: 反馈内容

###Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。
