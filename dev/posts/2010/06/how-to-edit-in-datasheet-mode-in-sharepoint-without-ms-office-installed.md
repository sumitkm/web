---
title: "How To: Edit in Datasheet View in Sharepoint without MS Office installed"
date: "2010-06-20"
tags: 
  - "accessdatabaseengine"
  - "edit-in-datasheet"
  - "moss"
  - "moss-2007"
  - "sharepoint"
---

Realized this interesting thing today. We know that all sharepoint lists have this “Edit in Datasheet View” shortcut that gives a nice grid interface in case you want to do bulk updates or deletes. However you will note it gives an error if you don’t have office installed on the machine you are accessing it from (for e.g. the development servers don’t usually have office). I found out if you install the AccessDatabaseEngine (free download) from MS, it will give you the edit in datasheet mode.

You can download the database engine from the following location: [http://www.microsoft.com/downloads/details.aspx?familyid=C06B8369-60DD-4B64-A44B-84B371EDE16D&displaylang=en](http://www.microsoft.com/downloads/details.aspx?familyid=C06B8369-60DD-4B64-A44B-84B371EDE16D&displaylang=en)

There are other interesting things you can do with the AccessDatabaseEngine like writing/reading excel files without Office automation etc. But that's for another day...
