# Greedy - Algorithms to Learn

## 1. Activity Selection Problem

### Problem
Select maximum number of non-overlapping activities.

### Algorithm
```python
def activity_selection(activities):
    # Sort by end time
    activities.sort(key=lambda x: x[1])

    result = [activities[0]]
    last_end = activities[0][1]

    for start, end in activities[1:]:
        if start >= last_end:
            result.append((start, end))
            last_end = end

    return result
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(1)

---

## 2. Jump Game (Can Reach End)

### Problem
Determine if you can reach the last index.

### Algorithm
```python
def can_jump(nums):
    max_reach = 0

    for i, num in enumerate(nums):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + num)

    return True
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 3. Jump Game II (Minimum Jumps)

### Problem
Find minimum jumps to reach end.

### Algorithm
```python
def jump(nums):
    n = len(nums)
    if n <= 1:
        return 0

    jumps = 0
    current_end = 0
    farthest = 0

    for i in range(n - 1):
        farthest = max(farthest, i + nums[i])

        if i == current_end:
            jumps += 1
            current_end = farthest

            if current_end >= n - 1:
                break

    return jumps
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 4. Gas Station Problem

### Problem
Find starting gas station to complete circuit.

### Algorithm
```python
def can_complete_circuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1

    total = 0
    start = 0

    for i in range(len(gas)):
        total += gas[i] - cost[i]
        if total < 0:
            total = 0
            start = i + 1

    return start
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 5. Candy Distribution

### Problem
Distribute candies with rating constraints.

### Algorithm
```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n

    # Left to right pass
    for i in range(1, n):
        if ratings[i] > ratings[i - 1]:
            candies[i] = candies[i - 1] + 1

    # Right to left pass
    for i in range(n - 2, -1, -1):
        if ratings[i] > ratings[i + 1]:
            candies[i] = max(candies[i], candies[i + 1] + 1)

    return sum(candies)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 6. Partition Labels

### Problem
Partition string into max parts so each letter appears in at most one part.

### Algorithm
```python
def partition_labels(s):
    # Find last occurrence of each character
    last_occurrence = {c: i for i, c in enumerate(s)}

    result = []
    start = 0
    end = 0

    for i, c in enumerate(s):
        end = max(end, last_occurrence[c])

        if i == end:
            result.append(end - start + 1)
            start = i + 1

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) - fixed alphabet

---

## 7. Minimum Number of Arrows to Burst Balloons

### Problem
Find minimum arrows to burst all balloons (overlapping intervals).

### Algorithm
```python
def find_min_arrow_shots(points):
    if not points:
        return 0

    points.sort(key=lambda x: x[1])

    arrows = 1
    prev_end = points[0][1]

    for start, end in points[1:]:
        if start > prev_end:
            arrows += 1
            prev_end = end

    return arrows
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(1)

---

## 8. Task Scheduler (Greedy Approach)

### Problem
Minimum time to complete tasks with cooldown.

### Algorithm (Mathematical)
```python
def least_interval(tasks, n):
    from collections import Counter

    counts = Counter(tasks)
    max_count = max(counts.values())
    num_max = sum(1 for c in counts.values() if c == max_count)

    # Formula: max(len(tasks), (max_count - 1) * (n + 1) + num_max)
    return max(len(tasks), (max_count - 1) * (n + 1) + num_max)
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 9. Huffman Coding (Concept)

### Problem
Create optimal prefix-free codes.

### Algorithm
```python
import heapq
from collections import Counter

class HuffmanNode:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

    def __lt__(self, other):
        return self.freq < other.freq

def huffman_coding(text):
    freq = Counter(text)

    # Build min-heap
    heap = [HuffmanNode(char, f) for char, f in freq.items()]
    heapq.heapify(heap)

    # Build tree
    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)

        merged = HuffmanNode(None, left.freq + right.freq)
        merged.left = left
        merged.right = right

        heapq.heappush(heap, merged)

    # Generate codes
    codes = {}
    def generate_codes(node, code):
        if node.char:
            codes[node.char] = code
            return
        generate_codes(node.left, code + '0')
        generate_codes(node.right, code + '1')

    if heap:
        generate_codes(heap[0], '')

    return codes
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)
