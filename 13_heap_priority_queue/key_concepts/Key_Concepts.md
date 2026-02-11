# Heap - Key Concepts to Master

## 1. Complete Binary Tree Property

### Definition
A complete binary tree is filled at all levels except possibly the last, which is filled from left to right.

### Array Representation
```python
# For node at index i:
parent = (i - 1) // 2
left_child = 2 * i + 1
right_child = 2 * i + 2
```

## 2. Min-Heap vs Max-Heap

### Min-Heap
- Parent ≤ children
- Root is minimum
- Used for finding smallest elements

### Max-Heap
- Parent ≥ children
- Root is maximum
- Used for finding largest elements

## 3. Heap Operations

### Insert (Bubble Up)
```python
def heap_insert(heap, val):
    heap.append(val)
    i = len(heap) - 1

    while i > 0:
        parent = (i - 1) // 2
        if heap[parent] > heap[i]:  # Min-heap
            heap[parent], heap[i] = heap[i], heap[parent]
            i = parent
        else:
            break
```

### Extract Min (Bubble Down)
```python
def heap_extract_min(heap):
    if not heap:
        return None

    min_val = heap[0]
    heap[0] = heap[-1]
    heap.pop()

    i = 0
    n = len(heap)

    while True:
        smallest = i
        left = 2 * i + 1
        right = 2 * i + 2

        if left < n and heap[left] < heap[smallest]:
            smallest = left
        if right < n and heap[right] < heap[smallest]:
            smallest = right

        if smallest != i:
            heap[i], heap[smallest] = heap[smallest], heap[i]
            i = smallest
        else:
            break

    return min_val
```

## 4. Heapify Process

### Build Heap from Array
```python
def heapify(arr):
    n = len(arr)

    # Start from last non-leaf node
    for i in range(n // 2 - 1, -1, -1):
        sift_down(arr, i, n)

def sift_down(arr, i, n):
    smallest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] < arr[smallest]:
        smallest = left
    if right < n and arr[right] < arr[smallest]:
        smallest = right

    if smallest != i:
        arr[i], arr[smallest] = arr[smallest], arr[i]
        sift_down(arr, smallest, n)
```

### Complexity: O(n) for build heap

## 5. Python heapq Module

### Basic Operations
```python
import heapq

heap = []

# Insert
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)

# Extract min
min_val = heapq.heappop(heap)  # Returns 1

# Peek min
min_val = heap[0]  # Don't remove

# Build heap from list
arr = [3, 1, 4, 1, 5, 9]
heapq.heapify(arr)
```

### Max-Heap Trick
```python
max_heap = []
heapq.heappush(max_heap, -val)  # Negate on insert
max_val = -heapq.heappop(max_heap)  # Negate on extract
```

### heapq Functions
```python
# Get k smallest/largest
k_smallest = heapq.nsmallest(k, iterable)
k_largest = heapq.nlargest(k, iterable)

# Merge sorted iterables
merged = heapq.merge(iter1, iter2, iter3)

# Replace and pushpop
heapq.heapreplace(heap, item)  # Pop then push
heapq.heappushpop(heap, item)  # Push then pop
```

## 6. Heap Sort

```python
def heap_sort(arr):
    n = len(arr)

    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify_max(arr, n, i)

    # Extract elements
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify_max(arr, i, 0)

def heapify_max(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left
    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify_max(arr, n, largest)
```

## Time Complexity

| Operation | Time |
|-----------|------|
| Insert | O(log n) |
| Extract | O(log n) |
| Peek | O(1) |
| Build heap | O(n) |
| Heap sort | O(n log n) |

## Space Complexity
- O(n) for storing heap

## When to Use Heap

| Scenario | Use Case |
|----------|----------|
| Top k elements | nlargest/nsmallest |
| Merge sorted streams | heapq.merge |
| Median finding | Two heaps |
| Task scheduling | Priority queue |
| Dijkstra | Min-heap for distances |
