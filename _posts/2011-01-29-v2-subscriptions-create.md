---
category: v2
path: '/v2/hook-subscriptions'
title: 'Hook Subscriptions: Create'
type: 'POST'
layout: nil
---

# Creating a new hook-subscription

### Request
Requests should be made with the POST method to ```https://[api_endpoint]/v2/hook-subscriptions```.

Ex:
```
POST https://[api_endpoint]/v2/hook-subscriptions

{
  "target_url": "http://api.acme.com/trustedsearch/location-update",
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
    "target_url": "http://api.acme.com/trustedsearch/location-update",
    "updated_at": "2014-03-04 22:48:08",
    "user_id": 27
  },
  "message": "",
  "status": "success"
}
```

### Notes

* If you create multiple subscriptions for the same hook, we will notify you multiple times. This allows for you to setup different endpoints for the same hook if needed.
