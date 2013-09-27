---
category: v1
path: '/v1/directory-listings/:uuid'
title: 'Get Business Updates'
type: 'GET'

layout: nil
---

## Polling for Updates

At any time, a GET request can be made to retrieve the latest information about a business. Depending on the detail level, this call can include the full business data, the content of each directory listing associated with the account (e.g. data from Google+, Bing Local, etc.), as well as the current fulfillment status.

### Request

As this is a GET request, there is no entity or body associated with the call. All filtering is done in the query string parameters, but at the most basic level, a request to obtain details about a specific business would look like the following. Of course, all requests must be signed and authenticated.

```https://[api_endpoint]/v1/directory-listings/:uuid```


There is also a mechanism to request changes since a given point in time. This would be useful if there was a recurring call set up to poll for changes. By recording the timestamp of the previous request, that same timestamp can be used as a "since" parameter to indicate that only changes made since that last time should be returned. The since time is exclusive, meaning that any changes made at that second are not included in the response.

```https://[api_endpoint]/v1/directory-listings?since=1363385995```


```Authentication: bearer TOKEN```
```{
    name: 'My new thing'
}```

### Response

The entity or body of the response will contact a JSON object with details specific to the request.

For a /directory-listings?since=timestamp request, a response might look like:

**If succeeds**, returns the created thing.

```Status: 201 Created```
```{
  "uuid":"a043c791-72b2-4201-b19e-c6ca19a5108c",
  "externalId":"ABC2345",
  "directories":{
     "merchantcircle":{
        "label":"Merchant Circle",
        "lastupdate":1363367153,
        "status":20,
        "description":"Submitted and Published",
     "listingUrl":"http:\/\/www.merchantcircle.com\/business\/A.AAA.A1.Fast.Guaranteed.Appliance.Service.Scottsdale.AZ.480-991-1188",
        "duplicateUrl":null,
        "notes":[""]
     },
     "superpages":{
        "label":"Superpages",
        "lastupdate":1363366882,
        "status":30,
        "description":"Submitted and Awaiting Publishing",
        "listingUrl":null,
        "duplicateUrl":null,
        "notes":[""]
     }
  }
},
{
  "uuid":"f4c639dd-6331-46d1-9021-ccc2637e8cae",
  "externalId":"DEF12345",
  "directories":{
     "yelp":{
        "label":"Yelp",
        "lastupdate":1363367118,
        "status":31,
        "description":"Awaiting Phone Verification",
        "listingUrl":null,
        "duplicateUrl":null,
        "notes":[""]
     },
     "yahoolocal":{
        "label":"Yahoo Local",
        "lastupdate":1363367080,
        "status":40,
        "description":"Claimed Listing",
        "listingUrl":"http:\/\/local.yahoo.com\/info-20078829-a-aaa-a1-fast-guaranteed-appliance-service-scottsdale",
        "duplicateUrl":null,
        "notes":[""]
     }
  }
}```

For a /directory-listings/:uuid request, a response might look like:

```{
  "uuid":"1c9636cc-d2aa-4ea3-bd00-dd8bde98b520",
  "externalId":"ABC1234",
  "business":{
     "name":"Provencal Construction",
     "street":"50 Burr Ridge Parkway",
     "city":"Burr Ridge",
     "state":"IL",
     "postalCode":"60527",
     "phone":"(630) 323-6768",
     "website":{
        "url":"http:\/\/provencalconstruction.com",
        "screenshot":"http:\/\/clients.localsearchoptimization.com\/37b194e7c44f06c3ce61b7f5059d0a31\/screenshot\/baseline\/"
     },
     "slogan":"There is no substitution for experience.",
     "descriptionLong":"Provencal construction is a highly experienced, award winning, owner operated construction firm. Provencal Construction is a general contractor and specializes in custom home design and building, room additions, custom cabinetry, light commercial construction and general construction. Provencal's offices and showroom is conveniently located in suburban Burr Ridge. The companies main officers are Harry Liesenfelt (president) and Mike Candela (vice president).",
     "descriptionMedium":"Provencal construction is a highly experienced, award winning, owner operated construction firm. Provencal Construction is a general contractor and specializes in custom home design.",
     "descriptionShort":"Provencal construction is a highly experienced, award winning, owner operated construction firm.",
     "keywords":"home builder, general contractor, custom home builder, commercial construction, remodeling, room additions, cabinetry, builder, home designer",
     "category1":"Home Builders",
     "category2":"Home Improvement & Remodeling Services",
     "category3":"Architects & Builders Service",
     "hoursOfOperation":"Monday - Saturday 8:00am - 5:00pm",
     "productsOffered":"Residential and commercial construction including custom homes, light commercial, remodeling, renovations, design, and all forms of general construction.",
     "paymentMethods":[
        "Cash",
        "Check",
        "Debit",
        "MasterCard",
        "VISA",
        "Discover",
        "AmEx"
     ],
     "yearEstablished":"1956",
     "numberEmployees":"varies",
     "languagesSpoken":"English",
     "logoUrl":"http:\/\/clientimages.localmarketlaunch.com\/101478_51129a78d3e4d_.jpg",
     "imageUrl":[
        "http:\/\/clientimages.localmarketlaunch.com\/101478_51129a7abb80c_1.jpg",
        "http:\/\/clientimages.localmarketlaunch.com\/101478_51129a7b21121_2.jpg",
        "http:\/\/clientimages.localmarketlaunch.com\/101478_51129a7bafeee_3.jpg",
        "http:\/\/clientimages.localmarketlaunch.com\/101478_51129a7c55f0b_4.jpg",
        "http:\/\/clientimages.localmarketlaunch.com\/101478_51129a7ca6bc2_5.jpg"
     ],
     "videoUrl":"http:\/\/www.youtube.com\/watch?v=_la6watqZLw",
     "phoneTracking":[""],
     "coordinates":{
        "latitude":41.7505743,
        "longitude":-87.9141345
     }
  },
  "searchQueries":[
     "provencal construction in burr ridge, il",
     "home builder in burr ridge, il",
     "general contractor in burr ridge, il",
     "custom home builder in burr ridge, il",
     "commercial construction in burr ridge, il"
  ],
  "received":1360144915,
  "updated":1363307015,
  "contact":{
     "firstName":"Jill",
     "lastName":"Merk",
     "email":"jill@elevatewebdesigns.com",
     "phone":"(702) 480-3277"
  },
  "directories":{
     "googleplus":{
        "label":"Google Plus",
        "lastupdate":1360803310,
        "status":40,
        "description":"Claimed Listing",
        "listingUrl":"https:\/\/plus.google.com\/114128866452346403133\/about?gl=us&hl=en",
        "notes":[""],
        "log":{
           "1360803310":"Listing Claimed\/Published"
        },
        "listing":{
           "foreign_key":"",
           "name":"Provencal Construction",
           "street":"50 Burr Ridge Parkway",
           "city":"Burr Ridge",
           "state":"IL",
           "postal_code":"60527",
           "country":"",
           "country_iso_code":"",
           "local_phone":"6302530622",
           "toll_free_phone":"",
           "fax":"",
           "website":"http:\/\/www.provencalconstruction.com\/",
           "email":"",
           "slogan":"",
           "long_description":"",
           "short_description":"",
           "keywords":[
              "establishment"
           ],
           "payment_methods":[],
           "year_established":0,
           "number_of_employees":0,
           "products_offered":[],
           "languages_spoken":[],
           "hours_of_operation":{
              "mon":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              },
              "tue":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              },
              "wed":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              },
              "thu":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              },
              "fri":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              },
              "sat":{
                 "open":true,
                 "openingTime":"0800",
                 "closingTime":"1700"
              }
           },
           "logo_url":"",
           "square_logo_url":"",
           "image_urls":[],
           "video_urls":[],
        },
        "verificationMethod":"phone"
     },...
  }
}
```
<!---
For errors responses, see the [response status codes documentation](#{% post_url 2012-12-28-response-status-codes %}).
-->