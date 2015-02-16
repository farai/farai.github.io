---
layout: post
title: "Javascript NaN for new Date object in IE &amp; Safari"
date: 2015-02-16 12:44:42 +0000
comments: true
categories: 
---

Recently I came across an issue during some cross browser testing of a change I had made which highlighted an interesting issue. It appeared Internet Explorer and Safari seem to handle date strings differently when instantiating new date objects using javascript's ``` new Date() ```.

The date string I was trying to use to instantiate a new date object looked like the following:

``` 
'2015-02-16T12:44:42+0000' 

```

The above format is the basic ISO 8601 notation which includes the timezone offset via the value shown after "+". 

To the best of my knowledge this format is the most widely used across the web but when trying trying to instaniate a new date object like so:

```javascript 
	var dateTime = new Date('2015-02-16T12:44:42+0000');

```

This resulted in the NaN message being rendered everywhere I was trying to show a date in IE and Safari but other browsers seemed to handle the string accordingly without any issue.

Following closer inspection of my input datetime string and a few minutes of playing around with my trusty browser console and javascript's ``` Date() ```, it turns out the IE and Safari will only accept the the extended date time notation which looks like so:

``` 
'2015-02-16T12:44:42+00:00'
```

The difference between the extended notation and the basic notation I had been trying to use was just the inclusion of the colon in the timezone offset value. This left me intrigued as to whether the other browsers which had been working fine with the basic notation would be able to handle the creation of date objects with input strings in extended notation and turns out they could.

Having found out that using the extended notation is always going to be the safer option for cross browser compatibility, I found the solution below to do the trick:

```javascript
	var dateTimeString = '2015-02-16T12:44:42+0000';

	//add colon to timezone offet
	dateTime = dateTimeString.replace(/([+\-]\d\d)(\d\d)$/, "$1:$2");

```

Should you come across the same issue, hopefully you find this useful.







