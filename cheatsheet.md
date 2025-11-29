# 🧠 Coding Interview Patterns & Algorithms Cheatsheet

This cheatsheet summarizes core algorithmic patterns, when to use them, how they look in Python — with examples, common code lines, edge cases, and LeetCode links for practice.

---

## 📚 Table of Contents

1. [Sliding Window](#sliding-window)
2. [Prefix Sum](#prefix-sum)
3. [Dynamic Programming (DP)](#dynamic-programming-dp)
4. [Kadane's Algorithm](#kadanes-algorithm)
5. [Heap (Priority Queue)](#heap-priority-queue)
6. [Backtracking](#backtracking)
7. [Dijkstra’s Algorithm](#dijkstras-algorithm)
8. [Merge Sort](#merge-sort)
9. [Pattern Decision Tree](#pattern-decision-tree)
10. [Quick Reference Summary](#quick-reference-summary)

---

## 📌 Sliding Window

### 💻 Code Example

```python
def lengthOfLongestSubstring(s):
    left = 0
    window = {}
    max_len = 0

    for right in range(len(s)):
        char = s[right]
        if char in window and window[char] >= left:
            left = window[char] + 1
        window[char] = right
        max_len = max(max_len, right - left + 1)

    return max_len
```

### Explanation

The core idea of the algorithm, is to think that you have a window size and you need to be shrinking/expanding the size usually from the left. To give an example, you need to find the max average subarray that would be of length k, so immediately we know that the window size needs to be equal to `k`. So if we have the following:

```
[1,12,-5,-6,50,3], k = 4
```
And we would be setting the left to `0`, looping and then getting the window size which would be `right - left + 1`. So now the goal is to get the max avg with length k, so we need to calculate max. We would have the following in each loop:

```
##step 0
res = float('-inf')
curr = 1
window_size = 1 (0 - 0 + 1)

## step 1
res = float('-inf')
curr = 13
window_size = 2 (1 - 0 + 1)

## step 2
res = float('-inf')
curr = 8
window_size = 2 (1 - 0 + 1)

## step 3
res = float('-inf')
curr = 2
window_size = 3 (2 - 0 + 1)

## step 4
res = 0.5 (2/4)
curr = 2
window_size = 4 (3 - 0 + 1)
## here window size is 4 so we calculate max, since we need to keep iterating we use the max() function to keep track of the maximum avg subarray
## now we remove the first element form the current sum by doing curr -= nums[left] and left here is still 0 so we increment left to keep the window size same as `k` so `left+=1` and now `curr` is equal to `1`

## step 5
res = 12.75 (51/4)
curr = 51
window_size = 4 (4 - 1 + 1)
## again max is calculated here and stored to `res`, then again we remove `left` from the current sum and increment it once and keep going until we have iterated in the whole array.
```

#### Note

* `float('-inf')` Negative infinity
* `float('inf')` Positive infinity
* to convert a number to a float do `float(num)`, that's needed to get the correct decimal answer if using python 2

### 🔍 When to Use

* Process **contiguous subarrays/substrings** efficiently
* Common in max/min problems, frequency counts, anagrams
* doesn't work if negative value exists in the array

### 🧠 Core Lines You'll Always Write

```python
window_map = {}
left = 0
for right in range(len(s)):
    # add to window
    # shrink window if needed
```

### 💡 Edge Cases

* Window expands but never shrinks → can lead to overflow
* Right pointer reaches end, but left logic doesn’t catch up
  

### 🧪 Example Problem

* [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

## 📌 Prefix Sum

### 💻 Code Example

```python
def subarraySum(nums, k):
    count = 0
    prefix = {0: 1}
    total = 0

    for num in nums:
        total += num
        count += prefix.get(total - k, 0)
        prefix[total] = prefix.get(total, 0) + 1

    return count
```

### 🔍 When to Use

* Fast O(1) range sum lookups after O(n) pre-processing
* prefix sum calculation: prefix[i+1] = prefix[i] + nums[i]


### Notes

* you need to first be looping and getting the total sum
* then ask yourself have I ever seen a total sum that is `total - k`
* prefix = {0: 1} track all the prefix sum already seen
* If `total - k` exists in the hashmap, that means there’s a subarray ending at current index that sums to k, so add that to the hashmap.

#### Example

| Step | num | total | total - k | count | prefix                          |
|------|-----|-------|------------|--------|----------------------------------|
| 1    | 1   | 1     | -2         | 0      | {0:1, 1:1}                      |
| 2    | 2   | 3     | 0          | 1      | {0:1, 1:1, 3:1}                 |
| 3    | 3   | 6     | 3          | 2      | {0:1, 1:1, 3:1, 6:1}            |

nums = [1, 2, 3]
k = 3

### 🧠 Core Lines You'll Always Write

```python
prefix = [0]
for num in nums:
    prefix.append(prefix[-1] + num)
```

### 💡 Edge Cases

* Don't forget prefix starts at 0
* Watch off-by-one when using slice index j-i

### 🧪 Example Problem

* [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

One question also might be to find all subarray that have a sum divisible by `k`, in that case you can use modolus: `mod = (total % k + k) % k`

### Why it's necessary

* it makes the algorithm efficient by giving O(n) time complexity, if you don't use it then you need to brute force:

```python
def numSubarraysWithSum(nums, goal):
    count = 0
    for start in range(len(nums)):
        total = 0
        for end in range(start, len(nums)):
            total += nums[end]
            if total == goal:
                count += 1
    return count
```

So with prefix sum instead of calculating sum of each subarray from scratch, you track a running total (total). `start_total = total - goal`. For example:

```
[1,0,1] goal = 2 we need to find how many subarray that gives sum=2.

[0,1,1,2] is the prefix sum

step 1:

i = 0 / total = 1 / (total - goal) => 1-2 = -1 

step 2:

i = 1 / total = 1 / (total - goal) => 1-2 = -1

step 3

i = 2 / total = 2 / (total - goal) => 2-2 = 0 => 1 (so 0 would be equal to the base case which is 1)

that's why we initialize prefix = {0: 1} which means, before we started, we’ve already seen a sum of 0 exactly once. So this way we won't miss the subarray that starts at index 0.
```

---

## 📌 Dynamic Programming (DP)

Dynamic Programming is an optimization technique used to solve overlapping subproblems with optimal substructure, by storing intermediate results (memoization or tabulation) to avoid redundant work.

### 💻 Code Example

```python
def longestCommonSubsequence(text1, text2):
    dp = [[0] * (len(text2) + 1) for _ in range(len(text1) + 1)] ## creates a 2d array

    for i in range(1, len(text1) + 1):
        for j in range(1, len(text2) + 1):
            if text1[i - 1] == text2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    return dp[-1][-1]
```

### 🔍 When to Use

* When solution to a problem depends on **solutions to subproblems**
* Look for:
  * Optimal values (max/min/ways)
  * Recurrence relation (`dp[i] = dp[i-1] + dp[i-2]`)

### 🧠 Core Lines You'll Always Write

```python
dp = [0] * (n+1) ## this creates a list with 0s with size n+1
dp[0] = base_case
for i in range(1, n+1):
    dp[i] = ... # fill using relation
```

### 💡 Edge Cases

* Incorrect base cases cause full chain failure
* Index out of bounds (especially in top-down recursion)
* Not caching subproblem results → leads to TLE (time limit exceeded)

### 🔁 Types of DP

#### 1. Top-Down (Memoization)
- Recursive approach with caching
- Easy to write and understand
- Uses a hash map or `@lru_cache`

#### 2. Bottom-Up (Tabulation)
- Iterative approach
- Usually more efficient
- Builds from base case up

### 📘 Top-Down Template (with Memoization)

```python
memo = {}
def dp(i):
    if i in memo:
        return memo[i]
    if base_case:
        return ...
    memo[i] = combine(dp(i-1), dp(i-2))
    return memo[i]
```

### 📘 Bottom-Up Template (Tabulation)

```python
dp = [0] * (n + 1)
dp[0] = base_value

for i in range(1, n + 1):
    dp[i] = combine(dp[i-1], dp[i-2], ...)
```


### 🧪 Example Problem

* [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

---

## 📌 Kadane's Algorithm

### 💻 Code Example

```python
def maxSubArray(nums):
    max_sum = current = nums[0]
    for num in nums[1:]:
        current = max(num, current + num)
        max_sum = max(max_sum, current)
    return max_sum
```

### 🔍 When to Use

* Kadane’s Algorithm is used to find the maximum sum of a contiguous subarray within a 1D array of integers.
* Elegant linear-time DP trick

### 🧠 Core Lines You'll Always Write

```python
current = max_sum = nums[0]
for num in nums[1:]:
    current = max(num, current + num)
    max_sum = max(max_sum, current)
```

### 💡 Edge Cases

* All numbers negative: algorithm still works due to init
* Empty array? Return 0 or handle upfront

### 🧪 Example Problem

* [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

---

## 📌 Heap (Priority Queue)

### 💻 Code Example

```python
import heapq

def findKthLargest(nums, k):
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    return heapq.heappop(heap)
```

### Notes

* A **heap** is a **complete binary tree** used to efficiently get the **min or max** element.
* Commonly implemented using an **array**.
* It satisfies the **heap property**:
  - **Min-heap**: parent ≤ children → root is smallest
  - **Max-heap**: parent ≥ children → root is largest

* Python’s `heapq` is a min-heap by default
* To simulate a max-heap: store -x instead of x
* Operations:
    - `heapq.heappush(heap, x)` → O(log n) => pushes element to the heap
    - `heapq.heappop(heap)` → O(log n) => removes the smallest element in the heap in a min-heap
    - `heapq.heapify(list)` → O(n) => first you need to heapify the list
    - `heap[0]` -> in case you have a list called `heap` that is heapified then `heap[0]` would always have the smallest element

### 🔍 When to Use

* Efficiently fetch min/max in log time
* Common in scheduling, live-ranking, stream medians

### 🧠 Core Lines You'll Always Write

```python
import heapq
heapq.heappush(heap, item)
heapq.heappop(heap)
```

### 💡 Edge Cases

* For max heap use: `heapq.heappush(heap, -item)`
* Don't forget to pop before checking size limit (Top K)


### 🧪 Example Problem

* [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

---

## 📌 Backtracking

Backtracking = "Try a decision, go deeper, undo it, try next decision."

You build a solution incrementally, one piece at a time, and:
* If a partial solution is invalid or complete, you return (backtrack).
* Otherwise, recurse deeper by choosing the next option.

### 💻 Code Example

```python
def combinationSum(candidates, target):
    result = []

    def dfs(path, start, total):
        if total == target:
            result.append(path[:])
            return
        if total > target:
            return

        for i in range(start, len(candidates)):
            path.append(candidates[i])
            dfs(path, i, total + candidates[i])
            path.pop()

    dfs([], 0, 0)
    return result
```

### 🔍 When to Use

* Explore **all possible combinations** with pruning
* Great for permutations, subset generation, puzzles

### 🧠 Core Lines You'll Always Write

```python
def backtrack(path):
    if base_case:
        result.append(path[:]) ## copies list path to result
        return
    for option in options:
        path.append(option)
        backtrack(path)
        path.pop()
```

## Notes

* in python `a_list.append(a_dict)` → store a reference to `a_dict`, so if `a_dict` changes then also `a_list` changes. That's why you use `path[:]` to create a new list object in the heap with the same contents.

### 💡 Edge Cases

* Forgetting to backtrack (`path.pop()`) = incorrect answers
* Duplicate paths (need sorting + skip conditions)

## Example

If you are given:

Input: `s = "3z4"`
Output: `["3z4","3Z4"]`

You need to find all combination of the string `s`. In this case you need to backtrack to get all combinations, you can first think about it as a tree:

Backtracking Tree for Input: "3z4"

```
"" (index = 0)
└── "3" (index = 1)
    ├── "3z" (index = 2)
    │   └── "3z4" (index = 3) ✅ add to result
    └── "3Z" (index = 2)
        └── "3Z4" (index = 3) ✅ add to result

```
So here you need to be building the strings to add in the array, so the base case would be if the string that is build is same size as the original string then add to result and return. Then in the loop you backtrack and you add either lowercase, uppercase or digit to the string. You would have the following call stack:

```
dfs("", 0)
└── dfs("3", 1)         # '3' is digit → one path only
    ├── dfs("3Z", 2)    # 'z' → uppercase
    │   └── dfs("3Z4", 3) ✅ base case → add "3Z4"
    └── dfs("3z", 2)    # 'z' → lowercase
        └── dfs("3z4", 3) ✅ base case → add "3z4"

```


### 🧪 Example Problem

* [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

---

## 📌 Dijkstra’s Algorithm

### 💻 Code Example

```python
import heapq

def dijkstra(graph, start):
    heap = [(0, start)]
    dist = {node: float('inf') for node in graph}
    dist[start] = 0

    while heap:
        d, node = heapq.heappop(heap)
        for neighbor, weight in graph[node]:
            if d + weight < dist[neighbor]:
                dist[neighbor] = d + weight
                heapq.heappush(heap, (dist[neighbor], neighbor))

    return dist
```

### 🔍 When to Use

* **Shortest path** in a **weighted graph** with **non-negative weights**

### 🧠 Core Lines You'll Always Write

```python
heap = [(0, start)]
dist = {node: inf for node in graph}
dist[start] = 0

while heap:
    d, node = heappop(heap)
    for neighbor, weight in graph[node]:
        if d + weight < dist[neighbor]:
            dist[neighbor] = d + weight
            heappush(heap, (dist[neighbor], neighbor))
```

### 💡 Edge Cases

* Negative weights → Use Bellman-Ford instead
* Make sure not to reprocess outdated paths

### 🧪 Example Problem

* [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)

---

## 📌 Merge Sort

### 💻 Code Example

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result += left[i:]
    result += right[j:]
    return result
```

### 🔍 When to Use

* You need a **stable sort** in O(n log n)
* You’re solving a problem that requires **sorting + counting** (e.g., inversions)

### 🧠 Core Lines You'll Always Write

```python
mid = len(arr) // 2
left = merge_sort(arr[:mid])
right = merge_sort(arr[mid:])
return merge(left, right)
```

### 💡 Edge Cases

* Always return the **merged array** to avoid None
* Don’t modify the original array in-place unless asked

### 🎞 Visual

[Merge Sort Visual](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)

### 🧪 Example Problem

* [912. Sort an Array](https://leetcode.com/problems/sort-an-array/)

## 📌 Pattern Decision Tree

```text
Problem involves a Graph or Tree?
├── Yes:
│   ├── Unweighted shortest path? → BFS
│   ├── Weighted shortest path? → Dijkstra / Bellman-Ford / A*
│   ├── Need all paths, traversals, or recursion? → DFS
│   ├── Need to build combinations or choices in a tree? → Backtracking
│   ├── Topological ordering? → Kahn’s Algorithm / DFS with stack
│   ├── Cycle detection? → DFS with visited + stack or Union Find
│   └── Is it a Tree? → Recursive DFS / BFS / Binary Tree patterns

└── No:
    ├── Is input sorted or can be sorted?
    │   ├── Yes:
    │   │   ├── Searching a value? → Binary Search
    │   │   ├── Find pair/triplet with condition? → Two Pointers / Sliding Window
    │   │   └── Count comparisons / inversions? → Merge Sort
    │   └── No:
    │       ├── Can sorting help? → Try sorting first, then two pointers or greedy

    ├── Need to process every contiguous window/subarray?
    │   ├── Fixed size? → Sliding Window
    │   └── Variable size / max/min range? → Sliding Window + HashMap / Deque

    ├── Need prefix sums, range sum, or frequency tracking?
    │   ├── Sum of subarrays or ranges? → Prefix Sum / HashMap
    │   └── Frequency maps / counts? → HashMap + Prefix / Sliding Window

    ├── Need to track maximum/minimum efficiently?
    │   ├── Kth largest / median / streaming? → Heap (Priority Queue)
    │   └── With indexes/sliding range? → Monotonic Queue

    ├── Need optimal value or number of ways to reach a goal?
    │   └── Dynamic Programming
    │       ├── Overlapping subproblems? → Memoization (Top-down)
    │       └── Tabulation possible? → Bottom-up DP

    ├── Need to generate all combinations / subsets / permutations?
    │   └── Backtracking / DFS

    ├── Array with max sum / product / condition?
    │   └── Kadane's Algorithm / Greedy / DP

    ├── Need to merge, sort, or partition?
    │   ├── Sorting problem? → Merge Sort / Quick Sort
    │   └── Median or K-th element? → QuickSelect

    ├── Need to manage disjoint sets or components?
    │   └── Union-Find / DSU (Disjoint Set Union)

    ├── Repeated patterns / cyclic / modulo math?
    │   └── Hashing + Modulo / Cycle detection

    ├── Optimizing a greedy choice? → Greedy Algorithm
    │   ├── Intervals, scheduling, coin change, etc.

    ├── Need to search over a result or range space?
    │   └── Binary Search on Answer

    ├── Simulating constraints / time or space step-by-step?
    │   └── Brute Force / BFS / Simulation / Queue

    ├── Need to compress or encode efficiently?
    │   └── Huffman Encoding / Trie

    └── Pattern in strings or substrings?
        ├── Pattern search? → KMP / Rabin-Karp
        └── Palindromes, repeats, anagrams? → Sliding Window / HashMap / DP

```

---

## 📌 Quick Reference Summary

| Pattern        | Time Complexity   | Space Complexity | Common Use Case                    |
| -------------- | ----------------- | ---------------- | ---------------------------------- |
| Sliding Window | O(n)              | O(k)             | Substrings, max/min ranges         |
| Prefix Sum     | O(n) + O(1) query | O(n)             | Range sum / difference queries     |
| DP             | O(n²)             | O(n)             | Optimal value over choices         |
| Kadane         | O(n)              | O(1)             | Max subarray sum                   |
| Heap           | O(log n) ops      | O(n)             | Top-K, real-time min/max           |
| Backtracking   | Exponential       | O(n)             | Permutations, combinations         |
| Dijkstra       | O(E log V)        | O(V)             | Shortest path in weighted graph    |
| Merge Sort     | O(n log n)        | O(n)             | Stable sorting, inversion counting |
