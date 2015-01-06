---
path: '/white-labeling-email'
title: 'White Labeling Email'

layout: nil
---

# White Labeling Email.

There are currently 3 methods you can choose to setup email.

### Partially WhiteLabeled Option

* Sub Domain (Easiest) - ex: support@example.verifymylistings.com

### Fully WhiteLabeled Options

* Direct SMTP Access
* SPF

## How to configure Sub domain method 
This is the easiest method, simply choose a sub-domain tied to your business ex: "harrys" and all your emails will come from "harrys.verifymylistings.com".


## How to configure Direct SMTP method

Provide us with

* smtp domain
* port
* username
* password


## How configure SPF method

This is a 4 step process.

### Step 1
 
You need to provide us with a unique sub-domain ( one you are not using anywhere else), all emails we send will originate from this domain.

    Ex:
        If your site was www.abc.com, perhaps you chose "em.abc.com" for your unique email sub-domain. 
     
### Step 2

Provide us with the sub domain, and we will configure it on our end. 
We will then provide you with YourWhiteLabelIP ex: 192.168.1.1. address of server that we will use to send email from only for you.

* In the example below you would use "192.168.1.1" where you see the words "YourWhiteLabelIP"

### Step 3
    
| Record Type | Host | Data| 
|:-------:|:--------------|:--------|
|A|YourWhiteLabelIP|em.abc.com|
|CNAME|em.abc.com|sendgrid.net|
|TXT|v=spf1 include:sendgrid.net ~all|abc.com|
|TXT|smtpapi._domainkey.em.abc.com|k=rsa; t=s; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDPtW5iwpXVPiH5FzJ7Nrl8USzuY9zqqzjE0D1r04xDN6qwziDnmgcFNNfMewVKN2D1O+2J9N14hRprzByFwfQW76yojh54Xu3uSbQ3JP0A7k8o8GutRF8zbFUA8n0ZH2y0cIEjMliXY4W4LwPA7m4q0ObmvSjhd63O9d8z1XkUBwIDAQAB|
|TXT|smtpapi._domainkey.abc.com|k=rsa; t=s; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDPtW5iwpXVPiH5FzJ7Nrl8USzuY9zqqzjE0D1r04xDN6qwziDnmgcFNNfMewVKN2D1O+2J9N14hRprzByFwfQW76yojh54Xu3uSbQ3JP0A7k8o8GutRF8zbFUA8n0ZH2y0cIEjMliXY4W4LwPA7m4q0ObmvSjhd63O9d8z1XkUBwIDAQAB|

### Step 4

You are done!
Just let us know when you are done, and we will confirm the rest on our end.