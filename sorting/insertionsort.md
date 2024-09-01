# Insertion Sort
------

## Definition
- Insertion sort is a simple sorting algorithm that works similar to the way you sort playing cards in your hands. The array is virtually split into a sorted and an unsorted part. Values from the unsorted part are picked and placed at the correct position in the sorted part.

## What You need to Know

- works left to right
- examine each item and compare it to the items on the left
insert the item in the correct position in the array
the array will form sorted and unsorted paritition (sorted will be on the left).
- basically first check the first element, there is no element to the left of it then it is sorted, then check the next element and compare it to it's left element. Then go to the element after it and compare it to the left element this will lead to a sorted array in the left and unsorted on the right until it's all sorted.
- In bubble sort each element is compared to the element to its right, until a sorted partition forms at the end of the array. So basically bubble and insertion sort are different than in each other, since in insertion sort you will have a sorted to the left and unsorted parititon while in bubble sort you will have the sorted partition to the right which is good to get the highest number in an array.

## Time Complexity
- Best Average Worst
- O(N) O(N^2) O(N^2)
## Space Complexity
- O(1)

## Graph

![](https://media.geeksforgeeks.org/wp-content/uploads/insertionsort.png)

## Insertion Sort Implemenation

<details>
<summary>
Java Implementation
</summary>

```java
package tests;

//Java program for implementation of Insertion Sort 
class InsertionSort { 
	/*Function to sort array using insertion sort*/
	void sort(int arr[]) 
	{ 
		int n = arr.length; 
		for (int i = 1; i < n; ++i) { 
			int key = arr[i]; //11
			int j = i - 1; //0

			/* Move elements of arr[0..i-1], that are 
			greater than key, to one position ahead 
			of their current position */
			while (j >= 0 && arr[j] > key) { 
				arr[j + 1] = arr[j]; //12 at arr index 1
				j = j - 1; 
			} 
			arr[j + 1] = key; 
		} 
	} 

	/* A utility function to print array of size n*/
	static void printArray(int arr[]) 
	{ 
		int n = arr.length; 
		for (int i = 0; i < n; ++i) 
			System.out.print(arr[i] + " "); 

		System.out.println(); 
	} 

	// Driver method 
	public static void main(String args[]) 
	{ 
		int arr[] = { 12, 11, 13, 5, 6 }; 

		InsertionSort ob = new InsertionSort(); 
		ob.sort(arr); 

		printArray(arr); 
	} 
} /* This code is contributed by Rajat Mishra. */
//https://www.geeksforgeeks.org/insertion-sort/

```

</details>


<details>
<summary>
Python Implementation
</summary>

```python
def insertionSort(arr):
	n = len(arr) # Get the length of the array
	
	if n <= 1:
		return # If the array has 0 or 1 element, it is already sorted, so return

	for i in range(1, n): # Iterate over the array starting from the second element
		key = arr[i] # Store the current element as the key to be inserted in the right position
		j = i-1
		while j >= 0 and key < arr[j]: # Move elements greater than key one position ahead
			arr[j+1] = arr[j] # Shift elements to the right
			j -= 1
		arr[j+1] = key # Insert the key in the correct position

# Sorting the array [12, 11, 13, 5, 6] using insertionSort
arr = [12, 11, 13, 5, 6]
insertionSort(arr)
print(arr)
```
</details>