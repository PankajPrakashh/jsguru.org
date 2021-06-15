---
title: "Working with Date and Time in JavaScript"
date: 2021-06-08T20:50:50+05:30
draft: true

weight: 1
author: Pankaj Prakash
authorLink: https://jsguru.org
description: "JavaScript Date is an object containing integer that represent time elapsed in milliseconds since 1 January 1970 UTC midnight. It’s implementation is inspired from the early implementations of java.util.Date class. In this article we will learn to different ways to create date instance, min/max representable date, bugs in existing Date API"
images: []

tags: ["JavaScript", "Date"]
categories: ["JavaScript"]
keywords: ["JavaScript", "Date", "Bug", "minimum and maximum date range"]
featuredImage: "/images/javascript/working-with-date-time/feature.png"

lightgallery: true
---

Working with dates in JavaScript is a common requirement for most of the projects. In this article we will learn about the JavaScript Date API. We will learn to get current datetime and work with its instance.


<!-- more -->

## Date API
JavaScript `Date` is an object containing integer that represent time elapsed in milliseconds since **1 January 1970 UTC** midnight. It's implementation is inspired from the early implementations of `java.util.Date` [class](https://docs.oracle.com/javase/7/docs/api/java/util/Date.html).


There are several ways to get instance of Date. Lets run through each of them.

## The `new Date()` constructor
The JavaScript `Date` constructor accepts up to seven parameters (all optional), that lets you configure the instance.

### No parameter
Invoking the `Date` constructor with no parameter returns a new `Date` object which specify the current datetime.
```js
// Assigns an instance of current date to date variable
let date = new Date();

// Print current datetime to console
console.log(date);
```

### Single string parameter
You can pass a single [ISO date string](https://en.wikipedia.org/wiki/ISO_8601) to `Date` constructor. The Date API then tries to parse the ISO date string as a date instance. This is mostly similar to `Date.parse()` static method.

```ts
// Wed Jun 09 2021 21:02:43 GMT+0530 (India Standard Time)
new Date("2021-06-09T15:32:43.070Z");
```

> **Warning:**
> Parsing date string is not advisable, it may result in discrepancy among browsers. Never use in production environments.

### Single numeric parameter
When passed a single number to the `Date` constructor, the value is treated as milliseconds elapsed since **1 January 1970 UTC** midnight. It must be noted that, you can represent up to ±8,640,000,000,000,000 milliseconds. Hence it defines the min/max possible date you can represent in JavaScript.

```ts
new Date(8640000000000000);  // Sat, 13 Sep 275760 00:00:00 GMT
new Date(-8640000000000000); // Tue, 20 Apr -271821 00:00:00 GMT
```

**Note:** For a beginner it might be confusing to represent a negative year. But it's fine for specific use case, which I will explain in different post.

### Two or more numeric parameter
You can create a new `Date` instance by specifying exact `year`, `month`, `date`, `hours`, `minutes`, `seconds` and `milliseconds` to the constructor.

The general syntax is: `new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds)` where `year` and `monthIndex` is required, rest all params are optional (default value is 0).
`monthIndex` is a 0 based month number index (0-11).

```ts
new Date(2021, 5);                  // 2021-05-31T18:30:00.000Z
new Date(2021, 5, 9);               // 2021-06-08T18:30:00.000Z
new Date(2021, 5, 9, 21);           // 2021-06-09T15:30:00.000Z
new Date(2021, 5, 9, 21, 2);        // 2021-06-09T15:32:00.000Z
new Date(2021, 5, 9, 21, 2, 43);    // 2021-06-09T15:32:43.000Z
new Date(2021, 5, 9, 21, 2, 43, 7); // 2021-06-09T15:32:43.007Z
```

{{< admonition type=warning open=true >}}
You must be careful while passing the year param. If passed between 0-99, it considers `1900 + year` as the year. Otherwise if year is greater than 100 then it considers the actual year passed as the year.

Hence, `new Date(10, 1)` represents `1910-01-31T18:30:00.000Z` whereas `new Date(100, 1)` represent `0100-01-31T18:06:32.000Z`.
{{< /admonition >}}

## The `Date()` function
Invoking `Date()` as function returns string representation of current time (UTC). It is eventually same as calling `toString()` method on a date instance.
```js
// Initializes dateString with the string representation of current date
let dateString = Date();

// You can convert back the date string to date instance
let dateStringObj = new Date(dateString);

// Both the output will be same
console.log(dateString);
console.log(dateStringObj.toString());
```

## `Date.now()`
Returns a number representing time elapsed in milliseconds since **1 January 1970 00:00:00 UTC**. Invoking this is equivalent to `new Date().getTime()`.

```ts
Date.now();
```

## `Date.UTC()`
Same as the `new Date(year, monthIndex, hours, minutes, seconds, milliseconds)` constructor, but returns a number representing time in milliseconds instead of `Date` instance.

```ts
Date.UTC(2021, 5, 9, 21, 2, 43, 7); // 1623272563007
```

## `Date.parse()`
Same as `new Date(dateString)` constructor, but returns a number representing time in milliseconds instead of `Date` instance.

```ts
Date.parse('2021-06-09T15:32:43.070Z'); // 1623252763070
```

{{< admonition type=warning open=true >}}
As mentioned earlier parsing string representation of dates should be avoided, due to browser inconsistencies.
{{< /admonition >}}

## Min and Max possible date
JavaScript can represent approximately total of 273,790 years forward or backward from **1 January 1970 00:00:00 UTC**. Going forward represents [A.D.](https://en.wikipedia.org/wiki/Anno_Domini) similarly going backward represents B.C.

The valid date ranges that can be represented in JavaScript is `Tue, 20 Apr -271821 00:00:00 GMT` to `Sat, 13 Sep 275760 00:00:00 GMT`.

## Problems with Date API
As mentioned the JavaScript Date API reflects the early implementation of `java.util.Date` class from Java. The `java.util.Date` itself was having several issues. The Java team has to rewrite a complete new API deprecating most of the existing `java.util.Date` API which was released in the Java 1.1 version.

However we are still living with the same old API, that must be replaced with a new robust Date API **without breaking the web**. Good news is TC39 is already working on a brand new [Temporal Date API](https://tc39.es/proposal-temporal/docs/index.html). But its a long way and not yet available for use.


> **References**
> - [MDN Web Docs](https://developer.mozilla.org/en-US/docs/web/javascript/reference/global_objects/date)
> - [ECMAScript](https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-date-constructor)
> - [Fixing JavaScript Date](https://maggiepint.com/2017/04/09/fixing-javascript-date-getting-started/)