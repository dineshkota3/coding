# Arrays & Matrix - Practice Problems

## Easy Problems

### 1. Two Sum
**LeetCode:** #1

**Description:**
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**
```
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

**Approach Hint:** Use a hash map to store seen elements and check for complement.

---

### 2. Best Time to Buy and Sell Stock
**LeetCode:** #121

**Description:**
You are given an array `prices` where `prices[i]` is the price of a given stock on the i-th day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

**Example:**
```
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy on day 1 (price = 1) and sell on day 4 (price = 6), profit = 6-1 = 5.
```

**Approach Hint:** Track minimum price seen so far and maximum profit.

---

### 3. Contains Duplicate
**LeetCode:** #217

**Description:**
Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

**Example:**
```
Input: nums = [1, 2, 3, 1]
Output: true
```

**Approach Hint:** Use a set to check for duplicates in O(n) time.

---

### 4. Maximum Subarray
**LeetCode:** #53

**Description:**
Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

**Example:**
```
Input: nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6
Explanation: The subarray [4, -1, 2, 1] has the largest sum 6.
```

**Approach Hint:** Use Kadane's algorithm - track current sum and maximum sum.

---

### 5. Move Zeros
**LeetCode:** #283

**Description:**
Given an integer array `nums`, move all 0's to the end of it while maintaining the relative order of the non-zero elements. Do this in-place without making a copy of the array.

**Example:**
```
Input: nums = [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]
```

**Approach Hint:** Use two pointers - one for current position, one for next non-zero position.

---

## Medium Problems

### 6. Product of Array Except Self
**LeetCode:** #238

**Description:**
Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

You must write an algorithm that runs in O(n) time and without using the division operation.

**Example:**
```
Input: nums = [1, 2, 3, 4]
Output: [24, 12, 8, 6]
```

**Approach Hint:** Two passes - compute left products, then multiply with right products.

---

### 7. Set Matrix Zeroes
**LeetCode:** #73

**Description:**
Given an m x n integer matrix, if an element is 0, set its entire row and column to 0's. You must do it in place.

**Example:**
```
Input: matrix = [[1, 1, 1], [1, 0, 1], [1, 1, 1]]
Output: [[1, 0, 1], [0, 0, 0], [1, 0, 1]]
```

**Approach Hint:** Use first row and column as markers to achieve O(1) space.

---

### 8. 3Sum
**LeetCode:** #15

**Description:**
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

The solution set must not contain duplicate triplets.

**Example:**
```
Input: nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
```

**Approach Hint:** Sort array, then use two pointers for each element.

---

### 9. 4Sum
**LeetCode:** #18

**Description:**
Given an array nums of n integers, return an array of all the unique quadruplets `[nums[a], nums[b], nums[c], nums[d]]` such that their sum equals target.

**Example:**
```
Input: nums = [1, 0, -1, 0, -2, 2], target = 0
Output: [[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]
```

**Approach Hint:** Sort and use two nested loops with two pointers.

---

### 10. Merge Intervals
**LeetCode:** #56

**Description:**
Given an array of intervals where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

**Example:**
```
Input: intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
Output: [[1, 6], [8, 10], [15, 18]]
```

**Approach Hint:** Sort by start time, then merge overlapping intervals.

---

## Hard Problems

### 11. Search a 2D Matrix II
**LeetCode:** #240

**Description:**
Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:
- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example:**
```
Input: matrix = [[1, 4, 7, 11], [2, 5, 8, 12], [3, 6, 9, 16], [10, 13, 14, 17]], target = 5
Output: true
```

**Approach Hint:** Start from top-right corner, eliminate row or column each step.

---

## Additional Practice

### Spiral Matrix (Medium) - #54
Traverse matrix in spiral order.

### Rotate Image (Medium) - #48
Rotate n x n matrix 90 degrees clockwise in-place.

### Container With Most Water (Medium) - #11
Find two lines that together with x-axis forms container holding most water.

### Sliding Window Maximum (Hard) - #239
Find the max in each sliding window of size k.

### First Missing Positive (Hard) - #41
Find the smallest missing positive integer.

### Trapping Rain Water (Hard) - #42
Compute how much water can be trapped after raining.

---

## Problem-Solving Tips

1. **Always clarify:**
   - Can the array be empty?
   - Can there be duplicates?
   - Is the array sorted?
   - What's the expected time/space complexity?

2. **Common optimizations:**
   - Two pointers for sorted arrays
   - Sliding window for contiguous subarrays
   - Hash map for O(1) lookups
   - Prefix sums for range queries

3. **Edge cases to consider:**
   - Empty array
   - Single element
   - All same elements
   - Negative numbers
   - Integer overflow
