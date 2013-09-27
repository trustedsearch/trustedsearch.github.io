---
path: '/getting-started'
title: 'Getting Started'

layout: nil
---

# Getting Started.


### Sandbox & Production Environments

There are two endpoints / environments.

- __Production__:   https://api.trustedsearch.org
- __Sandbox__: http://api.sandbox.trustedsearch.org

You can use the above endpoints in place of the [api_endpoint] references you will see throughout the api docs.
### Credentials

There are separate credentials for each environment.

At the time of your account creation, you will be provided initially with sandbox credentials to conduct integration and testing. Once you believe you are ready for the production environment, please contact support@trustedsearch.org for production credentials.

To authenticate your requests we use an [hmac authenticaion protocol]({% post_url 2012-12-28-authentication %}). 
You will be provided with a public & private key for each environment.

