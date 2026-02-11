# Arrays & Matrix - Algorithms to Learn

## 1. Two Sum (Hash Map Approach)

### Problem
Given an array of integers and a target sum, return indices of two numbers that add up to target.

### Algorithm
```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

### Key Insight
Trade space for time by using hash map to store seen elements.

---

## 2. Maximum Subarray (Kadane's Algorithm)

### Problem
Find the contiguous subarray with the largest sum.

### Algorithm
```python
def max_subarray(nums):
    max_sum = current_sum = nums[0]
    start = end = temp_start = 0

    for i in range(1, len(nums)):
        if nums[i] > current_sum + nums[i]:
            current_sum = nums[i]
            temp_start = i
        else:
            current_sum += nums[i]

        if current_sum > max_sum:
            max_sum = current_sum
            start = temp_start
            end = i

    return max_sum
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

### Key Insight
At each position, decide whether to start fresh or extend previous subarray.

---

## 3. Merge Intervals

### Problem
Merge all overlapping intervals.

### Algorithm
```python
def merge_intervals(intervals):
    if not intervals:
        return []

    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for current in intervals[1:]:
        # Overlapping intervals
        if current[0] <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], current[1])
        else:
            merged.append(current)

    return merged
```

### Complexity
- **Time:** O(n log n) for sorting
- **Space:** O(n) for result

### Key Insight
Sort by start time, then merge overlapping intervals greedily.

---

## 4. Rotate Matrix (90 Degrees)

### Problem
Rotate an n x n matrix 90 degrees clockwise in-place.

### Algorithm
```python
def rotate_matrix(matrix):
    n = len(matrix)

    # Step 1: Transpose
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

    # Step 2: Reverse each row
    for row in matrix:
        row.reverse()

    return matrix
```

### Complexity
- **Time:** O(n²)
- **Space:** O(1)

### Key Insight
Transpose + reverse rows = 90° clockwise rotation.

---

## 5. Spiral Matrix Traversal

### Problem
Traverse matrix in spiral order.

### Algorithm
```python
def spiral_order(matrix):
    if not matrix:
        return []

    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1

    while top <= bottom and left <= right:
        # Right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1

        # Down
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1

        # Left
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1

        # Up
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1

    return result
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(1) excluding result

---

## 6. Sliding Window Maximum

### Problem
Find maximum in each sliding window of size k.

### Algorithm (Using Deque)
```python
from collections import deque

def max_sliding_window(nums, k):
    result = []
    dq = deque()  # Stores indices

    for i, num in enumerate(nums):
        # Remove indices outside window
        while dq and dq[0] < i - k + 1:
            dq.popleft()

        # Remove smaller elements
        while dq and nums[dq[-1]] < num:
            dq.pop()

        dq.append(i)

        if i >= k - 1:
            result.append(nums[dq[0]])

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(k)

### Key Insight
Maintain a decreasing deque - front always has maximum.

---

## 7. Container With Most Water

### Problem
Find two lines that form container holding most water.

### Algorithm
```python
def max_area(height):
    left, right = 0, len(height) - 1
    max_water = 0

    while left < right:
        width = right - left
        container_height = min(height[left], height[right])
        max_water = max(max_water, width * container_height)

        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_water
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

### Key Insight
Move pointer with smaller height - only way to potentially increase area.

---

## 8. Product of Array Except Self

### Problem
Return array where each element is product of all other elements.

### Algorithm
```python
def product_except_self(nums):
    n = len(nums)
    result = [1] * n

    # Left products
    left_product = 1
    for i in range(n):
        result[i] = left_product
        left_product *= nums[i]

    # Right products
    right_product = 1
    for i in range(n - 1, -1, -1):
        result[i] *= right_product
        right_product *= nums[i]

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) excluding output

### Key Insight
Two passes: left products and right products, multiply together.

---

## 9. Find Minimum in Rotated Sorted Array

### Problem
Find minimum in a rotated sorted array.

### Algorithm
```python
def find_min(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2

        if nums[mid] > nums[right]:
            left = mid + 1
        else:
            right = mid

    return nums[left]
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

### Key Insight
Compare mid with right to determine which half has minimum.

---

## 10. Search in 2D Matrix

### Problem
Search for target in sorted 2D matrix (row and column sorted).

### Algorithm
```python
def search_matrix(matrix, target):
    if not matrix or not matrix[0]:
        return False

    rows, cols = len(matrix), len(matrix[0])
    row, col = 0, cols - 1  # Start from top-right

    while row < rows and col >= 0:
        if matrix[row][col] == target:
            return True
        elif matrix[row][col] < target:
            row += 1
        else:
            col -= 1

    return False
```

### Complexity
- **Time:** O(m + n)
- **Space:** O(1)

### Key Insight
Start from top-right corner, eliminate row or column each step.

---

## 11. Trapping Rain Water

### Problem
Calculate how much rainwater can be trapped.

### Algorithm
```python
def trap(height):
    if not height:
        return 0

    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    water = 0

    while left < right:
        if left_max < right_max:
            left += 1
            left_max = max(left_max, height[left])
            water += left_max - height[left]
        else:
            right -= 1
            right_max = max(right_max, height[right])
            water += right_max - height[right]

    return water
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 12. 3Sum

### Problem
Find all unique triplets that sum to zero.

### Algorithm
```python
def three_sum(nums):
    nums.sort()
    result = []
    n = len(nums)

    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        left, right = i + 1, n - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]

            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1

    return result
```

### Complexity
- **Time:** O(n²)
- **Space:** O(1)

---

## 13. 4Sum

### Problem
Find all unique quadruplets that sum to target.

### Algorithm
```python
def four_sum(nums, target):
    nums.sort()
    result = []
    n = len(nums)

    for i in range(n - 3):
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        for j in range(i + 1, n - 2):
            if j > i + 1 and nums[j] == nums[j - 1]:
                continue

            left, right = j + 1, n - 1
            while left < right:
                total = nums[i] + nums[j] + nums[left] + nums[right]

                if total < target:
                    left += 1
                elif total > target:
                    right -= 1
                else:
                    result.append([nums[i], nums[j], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    left += 1
                    right -= 1

    return result
```

### Complexity
- **Time:** O(n³)
- **Space:** O(1)

---

## 14. Set Matrix Zeroes

### Problem
Set entire row and column to zero if element is zero.

### Algorithm
```python
def set_zeroes(matrix):
    rows, cols = len(matrix), len(matrix[0])
    first_row_zero = any(matrix[0][j] == 0 for j in range(cols))
    first_col_zero = any(matrix[i][0] == 0 for i in range(rows))

    # Use first row and column as markers
    for i in range(1, rows):
        for j in range(1, cols):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0

    # Set zeroes based on markers
    for i in range(1, rows):
        for j in range(1, cols):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0

    # Handle first row and column
    if first_row_zero:
        for j in range(cols):
            matrix[0][j] = 0
    if first_col_zero:
        for i in range(rows):
            matrix[i][0] = 0
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(1)

---

## 15. Longest Consecutive Sequence

### Problem
Find length of longest consecutive elements sequence.

### Algorithm
```python
def longest_consecutive(nums):
    num_set = set(nums)
    longest = 0

    for num in num_set:
        if num - 1 not in num_set:  # Start of sequence
            current = num
            streak = 1

            while current + 1 in num_set:
                current += 1
                streak += 1

            longest = max(longest, streak)

    return longest
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 16. Subarray Sum Equals K

### Problem
Find total number of continuous subarrays with sum equal to k.

### Algorithm
```python
def subarray_sum(nums, k):
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}

    for num in nums:
        prefix_sum += num
        if prefix_sum - k in sum_count:
            count += sum_count[prefix_sum - k]
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1

    return count
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 17. Find First and Last Position

### Problem
Find starting and ending position of target in sorted array.

### Algorithm
```python
def search_range(nums, target):
    def find_first():
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return left

    def find_last():
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] <= target:
                left = mid + 1
            else:
                right = mid - 1
        return right

    first, last = find_first(), find_last()
    if first <= last and first < len(nums) and nums[first] == target:
        return [first, last]
    return [-1, -1]
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 18. Minimum Size Subarray Sum

### Problem
Find minimal length of contiguous subarray with sum >= target.

### Algorithm
```python
def min_subarray_len(target, nums):
    left = 0
    current_sum = 0
    min_len = float('inf')

    for right, num in enumerate(nums):
        current_sum += num

        while current_sum >= target:
            min_len = min(min_len, right - left + 1)
            current_sum -= nums[left]
            left += 1

    return min_len if min_len != float('inf') else 0
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 19. Insert Interval

### Problem
Insert new interval and merge if necessary.

### Algorithm
```python
def insert_interval(intervals, new_interval):
    result = []
    i = 0
    n = len(intervals)

    # Add all intervals before new_interval
    while i < n and intervals[i][1] < new_interval[0]:
        result.append(intervals[i])
        i += 1

    # Merge overlapping intervals
    while i < n and intervals[i][0] <= new_interval[1]:
        new_interval[0] = min(new_interval[0], intervals[i][0])
        new_interval[1] = max(new_interval[1], intervals[i][1])
        i += 1

    result.append(new_interval)

    # Add remaining intervals
    while i < n:
        result.append(intervals[i])
        i += 1

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 20. Non-overlapping Intervals

### Problem
Find minimum number of intervals to remove to make non-overlapping.

### Algorithm
```python
def erase_overlap_intervals(intervals):
    if not intervals:
        return 0

    intervals.sort(key=lambda x: x[1])
    count = 0
    prev_end = intervals[0][1]

    for i in range(1, len(intervals)):
        if intervals[i][0] < prev_end:
            count += 1
        else:
            prev_end = intervals[i][1]

    return count
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(1)

---

## 21. Meeting Rooms II

### Problem
Find minimum number of meeting rooms required.

### Algorithm
```python
import heapq

def min_meeting_rooms(intervals):
    if not intervals:
        return 0

    intervals.sort(key=lambda x: x[0])
    heap = [intervals[0][1]]  # Min-heap of end times

    for start, end in intervals[1:]:
        if start >= heap[0]:
            heapq.heappop(heap)
        heapq.heappush(heap, end)

    return len(heap)
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)

---

## 22. Pancake Sorting

### Problem
Sort array using pancake flips.

### Algorithm
```python
def pancake_sort(arr):
    result = []
    n = len(arr)

    for size in range(n, 1, -1):
        max_idx = arr.index(max(arr[:size]))

        if max_idx != size - 1:
            if max_idx != 0:
                result.append(max_idx + 1)
                arr[:max_idx + 1] = arr[:max_idx + 1][::-1]

            result.append(size)
            arr[:size] = arr[:size][::-1]

    return result
```

### Complexity
- **Time:** O(n²)
- **Space:** O(1)

---

## 23. Peak Index in Mountain Array

### Problem
Find peak index in mountain array.

### Algorithm
```python
def peak_index_in_mountain_array(arr):
    left, right = 0, len(arr) - 1

    while left < right:
        mid = (left + right) // 2
        if arr[mid] < arr[mid + 1]:
            left = mid + 1
        else:
            right = mid

    return left
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 24. Game of Life

### Problem
Update board for Conway's Game of Life.

### Algorithm
```python
def game_of_life(board):
    rows, cols = len(board), len(board[0])

    def count_live_neighbors(r, c):
        count = 0
        for dr in [-1, 0, 1]:
            for dc in [-1, 0, 1]:
                if dr == 0 and dc == 0:
                    continue
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols:
                    if board[nr][nc] in [1, 3]:
                        count += 1
        return count

    # First pass: mark changes
    for r in range(rows):
        for c in range(cols):
            live = count_live_neighbors(r, c)

            if board[r][c] == 1:
                if live < 2 or live > 3:
                    board[r][c] = 3  # 1 -> 0 (dies)
            else:
                if live == 3:
                    board[r][c] = 2  # 0 -> 1 (lives)

    # Second pass: apply changes
    for r in range(rows):
        for c in range(cols):
            if board[r][c] == 2:
                board[r][c] = 1
            elif board[r][c] == 3:
                board[r][c] = 0
```

### Complexity
- **Time:** O(m × n)
- **Space:** O(1)
