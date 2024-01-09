---
title: Latency vs the Cloud
date: 2019-01-23T21:26:00.000-07:00
draft: false
url: /2019/01/latency-vs-cloud.html
description: Latency vs the Cloud
tags:
  - null
  - null
  - null
banner: /img/latency_x_roundtrips_400.png
---
"The cloud is so fast! We can spin up servers and services so quickly to extend our environment and then all the users across the globe can access these services, so why does it take so long for you to get our users into the cloud?"  

**(Latency) x (# of Round Trips)**

Most Cloud Identity Management APIs are built so that consumers must retrieve the data one object at a time or load it one object at a time. This means one roundtrip per object. Naturally, a data set in the cloud tends to be farther away than between two servers in the same data center. So the one object at time paradigm that worked ok in the data center works fine in the cloud for very small sets of objects. Once you start loading even moderately sized data sets of objects the additional latency shows up quite harshly. More bandwidth won't solve the problem.

Let's try an analogy: bandwidth is like the number of lanes on a freeway, which means more traffic can pass through the same point at the same time, whereas latency is like the length of the freeway between your source and destination, the farther away you are from your destination the longer the trip will take. 

Building in a bulk mechanism for cloud APIs is a must! When moving across the country I want to load my stuff into a moving truck, not take one object at a time in my car! The same applies to the act of moving data, which I move across the country a whole lot more frequently than I do my family. Please, owners of Cloud APIs, don't force me to get/load one object a time, let me use a moving truck (bulk export and import)!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices