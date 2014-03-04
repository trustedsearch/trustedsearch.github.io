---
category: v2
path: '/v2/hook-subscriptions/:id'
title: 'Hook Subscriptions: Editing a hook subscription.'
type: 'PUT'
layout: nil
---

# Editing a hook subscription


### Request
Requests should be made with the PUT method to ```https://[api_endpoint]/v2/hook-subscriptions/:id```.

Ex:
```
PUT https://[api_endpoint]/v2/hook-subscriptions/5f091ee8-255c-40c9-b985-9afa4cd6de0b

{
  "target_url": "http://api.acme.com/trustedsearch/location-updates",
  "hook": "location.updates"
}
```


### Response
```
{
  "code": 200,
  "data": {
    "created_at": "2014-03-04 22:48:08",
    "hook_id": 1,
    "id": "5f091ee8-255c-40c9-b985-9afa4cd6de0b",
    "target_url": "http://api.acme.com/trustedsearch/location-updates",
    "updated_at": "2014-03-04 23:19:17",
    "user_id": 27
  },
  "message": "",
  "status": "success"
}
```
