---
category: v1
path: '/v1/local-business'
title: 'Submitting a Business'
type: 'POST'
layout: nil
---

## Submitting a Location

Submitting a location is the equivalent of placing an order. The API request contains the information about the business (name, address, phone number, description, hours of operation, etc.), the primary contact for the location (unpublished), the directories/packages to be fulfilled, some white-labelling options, and an optional user account to associate with the location for dashboard access.

## External ID

We provide a pass-through parameter for partners to specify their unique ID for each client. This external ID will be passed back in all API-based communcations about a business. The use of an external ID is required, and must be unique within the partner's account.

## Universally Unique Identifier (UUID)

All businesses are identified by a UUID (defined in [RFC 4122](http://www.ietf.org/rfc/rfc4122.txt)). A UUID will be created for each location received and passed back in the response. An example of a UUID is: 94c459ea-7064-4ff0-8da1-43b669bf62f6.

## Phone Verification and "On Behalf Of"

For Business Listings Management, there are a number of directories that require phone verification in order for a listing to publish and become owner-verified. To complete this verification process, a phone verification specialist (PVS) will trigger telephone calls to the business location phone number. That phone call (typically a robo-call) will either provide or ask for a PIN. In the event that a PIN is provided to the business, that PIN must be relayed back to the PVS; in the event a PIN is requested, that PIN will be given by the PVS.

To facilitate this, A PVS must be on a phone call or an online chat with the business (typically through http://verifymylistings.com), and when we make initial contact, we provide the option to our partners to request that we call "on behalf of" them. The text provided in this field will be used verbatim in any communication with the client to maintain a white-labelled experience. Any online interaction (email, website) will be conducted in a similar manner.

## Packages and Directories

Depending upon your partner relationship, either the ``packages`` or ``directories`` nodes will be used within ``order``. If the partner agreement was based around one or more packages, those IDs will be provided to you; for those with directory-based relationships, a list of available directories will be provided to you prior to integration.

Only one of ``packages`` or ``directories`` may be specified within a request.

## Updating Business Data

When sending updated business data (after the initial submission), essentially the same request can be triggered with any number of data fields provided. In other words, if there is only a change to the business' phone number, a request may be made that only includes the phone number; all other data will remain untouched.

Please note that any content within the ``order`` or ``user`` blocks (detailed below) will be ignored in reubsmissions.

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
            "see note above"
         ],
         "directories":[
            "see note above"
         ]
      },
      "contact":{
         "firstName":"Bob",
         "lastName":"Jones",
         "email":"bob@domain.com",
         "phone":"8005551234"
      },
      "business":{
         "name":"Bob's Fish Tacos",
         "street":"247 Ocean Way",
         "city":"San Luis Obispo",
         "state":"CA",
         "postalCode":"93401",
         "phoneLocal":"(805) 555-9876",
         "phoneTollFree":"(800) 555-4567",
         "fax":"(805) 555-0142",
         "website":"http://www.bobsfishtacos.com",
         "email":"greatfood@bobsfishtacos.com",
         "slogan":"The freshest Mexican food you'll ever eat.",
         "descriptionLong":"A really long description (maximum 1000 characters)",
         "descriptionMedium":A description that is no longer than 200 characters.",
         "descriptionShort":"A description that is no longer than 140 characters.",
         "keywords":"fish taco, mexican food, salsa",
         "paymentMethods":[
            "mastercard",
            "visa",
            "discover",
            "amex",
            "check",
            "cash"
         ],
         "yearEstablished":"2011",
         "numberEmployees":"7",
         "productsOffered":"mexican food, fish tacos",
         "languagesSpoken":"english, spanish",
         "hoursOfOperation":"MF08001700H",
         "logoUrl":"http://www.bobsfishtacos.com/logo.jpg",
         "logoSquareUrl":"http://www.bobsfishtacos.com/logo.jpg",
         "imageUrl":[
            "http://images.bobsfishtacos.com/100702_5009d194859.jpg",
            "http://images.bobsfishtacos.com/100702_5009d195016.jpg",
            "http://images.bobsfishtacos.com/100702_5009d19577a.jpg",
            "http://images.bobsfishtacos.com/100702_5009ccdf005.jpg",
            "http://images.bobsfishtacos.com/100702_5009ccdf4d0.jpg"
         ],
         "videoUrl":[
            "http://www.youtube.com/watch?v=cXuTiAHdxTg"
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
