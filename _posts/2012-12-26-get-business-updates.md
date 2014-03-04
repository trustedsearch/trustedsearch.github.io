---
category: v1
path: '/v1/directory-listings'
title: 'Get Business Updates'
type: 'GET'

layout: nil
---

# Receiving Location Updates

A number of mechanisms are in place to allow a partner to receive the latest information about a location and its listings. Depending on the detail level requested, this call can include the full business data, the content of each directory listing associated with the account (e.g. data obtained directly from Google+, Bing Local, etc.), as well as the current fulfillment status.

## Requesting an update about a specific location

As this is a GET request, there is no entity or body associated with the call. All filtering is done in the query string parameters, but at the most basic level, a request to obtain details about a specific location would look like the following. Of course, all requests must be signed and authenticated. ":uuid" would be replaced by the location's UUID provided in the response of the /local-business call.

```
https://[api_endpoint]/v1/directory-listings/:uuid
```

## Regular Polling for Updates

There is also a mechanism to request changes since a given point in time. This would be useful if there was a recurring call set up to poll for changes. By recording the timestamp of the previous request, that same timestamp can be used as a "since" parameter to indicate that only changes made since that last time should be returned. The since time is exclusive, meaning that any changes made at that second are not included in the response.

```
https://[api_endpoint]/v1/directory-listings?since=1363385995
```

## Update Pushes (Callbacks)

The API response described below is also available via a callback method. By providing an endpoint at which to receive callback messages, the most up-to-date information about a location and its listings can be pushed to a partner's servers. Currently, data is aggregated every thirty minutes, and it is immediately following those aggregations that a callback would be fired.

If there have been no updates within a thirty minute window, no callback would be fired.

## Pagination

Due to the potential for large amounts of data, the detail level of /directory-listings without a UUID is set lower than that of /directory-listings/:uuid. When performing a non-UUID request for a large span of time (a "since" parameter far in the past), the response may be returned in a paged format, where subsequent pages would require a separate API call with a "page" parameter.

### Understanding callback data:
When looking at publishers data, if the errors block  is an empty array ex: [], you can assume that we correctly found the listing and there were no issues extracting the listing data from the publisher.

### Errors
If you see that the errors block is not empty, then there could be many reasons:
* Publisher was down
* Publisher website changed
* Publisher search via api or crawl returned no records w/ a high enough match rate or not matches were found at all.


### Response

The entity or body of the response will contain a JSON object with details specific to the request.

For a /directory-listings?since=:timestamp request, a response might look like:

```Status: 200 Success```
```{
  "directories": {
    "googleplus": {
      "description": "Submitted and Published",
      "lastupdate": 1381438418,
      "listingUrl": "https://plus.google.com/110443031077278695323/about?gl=us&hl=en",
      "log": {
        "1380901043": "In Progress",
        "1381438418": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Google+",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": [],
        "id": 1206293,
        "image_urls": [
          "https://lh3.googleusercontent.com/-kTM08MZhN6k/Uk7gXmLGYII/AAAAAAAALvw/F2Ka-hU2Y-o/w800-h800/photo.jpg",
          "https://lh4.googleusercontent.com/-UaJsfxEuuyM/Uk7gXgprIII/AAAAAAAALvo/uy9ldrVfx5E/w800-h800/photo.jpg",
          "https://lh4.googleusercontent.com/-edKyC9OzUHg/Uk7gYZ3MszI/AAAAAAAALvs/UpkTvexotqU/w800-h800/photo.jpg",
          "https://lh6.googleusercontent.com/-2zCKVPu1ALY/Uk7gXkWxdwI/AAAAAAAALvk/cNaZFyaDuqk/w800-h800/photo.jpg"
        ],
        "keywords": [
          "establishment",
          "food",
          "grocery_or_supermarket",
          "health",
          "store"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:20",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "https://lh6.googleusercontent.com/-2zCKVPu1ALY/Uk7gXkWxdwI/AAAAAAAALvk/cNaZFyaDuqk/s0/photo.jpg",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. \r\n\r\nWe specialize in:\r\n\r\nBulk Organic Herbs\r\nTeas &amp; Spices\r\nHighest Quality Vitamins &amp; Supplements\r\nHerbal Extracts\r\nAromatherapy\r\nHomeopathy",
        "name": "Herb Shop",
        "number_of_employees": 0,
        "object_hash": "a90a08b1fe47520c3cb8b4573ef6e8dc8d9ff828da7e7332aa8198898ba2f9ef",
        "payment_methods": [],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. \r\n\r\nWe specialize in:\r\n\r\nBulk Organic Herbs\r\nTeas &amp; Spices\r\nHighest Quality Vitamins &amp; Supplements\r\nHerbal Extracts\r\nAromatherapy\r\nHomeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 Southwest G Street",
        "toll_free_phone": "",
        "url": "https://plus.google.com/116177505411303068587/about?hl=en",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": true,
        "videoUrl": false,
        "website": true
      }
    },
    "yahoolocal": {
      "description": "Submitted and Awaiting Publishing",
      "lastupdate": 1381438782,
      "log": {
        "1380902707": "In Progress",
        "1381438782": "Fulfillment Complete"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 30,
      "label": "Yahoo Local",
      "listing": {
        "city": "Grants Pass",
        "country": "USA",
        "country_iso_code": "",
        "email": "herbshop@bulkherbshop.com",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": [],
        "id": 1206299,
        "image_urls": [
          "http://l.yimg.com/lo/api/res/1.2/WE8nLuNhByALdHQyxWF5IQ--/YXBwaWQ9eXlhaG9vbG9jYWxzO2JnPWZmZmZmZjtjYz0zMTUzNjAwMDA7Zmk9Zml0O2g9MTUzO3E9MTAwO3c9NjAw/http://localcontent.zenfs.com/269c/269c21408599a4fd65734f8758fb808e.jpg.cf.jpg"
        ],
        "keywords": [
          "Alternative Medicine Retailers",
          "Nutrition & Supplements"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:21",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "",
        "name": "Herb Shop",
        "number_of_employees": 0,
        "object_hash": "4d41bb9a2b9fd1ab5c0d00825a2e93d1c44cb4ddb731218d99a05803dbde0ffe",
        "payment_methods": [
          "American  more...",
          "American Express",
          "Diners Club",
          "Discover",
          "MasterCard",
          "MasterCard",
          "Visa",
          "Visa"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 Sw G St",
        "toll_free_phone": "",
        "url": "http://local.yahoo.com/info-22039232-herb-shop-grants-pass",
        "video_urls": [],
        "website": "bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": false,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "binglocal": {
      "description": "Submitted and Awaiting Publishing",
      "lastupdate": 1381438360,
      "log": {
        "1380900649": "In Progress",
        "1381438360": "Fulfillment Complete"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 30,
      "label": "Bing Local",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "sat": {
            "open": "false"
          },
          "sun": {
            "open": "false"
          },
          "thu": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          }
        },
        "id": 1206290,
        "image_urls": [
          "http://www.bing.com/th?id=AH%2bUTi43Y52josg480x360&h=80&w=80&pid=local&c=7",
          "http://www.bing.com/th?id=ALno1JXQXXTUQUA480x360&h=80&w=80&pid=local&c=7",
          "http://www.bing.com/th?id=APGH0qFDxbID18w480x360&h=80&w=80&pid=local&c=7",
          "http://www.bing.com/th?id=AaFv0vngB02%2fE3Q480x360&h=80&w=80&pid=local&c=7"
        ],
        "keywords": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:19",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas &amp; Spices Highest Quality Vitamins &amp; Supplements Herbal Extracts Aromatherapy Homeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "b980767e2e8e2621d4b4df19ebd2a3800a684c49ebbd99cf2e234aa928ee8f9b",
        "payment_methods": [],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas &amp; Spices Highest Quality Vitamins &amp; Supplements Herbal Extracts Aromatherapy Homeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 Sw G St",
        "toll_free_phone": "",
        "url": "http://www.bing.com/local/details.aspx?lid=YN723x12583495",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "yelp": {
      "description": "Submitted and Published",
      "lastupdate": 1381441229,
      "listingUrl": "http://www.yelp.com/biz/the-herb-shop-grants-pass",
      "log": {
        "1380903598": "In Progress",
        "1381441229": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Yelp",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "other": {
            "freetext": "Sat 9 am - 5 pm"
          }
        },
        "id": 1206306,
        "image_urls": [
          "http://s3-media1.ak.yelpcdn.com/bphoto/N-f6IfilgrBs7uTQJsLyiQ/xss.jpg",
          "http://s3-media3.ak.yelpcdn.com/bphoto/8qFGVfetcGZ_JCEeasJv6A/xss.jpg",
          "http://s3-media3.ak.yelpcdn.com/bphoto/JoR-QG7bcQPf2eJeYd-o5g/ms.jpg",
          "http://s3-media4.ak.yelpcdn.com/bphoto/MQhfSFrfNzzDm3bGKq9XWA/xss.jpg"
        ],
        "keywords": [
          "Herbs & Spices",
          "herbsandspices"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:23",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "http://s3-media3.ak.yelpcdn.com/bphoto/JoR-QG7bcQPf2eJeYd-o5g/ms.jpg",
        "long_description": "Specialties: The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas &amp; Spices Highest Quality Vitamins &amp; Supplements Herbal Extracts Aromatherapy Homeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "fcd437fd9ffd46d99f336b23c0f41a309541be1dc1f7b8f95664620bd78aaa5f",
        "payment_methods": [
          "Credit Cards"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "Very friendly staff who know their stuff.  I was impressed by the size of the store, which is huge.  I was also impressed that they carry a huge variety of...",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://www.yelp.com/biz/the-herb-shop-grants-pass",
        "video_urls": [],
        "website": "bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": true,
        "videoUrl": false,
        "website": true
      }
    },
    "mapquest": {
      "description": "Submitted and Published",
      "lastupdate": 1380902449,
      "listingUrl": "http://www.mapquest.com/places/the-herb-shop-grants-pass-or-12477172/",
      "log": {
        "1380902449": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": true,
        "website": true
      }
    },
    "yellowpages": {
      "description": "Submitted and Published",
      "lastupdate": 1381858188,
      "listingUrl": "http://www.yellowpages.com/grants-pass-or/mip/herb-shop-1450956",
      "log": {
        "1380902756": "In Progress",
        "1381438569": "Fulfillment Complete",
        "1381858188": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Yellow Pages",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "herbshop@bulkherbshop.com",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "sat": {
            "closingTime": "1700",
            "open": "true",
            "openingTime": "0900"
          },
          "thu": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          }
        },
        "id": 1206285,
        "image_urls": [],
        "keywords": [
          "Health & Diet Food Products",
          "Herbs",
          "Vitamins & Food Supplements"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:18",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible.  \n \nWe specialize in: \n \nBulk Organic Herbs \nTeas & Spices \nHighest Quality Vitamins & Supplements \nHerbal Extracts \nAromatherapy \nHomeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "b4ccfb72d9239afbc8d4652f3fc211b119e1a5c090ecdd7ac24badca4b1bcfa6",
        "payment_methods": [
          "AMEX",
          "CASH",
          "CHECK",
          "DEBIT",
          "DISCOVER",
          "MASTER CARD",
          "VISA"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "",
        "slogan": "Herbs, Teas & Spices, Vitamins and More.",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "whitepages": {
      "description": "Submitted and Awaiting Publishing",
      "lastupdate": 1380902605,
      "log": {
        "1380902605": "Fulfillment Complete"
      },
      "notes": [
        "90 Days to Publish via infogroup"
      ],
      "percentComplete": 100,
      "status": 30,
      "label": "Whitepages",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "other": {
            "freetext": "Sun: Closed, Mon: 9:00am-6:00pm, Tue: 9:00am-6:00pm, Wed: 9:00am-6:00pm, Thu: 9:00am-6:00pm, Fri: 9:00am-6:00pm, Sat: 9:00am-5:00am"
          }
        },
        "id": 1206364,
        "image_urls": [],
        "keywords": [
          "Acupuncture",
          "Herbs",
          "Importers",
          "Massage Therapists",
          "Vitamins & Food Supplements",
          "Weight Control Service"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:25:00",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "",
        "name": "Herb Shop",
        "number_of_employees": 0,
        "object_hash": "5881f78ae92b9f9f18023e0ee9d04d57a2a4c3bc6f4ab47560cae3d64d198a02",
        "payment_methods": [],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://www.whitepages.com/business/herb-shop-grants-pass-or",
        "video_urls": [],
        "website": "http://bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": false,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": true,
        "videoUrl": false,
        "website": true
      }
    },
    "manta": {
      "description": "Submitted and Published",
      "lastupdate": 1380902303,
      "listingUrl": "http://www.manta.com/c/mmgl4xd/the-herb-shop",
      "log": {
        "1380902303": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Manta",
      "listing": {
        "city": "",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [
          "LML\\DirectoryBot\\Bots\\Manta_Bot: Could not get Business Information: Could not find ForeignKey from search. Could not get HTML from http://www.manta.com/mb?search=herb+shop+97526"
        ],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": [],
        "id": 1206483,
        "image_urls": [],
        "keywords": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:26:06",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "",
        "logo_url": "",
        "long_description": "",
        "name": "",
        "number_of_employees": 0,
        "object_hash": "3a4a32c0f43815782dba3ca161cdf29ad8a15afddab79a9a874d3385bcb9586b",
        "payment_methods": [],
        "postal_code": "",
        "products_offered": [],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "",
        "status": "NOK",
        "street": "",
        "toll_free_phone": "",
        "video_urls": [],
        "website": "",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": true,
        "videoUrl": false,
        "website": true
      }
    },
    "foursquare": {
      "description": "Postcard Verification Attempts Exhausted",
      "lastupdate": 1383247640,
      "log": {
        "1380900721": "In Progress",
        "1383247640": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 44,
      "label": "Foursquare",
      "listing": {
        "city": "Grants Pass",
        "country": "United States",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": [],
        "id": 1206289,
        "image_urls": [],
        "keywords": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:19",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "63b1690fc1d2451b74fd53ee87fb1d646359164f09c6879f51762e9a0f6d9cf5",
        "payment_methods": [],
        "postal_code": "",
        "products_offered": [],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "localcom": {
      "description": "Submitted and Published",
      "lastupdate": 1381335568,
      "listingUrl": "http://www.local.com/business/details/grants-pass-or/the-herb-shop-41698659/",
      "log": {
        "1380902095": "Fulfillment Complete",
        "1381335568": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "merchantcircle": {
      "description": "Submitted and Published",
      "lastupdate": 1385510921,
      "listingUrl": "http://www.merchantcircle.com/business/The.Herb.Shop.5414793602",
      "log": {
        "1380902457": "In Progress",
        "1385510921": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Merchant Circle",
      "listing": {
        "city": "Grants Pass",
        "country": "USA",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "other": {
            "freetext": "Mon, 9am-6pm ; Tue, 9am-6pm ; Wed, 9am-6pm ; Thu, 9am-6pm ; Fri, 9am-6pm ; Sat, 9am-5pm ; Sun, Closed."
          }
        },
        "id": 1206362,
        "image_urls": [
          "http://media.merchantcircle.com/12042051/1_full.jpeg",
          "http://media.merchantcircle.com/12042051/2_full.jpeg",
          "http://media.merchantcircle.com/12042051/3_full.jpeg",
          "http://media.merchantcircle.com/12042051/Logo_full.jpeg"
        ],
        "keywords": [
          "Banquet Rooms",
          "Beverage &amp; Drinks",
          "Beverages",
          "Candy &amp; Sweets",
          "Catering Services",
          "Culinary Schools",
          "Fast Food",
          "Food &amp; Produce Wholesale",
          "Food Services",
          "Grocery Stores",
          "Meats",
          "Organic Foods",
          "Produce Retailers",
          "Restaurant Equipment &amp; Services",
          "Restaurants",
          "Specialty Food Stores"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:25:00",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "http://media.merchantcircle.com/12042051/Logo_medium.jpeg",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in:Bulk Organic HerbsTeas &amp; SpicesHighest Quality Vitamins &amp; SupplementsHerbal ExtractsAromatherapyHomeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "aea83cc6701c5fa6773d74e9d3863955b767056f67528ffa33ec7e774a7517d7",
        "payment_methods": [
          "ATM/Debit",
          "American Express",
          "Discover",
          "Mastercard",
          "Personal Checks",
          "Visa"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in:Bulk Organic HerbsTeas &amp; SpicesHighest Quality Vitamins &amp; SupplementsHerbal ExtractsAromatherapyHomeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://www.merchantcircle.com/business/The.Herb.Shop.5414793602",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "superpages": {
      "description": "Submitted and Published",
      "lastupdate": 1380903483,
      "listingUrl": "http://www.superpages.com/bp/Grants-Pass-OR/The-Herb-Shop-L0138756220.htm",
      "log": {
        "1380903483": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "SuperPages",
      "listing": {
        "city": "Grants Pass",
        "country": "USA",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "sat": {
            "closingTime": "1700",
            "open": "true",
            "openingTime": "0900"
          },
          "thu": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": "true",
            "openingTime": "0900"
          }
        },
        "id": 1206357,
        "image_urls": [
          "http://media.superpages.com/media/photos/01/38/75/62/20/images/01387562201451.jpg",
          "http://media.superpages.com/media/photos/01/38/75/62/20/images/01387562205184.jpg",
          "http://media.superpages.com/media/photos/01/38/75/62/20/images/01387562205209.jpg",
          "http://media.superpages.com/media/photos/01/38/75/62/20/images/01387562205646.jpg"
        ],
        "keywords": [
          "Herbs Retail",
          "Herbs Wholesale",
          "Natural Healing Products &amp; Services",
          "Vitamins &amp; Food Supplements Retail"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:59",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas & Spices Highest Quality Vitamins & Supplements Herbal Extracts Aromatherapy Homeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "80310a11c42b05a47e564767c4343d2c59bae56f1c15f1efb6b63345b96e4577",
        "payment_methods": [
          "American Express",
          "Cash",
          "Debit Cards",
          "Discover",
          "Less",
          "MasterCard",
          "More",
          "Personal Checks",
          "VISA"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas & Spices Highest Quality Vitamins & Supplements Herbal Extracts Aromatherapy Homeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://www.superpages.com/bp/Grants-Pass-OR/The-Herb-Shop-L0138756220.htm",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "citysearch": {
      "description": "Submitted and Awaiting Publishing",
      "lastupdate": 1381440850,
      "log": {
        "1380903626": "In Progress",
        "1381440850": "Fulfillment Complete"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 30,
      "label": "Citysearch",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "sat": {
            "closingTime": "1700",
            "open": true,
            "openingTime": "0900"
          },
          "sun": {
            "closingTime": "",
            "open": false,
            "openingTime": ""
          },
          "thu": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          }
        },
        "id": 1206300,
        "image_urls": [
          "http://images1.citysearch.net/jawr/reinvent/img/cb3120600175/assets/reinvent/img/citysearch/blank.gif"
        ],
        "keywords": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:22",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "691b72aa06a849012ebe60d629583919d934161582e870f9a2c9838a5a81a7e9",
        "payment_methods": [],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "",
        "slogan": "Herbs, Teas & Spices, Vitamins and More.",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://national.citysearch.com/profile/8547746/grants_pass_or/the_herb_shop.html?impressionId=000b00000006d1adf7775c4cfa98322f55e56ca567",
        "video_urls": [],
        "website": "",
        "year_established": 0
      },
      "content": {
        "description": false,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "hotfrog": {
      "description": "Submitted and Published",
      "duplicateUrl": "http://www.hotfrog.com/Companies/The-Herb-Shop_6535926",
      "lastupdate": 1380901157,
      "listingUrl": "http://www.hotfrog.com/Companies/The-Herb-Shop_30865778",
      "log": {
        "1380901157": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Hotfrog",
      "listing": {
        "city": "",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [
          "LML\\DirectoryBot\\Bots\\Hotfrog_Bot: Could not get Business Information: Found ForeignKey from search but probability too low. Expected >= 60%. [51.425 %][http://www.hotfrog.com/Companies/The-Herb-Shop_6535926]"
        ],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": [],
        "id": 1206518,
        "image_urls": [],
        "keywords": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:26:30",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "",
        "logo_url": "",
        "long_description": "",
        "name": "",
        "number_of_employees": 0,
        "object_hash": "89f24b06dfda4e7b71ec933ad591fc79c6b766fcdad2a81ca64ebe186d6d4412",
        "payment_methods": [],
        "postal_code": "",
        "products_offered": [],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "",
        "status": "NOK",
        "street": "",
        "toll_free_phone": "",
        "video_urls": [],
        "website": "",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "yellowbook": {
      "description": "Claimed Listing",
      "lastupdate": 1380903534,
      "listingUrl": "http://beta.yellowbook.com/profile/herb-shop-the_1848123204.html",
      "log": {
        "1380903534": "Listing Claimed/Published"
      },
      "notes": [
        "Update Recommended"
      ],
      "percentComplete": 100,
      "status": 40,
      "label": "Yellowbook",
      "listing": {
        "city": "",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [
          "LML\\DirectoryBot\\Bots\\YellowBook_Bot: Could not get Business Information: Could not find ForeignKey from search. Could not get HTML from http://www.yellowbook.com/yellow-pages?what=herb+shop&where=97526"
        ],
        "fax": "",
        "foreign_key": "",
        "id": 1206334,
        "image_urls": [],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:49",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "",
        "logo_url": "",
        "long_description": "",
        "name": "",
        "number_of_employees": 0,
        "object_hash": "5a051eaf7767f8870e0ee9006a3d262332819fc29a4ea07c5dc07c999db96d31",
        "postal_code": "",
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "",
        "status": "NOK",
        "street": "",
        "toll_free_phone": "",
        "video_urls": [],
        "website": "",
        "year_established": 0
      },
      "content": {
        "description": false,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "insiderpages": {
      "description": "Submitted and Published",
      "lastupdate": 1380901679,
      "listingUrl": "http://www.insiderpages.com/b/3720320499/herb-shop-grants-pass",
      "log": {
        "1380901679": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "InsiderPages",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "other": {
            "freetext": "Monday: 09:00 AM - 06:00 PM,Tuesday: 09:00 AM - 06:00 PM,Wednesday: 09:00 AM - 06:00 PM,Thursday: 09:00 AM - 06:00 PM,Friday: 09:00 AM - 06:00 PM,Saturday: 09:00 AM - 05:00 PM,Sunday: Closed"
          }
        },
        "id": 1206354,
        "image_urls": [],
        "keywords": [
          "Food Stores",
          "Health Food Stores",
          "Herbs, nutrients, vitamins, bulk herbs, supplements, herbal formulas, organic herbs, teas, spices, herbal extracts, aromatherapy, homeopathy"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:57",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "Herbs, Teas & Spices, Vitamins and More.\nThe Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible.     We specialize in:    Bulk Organic Herbs  Teas & Spices  Highest Quality Vitamins & Supplements  Herbal Extracts  Aromatherapy  Homeopathy",
        "name": "Herb Shop",
        "number_of_employees": 0,
        "object_hash": "42f12302245562342584b9a37b39dabbdaa71c86aa6e2817afb385b0516bdd9b",
        "payment_methods": [],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "Herbs, Teas & Spices, Vitamins and More.\nThe Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible.     We specialize in:    Bulk Organic Herbs  Teas & Spices  Highest Quality Vitamins & Supplements  Herbal Extracts  Aromatherapy  Homeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247  SW G St",
        "toll_free_phone": "",
        "url": "http://www.insiderpages.com/b/3720320499/herb-shop-grants-pass",
        "video_urls": [],
        "website": "https://bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "kudzu": {
      "description": "Submitted and Published",
      "lastupdate": 1380901469,
      "listingUrl": "http://www.kudzu.com/m/The-Herb-Shop-12668001",
      "log": {
        "1380901469": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "Kudzu",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "sat": {
            "closingTime": "1700",
            "open": true,
            "openingTime": "0900"
          },
          "sun": {
            "open": false
          },
          "thu": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          }
        },
        "id": 1206304,
        "keywords": [
          "Food & Entertainment",
          "Health Food & Supplements"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:24:23",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": true,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "http://www.kudzu.com/uploadImages/11000000/11979778/logo.jpg",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. \r\n\r\nWe specialize in:\r\n\r\nBulk Organic Herbs\r\nTeas & Spices\r\nHighest Quality Vitamins & Supplements\r\nHerbal Extracts\r\nAromatherapy\r\nHomeopathy",
        "name": "The Herb Shop",
        "number_of_employees": 0,
        "object_hash": "9aa86bf4106cf7c1a6184c04dabceb25b03021324edb6029bd2566c088f33d31",
        "payment_methods": [
          "American Express",
          "Debit Card",
          "Discover",
          "Mastercard",
          "Personal Checks",
          "Visa"
        ],
        "postal_code": "97526",
        "products_offered": [],
        "short_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. \r\n\r\nWe specialize in:\r\n\r\nBulk Organic Herbs\r\nTeas & Spices\r\nHighest Quality Vitamins & Supplements\r\nHerbal Extracts\r\nAromatherapy\r\nHomeopathy",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 SW G St",
        "toll_free_phone": "",
        "url": "http://www.kudzu.com/m/The-Herb-Shop-12668001",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": true,
        "logoUrl": true,
        "videoUrl": false,
        "website": true
      }
    },
    "mojopages": {
      "description": "Submitted and Published",
      "lastupdate": 1380902520,
      "listingUrl": "http://www.mojopages.com/biz/grants-pass-or-the-herb-shop-15372932",
      "log": {
        "1380902520": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20,
      "label": "MojoPages",
      "listing": {
        "city": "Grants Pass",
        "country": "",
        "country_iso_code": "",
        "email": "",
        "errors": [],
        "fax": "",
        "foreign_key": "",
        "hours_of_operation": {
          "fri": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "mon": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "sat": {
            "closingTime": "1700",
            "open": true,
            "openingTime": "0900"
          },
          "sun": {
            "closingTime": "",
            "open": false,
            "openingTime": ""
          },
          "thu": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "tue": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          },
          "wed": {
            "closingTime": "1800",
            "open": true,
            "openingTime": "0900"
          }
        },
        "id": 1206388,
        "image_urls": [],
        "keywords": [
          "Alternative Medicine",
          "Aromatherapy",
          "Bulk Herbs",
          "Health &amp; Diet Food Products Retail",
          "Herbal Extracts",
          "Herbs",
          "Herbs",
          "Homeopathy",
          "Spices",
          "Supplements",
          "Teas",
          "Vitamins",
          "herbal formulas",
          "nutrients",
          "organic herbs"
        ],
        "languages_spoken": [],
        "last_errors": [],
        "last_updated": {
          "date": "2014-01-10 18:25:10",
          "timezone": "GMT",
          "timezone_type": 3
        },
        "listing_claimed": false,
        "listing_verified": false,
        "local_phone": "5414793602",
        "logo_url": "",
        "long_description": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients. Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. We specialize in: Bulk Organic Herbs Teas & Spices Highest Quality Vitamins & Supplements Herbal Extracts Aromatherapy Homeopathy",
        "name": "Herb Shop",
        "number_of_employees": 0,
        "object_hash": "83d7d67edf10a240c43525ae744fe59c8ffd5b5828460ea57300aac696e50679",
        "payment_methods": [
          "American Express",
          "Cash",
          "Check",
          "Debit",
          "Discover",
          "Master Card",
          "Visa"
        ],
        "postal_code": "97526",
        "products_offered": [
          "Aromatherapy",
          "Books",
          "Books",
          "Bulk Foods",
          "Flower Essences",
          "Herbal Supplements",
          "Herbs",
          "Homeopathic Remedies",
          "Nature&#039;s Life",
          "Order by Mail"
        ],
        "short_description": "",
        "slogan": "",
        "square_logo_url": "",
        "state": "OR",
        "status": "OK",
        "street": "247 Sw G St",
        "toll_free_phone": "",
        "url": "http://www.mojopages.com/biz/grants-pass-or-herb-shop-15372932?sl=35520359&so=0",
        "video_urls": [],
        "website": "http://www.bulkherbshop.com",
        "year_established": 0
      },
      "content": {
        "description": true,
        "hoursOfOperation": true,
        "imageUrl": false,
        "logoUrl": false,
        "videoUrl": false,
        "website": true
      }
    },
    "expressupdate": {
      "description": "Submitted and Published",
      "lastupdate": 1381441031,
      "listingUrl": "http://www.expressupdate.com/places/9808414c635311e29d52411a5089b2ab",
      "log": {
        "1380900688": "In Progress",
        "1381441031": "Listing Claimed/Published"
      },
      "notes": [
        ""
      ],
      "percentComplete": 100,
      "status": 20
    }
  },
  "business": {
    "city": "Grants Pass",
    "coordinates": {
      "latitude": 42.4395496,
      "longitude": -123.3295961
    },
    "countryCode": "US",
    "name": "Herb Shop, The",
    "phone": "5414793602",
    "postalCode": "97526",
    "state": "OR",
    "street": "247 SW G St",
    "website": {
      "url": "http://www.bulkherbshop.com/"
    },
    "descriptionLong": "The Herb Shop, located in Grants Pass Oregon, has a large selection of high quality herbs and nutrients.   Many people seeking alternative medicine and lifestyles have enjoyed the store. Our main goal is to provide the largest selection of high quality herbs and nutrients and formulas (like Essiac) that are available on the market today. Most of our herbs are purchased from local growers in the Rogue Valley, providing organic or wild crafted herbs whenever possible. \n\nWe specialize in:\n\nBulk Organic Herbs\nTeas & Spices\nHighest Quality Vitamins & Supplements\nHerbal Extracts\nAromatherapy\nHomeopathy",
    "descriptionMedium": null,
    "descriptionShort": null,
    "hoursOfOperation": "MF09001800HSS09001700H",
    "imageUrl": {
      "1": "http://clientimages.localmarketlaunch.com/4be9527dd153c6938dd16d427c1a465e/524e05eec8c1c_1.jpg"
    },
    "keywords": null,
    "languagesSpoken": "",
    "logoSquareUrl": null,
    "logoUrl": null,
    "numberEmployees": null,
    "paymentMethods": [
      "amex",
      "cash",
      "check",
      "debit",
      "discover",
      "mastercard",
      "visa"
    ],
    "phoneTracking": [
      ""
    ],
    "productsOffered": null,
    "slogan": "Herbs, Teas & Spices, Vitamins and More.",
    "videoUrl": null,
    "yearEstablished": null
  },
  "externalId": "f~29gcn1gv",
  "uuid": "f2c8f956-f886-5c3d-b874-c616a28f870b",
  "contact": {
    "email": "nmason@bulkherbshop.com",
    "firstName": "Nicholas",
    "lastName": "Mason",
    "phone": "541 479 3602"
  },
  "received": 1380845042,
  "updated": 1385512383
}
```
