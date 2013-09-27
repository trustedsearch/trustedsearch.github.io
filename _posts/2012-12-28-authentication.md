---
path: '/login'
title: 'Authenticate'

layout: nil
---

## Request Signing
The API uses HMAC hashing with a public/private key pair to sign all requests.

To sign each request, you will need the following:

-	public_key - assigned during account creation.
-	private_key - assigned during account creation.
-	request_uri - Request URI. This does not include the hostname or query string. (e.g. "/v1/local-business")
-	timestamp - Current epoch timestamp.
-	content_md5 - Content MD5 hash of the request body. For POST and PUT requests, this will be the value as specified in RFC 1864 (the base64-encoded binary MD5 hash of the content). For GET requests, this will generally be an empty string.

In the programming language of your choice, concatenate the request URI, Content MD5, and timestamp with no delimiters. Use an HMAC hashing method with the SHA1 algorithm to calculate the (binary) hashed value of the concatenated string, using the private key. After base64-encoding the result, you have a valid signature for the request.


*php example*
```$privateKey = "12345privatekey67890";
$stringToSign = $request_uri . $content_md5 . $timestamp;
$signature = base64_encode( hash_hmac( 'sha1', $stringToSign, $privateKey, true ) ); //wnl1AVcJAwHoCm7FK9l13ZuMx8g=
```

#### Sample Post Data

-	Public key: 1234567890abcdeffedcba0987654321
-	Private key: 12345privatekey67890
-	Request URI: /v1/local-business/47139840-870c-11e2-9e96-0800200c9a66
-	Epoch timestamp: 1362648813
-	Content MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

__POST body__

```{
    business: {
        name: "Joe's Plumbing",
        street: "123 Main St",
        city: "Los Angeles",
        state: "CA",
        postalCode: "90008",
        phoneLocal: "2135559876"
    }
}
```

#### Request Params
Once the signature is generated, simply append it to the query string of the request, along with the public key and timestamp from above:

```
https://[api_endpoint]/v1/local-business?apikey=1234567890abcdeffedcba0987654321&signature=wnl1AVcJAwHoCm7FK9l13ZuMx8g=&timestamp=1362648813
```

For errors responses, see the [response status codes documentation](#{% post_url 2012-12-28-response-status-codes %}).
