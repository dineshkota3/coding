# Searching - Key Concepts to Master

## 1. Standard Binary Search

### Implementation
```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

### Key Points
- Use `left <= right` for inclusive bounds
- `mid = left + (right - left) // 2` avoids overflow (not needed in Python)
- Return index if found, -1 or appropriate value if not found

## 2. Lower Bound (First Position)

### Find first element >= target
```python
def lower_bound(nums, target):
    left, right = 0, len(nums)

    while left < right:
        mid = (left + right) // 2

        if nums[mid] >= target:
            right = mid
        else:
            left = mid + 1

    return left  # Index of first element >= target
```

### Using bisect module
```python
from bisect import bisect_left
idx = bisect_left(nums, target)
```

## 3. Upper Bound (Last Position + 1)

### Find first element > target
```python
def upper_bound(nums, target):
    left, right = 0, len(nums)

    while left < right:
        mid = (left + right) // 2

        if nums[mid] > target:
            right = mid
        else:
            left = mid + 1

    return left  # Index of first element > target
```

### Using bisect module
```python
from bisect import bisect_right
idx = bisect_right(nums, target)
```

## 4. Search in Rotated Sorted Array

### Find Pivot
```python
def find_pivot(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2

        if nums[mid] > nums[right]:
            left = mid + 1
        else:
            right = mid

    return left  # Index of minimum element
```

### Search in Rotated Array
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

## 5. Binary Search on Answer

### When to Use
- Optimization problems with monotonic property
- Find minimum/maximum value satisfying condition
- Problems asking for "minimum X such that..."

### Template
```python
def binary_search_on_answer(low, high, condition):
    left, right = low, high

    while left < right:
        mid = (left + right) // 2

        if condition(mid):
            right = mid  # Look for smaller
        else:
            left = mid + 1  # Need larger

    return left
```

### Example: Sqrt(x)
```python
def my_sqrt(x):
    if x < 2:
        return x

    left, right = 1, x // 2

    while left <= right:
        mid = (left + right) // 2
        square = mid * mid

        if square == x:
            return mid
        elif square < x:
            left = mid + 1
        else:
            right = mid - 1

    return right  # Floor of sqrt
```

## 6. Ternary Search

### Find Maximum in Unimodal Function
```python
def ternary_search(f, left, right, epsilon=1e-9):
    while right - left > epsilon:
        mid1 = left + (right - left) / 3
        mid2 = right - (right - left) / 3

        if f(mid1) < f(mid2):
            left = mid1
        else:
            right = mid2

    return (left + right) / 2
```

## 7. Exponential Search

### For Unbounded Arrays
```python
def exponential_search(nums, target):
    if nums[0] == target:
        return 0

    # Find range
    bound = 1
    while bound < len(nums) and nums[bound] < target:
        bound *= 2

    # Binary search in range
    left, right = bound // 2, min(bound, len(nums) - 1)
    return binary_search(nums[left:right+1], target)
```

## Time Complexity Reference

| Algorithm | Best | Average | Worst |
|-----------|------|---------|-------|
| Linear Search | O(1) | O(n) | O(n) |
| Binary Search | O(1) | O(log n) | O(log n) |
| Ternary Search | O(1) | O(log n) | O(log n) |
| Exponential Search | O(1) | O(log n) | O(log n) |

## Common Patterns

1. **Standard binary search:** Find exact element
2. **Lower bound:** Find first element >= target
3. **Upper bound:** Find first element > target
4. **Rotated array:** Determine sorted half, search accordingly
5. **Binary search on answer:** Optimization with monotonic property
