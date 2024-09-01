## Binary Search
---

## About
- Binary search is a fast search algorithm with run-time complexity of Ο(log n). 
- This search algorithm works on the principle of divide and conquer. 
- For this algorithm to work properly, the data collection should be in the sorted form.

## Binary Search Implemenation

<details>
<summary>
Java Implementation
</summary>

```java
package tests;

//Binary search is a fast search algorithm with run-time complexity of Ο(log n). 
//This search algorithm works on the principle of divide and conquer. 
//For this algorithm to work properly, the data collection should be in the sorted form.
//it should be sorted Arrays.sort(arr)
//iterative case
// Java implementation of iterative Binary Search
class BinarySearch {
    // Returns index of x if it is present in arr[],
    // else return -1
    int binarySearch(int[] arr, int x)
    {
        int first = 0, last = arr.length - 1;
        while (first <= last) {
            int m = first + (last - first) / 2;

            // Check if x is present at mid
            if (arr[m] == x)
                return m;

            // If x greater, ignore left half
            if (arr[m] < x)
                first = m + 1;

                // If x is smaller, ignore right half
            else
                last = m - 1;
        }

        // if we reach here, then element was
        // not present
        return -1;
    }

    // Driver method to test above
    public static void main(String[] args)
    {
        BinarySearch ob = new BinarySearch();
        int[] arr = {2,5,7,8,9,12};
        int n = arr.length;
        int x = 8;
        int result = ob.binarySearch(arr, x);
        if (result == -1)
            System.out.println("Element not present");
        else
            System.out.println("Element found at "
                    + "index " + result);
    }
}


//recursive case
class BinarySearchExample1{  
    public static int binarySearch(int arr[], int first, int last, int key){  
        if (last>=first){  
            int mid = first + (last - first)/2;  
            if (arr[mid] == key){  
            return mid;  
            }  
            if (arr[mid] > key){  
            return binarySearch(arr, first, mid-1, key);//search in left subarray  
            }else{  
            return binarySearch(arr, mid+1, last, key);//search in right subarray  
            }  
        }  
        return -1;  
    }  
    public static void main(String args[]){  
        int arr[] = {10,20,30,40,50};  
        int key = 30;  
        int last=arr.length-1;  
        int result = binarySearch(arr,0,last,key);  
        if (result == -1)  
            System.out.println("Element is not found!");  
        else  
            System.out.println("Element is found at index: "+result);  
    }  
}  
```
</details>


<details>
<summary>
Python Implementation
</summary>

```python
# Python 3 program for recursive binary search.
# Modifications needed for the older Python 2 are found in comments.

# Returns index of x in arr if present, else -1
def binary_search(arr, low, high, x):

	# Check base case
	if high >= low:

		mid = (high + low) // 2

		# If element is present at the middle itself
		if arr[mid] == x:
			return mid

		# If element is smaller than mid, then it can only
		# be present in left subarray
		elif arr[mid] > x:
			return binary_search(arr, low, mid - 1, x)

		# Else the element can only be present in right subarray
		else:
			return binary_search(arr, mid + 1, high, x)

	else:
		# Element is not present in the array
		return -1

# Test array
arr = [ 2, 3, 4, 10, 40 ]
x = 10

# Function call
result = binary_search(arr, 0, len(arr)-1, x)

if result != -1:
	print("Element is present at index", str(result))
else:
	print("Element is not present in array")

```
</details>



## Binary search templates:

1- normal binary search

2- advanced binary search (It is used to search for an element or condition which requires accessing the current index and its immediate right neighbor's index in the array):
```
  int left = 0, right = nums.length;
  while(left < right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid; }
  }
   // Post-processing:
  // End Condition: left == right
  if(left != nums.length && nums[left] == target) return left;
  return -1;
  ```
  Search left => right = mid
  
  search right => left = mid + 1
  
  termination => left = right
  
  left = mid + 1, means that we can add the target at that index
  right = mid means that the target can be equal to the right
  (we need to calculate it to choose which version)
  if you do right = mid then you have to do left < right and you have to do post processing because there is one element not searched.
  Use this method when you want to access the immediate right index.
  
  3- It is used to search for an element or condition which requires accessing the current index and its immediate left and right neighbor's index in the array.
  ```
  int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0)
        return -1;

    int left = 0, right = nums.length - 1;
    while (left + 1 < right){
        // Prevent (left + right) overflow
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }

    // Post-processing:
    // End Condition: left + 1 == right
    if(nums[left] == target) return left;
    if(nums[right] == target) return right;
    return -1;
}
```

- if return -1 then use first <= last else use first < last. Usually in rotated sorted array we use first < last
## Template 1:
- normal binary search (first <= last), therefore when you get out there wont be any elements (left = mid + 1 and right = mid - 1)

## Template 2:
- advanced binary search (first < last), use it when you care about your right neighbor (left = mid + 1 and right = mid) and in post processing just return right

## Template 3:
- advanced binary search (first < last) use it when you care about both right and left neighbor (left = mid and right = mid) in post processing check both right and left

