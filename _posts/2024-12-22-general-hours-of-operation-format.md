---
category: reference
path: '/hours-of-operation'
title: 'Hours of Operation'

layout: nil
---

# Specifying Hours of Operation

Hours of operation should be passed in a standardized format, which consists of an 11-character block per period of open business hours. 

The format is DDHHMMHHMMT, where

- D = First day of week for this time period
- D = Last day of week for this time period
- HHMM = Opening time (24-hour notation)
- HHMM = Closing time (24-hour notation)
- T = Type of time period

## Stringing multiple blocks

An example of a block is MF09001700H, which indicates that the business is open Monday through Friday, from 9:00am to 5:00pm.

You can string multiple blocks together to indicate different hours for different days: MF10002000HSS10001800HNN12001700H, which indicates the hours Monday-Friday 10 - 8, Saturday 10 - 6, Sunday 12 - 5.

### D

The day of the week is specified as follows:

- __M__	Monday
- __T__	Tuesday
- __W__	Wednesday
- __R__	Thursday
- __F__	Friday
- __S__	Saturday
- __N__	Sunday

### HHMM

The times use a 24-hour clock. For example, 5:00PM is 1700. If the business is open 24 hours, use 00000000.

Another would be “MNNONENONEH” which means that no hours are specified.

### T

The type of timeperiod should be specified as follows. The most common type is H:

- __H__	Hours Open
- __A__	Appointment
- __E__	Emergency
- __S__	Service
- __D__	Delivery
- __C__	Access
- __M__ Same Day Service/Delivery
- __N__	Next Day Service/Delivery
- __1__	1 Hour Service
- __L__	Closed


## Multiple time blocks per day

While we will accept multiple time blocks per day (e.g. Open Monday through Friday from 8am to 12pm, closed from 12pm to 1pm, open from 1pm to 6pm), most publishers cannot accept split hours

The example above would be formatted as MF08001200HMF13001800H, however, we will omit the "closed" portion and publish Monday through Friday 8am to 6pm.

## Common Scenarios:

Open 24/7: MN00000000H

Open 8am to 5pm, Monday through Friday: MF08001700H
 
Hours not specified: MNNONENONEH
