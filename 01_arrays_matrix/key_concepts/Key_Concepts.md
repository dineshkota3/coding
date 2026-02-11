# Arrays & Matrix - Key Concepts to Master

## 1. Two Pointers Technique

### Opposite Ends Pattern
```python
# Two pointers moving towards each other
left, right = 0, len(arr) - 1
while left < right:
    # Process arr[left] and arr[right]
    left += 1
    right -= 1
```
**Use Cases:**
- Reverse array
- Two sum in sorted array
- Container with most water
- Palindrome validation

### Fast-Slow Pointers
```python
# Fast pointer moves twice as fast
slow = fast = 0
while fast < len(arr):
    slow += 1
    fast += 2
```
**Use Cases:**
- Remove duplicates in sorted array
- Cycle detection
- Find middle element

## 2. Sliding Window

### Fixed Size Window
```python
window_sum = sum(arr[:k])
for i in range(len(arr) - k):
    window_sum = window_sum - arr[i] + arr[i + k]
    # Process window_sum
```

### Variable Size Window
```python
left = 0
for right in range(len(arr)):
    # Expand window by adding arr[right]
    while condition_not_met:
        # Shrink window from left
        left += 1
```
**Use Cases:**
- Maximum/minimum subarray sum with size k
- Longest substring without repeating characters
- Minimum window substring

## 3. Matrix Rotation

### 90° Clockwise Rotation
```python
# Step 1: Transpose
for i in range(n):
    for j in range(i, n):
        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

# Step 2: Reverse each row
for row in matrix:
    row.reverse()
```

### 90° Counter-Clockwise Rotation
```python
# Step 1: Transpose
for i in range(n):
    for j in range(i, n):
        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

# Step 2: Reverse each column
matrix.reverse()
```

## 4. Spiral Matrix Traversal

```python
def spiral_order(matrix):
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1

    while top <= bottom and left <= right:
        # Traverse right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1

        # Traverse down
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1

        # Traverse left
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1

        # Traverse up
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1

    return result
```

## 5. Prefix Sums

```python
# Build prefix sum array
prefix = [0] * (len(arr) + 1)
for i in range(len(arr)):
    prefix[i + 1] = prefix[i] + arr[i]

# Query sum from index i to j (inclusive)
range_sum = prefix[j + 1] - prefix[i]
```
**Use Cases:**
- Range sum queries
- Subarray sum equals K
- Find pivot index

## 6. Kadane's Algorithm (Maximum Subarray)

```python
def max_subarray(nums):
    max_sum = current_sum = nums[0]
    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
    return max_sum
```
**Key Insight:** At each position, decide whether to:
- Start a new subarray at current element
- Extend the previous subarray

## 7. Merge Intervals Pattern

```python
def merge_intervals(intervals):
    if not intervals:
        return []

    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for current in intervals[1:]:
        if current[0] <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], current[1])
        else:
            merged.append(current)

    return merged
```

## Time Complexity Reference

| Operation | Time Complexity |
|-----------|----------------|
| Access by index | O(1) |
| Search (unsorted) | O(n) |
| Search (sorted) | O(log n) |
| Insert at end | O(1) amortized |
| Insert at beginning | O(n) |
| Delete | O(n) |
| Two pointers | O(n) |
| Sliding window | O(n) |

## Common Patterns Summary

1. **Two Pointers**: When array is sorted or you need to find pairs
2. **Sliding Window**: For subarray/substring problems with constraints
3. **Prefix Sums**: For range sum queries
4. **Kadane's**: For maximum/minimum subarray problems
5. **In-place**: When O(1) space is required
