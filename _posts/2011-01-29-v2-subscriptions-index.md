---
category: hooks
path: '/v2/hook-subscriptions/:id'
title: 'Show all Subscriptions'
type: 'GET'
layout: nil
---


# Get a single subscription

### Request
Requests should be made with the GET method to ```https://[api_endpoint]/v2/hook-subscriptions```

Ex:
```
GET https://[api_endpoint]/v2/hook-subscriptions
```

### Response

```
{
  "code": 200,
  "data": [
    {
      "created_at": "2014-03-04 23:40:37",
      "hook_id": 2,
      "id": "20d01ac1-af2e-4c58-8e02-236c723ccfde",
      "target_url": "http://api.acme.com/trustedsearch/location-audit",
      "updated_at": "2014-03-04 23:40:37",
      "user_id": 27
    },
    {
      "created_at": "2014-03-04 22:48:08",
      "hook_id": 1,
      "id": "5f091ee8-255c-40c9-b985-9afa4cd6de0b",
      "target_url": "http://api.acme.com/trustedsearch/location-updates",
      "updated_at": "2014-03-04 23:19:17",
      "user_id": 27
    }
  ],
  "message": "",
  "status": "success"
}
```
