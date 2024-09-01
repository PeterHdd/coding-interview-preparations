# Arrays
---

## Definition
* Stores data elements based on an sequential, most commonly 0 based, index.
* Based on tuples from set theory.
* They are one of the oldest, most commonly used data structures.
* Arrays are used to implement list and strings.

## What you need to know
- Arrays provide random access to data, random(direct) access implies the ability to access any entry in a array in constant time (independent of its position in the array and of array's size). And that is big advantage.
- Optimal for indexing; bad at searching, inserting, and deleting (except at the end).
- Arrays are stored in memory contiguously, or in one chunk of space, so the memory address of each element in the array can be computed using this formula `address = start + (cellsize * index)` https://softwareengineering.stackexchange.com/questions/252407/why-is-the-complexity-of-fetching-a-value-from-an-array-be-o1 (cellsize is array length)
- Static arrays have a size that is fixed when they are created and consequently do not allow elements to be inserted or removed. However, by allocating a new array and copying the contents of the old array to it, it is possible to effectively implement a dynamic version of an array. If this operation is done infrequently, insertions at the end of the array require only amortized constant time.
-  Searching is done by iterating through the array and seeing if the value equals the item you are searching for.
-  Insertion is done by recreating the array, which means that each item must be recreated.
-  Deletion is done by recreating the array, which means that each item must be recreated.
- **Linear arrays**, or one dimensional arrays, are the most basic.
    - Are static in size, meaning that they are declared with a fixed size.
- **Dynamic arrays** are like one dimensional arrays, but have reserved space for additional elements.
    - If a dynamic array is full, it copies its contents to a larger array.
    - Dynamic arrays or growable arrays are similar to arrays but add the ability to insert and delete elements; adding and deleting at the end is particularly efficient. However, they reserve linear `(Θ(n))` additional storage, whereas arrays do not reserve additional storage.
- **Multi dimensional arrays** nested arrays that allow for multiple dimensions such as an array of arrays providing a 2 dimensional spacial representation via x, y coordinates.


## Complexity

|Operation|Complexity|
|---------|----------|
|Access   |O(1)      |
|Search   |O(n)      |
|Insert   |O(n)      |
|Delete   |O(n)      | 

