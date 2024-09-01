# Quicksort
----

## Definition
---
- A divide and conquer algorithm (breaks a problem into subproblems that are similar to the original problem, recursively solves the subproblems, and finally combines the solutions to the subproblems to solve the original problem.)
- Partitions entire data set in half by selecting a random pivot element and putting all smaller elements to the left of the element and larger ones to the right.
- It repeats this process on the left side until it is comparing only two elements at which point the left side is sorted.
- When the left side is finished sorting it performs the same operation on the right side.
- Computer architecture favors the quicksort process.
- Changes the array in place.

## What you need to know
- Quicksorting is an algorithm in which a random element is selected from the array (called pivot) and then the array is partitioned so that all the numbers less than the element are placed before it and the ones greater than it are placed after it.
- This algorithm is efficient since swapping two elements in an array is usually a very quick process and it doesn't require using another data structure in intermediate steps. If the randomly selected element isn't near the median, quicksorting can be inefficient.
- While it has the same Big O as (or worse in some cases) many other sorting algorithms it is often faster in practice than many other sorting algorithms, such as merge sort.
- So first you need to choose a pivot, it can be beginning or end or middle. Then `paritition` method is called. In that method you need to get smallest element and the highest element and the pivot, then as long as lowest element is less than high element therefore you loop. Inside the loop you need to check if the element is smaller than swap it, and increment `i`. You keep checking until lowest element is greater than high. After that you need to add the pivot in the correct position by swapping and then returning the index where the partition was done.
- Steps:
	- 1. Select the Pivot Element, for example select right most element.
	- 2. Rearrange the Array, now the elements of the array are rearranged so that elements that are smaller than the pivot are put on the left and the elements greater than the pivot are put on the right.
	- 3. Divide Subarrays, pivot elements are again chosen for the left and the right sub-parts separately. And, step 2 is repeated.
- To rearrange array, first choose pivot then do `int i = (low - 1)`, then iterate normally in the array and check if elements are less than the pivot, if they are then increment `i` and swap the elements. After the loop finishes, swap the pivot element with the greater element specified by i. This will add pivot in correct location and then return index of pivot.





## Space Complexity: O(log(n))

## Time Complexity
| Best          | Average     | Worst |
| --------------|:-----------:| -----:|
| O(n (log(n))) | O(n log(n)) | O(N^2)|

## Graph

![](https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/01/QuickSort2.png)

* [Animated Quick Sort Display](https://www.toptal.com/developers/sorting-algorithms/quick-sort)


## Quick Sort Implementation

<details>
<summary>
Java implementation
</summary>

```java
package tests;

// Quick sort in Java

import java.util.Arrays;

class Quicksort {

    // method to find the partition position
    static int partition(int[] array, int low, int high) {

        // choose the rightmost element as pivot
        int pivot = array[high];

        // pointer for greater element
        int i = (low - 1);

        // traverse through all elements
        // compare each element with pivot
        for (int j = low; j < high; j++) {
            if (array[j] <= pivot) {

                // if element smaller than pivot is found
                // swap it with the greater element pointed by i
                i++;

                // swapping element at i with element at j
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }

        }

        // swap the pivot element with the greater element specified by i
        int temp = array[i + 1];
        array[i + 1] = array[high];
        array[high] = temp;

        // return the position from where partition is done
        return (i + 1);
    }

    static void quickSort(int[] array, int low, int high) {
        if (low < high) {

            // find pivot element such that
            // elements smaller than pivot are on the left
            // elements greater than pivot are on the right
            int pi = partition(array, low, high);

            // recursive call on the left of pivot
            quickSort(array, low, pi - 1);

            // recursive call on the right of pivot
            quickSort(array, pi + 1, high);
        }
    }
}

// Main class
class Main {
    public static void main(String[] args) {

        int[] data = { 8, 7, 2, 1, 0, 9, 6 };
        System.out.println("Unsorted Array");
        System.out.println(Arrays.toString(data));

        int size = data.length;

        // call quicksort() on array data
        Quicksort.quickSort(data, 0, size - 1);

        System.out.println("Sorted Array in Ascending Order: ");
        System.out.println(Arrays.toString(data));
    }
}

```

</details>


<details>
<summary>Python implementation</summary>

```python
# Python program for implementation of Quicksort Sort

# This implementation utilizes pivot as the last element in the nums list
# It has a pointer to keep track of the elements smaller than the pivot
# At the very end of partition() function, the pointer is swapped with the pivot
# to come up with a "sorted" nums relative to the pivot


# Function to find the partition position
def partition(array, low, high):

    # choose the rightmost element as pivot
    pivot = array[high]

    # pointer for greater element
    i = low - 1

    # traverse through all elements
    # compare each element with pivot
    for j in range(low, high):
        if array[j] <= pivot:

            # If element smaller than pivot is found
            # swap it with the greater element pointed by i
            i = i + 1

            # Swapping element at i with element at j
            (array[i], array[j]) = (array[j], array[i])

    # Swap the pivot element with the greater element specified by i
    (array[i + 1], array[high]) = (array[high], array[i + 1])

    # Return the position from where partition is done
    return i + 1

# function to perform quicksort


def quickSort(array, low, high):
    if low < high:

        # Find pivot element such that
        # element smaller than pivot are on the left
        # element greater than pivot are on the right
        pi = partition(array, low, high)

        # Recursive call on the left of pivot
        quickSort(array, low, pi - 1)

        # Recursive call on the right of pivot
        quickSort(array, pi + 1, high)


data = [1, 7, 4, 1, 10, 9, -2]
print("Unsorted Array")
print(data)

size = len(data)

quickSort(data, 0, size - 1)

print('Sorted Array in Ascending Order:')
print(data)
```

</details>
