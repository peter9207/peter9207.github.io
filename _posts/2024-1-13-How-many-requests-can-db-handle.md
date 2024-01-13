---
layout: post
title: How many requests can a DB handle?
---

Recently in a system design interview, I was asked to design a warehouse inventory system that handles 1k writes per second.  

I didn't do very well in that interview.


After that interview, I got very curious in what is a reasonable amount of traffic a database might handle. So I looked up various database benchmarks. The benchmarks all uses a standard query from some dataset, and most measured the time it took to ran the query, and compared them against each other. While this is very easy to understand, its not very applicable to real world applications.  

A count * query is not ran in a vacuum, aggregations are slow, but the real problem they cause is because they lock the table so other queries cannot run.  

So I created a small program [here](https://github.com/peter9207/dbcompare) to run some simple queries that might exist in an API server, and have concurrently process that trigger them. To see in a given time how many requests can be ran. 

The result is 

| read write worker ratio | reads in 5 seconds | writes in 5 seconds|
| ---------------- | ------------------- | -------------------- |
|5/10 | 13665 | 5980 |
|10/10 | 22355 | 4763|
|10/5 | 25861 | 2950| 
|10/3 | 27368 | 1902| 
|10/2 | 27674| 1301| 
|10/1 | 31093| 721 | 
|10/0 | 31383 | 0 | 


It's interesting to see that reads are basically uneffected between 0 vs 1 worker, and write workers scale prettly linearly at least for the few concurrent goroutines I have running.  

Ofcourse this is with a very simple schema I setup, and the database only have a few thousand records running in it. Next step is to find a real dataset, maybe I can download one of the ones from other database benchmarks, and update the queries for the respectable dataset. Also having goroutines run loops to call select queries seems rather clunky, I would have to come up with a smarter way to generate traffic. 

 

