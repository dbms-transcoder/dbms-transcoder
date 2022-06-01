---
layout: post
title:  "Concurrency Control on Internal Resources"
date:   2022-05-29 18:00:00 -0700
author: Ember Crooks
tags: dbms-architecture db2 mysql
---

This is actually the concept that inspired this site. I was reading about MySQL as a Db2 expert, and kept reading the term 'mutex'. After the second or third time, I looked it up, and went, "Oh, a LATCH!"

## General Description
The concept/object covered here is NOT a lock. A lock is on logical objects within a database such as a row or a table. Here, we're talking about something ensuring exclusive access to some sort of physical object such as a file or a memory location. This is concurrency control on internal objects, not database objects. This is something that any multi-threaded application has to manage, including database management systems.

This is not a concept that is likely to come up or be an issue in the front-lines of either DBA work or of development work. Often if you're dealing with an issue with this, you're talking either vendor support, opening an issue, or digging into the code depending on whether the dbms you're working with is proprietary or open source. It is most likely to come up as an issue in apparent hang situations or in the investigation of unusual performance problems.

## DBMS Platform Specifics
{% tabs internal-concurrency %}

{% tab internal-concurrency Db2 %}
### Latch
Db2 calls this a Latch. Most often the latches we're working with are ones related to bufferpool page contention, but there can be other types. If you suspect latch contention or latch-wait issues, you're often going to be opening a ticket with IBM Db2 support. You can view latches using this sytax:
```
db2pd -latches
```
Often you'll need to run this repeatedly and compare output. The output is likely to be long, but it shows the latch holder and the latch waiter, along with the latch memory address. Here are a few interesting articles on investigating and working with latching issues:  

[IBM Tech Doc on Identifying Bufferpool Latch Contention](https://www.ibm.com/support/pages/identifying-bufferpool-latch-contention)  
[IBM Tech Doc on Measuring Latching Overhead](https://www.ibm.com/support/pages/measuring-latching-overhead-monitoring-functions-db2)  
test2
{% endtab %}

{% tab internal-concurrency MySQL %}
### Mutex
MySQL referrs to this concept as a Mutex. Mutex is short for 'Mutually exclusive'. Generally if there are problems with mutexes, it is an issue for a MySQL developer to work on.
You can enable monitoring in the performance schema using:
```
performance-schema-instrument='wait/synch/mutex/innodb/%=ON'
```
The restart the server.
Use the following to update teh setup_consumers table, if needed:
```SQL
UPDATE performance_schema.setup_consumers
       SET enabled = 'YES'
       WHERE name like 'events_waits%';
```
Then the information collected can be queried using something like this:
```SQL
SELECT EVENT_NAME, COUNT_STAR, SUM_TIMER_WAIT/1000000000 SUM_TIMER_WAIT_MS
       FROM performance_schema.events_waits_summary_global_by_event_name
       WHERE SUM_TIMER_WAIT > 0 AND EVENT_NAME LIKE 'wait/synch/mutex/innodb/%'
       ORDER BY COUNT_STAR DESC;
```
Here are a few interesting articles with more information on mutexes:  

[Blog: What is a mutex, anyway?](http://www.tocker.ca/what-is-a-mutex-anyway.html)  
[MySQL Documentation: Monitor Mutex Waits](https://dev.mysql.com/doc/refman/5.7/en/monitor-innodb-mutex-waits-performance-schema.html)
[Percona's Blog on Getting mutex information from MySQL's performance_schema](https://www.percona.com/blog/2015/01/06/getting-mutex-information-from-mysqls-performance_schema/)  

{% endtab %}

{% endtabs %}

## Summary
While this isn't a concept you're likely to have to deal with in the normal course of running a dbms, it is good to have an understanding of what it is and what it does when digging into thornier performance or hang problems.
