---
layout: post
title: Python Performance Investigation
tags: [python]
categories: [skill]
---

In this post, we investigate how to efficiently delete certain elements from a Python list. More specifically, you want to delete certain elements, whose indices are given.


Solution A: Move to A New List
------------------------------

```python
def removeA(myList, removalIndices):
    if not isinstance(removalIndices, set):
        removalIndices = set(removalIndices)
    return [v for i, v in enumerate(myList) if not (i in removalIndices)]
```

This solution moves elements that do not need remove to a new list. Clearly, it would not be quite efficient when the number of removals is much less than the length of the original list. Besides, if the indices of the removals are not stored in a `set` but a `list`, the conversion from `list` to `set` would further drop the efficiency.


Solution B: Remove From The Last
--------------------------------

```python
def removeB(myList, removalIndices):
    for removalIndex in removalIndices[::-1]:
        del myList[removalIndex]
    return myList
```

This solution removes the elements from the last (the one with the largest index) to the first (the one with the smallest index). This solution assumes that the indices of removals are sorted in an ascending order. Note that, removing from the first one is not a good idea, since each removal will change the indices of the remaining removals. In other words, for removals other than the first one, you have to recalculate the index before removing.


Solution C: Shift Removals Together Then Remove
-----------------------------------------------

```python
def removeC(myList, removalIndices):
    nextRemovalIndex = removalIndices[0]
    indexOfRemovalIndices = 1

    numOfRemovals = len(removalIndices)
    lenOfList = len(myList)

    currentIndex = nextRemovalIndex + 1
    while currentIndex < lenOfList:
        nextIndex = removalIndices[indexOfRemovalIndices] if indexOfRemovalIndices < numOfRemovals else lenOfList
        while currentIndex < nextIndex:
            myList[nextRemovalIndex] = myList[currentIndex]
            nextRemovalIndex += 1
            currentIndex += 1
        indexOfRemovalIndices += 1
        currentIndex += 1
    # pay attention
    myList[-numOfRemovals:] = []

    return myList
```

This solution first shifts all the removals to the end of the list, and then removes them. Note that, this solution also assumes the indices of removals are sorted in an ascending order. Compare to **Solution B**, it guarantees that every element that needs move just moves once.


Which One Will Be More Efficient?
---------------------------------

+ Dense Cases (`myList` has $$10^6$$ elements, removing $$80\%$$)
  + Random locations

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 159.12ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 134.69ms
      Solution B: 1.13ms
      Solution C: 132.39ms

    **Remarks:** during the measurements, I found that the `set` create from different status (_e.g.,_ sorted or unsorted) of a `list` will have different efficiency. I will investigate this in details in future.

  + From the beginning

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 187.58ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 133.30s
      Solution B: 7403.70ms
      Solution C: 221.80ms

  + From the ending

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 133.34ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 142.03s
      Solution B: 0.74ms
      Solution C: 121.12ms

+ Sparse Cases (`myList` has $$10^6$$ elements, removing $$0.2\%$$)
  + Random locations

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 134.81ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 149.77ms
      Solution B: 216.96ms
      Solution C: 159.68ms

  + From the beginning

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 150.39ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 153.45ms
      Solution B: 2098.12ms
      Solution C: 182.74ms

  + From the ending

    > solution A (with `list` representing removals, _i.e.,_ `removalIndices` is a `list`): 131.15ms
      solution A (with `set` representing removals, _i.e.,_ `removalIndices` is a `set`): 134.47s
      Solution B: 204.69ms
      Solution C: 163.19ms











TODO
====

1. efficiency of set creating from different status of a list
2. while loop versus splicing
