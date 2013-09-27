---
category: V1
path: '/v1/user'
title: 'Creating a User'
type: 'PUT'

layout: nil
---

## Primary User for a Partner Account

Upon creation of a partner account, a user is automatically created as the default/primary for that partner. This user has an associated public and private key for API interactions, as well as a username and password for UI-based authentication. All operations initiated by the partner to LML (including the creation of additional users) should use these credentials.


### Username and Password Requirements

### Username requirements

- are case-insensitive
- must be between 3 and 30 characters in length
- may contain any letter or numeric digit (a-z, 0-9)

### Password requirements

- are case-sensitive
- must be between 8 and 15 characters in length
- must contain at least one character from two of the following groups of characters
- lower case letters (a-z)
- upper case letters (A-Z)
- numbers (0-9)
- symbols
- spaces are not allowed

### Request

Requests should be made with the PUT method to https://api_endpoint/v1/user/username?pwd=password, where username is the username of the user to create, and "password" is the SHA1 hash of the raw password. All requests must be 
[authenticated](#{% post_url 2012-12-28-authentication %}) using the primary partner user's keys.

To create a user with username "lmluser09" and password "password123", the following PUT request should be made:

https://api.trustedsearch.org/v1/user/lmluser09?pwd=cbfdac6008f9cab4083784cbd1874f76618d2a97&apikey=1234567890abcdeffedcba0987654321&timestamp=1362648813&signature=wnl1AVcJAwHoCm7FK9l13ZuMx8g=

### Response

Sends back a collection of things.

```Status: 200 OK```
```{
"user_name": "lmluser09",
"public_key": "3ae061c0ce1683ad766184c7c52c7805",
"private_key": "9Ho2spIEW1Ou6lajOap4Oaci",
"settings": ""
}```

<!---
For errors responses, see the [response status codes documentation](#{% post_url 2012-12-28-response-status-codes %}).
-->