---
layout: post
title: The JavaScript Date Constructor
---

I came across a little gotcha with the Date constructor recently. The `new Date()` [constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) takes a unix timestamp or a dateString, which according to mozilla should allow a [version of ISO8601](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15).

## Here's the issue

If my timezone is Easter Standard Time (US east coast) and I create a new date without a time zone.

Something like:

```
new Date('2019-01-29');
```

My browser actually assumes the date is in UTC timezone and returns.

```
Mon Jan 28 2019 19:00:00 GMT-0500 (Eastern Standard Time)
```

## Possible Solutions

Appending a time to the date string will force the browser to parse it the local time zone of the browser.

```
new Date('2019-01-29' + 'T00:00:00');
```

or if you are using [moment js](https://momentjs.com/), you can pass your date string directly to moment.

```
moment('2019-01-29')
```

Both solutions correctly return

```
Tue Jan 29 2019 00:00:00 GMT-0500 (Eastern Standard Time)
```
