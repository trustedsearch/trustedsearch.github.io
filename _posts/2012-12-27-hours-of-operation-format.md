---
path: '/hours-of-operation'
title: 'Hours of Operation'

layout: nil
---


# Standardized Hours Format
This is specified in blocks of 11 characters in form of DDHHMMHHMMT, where

- D = First day of week for this time period
- D = Last day of week for this time period
- HHMM = Opening time
- HHMM = Closing time
- T = Type of time period

## Multiple blocks can be specified. No separator should be used.

An example of a block is “MF09001700H”. This indicates that the hours of operation are Monday through Friday, from 9:00am to 5:00pm.

An example of multiple blocks is “MF10002000HSS10001800HNN12001700H”, which indicates the hours Monday-Friday 10 - 8, Saturday 10 - 6, Sunday 12 - 5.

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

The times use a 24-hour clock. For example, 5:00PM is 1700. If the business is open 24 hours, use 00000000. Alternatively, the following codes can be used instead of exact times:

- __ALLD__	All Day
- __DAYS__	Daytime
- __ERLY__	Early Morning
- __MORN__	Morning
- __AFTR__	Afternoon
- __EVNG__	Evening
- __LATE__	Late Evening
- __NITE__	Night
- __NONE__	Nothing Specified
- __WKLY__	Weekly
- __AFHR__	After Hours
- __SEAS__	Seasonal

An example of non-integer time periods would be “MFALLDALLDA”, which means that the business is open Monday-Friday all day by appointment.

Another would be “SNNONENONEH” which means that no hours are specified.

### T

The type of timeperiod should be specified as follows. The most common type is H:

- __H__	Hours Open
- __A__	Appointment
- __E__	Emergency
- __S__	Service
- __D__	Delivery
- __C__	Access
- __M__ 	Same Day Service/Delivery
- __N__	Next Day Service/Delivery
- __1__	1 Hour Service
- __L__	Closed
