---
category: v2
path: '/v2/locations/:id/listings'
title: 'Listings by Location'
type: 'GET'
layout: nil
---

# Retrieving your listings based upon a location id.


### Request
Requests should be made with the GET method to ```https://[api_endpoint]/v2/locations/:id/listings```

Ex:
```
PUT https://[api_endpoint]/v2/locations/c13bdr7y-4024-58be-8c23-b4782f309ad0/listings
```


### Response
```
{
   "status":"success",
   "code":200,
   "message":"",
   "messages":[],
   "data":[
      {
         "id":"1794d5ee-52c2-4375-988d-a0c245a22d20",
         "location_id":"c13bdr7y-4024-58be-8c23-b4782f309ad0",
         "product_id":31,
         "listing_status_id":1,
         "username":"arandomusername@somedomain.com",
         "password":"abc123927",
         "security_answer_1":"chair",
         "security_answer_2":"connection",
         "fulfillment_status_id":20,
         "url":null,
         "deleted_at":null,
         "created_at":"2014-01-23 23:01:03",
         "updated_at":"2014-03-17 23:23:06",
         "external_id":null,
         "notes":null
      },
      {
         "id":"ec1a2d02-5016-429f-ab31-f213a0a0587b",
         "location_id":"c13bdr7y-4024-58be-8c23-b4782f309ad0",
         "product_id":36,
         "listing_status_id":1,
         "username":"arandomusername",
         "password":"abc123927",
         "security_answer_1":"chair",
         "security_answer_2":"connection",
         "fulfillment_status_id":30,
         "url":"http:\/\/www.abcd.com\/m\/yourte-Tree-Service-LLC-60618958",
         "duplicate_url":[],
         "deleted_at":null,
         "created_at":"2014-01-23 23:01:03",
         "updated_at":"2014-03-17 23:23:06",
         "external_id":null,
         "notes":null
      },
      {
         "id":"00022220-4587-4020-88b2-057f8bca92e3",
         "location_id":"c13bdr7y-4024-58be-8c23-b4782f309ad0",
         "product_id":40,
         "listing_status_id":1,
         "username":"arandomusername@somedomain.com",
         "password":"abc123927",
         "security_answer_1":"chair",
         "security_answer_2":"connection",
         "fulfillment_status_id":30,
         "url":null,
         "duplicate_url":[],
         "deleted_at":null,
         "created_at":"2014-01-23 23:01:03",
         "updated_at":"2014-03-17 23:23:06",
         "external_id":null,
         "notes":null
      },
      {
         "id":"001f95c6-ba32-4024-8640-a923c41ee387",
         "location_id":"c13bdr7y-4024-58be-8c23-b4782f309ad0",
         "product_id":43,
         "listing_status_id":1,
         "username":"arandomusername@somedomain.com",
         "password":"abc123927",
         "security_answer_1":"chair",
         "security_answer_2":"connection",
         "fulfillment_status_id":43,
         "url":"http:\/\/www.hijklymno.com\/m\/yourte-Tree-Service-LLC-60618958",
         "duplicate_url":[],
         "deleted_at":null,
         "created_at":"2014-01-23 23:01:03",
         "updated_at":"2014-03-28 08:01:30",
         "external_id":null,
         "notes":null
      }
   ]
}
```
