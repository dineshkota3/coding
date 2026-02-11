# Heap & Priority Queue - Practice Problems

## Easy Problems

### 1. Kth Largest Element in an Array
**LeetCode:** #215

**Description:**
Find the kth largest element in an unsorted array.

**Example:**
```
Input: nums = [3, 2, 1, 5, 6, 4], k = 2
Output: 5
```

**Approach Hint:** Use min-heap of size k or quick select.

---

### 2. Last Stone Weight
**LeetCode:** #1046

**Description:**
Smash stones: heaviest two, if unequal, return difference. Return last stone weight or 0.

**Example:**
```
Input: stones = [2, 7, 4, 1, 8, 1]
Output: 1
```

**Approach Hint:** Use max-heap, always pop two largest.

---

### 3. Relative Ranks
**LeetCode:** #506

**Description:**
Given scores, return ranks: "Gold Medal", "Silver Medal", "Bronze Medal", "4", "5", ...

**Example:**
```
Input: score = [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
```

**Approach Hint:** Use heap to get sorted indices.

---

## Medium Problems

### 4. Top K Frequent Elements
**LeetCode:** #347

**Description:**
Return k most frequent elements.

**Example:**
```
Input: nums = [1, 1, 1, 2, 2, 3], k = 2
Output: [1, 2]
```

**Approach Hint:** Count frequency, use min-heap of size k.

---

### 5. Merge K Sorted Lists
**LeetCode:** #23

**Description:**
Merge k sorted linked lists into one sorted list.

**Example:**
```
Input: lists = [[1, 4, 5], [1, 3, 4], [2, 6]]
Output: [1, 1, 2, 3, 4, 4, 5, 6]
```

**Approach Hint:** Use min-heap with (value, list_index, node).

---

### 6. Find Median from Data Stream
**LeetCode:** #295

**Description:**
Design data structure to add numbers and find median.

**Example:**
```
medianFinder.addNum(1)
medianFinder.addNum(2)
medianFinder.findMedian() -> 1.5
medianFinder.addNum(3)
medianFinder.findMedian() -> 2.0
```

**Approach Hint:** Two heaps: max-heap for smaller half, min-heap for larger half.

---

### 7. Kth Smallest Element in a Sorted Matrix
**LeetCode:** #378

**Description:**
Find kth smallest in n×n matrix where rows and columns are sorted.

**Example:**
```
Input: matrix = [[1, 5, 9], [10, 11, 13], [12, 13, 15]], k = 8
Output: 13
```

**Approach Hint:** Use min-heap with first elements of each row.

---

### 8. Reorganize String
**LeetCode:** #767

**Description:**
Rearrange string so no adjacent characters are same.

**Example:**
```
Input: s = "aab"
Output: "aba"
```

**Approach Hint:** Use max-heap by frequency, always pick most frequent.

---

### 9. K Closest Points to Origin
**LeetCode:** #973

**Description:**
Find k points closest to origin.

**Example:**
```
Input: points = [[1, 3], [-2, 2]], k = 1
Output: [[-2, 2]]
```

**Approach Hint:** Use max-heap of size k.

---

### 10. Sort Characters By Frequency
**LeetCode:** #451

**Description:**
Sort characters by frequency in descending order.

**Example:**
```
Input: s = "tree"
Output: "eert" or "eetr"
```

**Approach Hint:** Count frequency, use max-heap.

---

### 11. Task Scheduler
**LeetCode:** #621

**Description:**
Minimum time to complete tasks with cooldown n between same tasks.

**Example:**
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8 (A -> B -> idle -> A -> B -> idle -> A -> B)
```

**Approach Hint:** Max-heap for most frequent + queue for cooldown.

---

## Hard Problems

### 12. Sliding Window Maximum
**LeetCode:** #239

**Description:**
Find max in each sliding window of size k.

**Example:**
```
Input: nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3
Output: [3, 3, 5, 5, 6, 7]
```

**Approach Hint:** Use deque (monotonic) or heap with lazy removal.

---

## Additional Practice

### IPO (Hard) - #502
Maximize capital with k projects.

### Find Right Interval (Medium) - #436
Find right interval using heap.

### Minimum Cost to Connect Sticks (Medium) - #1167
Connect sticks with minimum cost.

### Range Module (Hard) - #715
Track ranges with intervals.

### Minimize Deviation in Array (Hard) - #1675
Minimize max-min difference.

### Stone Game III (Hard) - #1406
Optimal game strategy.

---

## Problem-Solving Tips

1. **When to use heap:**
   - Need k largest/smallest
   - Need to process by priority
   - Need efficient min/max access
   - Merging sorted streams

2. **Heap tricks:**
   - Negate values for max-heap
   - Use tuples for custom ordering
   - Lazy removal for sliding window
   - Two heaps for median

3. **Common patterns:**
   - Top k: Min-heap of size k
   - Merge k: Heap with (value, source)
   - Median: Two heaps (small/large)
   - Scheduler: Heap + queue

4. **Time complexity:**
   - Build heap: O(n)
   - Insert/extract: O(log n)
   - k operations: O(k log n)

5. **Edge cases:**
   - Empty heap
   - Single element
   - k > n
   - All same values
