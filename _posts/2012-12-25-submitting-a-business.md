---
category: v1
path: '/v1/local-business/:id'
title: 'Submitting a Business'
type: 'POST'
layout: nil
---


## Universally Unique Identifier (UUID)

All businesses are identified by a version 4 or version 5 UUID (defined in [RFC 4122](http://www.ietf.org/rfc/rfc4122.txt)). A UUID will be created for each location received and passed back to you in the response. An example of a UUID is: 94c459ea-7064-4ff0-8da1-43b669bf62f6.

## Phone Verification and "On Behalf Of"

For Business Listings Management, there is a number of directories that require phone verification in order for a listing to publish and become owner-verified. To complete this verification process, a phone verification specialist will trigger telephone calls to the business location phone number. That phone call (typically a robo-call) will either provide or ask for a PIN. In the event that a PIN is provided to the business, that PIN must be relayed back to LML; in the event a PIN is requested, that PIN will be given by LML.

To facilitate this, we must be on a phone call or a chat with the business, and when we make initial contact, we provide the option to our partners to request that we call "on behalf of" them. This text will be used verbatim in any communication with the client to maintain as white-labelled an experience as possible. Any online interaction (email, website) will be through the intentionally unbranded verifymylistings.com.

## External ID

We allow a pass-through parameter for our partners to specify their unique ID for each client. This external ID will be passed back in all responses. The use of an external ID is encouraged.

## Updating Business Data

When sending updated business data (after the initial submission), there are changes that need to be made to the request, other than the omission of the "order" block (if the "order" block is included in a resubmission, it will be ignored).

### Request

#### Request Data Format

When preparing to submit business information to the API server, data must be packaged into JSON objects and organized in the following way. There are three main sections of data:
business: all details about the business location, as well as related meta data.
order: details about the services being requested (generally a list of product or package skus).
contact: unpublished data about the primary contact at the location, typically so that we know who to ask for when performing phone verification.

It is possible to submit multiple businesses within one call. Simply comma-separate individual location entries.


#### Fields

#### Top Level

| field | type( length ) | required | options | Description |
|-------|:--------------:|:--------:|:-------:|-------------|
| externalId | string | * |-| A unique identifier to be used by developers to keep track of their own locations. |
| order | object | * |-| The details about which types of products or packages the developer wants applied to the locations in this order. |
| contact | object | * |-| The listing status of this listing |
| url | varchar |  |-| Listing url |
| duplicate_url | text |  |-| Any duplicate urls, comma delimited |
| username | varchar |  |-| For login to this listing |
| password | varchar |  |-| For login to this listing |
| verification | enum |  |-| Verification type |
| created_at | timestamp | * |-| automatic |
| updated_at | timestamp | * |-| automatic |
| deleted_at | timestamp |  |-| only if deleted |


#### order object
| field | type( length ) | required | options | Description |
|-------|:--------------:|:--------:|:-------:|-------------|
| onBehalfOf | string | - |-| Name of Partner for whome this order is being placed on behalf of. |
| packages | array | - |-| Array of string names representing packages available to developer. These will be custom provided by sales rep. |
| products | array | - |-| Array of string names representing products available to developer. These will be custom provided by sales rep. |


#### contact object
| field | type( length ) | required | options | Description |
|-------|:--------------:|:--------:|:-------:|-------------|
| firstName | string | * |-| First name of person trustedsearch should contact for non public issues. |
| lastName | string | * |-| Last name of person trustedsearch should contact for non public issues. |
| email | string | * |-| Email of person trustedsearch should contact for non public issues. |
| phone | string | * |-| Phone number of person trustedsearch should contact for non public issues. |

#### business object
| field | type( length ) | required | options | Description |
|-------|:--------------:|:--------:|:-------:|-------------|
| name | string | * |-| First name of person trustedsearch should contact for non public issues. |
| street | string | * |-| Last name of person trustedsearch should contact for non public issues. |
| city | string | * |-| Email of person trustedsearch should contact for non public issues. |
| state | string(2) | * |-| State abbreviation uppercased. |
| postalCode | string | * |-| 5 digit postal code |
| phoneLocal | string | * |-| Local phone number. Format: (555) 555-5555 |
| phoneTollFree | string | - |-| Toll Free phone number. Format: (800) 555-5555|
| fax | string | - |-| Fax number |
| website | string | * |-| Well formed url of the company. ex: http://www.trustedsearch.org |
| email | string | - |-| Published contact email address. ex: info@yoursitehere.com |
| slogan | string | - |-| "A diamond is forever." |
| descriptionLong | string | - |-| A long description describing the business. |
| descriptionShort | string | - |-| A shorter description of the business. |
| keywords | string | - |-| comma separated list of keywords that should be assigned to business for SEO purposes. |
| paymentMethods | array | - |-| Array of options business supports. Options : "mastercard", "visa", "discover", "amex", "check", "cash" |
| yearEstablish | string(4) | - |-| Year business was established. |
| numberEmployees | int | - |-| Number of employees. |
| productsOffered | string | - |-| Comma separated list of products offered. |
| languagesSpoken | string | - |-| Comma separated list of languages spoken. |
| hoursOfOperation | string | - |-| YellowPages standards for hours of operation. |
| logoUrl | string | - |-| Well formed url of business logo. |
| logoSquaredUrl | string | - |-| Well formed url for a square version of your business logo. Ideally 640px. We will scale it up so make it good quality.|
| imageUrl | array(5) | - |-| Well formed array of images. |
| videoUrl | string | - |-| A youtube.com video url. ex: http://www.youtube.com/watch?v=VIrBecB746c |

Requests should be made with the POST method to ```https://[api_endpoint]/v1/local-business```.

```
[
   {
      "externalId":"ABC12345678",
      "order":{
         "onBehalfOf":"Partner ABC",
         "packages":[
            "abc001",
            "abc017"
         ]
      },
      "contact":{
         "firstName":"Travis",
         "lastName":"Purdy",
         "email":"travis@localmarketlaunch.com",
         "phone":"8007203291"
      },
      "business":{
         "name":"Local Market Launch",
         "street":"419 State St",
         "city":"Santa Barbara",
         "state":"CA",
         "postalCode":"93101",
         "phoneLocal":"(805) 960-5545",
         "phoneTollFree":"(800) 720-3291",
         "fax":"(805) 960-5571",
         "website":"http://localmarketlaunch.com",
         "email":"info@localmarketlaunch.com",
         "slogan":"Your business first.",
         "descriptionLong":"A really long desc....",
         "descriptionShort":"Our team has been helping businesses like yours navigate the complexities of online marketing since the beginning of the Internet.",
         "keywords":"internet marketing, local search optimization, local search engine optimization, search portals, directory listing service, local directory listing, local search portals, directory listing, advertising yellow pages, businessdirectory",
         "paymentMethods":[
            "mastercard",
            "visa",
            "discover",
            "amex",
            "check",
            "cash"
         ],
         "yearEstablished":"2011",
         "numberEmployees":"25",
         "productsOffered":"directory listing service, internet marketing",
         "languagesSpoken":"english, spanish",
         "hoursOfOperation":"MF08001700H",
         "logoUrl":"http://clientimages.localmarketlaunch.com/100702_5009d2a1d45a4_.jpg",
         "logoSquareUrl":"http://clientimages.localmarketlaunch.com/100702_5009d2a2a319f.jpg",
         "imageUrl":[
            "http://clientimages.localmarketlaunch.com/100702_5009d194859b4_1.jpg",
            "http://clientimages.localmarketlaunch.com/100702_5009d195016e0_2.jpg",
            "http://clientimages.localmarketlaunch.com/100702_5009d19577a6b_3.jpg",
            "http://clientimages.localmarketlaunch.com/100702_5009ccdf00535_4.jpg",
            "http://clientimages.localmarketlaunch.com/100702_5009ccdf4d062_5.jpg"
         ],
         "videoUrl":[
            "http://www.youtube.com/watch?v=cXuTiAHdwTg"
         ]
      }
   },{...}
]
```

### Response

Sends back a collection of things.

```Status: 200 OK```
```[
   {
      "externalId":"ABC12345678",
      "uuid":"94c459ea-7064-4ff0-8da1-43b669bf62f6",
      "status":201
   },...
]```

### status codes and their meanings

The status will indicate the success of that particular location:

- 200 indicates general success
- 201 indicates that a new business was created
- 202 indicates that the data was received and enqueued (but not yet processed). No further action is needed.
- 400 indicates an error in the request
- 401 indicates an authentication error
