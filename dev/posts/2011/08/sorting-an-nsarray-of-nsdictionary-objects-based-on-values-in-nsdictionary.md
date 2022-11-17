---
title: "Sorting an NSArray of NSDictionary objects, based on values in NSDictionary"
date: "2011-08-07"
categories: 
  - "cocoa"
  - "ios"
  - "objective-c"
tags: 
  - "nsarray"
  - "sortedarrayusingfunction"
  - "sorting"
---

## How to use sortedArrayUsingFunction

Today I came across a requirement where I had to Sort an NSArray. Each element of the array had a NSDictionary which had only one element, which was a NSArray. Structure was like:

NSArray

\---->NSDictionary

\---->---->"somekey1" - NSArray \[val1, val2, val3... val-n\]

\---->NSDictionary

\---->---->"somekey2" - NSArray \[val1, val2, val3... val-m\]

\---->NSDictionary

\---->---->"somekey3" - NSArray \[val1, val2, val3... val-o\]

:

:

\---->NSDictionary

\---->---->"somekey-x" - NSArray \[val1, val2, val3... val-w\]

(where n!=m!=o!=w)

I wanted this NSArray to be sorted so that the NSDictionary with the largest number of NSArray values in it should come on sorted.

After looking at the available options in Apple's Documentation [here](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/Collections/Articles/Arrays.html#//apple_ref/doc/uid/20000132-SW5) I decided to define a selector ('delegate' for other .NET folks like me) and provide the selector to the sortedArrayUsingFunction method available for an NSArray.

The sorting function looks like this

\[code\] NSInteger sortByArrayCount(id dictionary1, id dictionary2, void \*reverse) {

NSMutableDictionary \*dict1 = (NSMutableDictionary \*)dictionary1; NSMutableDictionary \*dict2 = (NSMutableDictionary \*)dictionary2;

NSArray \*arr1 = (NSArray \*)\[\[dict1 objectEnumerator\] nextObject\]; NSArray \*arr2 = (NSArray \*)\[\[dict2 objectEnumerator\] nextObject\];

NSLog(@"Count of Array 1: %d, Array 2: %d", \[arr1 count\], \[arr2 count\]); if(\*(BOOL \*)reverse == YES) { return (\[arr2 count\] > \[arr1 count\]); } else { return (\[arr1 count\] > \[arr2 count\]); } }

\[/code\]

I think the code is quite self explanatory, we convert the values passed into the method. Then extract the first element in the dictionary as NSArray, finally I check if reverse==YES is passed or not this flag indicates whether you want a Descending sort or not. Finally do the comparison.

To sort an array you call it as follows:

\[code\]

NSArray \*sortedArray; BOOL reverseSort = NO; sortedArray = \[catList sortedArrayUsingFunction:sortByArrayCount context:&reverseSort\];

\[/code\]

Point to note here is once you have got the NSDictionary you could make the sorting condition on any of the values in the dictionary. For example string compare the Key of the two inputs.

The sortArrayByFunction method offers a lot of flexibility in terms of deciding how you want to sort. My case was a unique one.

Other options to explore are ofcourse using sortDescriptors if you wanted to sort based on string values in NSArray of NSDictionaries.

That's about it for now. Have fun.

(Yay! to my first iOS article)
