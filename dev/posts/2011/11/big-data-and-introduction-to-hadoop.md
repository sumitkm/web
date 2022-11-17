---
title: "Big Data and Introduction to Hadoop"
date: "2011-11-05"
categories: 
  - "big-data"
tags: 
  - "hadoop"
  - "hbase"
  - "hive"
  - "map-reduce"
---

Last weekend (October 29, 2011) I attended a training on Hadoop, arranged by my employer. It started on Friday afternoon ended Sunday evening, in 6 batches of 4 hours each. In the end, all 20 attendees had their brains spilling out of their ears, but each one of us had a blast! It was a fabulous series!

Following (semi-technical) account is my 101 level take-away from some of the sessions.

**What is Hadoop?**

Cloudera the leading vendor for Hadoop distributions defines it as follows at their website

Technically, Hadoop consists of two key services: reliable data storage using the Hadoop Distributed File System (HDFS) and high-performance parallel data processing using a technique called MapReduce.

There you have it, from the horse's mouth!

Little bit of history, Hadoop was sponsored by Yahoo! (yes, you read that right), with Dough Cutting being the principal architect of the project. Once Hadoop was mature enough Yahoo made Hadoop an Apache project. Dough left Yahoo and formed Cloudera which is now considered the 'Red Hat' of Hadoop distributions. If you really haven't read Wikipedia about how Hadoop got it's name, it got it's name from Doug's son's toy elephant!

More trivia, Hadoop project is based on Google's papers on their implementation of GFS and Big Table that google internally uses.

**If it is just a file system + a technique how is it related to the cloud hoopla?**

Well when we say Hadoop in context of a cloud we mean things on top of HDFS and MapReduce. Basically Hadoop is the entire ecosystem built on top of the 'classic definition'. It consists of Hbase as database, Hive as a Data Warehouse, Pig as the query language all built on top of Hadoop and the Map-Reduce framework.

HDFS is designed ground up to scale seamlessly as you throw hardware at it. That's it's strength! Anyone designing server farms will agree, scaling horizontally is non-trivial in most cases. For HDFS, problem of scale is simply solved by throwing more hardware at the Farm. A lot of it is because actions on HDFS are asynchronous. But the concept of throwing hardware at a farm and getting scaling automatically is what endears Hadoop to Cloud computing.

**Okay how is this different from SQL Server 2008 R2 running on top of Windows 2008 R2's NTFS?**

Ah ha! Now that's a loaded question. Let's try to go one by one (list below is pretty random with respect to importance or concepts, I am just doing a brain dump here)

1\. Data is not stored in the traditional table column format. At best some of the database layers mimic this, but deep in the bowels of HDFS, there are no tables, no primary keys, no indexes. Everything is a flat file with predetermined delimiters. HDFS is optimized to recognize <Key, Value> mode of storage. Every things maps down to <Key, Value> pairs.

2\. HDFS supports only forward only parsing. So you are either reading ahead or appending to the end. There is no concept of 'Update' or 'Insert'.

3\. Databases built on HDFS don't guarantee ACID properties. Specially 'Consistency'. It offers what is called as 'Eventual Consistency', meaning data will be saved eventually, but because of the highly asynchronous nature of the file system you are not guaranteed at what point it will finish. So HDFS based systems are NOT ideal for OLTP systems. RDBMS still rock there.

4\. Taking code to the data. In traditional systems you fire a query to get data and then write code on it to manipulate it. In MapReduce, you write code and send it to Hadoop's data store and get back the manipulated data. Essentially you are sending code to the data.

5\. Traditional databases like SQL Server scale better vertically, so more cores, more memory, faster cores is the way to scale. However Hadoop by design scales horizontally. Keep throwing hardware at it and it will scale.

**I am beginning to get it, why is it said Hadoop deals with unstructured data? How do we store data actually?**

Unstructured is a slight misnomer in the very basic sense. By Unstructured, Hadoop implies it doesn't know about column names, column data types, column sizes or even number of columns. Also there is no implicit concept of table. Data is stored in flat files! Flat files with some kind of delimiters that needs to be agreed upon by all users of the data store. So it could me comma delimited, pipe delimited, tab delimited. Line feed, as a thumb-rule, is always treated as the end of record. So there is a method to the madness ('unstructured-ness') but there are no hard-binding as employed by traditional databases. When you are dealing with data from Hadoop you are on your own with respect to data cleansing.

Data input in hadoop is as simple as loading your data file into HDFS, and by loading it's very very close to copying files in the usual sense on any OS.

**Okay, so there is no SQL, no Tables, no Columns, once I load my data how do I get it back?**

In Short: Write code to do Map-Reduce.

**Huh! Seriously? Map-Reduce... wha...?**

Yes. You have to write code to get data from a Hadoop System. The abstractions on top of Hadoop are a few and all are sub-optimal. So the best way to get data is to write Java code that calls the MapReduce framework that slices and dices the stored data for you on the fly.

The Map-Reduce framework works in two steps, (no points for guessing), step 1 is Map and step 2 is Reduce.

Mapping Data: If it is plain de-limited text data, you have the freedom to pick your selection of keys from the record (remember records are typically linefeed separated) and values and tell the framework what your Key is and what values that key will hold. MR will deal with actual creation of the Map. When the map is being created you can control on what keys to include or what values to filter out. In the end you end up with a giant hashtable of filtered key value pairs. Now what?

Reducing Data: Once the map phase is complete code moves on to the reduce phase. The reduce phase works on mapped data and can potentially do all the aggregation and summation activities.

Finally you get a blob of the mapped and reduced data.

**But... but... Do I really have to write Java?**

Well, if you are that scared of Java, then you have Pig. No, I am not calling names here. Pig is a querying engine that has more 'business-friendly' syntax but spits out MapReduce code in the backend and does all the dirty work for you. The syntax for Pig is called, of course, Pig Latin.

When you write queries in Pig Latin, Pig converts it into MapReduce and sends it off to Hadoop, then retrieves the results and hands it back to you.

Analysis shows you get about half the performance of raw optimal hand written MapReduce java code, but the same code takes more than 10 times the time to write when compared to a Pig query.

If you are in the mood for a start-up idea, generating optimal MapReduce code from Pig Latin is a topic to consider ;-)...

For those in the .NET world, Pig Latin is very similar syntactically to LINQ.

**Okay, my head is now spinning, where does Hive and HBase fit in?**

Describing Hive and HBase requires full articles of their own. A very brief intro to them is as follows:

HBase

HBase is a key value store that sits on top of HDFS. It is a NOSql Database.

It has a very thin veneer over raw HDFS where in it mandates that data is grouped in a Table that has rows of data.

Each row can have multiple 'Column Families' and each 'Column Family' can contain multiple columns.

Each column name is the key and it has it's corresponding column value.

So a column of data can be represented as

row\[family\]\[column\] = value

Each row need not have the same number of columns. Think of each row as a horizontal linked list, that links to a column family and then each column family links to multiple columns as <Key, Value> pairs.

<table border="0" cellspacing="0" cellpadding="2"><tbody><tr><td>row1</td><td>-&gt;</td><td>family1</td><td>-&gt;</td><td>col A = val A</td></tr><tr><td></td><td>-&gt;</td><td>family2</td><td>-&gt;</td><td>col B = val B</td></tr><tr><td colspan="5">and so on.</td></tr></tbody></table>

Hive

Hive is a little closer to traditional RDBMS systems. In fact it is a Data Warehousing system that sits on top of HDFS but maintains a meta layer that helps data summation, ad-hoc queries and analysis of large data stores in HFDS.

Hive supports a high level language called Hive Query Language, that looks like SQL but restricted in a few ways like no, Updates or Deletes are allowed. However Hive has this concept of partitioning that can be used to update information, which is essentially re-writing a chunk of data whose granularity depends on the schema design.

Hive can actually sit on top of HBase and perform join operations between HBase tables.

**I heard Hadoop only requires 'Commodity Hardware' to run. Can I bunch together the 486 machines gathering dust in my garage and bring up a Hadoop cluster?**

In short: NO!

When Google originally set out to build it's search index 'powerful' computers implied room sized Cray Super Computers that costed a pretty penny and available only to the CIA!

So commodity hardware implies 'non-supercomputers' that can be purchased by everybody. Today you can string together 10-12 high end blade servers each with about 24Gb of RAM and 12-24 TB disk space and as many cores each as you can get, to build an entry level production ready Hadoop cluster.

That's a different point you can run code samples on a VM that will run ok on a laptop with the latest core processors and approx 8 Gigs of RAM. But that's only good for code samples! Even for PoCs spinning up a EC2 cluster is the best way to go.

* * *

Okay, with that I conclude this article. In upcoming articles we'll see installation as well as some real world use cases of big data on Hadoop!
