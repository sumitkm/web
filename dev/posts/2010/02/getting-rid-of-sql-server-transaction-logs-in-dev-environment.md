---
title: "Getting rid of SQL SERVER Transaction Logs in Dev Environment"
date: "2010-02-10"
tags: 
  - "sql-server"
  - "transaction-logs"
---

Please note this article is ‘strictly’ applicable to Development (non-production) Environments.

**Problem:** Huge SQL Server Transaction files that cannot be truncated.

Background: In Development Environment we often restore database from a production server to either do upgrades, enhancements or bug fixes. Most of the time production servers are setup to retain transaction logs and production environments are not typically constrained by disk space. Hence transaction logs for a heavily used database can go up over a period of time.

When such a database is restored to a development environment it can quickly eat up all available disk space.

**Use Case**: In my case I had restored a sharepoint content database and re-built the site using the restored database. However the content DB had transaction logs enabled and the log file was turning out to be about 15GB in size. It ate up all disk space on my development VM.

**Solution**:

**The solution here is not optimal. I am not a DB guru, I did the following by looking up various places on the internet. The fact that I had to do multiple searches to bring up the solution gave me the idea of putting these steps together. However, I strongly suggest not doing this on production environment because I do not know what the repercussions will be.**

Here go the steps:

1. Set Recovery mode to “Simple”.
    1. Using SQL Server Management Studio, select the database on the object browser, right click on it and navigate to “Properties”.
    2. In “Properties” pane, select “Options” on the left hand pane.
    3. Set “Recovery model” to Simple. Among other things it ensures Transaction Logs are not backed up (hence NOT advisable for production environments generally).

[![How to Change Recovery Model in SQL Server](/images/blog/2010/02/images/changerecoverymodel.jpg "How to Change Recovery Model in SQL Server")](/images/blog/2010/02/images/changerecoverymodel.jpg)

1. Now take a backup of the database
    1. Use the Full Backup
    2. Delete the database
    3. Restore the database from the backup in step 2
    4. Shrink the database using the following snippet. Replace WSS_CONTENT_APPS_4000 with your DB name and change the Log file name appropriately.

```sql
USE [WSS_CONTENT_APPS_4000]

GO

DBCC SHRINKFILE (N'WSS_Content_Apps_4000_log' , 0, TRUNCATEONLY)

GO
```
1. Go to the Messages page in Management Studio. It should not have any error messages. It should show something similar
```sql
(1 row(s) affected)
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
