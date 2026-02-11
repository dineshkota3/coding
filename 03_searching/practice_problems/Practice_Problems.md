# Searching - Practice Problems

## Easy Problems

### 1. Binary Search
**LeetCode:** #704

**Description:**
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, return its index. Otherwise, return -1.

**Example:**
```
Input: nums = [-1, 0, 3, 5, 9, 12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Approach Hint:** Implement standard binary search.

---

### 2. Search Insert Position
**LeetCode:** #35

**Description:**
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if inserted in order.

**Example:**
```
Input: nums = [1, 3, 5, 6], target = 5
Output: 2
```

**Approach Hint:** Use lower bound to find insertion position.

---

### 3. First Bad Version
**LeetCode:** #278

**Description:**
You are a product manager and currently leading a team to develop a new product. Since each version is developed based on the previous version, all the versions after a bad version are also bad. Find the first bad version.

**Example:**
```
Input: n = 5, bad = 4
Output: 4
Explanation: First bad version is 4.
```

**Approach Hint:** Binary search to find first version where isBadVersion returns true.

---

### 4. Sqrt(x)
**LeetCode:** #69

**Description:**
Given a non-negative integer x, compute and return the square root of x. Return the floor of the square root.

**Example:**
```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.828..., floor is 2.
```

**Approach Hint:** Binary search on answer from 0 to x.

---

## Medium Problems

### 5. Search in Rotated Sorted Array
**LeetCode:** #33

**Description:**
There is an integer array `nums` sorted in ascending order (with distinct values). Given the array after rotation, find the index of target.

**Example:**
```
Input: nums = [4, 5, 6, 7, 0, 1, 2], target = 0
Output: 4
```

**Approach Hint:** Determine which half is sorted, then check if target is in that half.

---

### 6. Find Minimum in Rotated Sorted Array
**LeetCode:** #153

**Description:**
Given the sorted rotated array `nums` of unique elements, return the minimum element of this array.

**Example:**
```
Input: nums = [3, 4, 5, 1, 2]
Output: 1
```

**Approach Hint:** Compare mid with right to determine which half has minimum.

---

### 7. Search a 2D Matrix
**LeetCode:** #74

**Description:**
Write an efficient algorithm that searches for a value `target` in an m x n integer matrix. Integers in each row are sorted from left to right. The first integer of each row is greater than the last integer of the previous row.

**Example:**
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

**Approach Hint:** Treat as 1D sorted array, use binary search with index conversion.

---

### 8. Find Peak Element
**LeetCode:** #162

**Description:**
A peak element is an element that is strictly greater than its neighbors. Given an integer array `nums`, find a peak element, and return its index.

**Example:**
```
Input: nums = [1, 2, 3, 1]
Output: 2
Explanation: 3 is a peak element at index 2.
```

**Approach Hint:** Binary search - if mid < mid+1, peak is on right, else on left.

---

## Hard Problems

### 9. Median of Two Sorted Arrays
**LeetCode:** #4

**Description:**
Given two sorted arrays `nums1` and `nums2`, return the median of the two sorted arrays.

**Example:**
```
Input: nums1 = [1, 3], nums2 = [2]
Output: 2.0
Explanation: merged array = [1, 2, 3] and median is 2.0
```

**Approach Hint:** Binary search on smaller array to find correct partition.

---

## Additional Practice

### Guess Number Higher or Lower (Easy) - #374
Use binary search to find the picked number.

### Arranging Coins (Easy) - #441
Find maximum number of complete rows with n coins.

### Find Smallest Letter Greater Than Target (Easy) - #744
Find smallest character greater than target.

### Search in Rotated Sorted Array II (Medium) - #81
Search in rotated array with duplicates.

### Find First and Last Position (Medium) - #34
Find starting and ending position of target.

### Time Based Key-Value Store (Medium) - #981
Design time-based key-value store using binary search.

### Find Right Interval (Medium) - #436
Find right interval for each interval.

### Split Array Largest Sum (Hard) - #410
Split array into m subarrays to minimize largest sum.

### Find Minimum in Rotated Sorted Array II (Hard) - #154
Find minimum with duplicates.

---

## Problem-Solving Tips

1. **When to use binary search:**
   - Array is sorted (or partially sorted)
   - Looking for optimal value with monotonic property
   - Need to find position/boundary

2. **Common patterns:**
   - `left <= right`: Find exact element
   - `left < right`: Find boundary/minimum/maximum
   - Save result and continue: Find first/last occurrence

3. **Edge cases:**
   - Empty array
   - Single element
   - Target at boundaries
   - All same elements
   - Duplicates

4. **Binary search on answer:**
   - Identify monotonic property
   - Define condition function
   - Search for minimum/maximum satisfying condition
