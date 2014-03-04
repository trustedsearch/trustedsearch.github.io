---
category: v2
path: '/v2/about-hooks'
title: 'Hooks: About'
type: ''
layout: nil
---

# Hooks
Rather than needing to poll our system for changes to your locations or products, you can be notified about events that happen in our system by subscribing to hooks.

You might then use these notifications on your end to do things like:

## WHY - You might want to use hooks.

* Update your system.
* Notify your customers about status updates.
* Notify you customers about actions they need to perform.
* Notify members of your company about actions they need to perform.

## WHAT - Hooks are available
### location.audit
A notification sent when an audit has completed.

##### Usage

* Subscribe to ```location.audit``` hook
* Submit an order for a location via the / POST v1/local-business API:
	* The package you specify must include the audit product.(Talk w/ your sales rep for this.)
	* The __audit__ flag must be set to true.
* After our system finishes the audit, a hook will be triggered and you will be notified at the resource you defined in your subscription.

##### Notes
* This is the only notification you will receive, however you can queue up another audit for a given location(Limits and Throttling of requests may apply)
* If there is an error, either update your system or disregard it. Regardless of the reason for an error,  results can change on  a daily basis as we continually improve  our audit match algorithm and update our bots when a publisher makes a change the layout of their site.



### Upcoming Hooks

* location.updates
* location.fullfilment.update
* location.report


## HOW - to setup hooks
Integration is easy, lets say you want to know about changes that happen to a location.

#### Step 1 - Configure your servers
Setup a resource on your servers:
[https://api.acme.com/trustedsearch/location-updates]()
that could accept a JSON POST, in this case the JSON data will be the same as that of the GET v1/directory-listings api call.

#### Step 2 - Subscribe
Subscribe to the ```location.update``` hook via the API.

#### Step 3 - What happens now.
When ever any location data on our end changes, we queue up a process that will notify any subscribers associated with that location.
