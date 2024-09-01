# Merge Sort

## Definition
- A divide and conquer algorithm.
- Recursively divides entire array by half into subsets until the subset is one, the base case.
- Once the base case is reached results are returned and sorted ascending left to right.
- Recursive calls are returned and the sorts double in size until the entire array is sorted.

## What you need to know
- This is one of the fundamental sorting algorithms.
- Know that it divides all the data into as small possible sets then compares them.
- Merge sorting is usually more efficient than bubble sorting unless the array is pre-sorted
- To do merge sort you need to use recursion.
- So basically you break the array into two halves, so you choose a middle element and all the elements in the first half belong to the first array and all elements in the second half belong to the second array. Then we sort each array and merge them to have one big sorted array.
- So basically after dividing in half the initial array, you will have 2 arrays then you keep dividing the 2 array until you have individual elements and then when you have individual elements you start comparing, example 3 and 5, 3 is smaller so you will have 3 5. Then you compare 3 and 1, 1 is smaller so you have 1 3 5..etc sort the first array like that and do the same thing in the second array. After that start comparing between the two arrays to have a sorted array.
- Merge sort is O(nlogn) since when the array reaches length=1 and we start sorting, then the worst case is 8 times to sort assuming we have an array of length=8. Then when we go one step up and we need to sort array with length=2, then the worst case is also 8 times to sort therefore we get O(n). Since the array we are dividing it by 2 (n/2), therefore when we do recursion we will have logn levels. Example log(8) = 3 levels in merge sort.
- Merge sort is divided until you have two items, then you sort those two items and merge the first half then merge the second and then you merge all array.
- Steps:
	- 1. get the first element and the last element, if first is less than last then you start the merge sort process.
	- 2. Then you get the middle element. Then recursively sort the left half and merge the right half.
	- 3. The two `sort()` functions, will cut the array in half as you can see in the image until it reaches one element. (follow steps in graph)
	- 4. Whenever you call `sort()`, the medium element is changing, when you reach 38 element and 27 alone then left will be equal to right and the `merge()` function will be called.
	- 5. In the merge function, first you need to get the size of the first array and then size of second array, which will most probably be size equal to 1 and the other size equal to 1. Then create two arrays with the two sizes that you got. Then do two for loops and put `{27}` and `{38}` in two arrays.
	- 6. After that you need to add the elements, sorted inside the initial array. So do a while loop that will keep iterating as long as i and j are less than the size of the two arrays. Inside the loop check if element in first array is less then you add the element in second array to the initial array. Also introduce a `k` variable that will be incremented after each iteration.
	- 7. In the end create two while loop , first loop will check if `i < n1` , second will check if `j < n2`. Inside the left loop, copy the remaning left element and increment `k` while inside the right loop copy the remaning right elements and increment `k`.

https://www.youtube.com/watch?v=i56B0xN7jSc&ab_channel=ComputerScience

## Space Complexity: O(n)

## Time Complexity: O(n log(n))

## Graph

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Merge-Sort-Tutorial.png)

## Merge Sort Implemenation

<details>
<summary>
Java Implementation
</summary>

```java
package tests;

/* Java program for Merge Sort */
public class MergeSort 
{
	// Merges two subarrays of arr[].
	// First subarray is arr[l..m]
	// Second subarray is arr[m+1..r]
	void merge(int arr[], int l, int m, int r) //initially it will get [12,11] which it sorts
	{
		// Find sizes of two subarrays to be merged
		int n1 = m - l + 1; //initial 1
		int n2 = r - m;//initial 1

		/* Create temp arrays */
		int L[] = new int[n1];
		int R[] = new int[n2];

		/*Copy data to temp arrays*/
		for (int i = 0; i < n1; ++i)
			L[i] = arr[l + i];
		for (int j = 0; j < n2; ++j)
			R[j] = arr[m + 1 + j];

		/* Merge the temp arrays */

		// Initial indexes of first and second subarrays
		int i = 0, j = 0;

		// Initial index of merged subarry array
		int k = l;
		while (i < n1 && j < n2) {
			if (L[i] <= R[j]) { //here u compare between the elements to put them in order
				arr[k] = L[i];
				i++;
			}
			else {
				arr[k] = R[j];
				j++;
			}
			k++;
		}

		/* Copy remaining elements of L[] if any */
		while (i < n1) { //copy elements from the array to the original array
			arr[k] = L[i];
			i++;
			k++;
		}

		/* Copy remaining elements of R[] if any */
		while (j < n2) { //copy elements from the array to the original array
			arr[k] = R[j];
			j++;
			k++;
		}
	}

	// Main function that sorts arr[l..r] using
	// merge()
	// l is left index and r is right index, initially l=0 and r=5
	void sort(int arr[], int l, int r)
	{
		//if l=r then there is one element, which means we divided the array until the end.
		if (l < r) {
			// Find the middle point 5/2=2.5 since int it will round down to 2
			int m = (l + r) / 2;

			// Sort first and second halves
			//this is done recursively, so when the sort call itself it is adding another sort to the stack (you can debug and check debug console)
			//when l is equal to r then the sort that is in the stack will exit, and the sort under it will take control and continue where it stopped.
			sort(arr, l, m); //bottom half
			sort(arr, m + 1, r); //top half

			// Merge the sorted halves
			//here we call merge array which is added in the stack,when the merge function finishes it will be removed from the stack.
			//and the sort function that is in the stack will regain control, and the sort function will come to a natural end and exit the stack,
			//which will call the other sort function and it will continue where it stopped.
			merge(arr, l, m, r);
		}
	}

	/* A utility function to print array of size n */
	static void printArray(int arr[])
	{
		int n = arr.length;
		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");
		System.out.println();
	}

	// Driver code
	public static void main(String args[])
	{
		int arr[] = { 12, 11, 13, 5, 6, 7 };

		System.out.println("Given Array");
		printArray(arr);

		MergeSort ob = new MergeSort();//arr:[12, 11, 13, 5, 6, 7] (arr.length -1 = 5)
		ob.sort(arr, 0, arr.length - 1);

		System.out.println("\nSorted array");
		printArray(arr);
	}
}
/* This code is contributed by Rajat Mishra */
//https://www.geeksforgeeks.org/merge-sort/
//https://www.youtube.com/watch?v=i56B0xN7jSc&ab_channel=ComputerScience
//Array 1:{2,5,7,8}
//Array 2:{2,4,7,12,32}
```
</details>

<details>
<summary>
Python Implementation
</summary>

```python
# Python program for implementation of MergeSort

# Merges two subarrays of arr[].
# First subarray is arr[l..m]
# Second subarray is arr[m+1..r]


def merge(arr, l, m, r):
	n1 = m - l + 1
	n2 = r - m

	# create temp arrays
	L = [0] * (n1)
	R = [0] * (n2)

	# Copy data to temp arrays L[] and R[]
	for i in range(0, n1):
		L[i] = arr[l + i]

	for j in range(0, n2):
		R[j] = arr[m + 1 + j]

	# Merge the temp arrays back into arr[l..r]
	i = 0	 # Initial index of first subarray
	j = 0	 # Initial index of second subarray
	k = l	 # Initial index of merged subarray

	while i < n1 and j < n2:
		if L[i] <= R[j]:
			arr[k] = L[i]
			i += 1
		else:
			arr[k] = R[j]
			j += 1
		k += 1

	# Copy the remaining elements of L[], if there
	# are any
	while i < n1:
		arr[k] = L[i]
		i += 1
		k += 1

	# Copy the remaining elements of R[], if there
	# are any
	while j < n2:
		arr[k] = R[j]
		j += 1
		k += 1

# l is for left index and r is right index of the
# sub-array of arr to be sorted


def mergeSort(arr, l, r):
	if l < r:

		# Same as (l+r)//2, but avoids overflow for
		# large l and h
		m = l+(r-l)//2

		# Sort first and second halves
		mergeSort(arr, l, m)
		mergeSort(arr, m+1, r)
		merge(arr, l, m, r)


# Driver code to test above
arr = [12, 11, 13, 5, 6, 7]
n = len(arr)
print("Given array is")
for i in range(n):
	print("%d" % arr[i],end=" ")

mergeSort(arr, 0, n-1)
print("\n\nSorted array is")
for i in range(n):
	print("%d" % arr[i],end=" ")

```
</details>

## Additional Links
* [Animated Merge Sort Display](https://www.toptal.com/developers/sorting-algorithms/merge-sort)
