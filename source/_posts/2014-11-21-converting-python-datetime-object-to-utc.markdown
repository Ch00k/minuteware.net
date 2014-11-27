---
layout: post
title: "Converting Python datetime object to UTC"
date: 2014-11-21 09:17:56 +0200
comments: true
categories: discoveries
tags: python programming
---

While adding [support](https://github.com/flask-restful/flask-restful/pull/345) for ISO 8601 date/time strings to [Flask-RESTful](http://flask-restful.readthedocs.org) I was struggling with all that hated Python timezone stuff, specifically with the need to convert a datetime object to UTC timezone. With the libraries that Flask-RESTful was already using this solution looked the easiest:

```python
In [1]: from datetime import datetime

In [2]: from calendar import timegm

In [3]: import pytz

In [5]: dt_offset = datetime(2014, 11, 21, 10, 30, 45, tzinfo=pytz.timezone('Europe/Kiev'))

In [6]: dt_no_offset = datetime(2014, 11, 21, 10, 30, 45)

In [7]: dt_offset
Out[7]: datetime.datetime(2014, 11, 21, 10, 30, 45, tzinfo=<DstTzInfo 'Europe/Kiev' LMT+2:02:00 STD>)

In [8]: dt_no_offset
Out[8]: datetime.datetime(2014, 11, 21, 10, 30, 45)

In [9]: datetime.fromtimestamp(timegm(dt_offset.utctimetuple()), tz=pytz.UTC)
Out[9]: datetime.datetime(2014, 11, 21, 8, 28, 45, tzinfo=<UTC>)

In [10]: datetime.fromtimestamp(timegm(dt_no_offset.utctimetuple()), tz=pytz.UTC)
Out[10]: datetime.datetime(2014, 11, 21, 10, 30, 45, tzinfo=<UTC>)
```

**UPD**

Actually there is a much cleaner way to do the same, using exclusively `pytz`:

```python
In [68]: def dt_to_utc(dt):
   ....:     return pytz.UTC.normalize(dt) if dt.tzinfo else dt.replace(tzinfo=pytz.UTC)
   ....:

In [69]: dt_to_utc(dt_offset)
Out[69]: datetime.datetime(2014, 11, 21, 8, 28, 45, tzinfo=<UTC>)

In [70]: dt_to_utc(dt_no_offset)
Out[70]: datetime.datetime(2014, 11, 21, 10, 30, 45, tzinfo=<UTC>)
```
