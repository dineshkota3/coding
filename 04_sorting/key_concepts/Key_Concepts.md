# Sorting - Key Concepts to Master

## 1. Comparison-Based Sorting Limitations

### Lower Bound
- Any comparison-based sort requires at least Ω(n log n) comparisons
- Decision tree model shows this limitation
- To do better, must exploit additional structure (integers, bounded range)

## 2. Divide and Conquer Approach

### Merge Sort
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
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### Quick Sort
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

# In-place version
def quick_sort_inplace(arr, low, high):
    if low < high:
        pivot_idx = partition(arr, low, high)
        quick_sort_inplace(arr, low, pivot_idx - 1)
        quick_sort_inplace(arr, pivot_idx + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

## 3. Stable vs Unstable Sorting

### Stable Sort
Preserves relative order of equal elements.
- Merge Sort (stable)
- Insertion Sort (stable)
- Bubble Sort (stable)
- Python's Timsort (stable)

### Unstable Sort
May change relative order of equal elements.
- Quick Sort (unstable)
- Heap Sort (unstable)
- Selection Sort (unstable)

## 4. Time-Space Tradeoffs

| Algorithm | Time (Best) | Time (Avg) | Time (Worst) | Space | Stable |
|-----------|-------------|------------|--------------|-------|--------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting | O(n + k) | O(n + k) | O(n + k) | O(k) | Yes |
| Radix | O(d(n + k)) | O(d(n + k)) | O(d(n + k)) | O(n + k) | Yes |

## 5. Counting Sort

### Integer Sorting with Bounded Range
```python
def counting_sort(arr):
    if not arr:
        return arr

    # Find range
    min_val, max_val = min(arr), max(arr)
    range_size = max_val - min_val + 1

    # Count occurrences
    count = [0] * range_size
    for num in arr:
        count[num - min_val] += 1

    # Reconstruct sorted array
    result = []
    for i, cnt in enumerate(count):
        result.extend([i + min_val] * cnt)

    return result
```

**When to use:** Small range of integers (k << n)

## 6. Radix Sort

### Sort by Individual Digits
```python
def radix_sort(arr):
    if not arr:
        return arr

    # Handle negative numbers
    max_num = max(arr)

    exp = 1
    while max_num // exp > 0:
        counting_sort_by_digit(arr, exp)
        exp *= 10

    return arr

def counting_sort_by_digit(arr, exp):
    n = len(arr)
    output = [0] * n
    count = [0] * 10

    # Count occurrences
    for num in arr:
        digit = (num // exp) % 10
        count[digit] += 1

    # Cumulative count
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Build output array (reverse for stability)
    for i in range(n - 1, -1, -1):
        digit = (arr[i] // exp) % 10
        output[count[digit] - 1] = arr[i]
        count[digit] -= 1

    # Copy back
    for i in range(n):
        arr[i] = output[i]
```

**When to use:** Integers with many digits but small digit range

## 7. Custom Comparators in Python

### Using key parameter
```python
# Sort by absolute value
sorted(arr, key=abs)

# Sort by second element
sorted(pairs, key=lambda x: x[1])

# Sort by multiple keys
sorted(arr, key=lambda x: (x[0], -x[1]))

# Sort strings by length, then alphabetically
sorted(strings, key=lambda x: (len(x), x))
```

### Using cmp_to_key for complex comparison
```python
from functools import cmp_to_key

def compare(a, b):
    if a + b > b + a:
        return -1
    elif a + b < b + a:
        return 1
    return 0

sorted(strings, key=cmp_to_key(compare))
```

## When to Use Each Algorithm

| Scenario | Best Algorithm |
|----------|----------------|
| General purpose | Timsort (Python built-in) |
| Large data, external memory | Merge Sort |
| Average case speed | Quick Sort |
| Guaranteed O(n log n), in-place | Heap Sort |
| Nearly sorted data | Insertion Sort |
| Small integer range | Counting Sort |
| Large integers | Radix Sort |
| Custom ordering | Use key/comparator |
