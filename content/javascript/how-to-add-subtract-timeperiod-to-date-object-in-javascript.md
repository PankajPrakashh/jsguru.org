---
title: "How to Add/Subtract Time Period to Date Object in Javascript"
date: 2021-09-27T20:51:29+05:30
lastmod: 2021-10-06T20:51:29+05:30
draft: false

weight: 1
author: Pankaj Prakash
authorLink: https://jsguru.org
description: "Adding/Subtracting `n` amount of minutes, hours or days etc. to an existing date object is a common problem in programming. In this article we will learn how to add/subtract `n` amount of time period to a date instance."
images: ["/images/javascript/feature.jpg"]

tags: ["JavaScript", "Date", "Snippets"]
categories: ["JavaScript"]
featuredImage: "/images/javascript/feature.jpg"

lightgallery: true
---

Adding/Subtracting `n` amount of minutes, hours or days etc. to/from an existing date object is a common problem in programming. In this article we will learn how to add/subtract `n` amount of time period to a date instance.

<!--more-->

## Background📖
JavaScript `Date` API provides several methods, out of which we are interested in a few:

| Method | Description |
|--------|-------------|
| `setFullYear()` | Sets specified year for a date instance according to local time. **Note:** Don't get confused with `setYear()` method. |
| `setMonth()` | Sets specified month for a date instance |
| `setHours()` | Sets specified hours for a date instance |
| `setMinutes()` | Sets specified minutes for a date instance |
| `setSeconds()` | Sets specified seconds for a date instance |
| `setMilliseconds()` | Sets specified milliseconds for a date instance |

We can use above methods to add/subtract a given time period to/from a date instance. 

## Code💻
Let's us see how to add and subtract given time period in minutes to existing date instance.

```javascript
/**
 * Adds specified time period in minutes to the given `date` instance.
 * 
 * @param {Date} date Date instance to add minutes
 * @param {number} amount Number of minutes to add 
 */
function addMinutes(date, amount) {
  // Don't change the original date object
  const newDate = new Date(date);
  return newDate.setMinutes(newDate.getMinutes() + amount);
}

/**
 * Subtracts specified time period in minutes from given `date` instance.
 * 
 * @param {Date} date Date instance to subtract minutes
 * @param {number} amount Number of minutes to subtract 
 */
function subtractMinutes(date, amount) {
  // Don't change the original date object
  const newDate = new Date(date);
  return newDate.setMinutes(newDate.getMinutes() - amount);
}

// Test functionality
let start = new Date();
let startPlus90Min = new Date(addMinutes(start, 90));
let startMinus90Min = new Date(subtractMinutes(start, 90));

// Log test results
console.log('Start Date = ', start);
console.log('Start + 90 min = ', startPlus90Min);
console.log('Start - 90 min = ', startMinus90Min);
```

Similar way we can add time periods in other units too.
```javascript
/**
 * Adds specified time period in given `unit` to the specified `date` instance.
 * 
 * @param {Date} date Date instance to add 
 * @param {'milliseconds'|'seconds'|'minutes'|'hours'|'days'|'months'|'years'} unit Time period unit
 * @param {number} amount Amount to add 
 */
function addTimePeriod(date, unit, amount) {
  // Check for errors
  if (!(date instanceof Date) || typeof amount !== 'number') return date;

  // Create new instance of date, don't modify existing date
  const newDate = new Date(date);
  
  switch (unit) {
    case 'milliseconds': newDate.setMilliseconds(newDate.getMilliseconds() + amount); break;
    case 'seconds': newDate.setSeconds(newDate.getSeconds() + amount); break;
    case 'minutes': newDate.setMinutes(newDate.getMinutes() + amount); break;
    case 'hours': newDate.setHours(newDate.getHours() + amount); break;
    case 'days': newDate.setDate(newDate.getDate() + amount); break;
    case 'months': newDate.setMonth(newDate.getMonth() + amount); break;
    case 'years': newDate.setFullYear(newDate.getFullYear() + amount); break;
  }

  return newDate;
}

// Test functionality
let start = new Date();
console.log('Start Date = ', start);
console.log('Start Date + 50ms = ', addTimePeriod(start, 'milliseconds', 50));
console.log('Start Date + 50s = ', addTimePeriod(start, 'seconds', 50));
console.log('Start Date + 50m = ', addTimePeriod(start, 'minutes', 50));
console.log('Start Date + 5hr = ', addTimePeriod(start, 'hours', 5));
console.log('Start Date + 5 day = ', addTimePeriod(start, 'days', 5));
console.log('Start Date + 5 month = ', addTimePeriod(start, 'months', 5));
console.log('Start Date + 5 year = ', addTimePeriod(start, 'years', 5));
```

**Note:**
I have left the subtraction of dates as an exercise for you. I guess it shouldn't be difficult now to try.

> **References**
> - [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)

&nbsp;  
&nbsp;  
Happy Coding :man_technologist: