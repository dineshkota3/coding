# Hashing - Practice Problems

## Easy Problems

### 1. Single Number
**LeetCode:** #136

**Description:**
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

**Example:**
```
Input: nums = [2, 2, 1]
Output: 1
```

**Approach Hint:** Use XOR or hash set.

---

### 2. Majority Element
**LeetCode:** #169

**Description:**
Given an array `nums` of size n, return the majority element (appears more than n/2 times).

**Example:**
```
Input: nums = [3, 2, 3]
Output: 3
```

**Approach Hint:** Use hash map for counting, or Boyer-Moore voting.

---

### 3. Valid Sudoku
**LeetCode:** #36

**Description:**
Determine if a 9 x 9 Sudoku board is valid. Only check for duplicates in rows, columns, and 3x3 sub-boxes.

**Example:**
```
Input: board = [["5","3",".",".","7",".",...] ...]
Output: true
```

**Approach Hint:** Use sets for each row, column, and sub-box.

---

### 4. Design HashSet
**LeetCode:** #705

**Description:**
Design a HashSet without using any built-in hash table libraries.

**Example:**
```
hashSet.add(1)
hashSet.add(2)
hashSet.contains(1) -> true
hashSet.contains(3) -> false
```

**Approach Hint:** Use array of linked lists with simple hash function.

---

### 5. Design HashMap
**LeetCode:** #706

**Description:**
Design a HashMap without using any built-in hash table libraries.

**Example:**
```
hashMap.put(1, 1)
hashMap.put(2, 2)
hashMap.get(1) -> 1
hashMap.get(3) -> -1
```

**Approach Hint:** Use array of linked lists storing key-value pairs.

---

## Medium Problems

### 6. Copy List with Random Pointer
**LeetCode:** #138

**Description:**
A linked list has a next pointer and a random pointer. Make a deep copy of the list.

**Example:**
```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: Deep copy of the list
```

**Approach Hint:** Use hash map to map original nodes to copies.

---

### 7. Insert Delete GetRandom O(1)
**LeetCode:** #380

**Description:**
Implement a data structure that supports insert, remove, and getRandom in O(1) time.

**Example:**
```
randomSet.insert(1)
randomSet.remove(2)
randomSet.getRandom() -> 1 or 2
```

**Approach Hint:** Use list + hash map. Swap with last element for O(1) removal.

---

### 8. Logger Rate Limiter
**LeetCode:** #359

**Description:**
Design a logger that accepts stream of messages and returns whether message should be printed (no duplicates within 10 seconds).

**Example:**
```
logger.shouldPrintMessage(1, "foo") -> true
logger.shouldPrintMessage(2, "bar") -> true
logger.shouldPrintMessage(3, "foo") -> false
```

**Approach Hint:** Use hash map to store last timestamp for each message.

---

### 9. Subarray Sum Equals K
**LeetCode:** #560

**Description:**
Given an array of integers and an integer k, find total number of continuous subarrays with sum equal to k.

**Example:**
```
Input: nums = [1, 1, 1], k = 2
Output: 2
```

**Approach Hint:** Use prefix sum + hash map.

---

### 10. Longest Consecutive Sequence
**LeetCode:** #128

**Description:**
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

**Example:**
```
Input: nums = [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive sequence is [1, 2, 3, 4].
```

**Approach Hint:** Use set, only start counting from sequence start.

---

## Hard Problems

### 11. LRU Cache
**LeetCode:** #146

**Description:**
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

**Example:**
```
cache = LRUCache(2)
cache.put(1, 1)
cache.put(2, 2)
cache.get(1) -> 1
cache.put(3, 3)  # evicts key 2
```

**Approach Hint:** Use OrderedDict or hash map + doubly linked list.

---

## Additional Practice

### Happy Number (Easy) - #202
Detect cycle using set.

### Contains Duplicate (Easy) - #217
Use set to check for duplicates.

### Contains Duplicate II (Easy) - #219
Check for nearby duplicates within k distance.

### Isomorphic Strings (Easy) - #205
Use two hash maps for bidirectional mapping.

### Word Pattern (Easy) - #290
Match pattern to string using hash map.

### Group Anagrams (Medium) - #49
Use sorted string as key.

### Top K Frequent Elements (Medium) - #347
Count frequency, then use heap or bucket sort.

### Find Duplicate Subtrees (Medium) - #652
Use serialization + hash map.

### Fraction to Recurring Decimal (Medium) - #166
Use hash map to detect repeating remainders.

### LFU Cache (Hard) - #460
Extend LRU with frequency tracking.

---

## Problem-Solving Tips

1. **When to use hashing:**
   - Need O(1) lookup time
   - Counting occurrences
   - Detecting duplicates
   - Grouping by property
   - Caching/memoization

2. **Common patterns:**
   - Seen set: Track visited elements
   - Frequency map: Count occurrences
   - Index map: Store positions
   - Prefix sum map: Subarray problems

3. **Python tips:**
   - Use `defaultdict` for auto-initialization
   - Use `Counter` for frequency counting
   - Use `set` for membership testing
   - Use `in` operator for O(1) lookup

4. **Edge cases:**
   - Empty input
   - Single element
   - All same elements
   - Negative numbers
   - Large numbers (hash collisions)
