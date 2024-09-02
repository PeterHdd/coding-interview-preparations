# Heaps

## About
**Heap** is a special case of balanced binary tree data structure where the root-node key is compared with its children and arranged accordingly. If α has child node β then:

```
key(α) ≥ key(β)
```

As the value of parent is greater than that of child, this property generates Max Heap. Based on this criteria, a heap can be of two types:

```
Input → 35 33 42 10 14 19 27 44 26 31
```
**Min-Heap** − Where the value of the root node is less than or equal to either of its children.
```
           10                     
        ↙      ↘              
      14            19                
    ↙  ↘         ↙   ↘
   26     31     42     27
 ↙  ↘      ↘
44   35       33
```
**Max-Heap** − Where the value of the root node is greater than or equal to either of its children.
```
           44                     
        ↙      ↘              
      42            35                
    ↙  ↘         ↙   ↘
   33     31     19     27
 ↙  ↘      ↘
10   26       14
```
Both trees are constructed using the same input and order of arrival.

## What You Need to Know
- A Heap is a specialized tree based structure data structure that satisfies the heap property: if A is a parent node of B, then the key (the value) of node A is ordered with respect to the key of node B with the same ordering applying across the entire heap.
- A heap can be classified further as either a "max heap" or a "min heap".
- In a max heap, the keys of parent nodes are always greater than or equal to those of the children and the highest key is in the root node.
- In a min heap, the keys of parent nodes are less than or equal to those of the children and the lowest key is in the root node.
- Basically min heap, you will have a node with a value less than the children. In max heap you will have a node with a value greater than it's children.
- In a heap the root node will be index = 0 then the left child will be index =1 and the right child index = 2, then under it left child equal to index = 3, so go from left to right. (level order traversal)
- To get the index there is a simple formula: 
  - left child: index * 2 + 1 
  - right child: index * 2 + 2 
  - parent child: (index-1)/2 
- Note: root node doesnt have a parent, this will give parent node of a particular node.
ex: index = 0, then left child => 0 2 +1 =1, right child => 02 + 2 = 2, parent child is 0-2/2 = 0
- Priority queue is an implementation of heap.
- When inserting you need to bubble down the elements until they reach the correct position if it's a min heap or max heap.
- The heap is implemented using array. So in case of min heap it is implemented from small to big in the array.
When inserting or deleting an element, you need to satisfy the heap rule. If the element that you inserted is larger than parent in max heap, then you need to start swapping until you fix the heap tree.
- When removing you always remove the root element, and replace it with the last element in the tree and then start swapping until you satisfy the heap tree.

## Max Heap Construction Algorithm

We shall use the same example to demonstrate how a Max Heap is created. The procedure to create Min Heap is similar but we go for min values instead of max values.

We are going to derive an algorithm for max heap by inserting one element at a time. At any point of time, heap must maintain its property. While insertion, we also assume that we are inserting a node in an already heapified tree.

* **Step 1** − Create a new node at the end of heap.
* **Step 2** − Assign new value to the node.
* **Step 3** − Compare the value of this child node with its parent.
* **Step 4** − If value of parent is less than child, then swap them.
* **Step 5** − Repeat step 3 & 4 until Heap property holds.

**Note** − In Min Heap construction algorithm, we expect the value of the parent node to be less than that of the child node.
![Max Heap Creation](/data_structures/animations/max_heap_animation.gif)

## Max Heap Deletion Algorithm

Let us derive an algorithm to delete from max heap. Deletion in Max (or Min) Heap always happens at the root to remove the Maximum (or minimum) value.

* **Step 1** − Remove root node.
* **Step 2** − Move the last element of last level to root.
* **Step 3** − Compare the value of this child node with its parent.
* **Step 4** − If value of parent is less than child, then swap them.
* **Step 5** − Repeat step 3 & 4 until Heap property holds.

![Max Heap Deletion](/data_structures/animations/max_heap_deletion_animation.gif)


## Complexity

|Operation|Complexity|
|---------|----------|
|Access Max / Min:   |O(1)      |
|Search   |O(n)      |
|Insert   | O(log(n)      |
|Remove Max / Min   |O(log(n)      | 


## Heap Implementation

<details>
<summary> Java Implementation </summary>

```java
package tests;

import java.util.Arrays;

public class MinIntHeap {
	
	private int capacity = 10;
	private int size = 0;
	
	int[] items = new int[capacity];
	
	private int getLeftChildIndex(int parentIndex) {return 2 * parentIndex + 1;}
	private int getRightChildIndex(int parentIndex) {return 2 * parentIndex + 2;}
	private int getParentIndex(int childIndex) {return (childIndex - 1)/2;}
	
	private boolean hasLeftChild(int index) { return getLeftChildIndex(index) < size; }
	private boolean hasRightChild(int index) { return getRightChildIndex(index) < size; }
	private boolean hasParent(int index) { return getParentIndex(index) >= 0; }
	
	private int leftChild(int index) {return items[getLeftChildIndex(index)];}
	private int rightChild(int index) {return items[getRightChildIndex(index)];}
	private int parent(int index) {return items[getParentIndex(index)];}
	
	//swap elements in array
	private void swap(int indexOne, int indexTwo) {
		int temp = items[indexOne];
		items[indexOne] = items[indexTwo];
		items[indexTwo] = temp;
	}
	
	//checks if array is full, if so creates a new array of double that size and copies all the elements over
	//this is the basic of how all arrays work.
	private void ensureExtraCapacity() {
		if(size == capacity) {
			items = Arrays.copyOf(items, capacity * 2);
			capacity *= 2;
		}
	}
	
	//peek which will return the top element in this case the min value in the array.
	public int peek() {
		if(size == 0) {
			throw new IllegalStateException();
		}
		return items[0];
	}
	
	// pull means removing, you always remove the root node if it was max or min heap
	public int pull() {
		if(size == 0) {
			throw new IllegalStateException();
		}
		int item = items[0]; //get the root node, if it was max or min value
		items[0] = items[size - 1]; //get the last element in the array and assign it to the first element or root node
		size--; //reduce the size since you removed an element
		heapifyDown(); //start swapping elements downward until you get a heap tree again
		return item;
	}
	
	// when adding you add at the end of the tree or an array since heap is implemented using array
	public void add(int item) {
		ensureExtraCapacity(); //check if there is space
		items[size] = item; //add the item at the end
		size++; //increase the size of the array
		heapifyUp(); //swap element with the above element to satisfy heap
	}
	
	//this method is used to swap the last element added in the tree upwards.
	public void heapifyUp() {
		int index = size - 1; //get the index of the last element in array
		//while loop, check if the last element has a parent and get the parent value, and check if the value of the parent is greater than the value of the child index
		// if it is greater enter the while loop and swap the two elements
		while(hasParent(index) && parent(index) > items[index]) {
			swap(getParentIndex(index), index); //swap
			index  = getParentIndex(index); //assign parent index to index
		}
	}
	
	//this is used when removing the top element and replacing it with the bottom element
	public void heapifyDown() {
		int index  = 0;
		//check if there is a left child, if there is not left child then there is no right child so only check the left child. (since the tree needs to be completed to be a heap tree)
		while(hasLeftChild(index)) {
			//since minheap, get the left index
			int smallerChildIndex = getLeftChildIndex(index);
			//if the root has a right child and they are less than the left child
			if(hasRightChild(index) && rightChild(index) < leftChild(index)) {
				smallerChildIndex = getRightChildIndex(index); //assign right child index to smallerchild index
			}
			
			if(items[index] < items[smallerChildIndex]) { // if root node less than smallerchildindex value then break
				break;
			} else { //swap if root is greater
				swap(index, smallerChildIndex);
			}
			index = smallerChildIndex;
		}
	}
}

```

</details>

<details>
<summary> Python Implementation </summary>

```python
class MinHeap:
    def __init__(self):
        self.heap = []

    def parent(self, i):
        return (i - 1) // 2

    def left_child(self, i):
        return 2 * i + 1

    def right_child(self, i):
        return 2 * i + 2

    def swap(self, i, j):
        self.heap[i], self.heap[j] = self.heap[j], self.heap[i]

    def insert(self, key):
        self.heap.append(key)
        self._heapify_up(len(self.heap) - 1)

    def _heapify_up(self, i):
        parent = self.parent(i)
        if i > 0 and self.heap[i] < self.heap[parent]:
            self.swap(i, parent)
            self._heapify_up(parent)

    def extract_min(self):
        if len(self.heap) == 0:
            return None
        if len(self.heap) == 1:
            return self.heap.pop()
        
        min_val = self.heap[0]
        self.heap[0] = self.heap.pop()
        self._heapify_down(0)
        return min_val

    def _heapify_down(self, i):
        min_index = i
        left = self.left_child(i)
        right = self.right_child(i)

        if left < len(self.heap) and self.heap[left] < self.heap[min_index]:
            min_index = left
        if right < len(self.heap) and self.heap[right] < self.heap[min_index]:
            min_index = right

        if min_index != i:
            self.swap(i, min_index)
            self._heapify_down(min_index)
```
</details>