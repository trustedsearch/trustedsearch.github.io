---
category: v1
path: '/v1/local-business'
title: 'Submitting a Business'
type: 'POST'
layout: nil
---

# Submitting a Location

Submitting a location is the equivalent of placing an order. The API request contains the information about the business (name, address, phone number, description, hours of operation, etc.), the primary contact for the location (unpublished), the products/packages to be fulfilled, some white-labelling options, and optionally a user account to associate with the location for dashboard access.

## External ID

We provide a pass-through parameter for partners to specify their unique ID for each location. This external ID will be passed back in all API-based communcations about a location. The use of an external ID is required, and must be unique within the partner's account.

## Universally Unique Identifier (UUID)

All locations are identified by a UUID (defined in [RFC 4122](http://www.ietf.org/rfc/rfc4122.txt)). A UUID will be created for each location received and passed back in the response. An example of a UUID is: 94c459ea-7064-4ff0-8da1-43b669bf62f6.

## Phone Verification and "On Behalf Of"

There are a number of directories that require phone verification in order for a listing to publish and become owner-verified. To complete this verification process, a phone verification specialist (PVS) will trigger telephone calls to the business location phone number. That phone call (typically a robo-call) will either provide a PIN over the phone which must be communciated to the PVS in real time, or there will be a prompt for the merchant to enter a PIN, which will be provided by the PVS.

To facilitate this, A PVS must be on a phone call or an online chat with an employee at the business location. We provide the option to our partners to request that a PVS call "on behalf of" a business or entity. The text provided in this field will be used verbatim in any communication with the location to maintain a white-labelled experience. Any online interaction (email, website) will be conducted in a similar manner.

## Packages and Products

Depending upon your partner relationship, either the "packages" or "products" nodes will be used within "order". If the partner agreement was based around one or more packages, those IDs will be provided to you; for those with product-based relationships, a list of available products will be provided to you prior to integration.

Only one of "packages" or "products" may be specified within a request.

## Updating Business Data

When sending updated business data (after the initial submission), essentially the same request can be triggered with any number of data fields provided. In other words, if there is only a change to the business' phone number, a request may be made that only includes the phone number; all other data will remain untouched.

Please note that any content within the "order" or "user" blocks (detailed below) will be ignored in reubsmissions.

### Request

#### Request Data Format

When preparing to submit business information to the API server, data must be packaged into JSON objects and organized in the following way. There are three main sections of data:

- business: all details about the business location, as well as related meta data.
- order: details about the services being requested (generally a list of product or package skus).
- contact: unpublished data about the primary contact at the location, typically so that we know who to ask for when performing phone verification.

It is possible to submit multiple businesses within one call. Simply comma-separate individual location entries.


#### Fields

#### Top Level
| field | type( length ) | required | options | description |
|-------|:--------------:|:--------:|:-------:|-------------|
| externalId | string | * |-| The partner's unique identifier for the location |
| order | object | * |-| Details related to the requested fulfillment of the location |
| business | object | * |-| The location's NAP+W and any associated data |
| contact | object | * |-| The primary contact at the location. This ideally is somebody aware of the work being performed. Any data contained herein will NOT be published. |


#### order object
| field | type( length ) | required | options | description |
|-------|:--------------:|:--------:|:-------:|-------------|
| packages | array | * |-| Array of string names representing packages available to partner. These will be provided prior to integration. |
| products | array | * |-| Array of string names representing products available to partner. These will be provided prior to integration. |
| termsAccepted | boolean | * |true / false| Must be true to complete an order. Indicates acceptance of TOS. |
| onBehalfOf | string | - |-| The business or entity name a phone verification specialist will use when calling on behalf of an organization. |


#### contact object
| field | type( length ) | required | options | description |
|-------|:--------------:|:--------:|:-------:|-------------|
| firstName | string(40) | * |-| First name of the primary contact at the physical location. For data- or verification-related issues. No special characters.|
| lastName | string(80) | * |-| Last name of the primary contact at the physical location. No Special characters |
| email | string(80) | * |-| Email address of the primary contact at the physical location. |
| phone | string(10) | * |-| Phone number of the primary contact. |

#### Description Rules

* At a minium please provide the descriptionLong in accordance with description formating rules.
* The enhancement process will use the descriptionLong to generate the descriptionMedium and descriptionShort.
* If you provide descriptionMedium or descriptionShort we will use exactly those values, however they may be reviewed for grammatical errors.
* If you provide descriptionLong and it is larger then 1000 characters, the enhancement process will update it to a single version with a length that adheres to a majority of our publishers. The medium and short descriptions will be a trimmed down version of this version.

#### Description Formating Rules

* No Html or special characters. They will be stripped out.
* Human readable.



#### business object
| field | type( length ) | required | options | description |
|-------|:--------------:|:--------:|:-------:|-------------|
| name | string(100) | * |-| The full name of the business as it should be published. "Doing Business As Name - Commonly known as name.  |
|| | || name: Cannot be provide in ALL CAPS, (except for abreviations).|
|| | || name: Cannot be a website. Business must have a physical store front, or be a service area business. (NO online-only businesses)|
| street | string(255) | * |-| The street address of the physical company. This can include a suite number |
| privateStreet | boolean | - |-| Indicates whether or not the street address should be published (defaults to true if not specified). |
| city | string(255) | * |-| City of the physical address. Alpha values only (period, hyphen and apostrophe allowed) |
| state | string(2) | * |-| State of the physical address. Should be state abbreviation, not spelled out.  US States only (DC Included)}|
| postalCode | string(5) | * |-| Zip code for the physical address. Zip code must be 5 digit (with leading zero if necessary).  Numeric values only.|
| countryCode | string(2) | - |-| The 2-digit ISO 3166-1-alpha-2 country code (currently only US is accepted). |
| phoneLocal | string(10) | * |-| The 10-digit local (non-toll-free) phone number of the location. This number will be used for verification purposes and must ring at the business location. No extensions are allowed. |
| phoneTollFree | string(10) | - |-| The 10-digit toll-free phone number of the location. |
| fax | string(10) | - |-| The 10-digit fax number of the location. |
| website | string(255) | - |-| Well-formed URL of the company's website (strongly recommended). ex: http://www.trustedsearch.org |
| email | string(80) | - |-| Business contact email address (to be published). ex: info@yoursitehere.com |
| slogan | string(80) | - |-| A short motto or slogan for the business. ex: "A diamond is forever." |
| descriptionLong | string(5000) | - |-| A long description for the business. *(see description rules) |
| descriptionMedium | string(200) | - |-| A medium-length description for the business. *(see description rules)|
| descriptionShort | string(140) | - |-| A short description for the business. *(see description rules) |
| keywords | string(255) | - |-| A comma-separated list of keywords that are relevent to the business (for SEO purposes). |
| paymentMethods | array | - |-| A comma-separated list of payment methods the business accepts. Options: 'Cash','Check','Mastercard','VISA','American Express','Discover','PayPal','Invoice' |
| yearEstablished | string(4) | - |-| Year business was established. |
| numberEmployees | int | - |-| The number of employees at the physical location. |
| productsOffered | string(255) | - |-| List the products and services that you offer. Free Text field, use a comma to separate multiple values. |
| languagesSpoken | string(100) | - |-| Languages spoken. Free Text field, use a comma to separate multiple values.  ex: english,spanish |
| hoursOfOperation | string(255) | - |-| The business' [hours of operation](#{% post_url 2012-12-27-hours-of-operation-format %}). ex: "MF08001700H" for Mon-Fri 8:00am-5:00pm |
| logoUrl | string(255) | - |-| Well-formed URL of the business logo. (JPG, PNG, GIF) |
| logoSquaredUrl | string | - |-| Well-formed URL for a square version of the business logo. (JPG, PNG, GIF) |
| imageUrl | array(5) :: string(255) per element | - |-| An array of well-formed URLs of images for the business. (JPG, PNG, GIF) |
| videoUrl | string(128) | - |-| A youtube.com video URL for the business. ex: http://www.youtube.com/watch?v=VIrBecB746c |

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
         "termsAccepted" : true,
         "products":[
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

Sends back an array of JSON objects, one for each submitted location containing the status, externalId, and assigned UUID.

```Status: 200 OK```
```[
   {
      "externalId":"ABC12345678",
      "uuid":"94c459ea-7064-4ff0-8da1-43b669bf62f6",
      "status":201
   },...
]```

### Status codes and their meanings

The status will indicate the success of that particular location:

- 200 indicates general success
- 400 indicates an error in the request
- 401 indicates an authentication error
