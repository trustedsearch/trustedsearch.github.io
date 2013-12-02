---
category: v1
path: '/v1/test-fulfillment/:uuid'
title: 'Seeding Fulfillment Data'
type: 'POST'

layout: nil
---

## Overview

Once a /local-business call has been made to the sandbox environment, there is no manual process taking place (i.e. fulfillment) to test the /directory-listings call.

Making a PUT request to /v1/test-fulfillment/:uuid, where :uuid is the UUID provided in the response of the /local-business call, will seed fake fulfillment statuses so that subsequent calls will show altered data, mimicking the real fulfillment process.

You may make as many calls to this API as necessary to complete integration testing of the /directory-listings call.

## Inner Workings

This call works by simply selecting two products (publishers) at random and altering the fulfillment status and associated listing URL and other timestamp data at random. The logic is not necessarily representative of the actual flow of data (that is, it will not necessarily move a particular product from "Received" to "In Progress" to "Submitted and Awaiting Publishing" to "Submitted and Published"). The logic is purely random and only for the purposes of testing the integration of the /directory-listings API.
