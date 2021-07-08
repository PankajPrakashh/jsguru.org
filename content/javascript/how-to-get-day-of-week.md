---
title: "How to Get Day of Week in JavaScript?"
date: 2021-07-06T16:35:10+05:30
lastmod: 2021-07-06T16:35:10+05:30
draft: false


weight: 1
author: JsGuru
authorLink: https://jsguru.org
description: "While learning JavaScript you might have stumbled across how to get name of the week day e.g. \"Sunday\" \"Monday\" etc from date. In this article we will learn to get the day name of the week in short and long format."
images: ["/images/javascript/feature.jpg"]

tags: ["JavaScript", "Snippets", "Date", "Intl"]
categories: ["JavaScript"]
featuredImage: "/images/javascript/feature.jpg"

lightgallery: true
---

While learning JavaScript you might have stumbled across how to get name of the week day e.g. "Sunday" "Monday" etc from a date. In this article we will learn to get the day name of the week in short and long format.

<!--more-->

## Date API 💻
[JavaScript date api](/javascript/working-with-date-time) provides `getDay()` method to get the week day index of a date instance. It returns a zero based integer from `0-6` specifying the day of week for the given date. 

- `0` means Sunday
- `1` means Monday and so on.

```js
let date = new Date("2021-07-06T11:24:49.891Z");
console.log(date.getDay());  // 2
```

The above code returns integer between 0-6 but we are interested in textual representation of day name e.g. `Monday` or `Mon`.

## The traditional way 🧓
We know `getDay()` returns integer between 0-6 where 0 means `Sunday`. Hence we can define an array of week day names and make use of index returned by `getDay()`.

```js
const DAY_NAME_OF_WEEK_SHORT = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
const DAY_NAME_OF_WEEK_LONG = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

let date = new Date("2021-07-06T11:24:49.891Z");

console.log(DAY_NAME_OF_WEEK_LONG[date.getDay()]);    // Tuesday
console.log(DAY_NAME_OF_WEEK_SHORT[date.getDay()]);   // Tue
```

The above code works undoubtedly, however the new `Intl` API provides a better solution. 

## The modern way 😎
`Intl.DateTimeFormat` provides a robust way to format date and times in different locales. The constructor accepts two optional params `Intl.DateTimeFormat(locale, options)`. The second param `options` accepts a variety of fields out of which we are interested in `weekday`. You can pass one out of three (`long`, `short`, `narrow`) values to `weekday`.

* `{ weekday: "long" }` Full textual representation of week day e.g. `Sunday` `Monday` etc.
* `{ weekday: "short" }` Short textual representation of week day e.g. `Sun` `Mon` etc.
* `{ weekday: "narrow" }` Initials of week day e.g. `S` `M` etc. **Note:** Use it with caution it may result in same result for week days with same initials e.g. Sunday and Saturday for both it represents `S`.


```js
let date = new Date("2021-07-06T11:24:49.891Z");

// Tuesday
console.log(new Intl.DateTimeFormat("en-us", { weekday: "long" }).format(date));

// Tue
console.log(new Intl.DateTimeFormat("en-us", { weekday: "short" }).format(date));

// T
console.log(new Intl.DateTimeFormat("en-us", { weekday: "narrow" }).format(date));
```

## Weekday in different locale 🌐
The `Intl.DateTimeFormat` simplifies the job a lot. You can use the API to get week day name in different locales (hindi, tamil etc.) too. Pass the desired locale in which you want week day name to the `Intl.DateTimeFormat()` constructor.

```js
let date = new Date("2021-07-06T11:24:49.891Z");

// मंगलवार
console.log(new Intl.DateTimeFormat("hi-in", { weekday: "long" }).format(date));

// मंगल
console.log(new Intl.DateTimeFormat("hi-in", { weekday: "short" }).format(date));

// మంగళవారం
console.log(new Intl.DateTimeFormat("te-in", { weekday: "long" }).format(date));

// మంగళ
console.log(new Intl.DateTimeFormat("te-in", { weekday: "short" }).format(date));
```

> **References**
> - [MDN Web Docs DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat)
> - [ECMAScript](https://tc39.es/ecma402/#sec-intl-datetimeformat-constructor)
> - [Check browser compatibility](https://caniuse.com/?search=intl)

&nbsp;  
&nbsp;  
Happy Coding :man_technologist: