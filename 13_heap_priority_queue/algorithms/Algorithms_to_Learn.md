# Heap - Algorithms to Learn

## 1. Min Heap Implementation

### Problem
Implement min-heap from scratch.

### Algorithm
```python
class MinHeap:
    def __init__(self):
        self.heap = []

    def parent(self, i):
        return (i - 1) // 2

    def left_child(self, i):
        return 2 * i + 1

    def right_child(self, i):
        return 2 * i + 2

    def insert(self, val):
        self.heap.append(val)
        self._sift_up(len(self.heap) - 1)

    def _sift_up(self, i):
        while i > 0 and self.heap[self.parent(i)] > self.heap[i]:
            self.heap[self.parent(i)], self.heap[i] = self.heap[i], self.heap[self.parent(i)]
            i = self.parent(i)

    def extract_min(self):
        if not self.heap:
            return None

        min_val = self.heap[0]
        self.heap[0] = self.heap[-1]
        self.heap.pop()

        if self.heap:
            self._sift_down(0)

        return min_val

    def _sift_down(self, i):
        n = len(self.heap)
        smallest = i

        left = self.left_child(i)
        right = self.right_child(i)

        if left < n and self.heap[left] < self.heap[smallest]:
            smallest = left
        if right < n and self.heap[right] < self.heap[smallest]:
            smallest = right

        if smallest != i:
            self.heap[i], self.heap[smallest] = self.heap[smallest], self.heap[i]
            self._sift_down(smallest)

    def get_min(self):
        return self.heap[0] if self.heap else None
```

### Complexity
- **Insert:** O(log n)
- **Extract:** O(log n)
- **Peek:** O(1)

---

## 2. Max Heap Implementation

### Problem
Implement max-heap from scratch.

### Algorithm
```python
class MaxHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        self.heap.append(val)
        self._sift_up(len(self.heap) - 1)

    def _sift_up(self, i):
        parent = (i - 1) // 2
        while i > 0 and self.heap[parent] < self.heap[i]:
            self.heap[parent], self.heap[i] = self.heap[i], self.heap[parent]
            i = parent
            parent = (i - 1) // 2

    def extract_max(self):
        if not self.heap:
            return None

        max_val = self.heap[0]
        self.heap[0] = self.heap[-1]
        self.heap.pop()

        if self.heap:
            self._sift_down(0)

        return max_val

    def _sift_down(self, i):
        n = len(self.heap)
        largest = i
        left = 2 * i + 1
        right = 2 * i + 2

        if left < n and self.heap[left] > self.heap[largest]:
            largest = left
        if right < n and self.heap[right] > self.heap[largest]:
            largest = right

        if largest != i:
            self.heap[i], self.heap[largest] = self.heap[largest], self.heap[i]
            self._sift_down(largest)
```

### Complexity
- **Insert:** O(log n)
- **Extract:** O(log n)

---

## 3. Heapify (Build Heap from Array)

### Problem
Build heap from unsorted array in O(n).

### Algorithm
```python
def build_heap(arr):
    n = len(arr)

    # Start from last non-leaf node
    for i in range(n // 2 - 1, -1, -1):
        heapify_down(arr, n, i)

    return arr

def heapify_down(arr, n, i):
    smallest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] < arr[smallest]:
        smallest = left
    if right < n and arr[right] < arr[smallest]:
        smallest = right

    if smallest != i:
        arr[i], arr[smallest] = arr[smallest], arr[i]
        heapify_down(arr, n, smallest)
```

### Complexity
- **Time:** O(n)

---

## 4. Heap Sort

### Problem
Sort array using heap.

### Algorithm
```python
def heap_sort(arr):
    n = len(arr)

    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify_max(arr, n, i)

    # Extract elements one by one
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify_max(arr, i, 0)

    return arr

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

### Complexity
- **Time:** O(n log n)
- **Space:** O(1)

---

## 5. Kth Largest Element in Array

### Problem
Find kth largest element.

### Algorithm
```python
import heapq

def find_kth_largest(nums, k):
    # Min-heap of size k
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)

    return heap[0]

# Alternative: Quick select
def find_kth_largest_quick(nums, k):
    k = len(nums) - k  # Convert to kth smallest index

    def quickselect(left, right):
        pivot = nums[right]
        p = left

        for i in range(left, right):
            if nums[i] <= pivot:
                nums[p], nums[i] = nums[i], nums[p]
                p += 1

        nums[p], nums[right] = nums[right], nums[p]

        if p == k:
            return nums[p]
        elif p < k:
            return quickselect(p + 1, right)
        else:
            return quickselect(left, p - 1)

    return quickselect(0, len(nums) - 1)
```

### Complexity
- **Heap:** O(n log k)
- **Quick select:** O(n) average

---

## 6. Merge K Sorted Lists

### Problem
Merge k sorted linked lists.

### Algorithm
```python
import heapq

def merge_k_lists(lists):
    heap = []

    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))

    dummy = ListNode()
    current = dummy

    while heap:
        val, i, node = heapq.heappop(heap)
        current.next = node
        current = current.next

        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))

    return dummy.next
```

### Complexity
- **Time:** O(n log k)
- **Space:** O(k)

---

## 7. Top K Frequent Elements

### Problem
Find k most frequent elements.

### Algorithm
```python
import heapq
from collections import Counter

def top_k_frequent(nums, k):
    count = Counter(nums)

    # Min-heap of size k with (frequency, element)
    heap = []
    for num, freq in count.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)

    return [num for freq, num in heap]

# Alternative: Bucket sort O(n)
def top_k_frequent_bucket(nums, k):
    count = Counter(nums)
    buckets = [[] for _ in range(len(nums) + 1)]

    for num, freq in count.items():
        buckets[freq].append(num)

    result = []
    for i in range(len(buckets) - 1, -1, -1):
        result.extend(buckets[i])
        if len(result) >= k:
            return result[:k]

    return result
```

### Complexity
- **Heap:** O(n log k)
- **Bucket:** O(n)

---

## 8. Find Median from Data Stream

### Problem
Find median from continuous stream.

### Algorithm
```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small = []  # Max-heap (negated)
        self.large = []  # Min-heap

    def addNum(self, num):
        # Add to max-heap
        heapq.heappush(self.small, -num)

        # Balance: max of small <= min of large
        if self.small and self.large and -self.small[0] > self.large[0]:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)

        # Balance sizes
        if len(self.small) > len(self.large) + 1:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        if len(self.large) > len(self.small) + 1:
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -val)

    def findMedian(self):
        if len(self.small) > len(self.large):
            return -self.small[0]
        if len(self.large) > len(self.small):
            return self.large[0]
        return (-self.small[0] + self.large[0]) / 2
```

### Complexity
- **Add:** O(log n)
- **Find:** O(1)

---

## 9. Task Scheduler

### Problem
Minimum time to complete tasks with cooldown.

### Algorithm
```python
import heapq
from collections import Counter, deque

def least_interval(tasks, n):
    count = Counter(tasks)
    max_heap = [-c for c in count.values()]
    heapq.heapify(max_heap)

    queue = deque()  # (count, ready_time)
    time = 0

    while max_heap or queue:
        time += 1

        if max_heap:
            cnt = heapq.heappop(max_heap) + 1
            if cnt < 0:
                queue.append((cnt, time + n))

        if queue and queue[0][1] == time:
            heapq.heappush(max_heap, queue.popleft()[0])

    return time
```

### Complexity
- **Time:** O(n × m)
- **Space:** O(m)

---

## 11. IPO

### Problem
Find maximal capital after k projects.

### Algorithm
```python
def find_maximized_capital(k, w, profits, capital):
    projects = sorted(zip(capital, profits))
    max_heap = []
    idx = 0

    for _ in range(k):
        while idx < len(projects) and projects[idx][0] <= w:
            heapq.heappush(max_heap, -projects[idx][1])
            idx += 1

        if not max_heap:
            break

        w += -heapq.heappop(max_heap)

    return w
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)

---

## 12. Kth Smallest Element in Sorted Matrix

### Problem
Find kth smallest in sorted matrix.

### Algorithm
```python
def kth_smallest(matrix, k):
    heap = [(row[0], i, 0) for i, row in enumerate(matrix)]
    heapq.heapify(heap)

    for _ in range(k - 1):
        val, row, col = heapq.heappop(heap)
        if col + 1 < len(matrix[0]):
            heapq.heappush(heap, (matrix[row][col + 1], row, col + 1))

    return heap[0][0]
```

### Complexity
- **Time:** O(k log n)
- **Space:** O(n)

---

## 13. Find Right Interval

### Problem
Find right interval for each interval.

### Algorithm
```python
def find_right_interval(intervals):
    starts = [(interval[0], i) for i, interval in enumerate(intervals)]
    starts.sort()

    result = []
    for interval in intervals:
        end = interval[1]
        left, right = 0, len(starts)
        while left < right:
            mid = (left + right) // 2
            if starts[mid][0] >= end:
                right = mid
            else:
                left = mid + 1

        if left < len(starts):
            result.append(starts[left][1])
        else:
            result.append(-1)

    return result
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)

---

## 14. Maximum Performance of a Team

### Problem
Find maximum performance of at most k engineers.

### Algorithm
```python
def max_performance(n, speed, efficiency, k):
    engineers = sorted(zip(efficiency, speed), reverse=True)
    min_heap = []
    total_speed = 0
    max_perf = 0

    for eff, spd in engineers:
        heapq.heappush(min_heap, spd)
        total_speed += spd

        if len(min_heap) > k:
            total_speed -= heapq.heappop(min_heap)

        max_perf = max(max_perf, total_speed * eff)

    return max_perf % (10**9 + 7)
```

### Complexity
- **Time:** O(n log k)
- **Space:** O(k)

---

## 15. Sliding Window Median

### Problem
Find median in each sliding window.

### Algorithm
```python
from bisect import insort

def median_sliding_window(nums, k):
    result = []
    window = sorted(nums[:k])

    for i in range(k, len(nums) + 1):
        if k % 2 == 0:
            median = (window[k // 2 - 1] + window[k // 2]) / 2
        else:
            median = window[k // 2]
        result.append(median)

        if i == len(nums):
            break

        # Remove old element
        window.pop(bisect.bisect_left(window, nums[i - k]))

        # Add new element
        insort(window, nums[i])

    return result
```

### Complexity
- **Time:** O(n × k)
- **Space:** O(k)

---

## 16. Total Cost to Hire K Workers

### Problem
Find total cost to hire k workers with two sessions.

### Algorithm
```python
def total_cost(costs, k, candidates):
    left_heap = []
    right_heap = []

    left = 0
    right = len(costs) - 1

    while left <= right and len(left_heap) < candidates:
        heapq.heappush(left_heap, costs[left])
        left += 1

    while right >= left and len(right_heap) < candidates:
        heapq.heappush(right_heap, costs[right])
        right -= 1

    total = 0

    for _ in range(k):
        if not right_heap or (left_heap and left_heap[0] <= right_heap[0]):
            total += heapq.heappop(left_heap)
            if left <= right:
                heapq.heappush(left_heap, costs[left])
                left += 1
        else:
            total += heapq.heappop(right_heap)
            if right >= left:
                heapq.heappush(right_heap, costs[right])
                right -= 1

    return total
```

### Complexity
- **Time:** O((candidates + k) log candidates)
- **Space:** O(candidates)

---

## 17. Construct Target Array with Multiple Sums

### Problem
Count operations to construct target array.

### Algorithm
```python
def is_possible(target):
    total = sum(target)
    max_heap = [-x for x in target]
    heapq.heapify(max_heap)

    while True:
        largest = -heapq.heappop(max_heap)
        total -= largest

        if largest == 1 or total == 1:
            return True

        if total == 0 or largest < total:
            return False

        prev = largest % total
        if prev == 0:
            prev = total

        if prev == largest:
            return False

        total += prev
        heapq.heappush(max_heap, -prev)

    return True
```

### Complexity
- **Time:** O(n log n × log max)
- **Space:** O(n)

---

## 18. Process Tasks Using Servers

### Problem
Assign tasks to servers.

### Algorithm
```python
def assign_tasks(servers, tasks):
    available = [(weight, i) for i, weight in enumerate(servers)]
    heapq.heapify(available)
    busy = []  # (end_time, weight, server_idx)
    result = []

    for time, task_time in enumerate(tasks):
        # Free up servers
        while busy and busy[0][0] <= time:
            _, weight, idx = heapq.heappop(busy)
            heapq.heappush(available, (weight, idx))

        # If no available server, fast forward time
        if not available:
            time = busy[0][0]
            while busy and busy[0][0] <= time:
                _, weight, idx = heapq.heappop(busy)
                heapq.heappush(available, (weight, idx))

        weight, idx = heapq.heappop(available)
        result.append(idx)
        heapq.heappush(busy, (time + task_time, weight, idx))

    return result
```

### Complexity
- **Time:** O((n + m) log n)
- **Space:** O(n)

---

## 19. Single Threaded CPU

### Problem
Process tasks by CPU.

### Algorithm
```python
def get_order(tasks):
    tasks = [(en, pro, i) for i, (en, pro) in enumerate(tasks)]
    tasks.sort()

    result = []
    heap = []
    time = 0
    idx = 0

    while idx < len(tasks) or heap:
        if not heap:
            time = max(time, tasks[idx][0])

        while idx < len(tasks) and tasks[idx][0] <= time:
            en, pro, i = tasks[idx]
            heapq.heappush(heap, (pro, i))
            idx += 1

        pro, i = heapq.heappop(heap)
        result.append(i)
        time += pro

    return result
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)

---

## 20. Reorganize String

### Problem
Rearrange string so no adjacent chars same.

### Algorithm
```python
def reorganize_string(s):
    count = Counter(s)
    max_heap = [(-cnt, char) for char, cnt in count.items()]
    heapq.heapify(max_heap)

    result = []
    prev = None

    while max_heap:
        cnt, char = heapq.heappop(max_heap)
        result.append(char)

        if prev and prev[0] < 0:
            heapq.heappush(max_heap, prev)

        cnt += 1
        prev = (cnt, char) if cnt < 0 else None

    return ''.join(result) if len(result) == len(s) else ""
```

### Complexity
- **Time:** O(n log k)
- **Space:** O(k)

---

## 21. Sort Characters by Frequency

### Problem
Sort string by character frequency.

### Algorithm
```python
def frequency_sort(s):
    count = Counter(s)
    max_heap = [(-cnt, char) for char, cnt in count.items()]
    heapq.heapify(max_heap)

    result = []
    while max_heap:
        cnt, char = heapq.heappop(max_heap)
        result.append(char * (-cnt))

    return ''.join(result)
```

### Complexity
- **Time:** O(n log k)
- **Space:** O(k)

---

## 22. Smallest K-Length Subsequence

### Problem
Find lexicographically smallest subsequence of length k.

### Algorithm
```python
def smallest_subsequence(s, k):
    stack = []
    n = len(s)
    remaining = [0] * 26

    for char in s:
        remaining[ord(char) - ord('a')] += 1

    for i, char in enumerate(s):
        remaining[ord(char) - ord('a')] -= 1

        while (stack and stack[-1] > char and
               len(stack) + (n - i) > k):
            stack.pop()

        if len(stack) < k:
            stack.append(char)

    return ''.join(stack)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 23. Maximum Average Pass Ratio

### Problem
Maximize average pass ratio by assigning extra students.

### Algorithm
```python
def max_average_ratio(classes, extra_students):
    # Calculate gain from adding one student
    def gain(pass_i, total_i):
        return (pass_i + 1) / (total_i + 1) - pass_i / total_i

    max_heap = []
    for pass_i, total_i in classes:
        heapq.heappush(max_heap, (-gain(pass_i, total_i), pass_i, total_i))

    for _ in range(extra_students):
        g, pass_i, total_i = heapq.heappop(max_heap)
        pass_i += 1
        total_i += 1
        heapq.heappush(max_heap, (-gain(pass_i, total_i), pass_i, total_i))

    return sum(p / t for _, p, t in max_heap) / len(classes)
```

### Complexity
- **Time:** O((n + extra) log n)
- **Space:** O(n)
