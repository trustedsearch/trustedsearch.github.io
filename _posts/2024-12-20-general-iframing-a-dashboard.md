---
category: Whitelabel
path: '/iframing-a-dashboard'
title: 'Iframing a Dashboard'
layout: nil
---

# IFRAMEing a Dashboard

### Steps

* Get an [auth token](#{% post_url 2012-12-27-v1-token-get %}) for the user whom you want to load a dashboard for. 
* Add an iframe in your website with the iframe url

Lets say your token that you get is : abcdef12345

The iframe url is:
[https://local.report/#?token=abcdef12345](https://local.report/#?token=abcdef12345)

So just add this into your html:

```
<iframe src="https://local.report/#?token=abcdef12345"></iframe>
```

By doing this, you will auto login your user to their dashboard where they can see the location(s) associated to them.
