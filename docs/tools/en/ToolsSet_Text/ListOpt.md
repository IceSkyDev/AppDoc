---
title: List Operate
class: heading_no_counter
keywords: List, Sort, Find, Take, Distinct
desc: List operations, such as sort, find, take, distinct, and pad
---

## Introduce

Provides a variety of operations on text list, include sort, find, pad, take, and more

![](../../assets/images/ToolsSet/TSTListOpt.png)

## How to use

* Enter the text to be processed in the text box on the left
* The middle part is the operation area, and the operations that can be performed are as follows
  * Sort: Type can be alphabet ascending, alphabet descending, random, length ascending, length descending, and reverse
    * The switch on the right side of the type option indicates whether to use numeric sorting, which is turned off by default, that is, using alphabetical sorting, which only works for the first two sorting methods
  * Find: Search for items in a specified way, start with, end with, contains, and equal to specified text
    * The switch on the right side of the text box can toggle equal and unequal states
  * Pad: Pad the text to a specified length with the specified characters, and you can specify that it is filled at the start or end position
    * By default, space is used when no character is specified, and each item is padded to the length of the longest item when length not specified
  * Take: Take the specified characters from the start or end position, you can specify the number or characters to skip and take
    * By default, the Skip and Extract parameters are numeric and can be switched to characters by selecting StopChar
    * The character judgment starts from the starting position, and you can specify whether the judgment method is equal or unequal
  * Below these is the operation of no parameter or one list parameter, and the list parameter can be entered in the text box below
    * Distinct: Removes duplicates from the list
    * Union: Merge two lists
    * Intersect: Gets the intersection of two lists, i.e., items that exist in both lists
    * Except: Gets items that exist in the first list and do not exist in the second list
    * Count: counts the number of items in the list
    * Reverse: Reverse character order of each item in the list
