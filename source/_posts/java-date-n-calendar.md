---
title: Java <b>Date</b> and <b>Calendar</b>
date: 2017-08-10 13:11:28
tags: Java
---

## How to convert a LocalDateTime to Date

```java
Date date = Date.from(localDateTime.atOffset(ZoneOffset.UTC).toInstant());
```

## Parse a String to `Date`

1. Parse by `DateFormat - SimpleDateFormat`

	When we use `public Date parse(String source)`, if the begining of the parameter cannot be parsed, it will throw a `ParseException`, otherwise return a `Date`
	
	If we choose `public abstract Date parse(String source, ParsePosition pos)`, it will return null when the string cannot be parsed without throw Exception.
	

2. Pattern of formatter

<!-- more -->
	The default format pattern of SimpleDateFormat is **"M/d/yy h:mm a"**, while the default pattern of Date.toString() is **"EEE MMM dd HH:mm:ss zzz yyyy"**. To parse the Date correctly we need to construct the StringDateFormat with `SimpleDateFormat formatter = new SimpleDateFormat("EEE MMM dd HH:mm:ss zzz yyyy");`
	
## Parse a String to `LocalDateTime`

We can use static method `parse` in `LocalDateTime.parse` to parse the string
LocalDateTime localDateTime = LocalDateTime.parse(dateString); The input String format should be 


* uuuu-MM-dd'T'HH:mm
* uuuu-MM-dd'T'HH:mm:ss
* uuuu-MM-dd'T'HH:mm:ss.SSS
* uuuu-MM-dd'T'HH:mm:ss.SSSSSS
* uuuu-MM-dd'T'HH:mm:ss.SSSSSSSSS



