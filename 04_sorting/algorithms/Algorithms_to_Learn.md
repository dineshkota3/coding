# Sorting - Algorithms to Learn

## 1. Bubble Sort

### Problem
Sort array by repeatedly swapping adjacent elements if they're in wrong order.

### Algorithm
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr
```

### Complexity
- **Time:** O(n²) worst/average, O(n) best (already sorted)
- **Space:** O(1)

---

## 2. Selection Sort

### Problem
Sort by finding minimum element and placing it at the beginning.

### Algorithm
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

### Complexity
- **Time:** O(n²) all cases
- **Space:** O(1)

---

## 3. Insertion Sort

### Problem
Sort by building sorted array one element at a time.

### Algorithm
```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr
```

### Complexity
- **Time:** O(n²) worst/average, O(n) best (already sorted)
- **Space:** O(1)

**Best for:** Small arrays, nearly sorted data

---

## 4. Merge Sort

### Problem
Sort using divide and conquer with guaranteed O(n log n).

### Algorithm
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

### Complexity
- **Time:** O(n log n) all cases
- **Space:** O(n)

**Best for:** Stable sort, external sorting, linked lists

---

## 5. Quick Sort

### Problem
Sort using pivot partitioning with average O(n log n).

### Algorithm
```python
def quick_sort(arr, low=0, high=None):
    if high is None:
        high = len(arr) - 1

    if low < high:
        pivot_idx = partition(arr, low, high)
        quick_sort(arr, low, pivot_idx - 1)
        quick_sort(arr, pivot_idx + 1, high)

    return arr

def partition(arr, low, high):
    # Randomize pivot for better average case
    pivot_idx = random.randint(low, high)
    arr[pivot_idx], arr[high] = arr[high], arr[pivot_idx]

    pivot = arr[high]
    i = low - 1

    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### Complexity
- **Time:** O(n log n) average, O(n²) worst
- **Space:** O(log n) for recursion

**Best for:** In-place sorting, average case speed

---

## 6. Heap Sort

### Problem
Sort using heap data structure with guaranteed O(n log n).

### Algorithm
```python
def heap_sort(arr):
    n = len(arr)

    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)

    return arr

def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left

    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
```

### Complexity
- **Time:** O(n log n) all cases
- **Space:** O(1)

**Best for:** Guaranteed O(n log n), in-place

---

## 7. Counting Sort

### Problem
Sort integers with small range in linear time.

### Algorithm
```python
def counting_sort(arr):
    if not arr:
        return arr

    min_val, max_val = min(arr), max(arr)
    range_size = max_val - min_val + 1

    count = [0] * range_size
    for num in arr:
        count[num - min_val] += 1

    result = []
    for i, cnt in enumerate(count):
        result.extend([i + min_val] * cnt)

    return result
```

### Complexity
- **Time:** O(n + k) where k is range
- **Space:** O(k)

**Best for:** Small range of integers

---

## 8. Radix Sort

### Problem
Sort integers by processing individual digits.

### Algorithm
```python
def radix_sort(arr):
    if not arr:
        return arr

    max_num = max(abs(num) for num in arr)
    exp = 1

    while max_num // exp > 0:
        arr = counting_sort_by_digit(arr, exp)
        exp *= 10

    return arr

def counting_sort_by_digit(arr, exp):
    output = [0] * len(arr)
    count = [0] * 10

    for num in arr:
        digit = (abs(num) // exp) % 10
        count[digit] += 1

    for i in range(1, 10):
        count[i] += count[i - 1]

    for i in range(len(arr) - 1, -1, -1):
        digit = (abs(arr[i]) // exp) % 10
        output[count[digit] - 1] = arr[i]
        count[digit] -= 1

    return output
```

### Complexity
- **Time:** O(d(n + k)) where d is digits, k is base
- **Space:** O(n + k)

**Best for:** Fixed-width integers

---

## 9. Bucket Sort

### Problem
Sort uniformly distributed values.

### Algorithm
```python
def bucket_sort(arr, num_buckets=10):
    if not arr:
        return arr

    min_val, max_val = min(arr), max(arr)
    bucket_range = (max_val - min_val) / num_buckets + 1

    buckets = [[] for _ in range(num_buckets)]

    for num in arr:
        idx = int((num - min_val) / bucket_range)
        buckets[idx].append(num)

    result = []
    for bucket in buckets:
        result.extend(sorted(bucket))

    return result
```

### Complexity
- **Time:** O(n) average with uniform distribution
- **Space:** O(n)

**Best for:** Uniformly distributed data
