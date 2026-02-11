# Sorting - Practice Problems

## Easy Problems

### 1. Sort Colors (Dutch National Flag)
**LeetCode:** #75

**Description:**
Given an array `nums` with n objects colored red, white, or blue (0, 1, 2), sort them in-place so that objects of the same color are adjacent.

**Example:**
```
Input: nums = [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
```

**Approach Hint:** Use three pointers (Dutch National Flag algorithm).

---

### 2. Merge Sorted Array
**LeetCode:** #88

**Description:**
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order. Merge them into a single array sorted in non-decreasing order.

**Example:**
```
Input: nums1 = [1, 2, 3, 0, 0, 0], m = 3, nums2 = [2, 5, 6], n = 3
Output: [1, 2, 2, 3, 5, 6]
```

**Approach Hint:** Merge from the end to avoid overwriting.

---

### 3. Relative Sort Array
**LeetCode:** #1122

**Description:**
Given two arrays `arr1` and `arr2`, sort the elements of `arr1` such that the relative ordering of items in `arr1` are the same as in `arr2`.

**Example:**
```
Input: arr1 = [2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 19], arr2 = [2, 1, 4, 3, 9, 6]
Output: [2, 2, 2, 1, 4, 3, 3, 9, 6, 7, 19]
```

**Approach Hint:** Use counting sort or custom comparator with index lookup.

---

## Medium Problems

### 4. Merge Intervals
**LeetCode:** #56

**Description:**
Given an array of intervals where `intervals[i] = [starti, endi]`, merge all overlapping intervals.

**Example:**
```
Input: intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
Output: [[1, 6], [8, 10], [15, 18]]
```

**Approach Hint:** Sort by start time, then merge.

---

### 5. Sort List
**LeetCode:** #148

**Description:**
Given the head of a linked list, return the list after sorting it in ascending order. Must be O(n log n) time.

**Example:**
```
Input: head = [4, 2, 1, 3]
Output: [1, 2, 3, 4]
```

**Approach Hint:** Use merge sort - find middle, sort halves, merge.

---

### 6. Largest Number
**LeetCode:** #179

**Description:**
Given a list of non-negative integers `nums`, arrange them such that they form the largest number.

**Example:**
```
Input: nums = [10, 2]
Output: "210"
```

**Approach Hint:** Custom comparator - compare a+b vs b+a.

---

### 7. Meeting Rooms II
**LeetCode:** #253

**Description:**
Given an array of meeting time intervals, find the minimum number of conference rooms required.

**Example:**
```
Input: intervals = [[0, 30], [5, 10], [15, 20]]
Output: 2
```

**Approach Hint:** Sort start and end times separately, use two pointers.

---

### 8. Wiggle Sort
**LeetCode:** #280

**Description:**
Given an unsorted array `nums`, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]...

**Example:**
```
Input: nums = [3, 5, 2, 1, 6, 4]
Output: [3, 5, 1, 6, 2, 4] (one possible answer)
```

**Approach Hint:** One pass - swap if condition not met at each position.

---

## Hard Problems

### 9. Pancake Sorting
**LeetCode:** #969

**Description:**
Given an array of distinct integers `arr`, sort the array using pancake flips. Return the k-values of flips.

**Example:**
```
Input: arr = [3, 2, 4, 1]
Output: [3, 4, 2, 3, 1, 2]
```

**Approach Hint:** Bring largest to front, then flip to end.

---

## Additional Practice

### Intersection of Two Arrays (Easy) - #349
Find intersection using sorting or hash set.

### Valid Anagram (Easy) - #242
Check if two strings are anagrams by sorting.

### Height Checker (Easy) - #1051
Count students out of place after sorting.

### Sort Characters By Frequency (Medium) - #451
Sort characters by frequency.

### Top K Frequent Elements (Medium) - #347
Find k most frequent elements using heap or bucket sort.

### Kth Largest Element (Medium) - #215
Find kth largest using quick select or heap.

### Sort Array by Parity (Medium) - #922
Sort array by parity (even at even index, odd at odd index).

### Reorganize String (Medium) - #767
Rearrange string so no adjacent characters are same.

---

## Problem-Solving Tips

1. **Pre-processing with sorting:**
   - Many problems become easier after sorting
   - Sort + two pointers is a common pattern
   - Consider sorting by different keys

2. **Custom sorting:**
   - Use `key` parameter for simple transformations
   - Use `cmp_to_key` for complex comparisons
   - Sort by multiple keys: `key=lambda x: (x[0], -x[1])`

3. **In-place sorting:**
   - Use list.sort() instead of sorted() for in-place
   - Be careful with indices and pointers

4. **Common patterns:**
   - Sort + two pointers (3Sum, merge)
   - Sort + binary search
   - Sort + greedy
   - Bucket sort for frequency problems
