---
author: "Sumit"
title: "Saving NSArray in iOS"
date: "2011-10-16"
categories: 
  - "cocoa"
  - "ios"
  - "objective-c"
  - "programming"
tags: 
  - "save"
---

This is quick and dirty post. It's more of a bookmark for me, because I find toggling between C# and Objective C makes me  terrible with Objective C if I am away from it for a month or so.

**The Requirement**

- Save a list of records on the iPhone quickly and retrieve them later as required.

**The Approach**

Use the NSKeyedArchiver to save and load arrays of data.

**Syntax**

Setting up a file name and path to save save

\[code\] // need a path - (NSString \*) getPath { NSString\* path = \[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject\]; return \[path stringByAppendingPathComponent:@"MyFile.dat"\]; } \[/code\]

Save the data

\[code\]

// save an array - (void) saveSettingsData: (NSArray\*)data { \[NSKeyedArchiver archiveRootObject:data toFile:\[self getPath\]\]; }

\[/code\]

Load the data

\[code\]

// get that array back - (NSArray \*) loadSavedData { return \[NSKeyedUnarchiver unarchiveObjectWithFile:\[self getPath\]\]; }

\[/code\]

That's about it. I have used it for saving an array of dictionary objects and it works just fine. I have not tried it for array of custom entities. Will update here as I try that. If that doesn't work I have go deeper into the ManageObjectContext and PersistentStoreCoordinator and of course blog about it.

UPDATE: Well that didn't take long. Just confirmed that you can only persist NSArray objects containing other NSArray or NSDictionary objects. You cannot serialize an NSArray instance of custom Entities. So the next article on ManageObjectContext is now on.
