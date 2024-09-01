# Bubble Sort
---

## Definition

- Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order.
- In order to implement this sort, the script starts on the left of the array and switches elements that are next to each other if they are in the wrong order. This usually requires multiple passes, unless the array is already sorted.
- Shouldnt be used in the real world since it is very slow.
Example: (https://www.geeksforgeeks.org/bubble-sort/) 

Example first pass:

```java
( 5 1 4 2 8 ) –> ( 1 5 4 2 8 ), Here, algorithm compares the first two elements, and swaps since 5 > 1.
( 1 5 4 2 8 ) –>  ( 1 4 5 2 8 ), Swap since 5 > 4
( 1 4 5 2 8 ) –>  ( 1 4 2 5 8 ), Swap since 5 > 2
( 1 4 2 5 8 ) –> ( 1 4 2 5 8 ), Now, since these elements are already in order (8 > 5), algorithm does not swap them.
```

## Space Complexity: O(1)

## Time Complexity
| Best | Average| Worst |
| -----|:------:| -----:|
| O(N) | O(N^2) | O(N^2)|

## Bubble Sort Implementation


<details>
<summary> Java Implementation</summary>

```java
package tests;

//Java program for implementation of Bubble Sort 
class BubbleSort 
{ 
	void bubbleSort(int arr[]) 
	{ 
		int n = arr.length; 
		for (int i = 0; i < n-1; i++)  //n is the length of the array and we do -1 since we are doing arr[j+1] later.
			for (int j = 0; j < n-i-1; j++) //if array is 7 then first iteration j < 6, second loop will keep iterating until it reaches last element,
				// then we go to the next index.
				if (arr[j] > arr[j+1]) 
				{ 
					// swap arr[j+1] and arr[j] 
					int temp = arr[j]; 
					arr[j] = arr[j+1]; 
					arr[j+1] = temp; 
				} 
	} 

	/* Prints the array */
	void printArray(int arr[]) 
	{ 
		int n = arr.length; 
		for (int i=0; i<n; ++i) 
			System.out.print(arr[i] + " "); 
		System.out.println(); 
	} 

	// Driver method to test above 
	public static void main(String args[]) 
	{ 
		BubbleSort ob = new BubbleSort(); 
		int arr[] = {64, 34, 25, 12, 22, 11, 90}; 
		ob.bubbleSort(arr); 
		System.out.println("Sorted array"); 
		ob.printArray(arr); 
	} 
} 
/* This code is contributed by Rajat Mishra */
```

</details>

<details>
<summary>
Python Implementation
</summary>

```python
def bubble_sort(arr):

    # Outer loop to iterate through the list n times
    for n in range(len(arr) - 1, 0, -1):

        # Inner loop to compare adjacent elements
        for i in range(n):
            if arr[i] > arr[i + 1]:

                # Swap elements if they are in the wrong order
                swapped = True
                arr[i], arr[i + 1] = arr[i + 1], arr[i]


# Sample list to be sorted
arr = [39, 12, 18, 85, 72, 10, 2, 18]
print("Unsorted list is:")
print(arr)

bubble_sort(arr)

print("Sorted list is:")
print(arr)
```
</details>

## Additional Links
* [Animated Bubble Sort Display](https://www.toptal.com/developers/sorting-algorithms/bubble-sort)

