# Contacts
`GET /contacts.json`  一次最多取500条记录

### Response

	[
		{
			"id":56,
			"name":"汪练",  
			"title":"CEO",
			"type":"Company/Person",
			"company":{"id": 34, "name": "WorkXP"},
			"other":"background info",
			"avatar":{"name":"avatar.png", "url":"http://workxp.info/avatar.png"},
			"contact_methods":[ 
													{
														"id":234,
														"type":"ContactPhone",
														"key":"office", 
														"value":"123123123321" 
													}
												]
		}
	]

### 数据说明
`contact_methods`的`type`取值`ContactPhone/ContactEmail/ContactWebsite/ContactIm/ContactAddress`
contact_methods中的key的值： 
电话：office/公司  work/工作 mobile/手机  fax/传真  home/住宅  other/其它  
邮箱：work/工作  personal/个人  other/其它  
IM: gtalk/GTalk  msn/MSN  qq/QQ  other/其它  
网站: office/公司  personal/个人  other/其它 
地址: office/公司  home/住宅  other/其它  

## Post contact
`POST /contacts.json`

###Params
`avatar`: 头像  
`data`:

	{
		"name":"汪练",  
		"title":"CEO",
		"company":"WorkXP",
		"other":"background info",
		"contact_methods":[ 
												{
													"id":234,
													"type":"ContactPhone",
													"key":"office", 
													"value":"123123123321" 
												}
											]
	}

###Response
`201 Created` 

	{"cid": "client id", "id": 83}