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


## Dynamic Array Implementation

```python
import ctypes


class DynamicArray(object):
	'''
	DYNAMIC ARRAY CLASS (Similar to Python List)
	'''

	def __init__(self):
		self.n = 0 # Count actual elements (Default is 0)
		self.capacity = 1 # Default Capacity
		self.A = self.make_array(self.capacity)

	def __len__(self):
		"""
		Return number of elements stored in array
		"""
		return self.n

	def __getitem__(self, k):
		"""
		Return element at index k
		"""
		if not 0 <= k < self.n:
			# Check it k index is in bounds of array
			return IndexError('K is out of bounds !')

		return self.A[k] # Retrieve from the array at index k

	def append(self, ele):
		"""
		Add element to end of the array
		"""
		if self.n == self.capacity:
			# Double capacity if not enough room
			self._resize(2 * self.capacity)

		self.A[self.n] = ele # Set self.n index to element
		self.n += 1

	def insertAt(self, item, index):
		"""
		This function inserts the item at any specified index.
		"""

		if index < 0 or index > self.n:
			print("please enter appropriate index..")
			return

		if self.n == self.capacity:
			self._resize(2*self.capacity)

		for i in range(self.n-1, index-1, -1):
			self.A[i+1] = self.A[i]

		self.A[index] = item
		self.n += 1

	def delete(self):
		"""
		This function deletes item from the end of array
		"""

		if self.n == 0:
			print("Array is empty deletion not Possible")
			return

		self.A[self.n-1] = 0
		self.n -= 1

	def removeAt(self, index):
		"""
		This function deletes item from a specified index..
		"""

		if self.n == 0:
			print("Array is empty deletion not Possible")
			return

		if index < 0 or index >= self.n:
			return IndexError("Index out of bound....deletion not possible")

		if index == self.n-1:
			self.A[index] = 0
			self.n -= 1
			return

		for i in range(index, self.n-1):
			self.A[i] = self.A[i+1]

		self.A[self.n-1] = 0
		self.n -= 1

	def _resize(self, new_cap):
		"""
		Resize internal array to capacity new_cap
		"""

		B = self.make_array(new_cap) # New bigger array

		for k in range(self.n): # Reference all existing values
			B[k] = self.A[k]

		self.A = B # Call A the new bigger array
		self.capacity = new_cap # Reset the capacity

	def make_array(self, new_cap):
		"""
		Returns a new array with new_cap capacity
		"""
		return (new_cap * ctypes.py_object)()

# Instantiate


arr = DynamicArray()

# append the new elements

arr.append(1)

arr.append(2)

arr.append(3)

# length of the given append in array

print(len(arr))

# access the given append in array

print(arr[1])

print(arr[2])

# remove the given the array

arr.removeAt(2)

# length of the array

print(len(arr))

# index of the array

print(arr[1])

	#This code Contribute by Raja.Ramakrishna

```
