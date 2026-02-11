# Searching - Algorithms to Learn

## 1. Standard Binary Search

### Problem
Find the index of target in a sorted array.

### Algorithm
```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 2. Binary Search - First Occurrence

### Problem
Find the first occurrence of target in sorted array with duplicates.

### Algorithm
```python
def first_occurrence(nums, target):
    left, right = 0, len(nums) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            result = mid
            right = mid - 1  # Continue searching left
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 3. Binary Search - Last Occurrence

### Problem
Find the last occurrence of target in sorted array with duplicates.

### Algorithm
```python
def last_occurrence(nums, target):
    left, right = 0, len(nums) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            result = mid
            left = mid + 1  # Continue searching right
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 4. Binary Search - Lower Bound

### Problem
Find the index of first element >= target.

### Algorithm
```python
def lower_bound(nums, target):
    left, right = 0, len(nums)

    while left < right:
        mid = (left + right) // 2

        if nums[mid] >= target:
            right = mid
        else:
            left = mid + 1

    return left
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 5. Binary Search - Upper Bound

### Problem
Find the index of first element > target.

### Algorithm
```python
def upper_bound(nums, target):
    left, right = 0, len(nums)

    while left < right:
        mid = (left + right) // 2

        if nums[mid] > target:
            right = mid
        else:
            left = mid + 1

    return left
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 6. Search in Rotated Sorted Array

### Problem
Search for target in a rotated sorted array with no duplicates.

### Algorithm
```python
def search_rotated(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)

---

## 7. Find Minimum in Rotated Sorted Array

### Problem
Find the minimum element in a rotated sorted array.

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

---

## 8. Search in 2D Matrix

### Problem
Search for target in matrix where each row is sorted and first element of each row > last element of previous row.

### Algorithm
```python
def search_matrix(matrix, target):
    if not matrix or not matrix[0]:
        return False

    rows, cols = len(matrix), len(matrix[0])
    left, right = 0, rows * cols - 1

    while left <= right:
        mid = (left + right) // 2
        row, col = mid // cols, mid % cols

        if matrix[row][col] == target:
            return True
        elif matrix[row][col] < target:
            left = mid + 1
        else:
            right = mid - 1

    return False
```

### Complexity
- **Time:** O(log(m × n))
- **Space:** O(1)

---

## 9. Median of Two Sorted Arrays

### Problem
Find the median of two sorted arrays.

### Algorithm
```python
def find_median_sorted_arrays(nums1, nums2):
    # Ensure nums1 is smaller
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1

    m, n = len(nums1), len(nums2)
    left, right = 0, m

    while left <= right:
        partition1 = (left + right) // 2
        partition2 = (m + n + 1) // 2 - partition1

        max_left1 = float('-inf') if partition1 == 0 else nums1[partition1 - 1]
        min_right1 = float('inf') if partition1 == m else nums1[partition1]

        max_left2 = float('-inf') if partition2 == 0 else nums2[partition2 - 1]
        min_right2 = float('inf') if partition2 == n else nums2[partition2]

        if max_left1 <= min_right2 and max_left2 <= min_right1:
            if (m + n) % 2 == 0:
                return (max(max_left1, max_left2) + min(min_right1, min_right2)) / 2
            else:
                return max(max_left1, max_left2)
        elif max_left1 > min_right2:
            right = partition1 - 1
        else:
            left = partition1 + 1
```

### Complexity
- **Time:** O(log(min(m, n)))
- **Space:** O(1)

---

## 10. Find Peak Element

### Problem
Find a peak element in array (element greater than neighbors).

### Algorithm
```python
def find_peak_element(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2

        if nums[mid] > nums[mid + 1]:
            right = mid
        else:
            left = mid + 1

    return left
```

### Complexity
- **Time:** O(log n)
- **Space:** O(1)
