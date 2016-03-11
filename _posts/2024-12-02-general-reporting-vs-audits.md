---
category: reference
path: '/general-reporting-vs-audits'
title: 'Location Audits'

layout: nil
---


## Audits:
* An audit is a best guess attempt to find the listing on a publisher.
* An audit does not require a unique identifier, only basic NAPW and its data is considered temporary.
* An audit is a one time process. It does not recur on a given interval.
* An audit is not based upon known listing urls, its an attempt to identify the listing url via the data * provided by the partner to extract data from the page identified.

There are two components to an audit:

* Listing identification
	* To identify a listing we employ many tactics:
	* Api's
	* Page crawling
	* Filtering of the original content (NAPW)) to find the best match.
* Listing data extraction from detected page.
	* Once we identify the listing that has a match rate that is acceptable we then extract the listing data.

An audit's identification and extraction accuracy varies based upon many factors: 

* Location info provided to TRUSTEDSearch vs data publisher has
* Publisher search options:
	* Available publisher api 
	* Publisher website search
* Changes to publisher websites

## Reporting:

* Reporting is based upon a known listing url that is verified during the fulfillment process.
* This verification process makes the identification and data accuracy very high.
* A report requires that the partner provides a unique external_id to refer back to  this location on their end.
* A report happens on a standard frequency which changes based upon publisher variables:
	publication times rate of website updates
* A higher frequency can be set. (Requires Reporting product and additional costs)

## Hooks
Refer to [Subscribing to Hooks](#{% post_url 2011-01-28-v2-hooks-about %}) to learn how you can recieve this data.