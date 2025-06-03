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
8. [Pattern Decision Tree](#pattern-decision-tree)
9. [Quick Reference Summary](#quick-reference-summary)

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

that's why we initialize prefix = {0: 1} which means, before we started, we’ve already seen a sum of 0 exactly once.So this way we won't miss the subarray that starts at index 0.
```

---

## 📌 Dynamic Programming (DP)

### 💻 Code Example

```python
def longestCommonSubsequence(text1, text2):
    dp = [[0] * (len(text2) + 1) for _ in range(len(text1) + 1)]

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
dp = [0] * (n+1)
dp[0] = base_case
for i in range(1, n+1):
    dp[i] = ... # fill using relation
```

### 💡 Edge Cases

* Incorrect base cases cause full chain failure
* Index out of bounds (especially in top-down recursion)


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

* Find **maximum sum of a contiguous subarray**
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
        result.append(path[:])
        return
    for option in options:
        path.append(option)
        backtrack(path)
        path.pop()
```

### 💡 Edge Cases

* Forgetting to backtrack (`path.pop()`) = incorrect answers
* Duplicate paths (need sorting + skip conditions)


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
Graph or Tree?
├── Yes:
│   ├── Need shortest path? → BFS / Dijkstra
│   └── Need all paths/combinations? → DFS / Backtracking
└── No:
    ├── Is input sorted? → Two Pointers / Binary Search
    ├── Need subarray sum/max? → Prefix Sum / Sliding Window / Kadane
    └── Optimal decision chain? → Dynamic Programming
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
