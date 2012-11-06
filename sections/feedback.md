# Feedback
用户可以通过此接口反馈问题,提建议和意见。

## Post note
`POST /feedback.json`

### Params

```json
	{
		"content": "feedback content"
	}
```

### Response
创建成功返回`201 Created`，如果用户没有权限返回`403 Forbidden`。
