#tasks
GET /tasks.json
##params
timestamp: 上次同步时间
一页100条记录，如果要取更多记录，需要加&page=2参数，&page=3以此类推。
##response
```json
[
    {
        "cid":client id,
        "id":server's task_id,
        "name":"task content",
        "contact_id":contact_id,
        "due_at":"yyyy-MM-dd HH:mm:ss",
        "category_id":category_id,
        "owner_id":owner_id,
        "assigned_to_id":user_id,
        "privacy":"public/private",
        "state":"pending/down",
        "task_chance":"机会名称"
    },
    {
        "cid":client id,
        "id":server's task_id,
        "name":"task content",
        "contact_id":contact_id,
        "due_at":"yyyy-MM-dd HH:mm:ss",
        "category_id":category_id,
        "owner_id":owner_id,
        "assigned_to_id":user_id,
        "privacy":"public/private",
        "state":"pending/down",
        "task_chance":"机会名称"
    }
]
```

如果没有新的数据，返回[]。




#post task
POST /sync_task.json
##params
```json

    "cid":client id,
    "id":server's task_id,
    "name":"task content",
    "contact_id":contact_id,
    "due_at":"yyyy-MM-dd HH:mm:ss",
    "category_id":category_id,
    "owner_id":owner_id,
    "assigned_to_id":user_id,
    "privacy":"public/private",
    "state":"pending/down",
    "task_chance":"机会名称"

```
##response
如果更新成功返回200 OK，如果失败返回403 Forbidden




#modify task
PUT /task/37.json
##params
```json
    "cid":client id,
    "id":server's task_id,
    "name":"task content",
    "contact_id":contact_id,
    "due_at":"yyyy-MM-dd HH:mm:ss",
    "category_id":category_id,
    "owner_id":owner_id,
    "assigned_to_id":user_id,
    "privacy":"public/private",
    "state":"pending/down",
    "task_chance":"机会名称"

```
##response
如果更新成功返回200 OK，如果用户没有权限修改返回403 Forbidden


