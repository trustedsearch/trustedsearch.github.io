---
category: v2
path: '/v2/hook-subscriptions'
title: 'Hook Subscriptions: Delete a hook subscription'
type: 'DELETE'
layout: nil
---

# Delete hook subscription


### Request
Requests should be made with the DELETE method to ```https://[api_endpoint]/v2/hook-subscriptions/:id```

Ex:
```
DELETE https://[api_endpoint]/v2/hook-subscriptions/5f091ee8-255c-40c9-b985-9afa4cd6de0b
```

### Response

```
{
  "code": 200,
  "data": [
    
  ],
  "message": "Successfully removed subscription : 5f091ee8-255c-40c9-b985-9afa4cd6de0b",
  "status": "success"
}
```