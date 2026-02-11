# Greedy - Practice Problems

## Easy Problems

### 1. Maximum Subarray (Kadane's)
**LeetCode:** #53

**Description:**
Find the contiguous subarray with the largest sum.

**Example:**
```
Input: nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6 (subarray [4, -1, 2, 1])
```

**Approach Hint:** Greedy: extend if positive, restart if sum goes negative.

---

### 2. Best Time to Buy and Sell Stock II
**LeetCode:** #122

**Description:**
You may complete as many transactions as you like. Maximize profit.

**Example:**
```
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 7 (buy at 1, sell at 5, buy at 3, sell at 6)
```

**Approach Hint:** Capture every upward movement.

---

### 3. Assign Cookies
**LeetCode:** #455

**Description:**
Assign cookies to children to maximize content children.

**Example:**
```
Input: g = [1, 2, 3], s = [1, 1]
Output: 1
```

**Approach Hint:** Sort both, assign smallest cookie to child with smallest greed.

---

### 4. Lemonade Change
**LeetCode:** #860

**Description:**
Return true if you can provide change to all customers.

**Example:**
```
Input: bills = [5, 5, 5, 10, 20]
Output: true
```

**Approach Hint:** Greedy: prefer $10 over two $5s for change.

---

## Medium Problems

### 5. Merge Intervals
**LeetCode:** #56

**Description:**
Merge all overlapping intervals.

**Example:**
```
Input: intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
Output: [[1, 6], [8, 10], [15, 18]]
```

**Approach Hint:** Sort by start, merge overlapping.

---

### 6. Non-overlapping Intervals
**LeetCode:** #435

**Description:**
Find minimum number of intervals to remove to make non-overlapping.

**Example:**
```
Input: intervals = [[1, 2], [2, 3], [3, 4], [1, 3]]
Output: 1 (remove [1, 3])
```

**Approach Hint:** Sort by end, keep track of last non-overlapping.

---

### 7. Queue Reconstruction by Height
**LeetCode:** #406

**Description:**
Reconstruct queue where each person is [h, k] (height, number of taller people ahead).

**Example:**
```
Input: people = [[7, 0], [4, 4], [7, 1], [5, 0], [6, 1], [5, 2]]
Output: [[5, 0], [7, 0], [5, 2], [6, 1], [4, 4], [7, 1]]
```

**Approach Hint:** Sort by height descending, insert at k position.

---

### 8. Boat to Save People
**LeetCode:** #881

**Description:**
Find minimum boats to save people (limit weight per boat, at most 2 people).

**Example:**
```
Input: people = [1, 2], limit = 3
Output: 1
```

**Approach Hint:** Sort, pair heaviest with lightest if possible.

---

### 9. Jump Game
**LeetCode:** #55

**Description:**
Determine if you can reach the last index.

**Example:**
```
Input: nums = [2, 3, 1, 1, 4]
Output: true
```

**Approach Hint:** Track maximum reachable index.

---

### 10. Jump Game II
**LeetCode:** #45

**Description:**
Find minimum jumps to reach end.

**Example:**
```
Input: nums = [2, 3, 1, 1, 4]
Output: 2
```

**Approach Hint:** BFS-like approach with current range.

---

### 11. Gas Station
**LeetCode:** #134

**Description:**
Find starting gas station to complete circuit.

**Example:**
```
Input: gas = [1, 2, 3, 4, 5], cost = [3, 4, 5, 1, 2]
Output: 3
```

**Approach Hint:** If total gas >= total cost, unique starting point exists.

---

### 12. Candy
**LeetCode:** #135

**Description:**
Distribute candies with rating constraints (higher rating = more candy).

**Example:**
```
Input: ratings = [1, 0, 2]
Output: 5 ([2, 1, 2])
```

**Approach Hint:** Two passes: left-to-right and right-to-left.

---

### 13. Partition Labels
**LeetCode:** #763

**Description:**
Partition string so each letter appears in at most one part.

**Example:**
```
Input: s = "ababcbacadefegdehijhklij"
Output: [9, 7, 8]
```

**Approach Hint:** Track last occurrence, extend partition greedily.

---

## Hard Problems

### 14. Minimum Number of Arrows to Burst Balloons
**LeetCode:** #452

**Description:**
Find minimum arrows to burst all balloons.

**Example:**
```
Input: points = [[10, 16], [2, 8], [1, 6], [7, 12]]
Output: 2
```

**Approach Hint:** Sort by end, group overlapping intervals.

---

## Additional Practice

### Array Partition (Easy) - #561
Maximize sum of min pairs.

### DI String Match (Easy) - #942
Construct permutation matching pattern.

### Largest Perimeter Triangle (Easy) - #976
Find largest perimeter triangle.

### Two City Scheduling (Medium) - #1029
Minimize cost to send people to two cities.

### Break a Palindrome (Medium) - #1328
Break palindrome with smallest change.

### Reduce Array Size to The Half (Medium) - #1338
Remove smallest set of integers to halve array.

### Minimum Deletion Cost to Avoid Repeating (Medium) - #1578
Minimize cost to avoid repeating characters.

### Maximum Performance of a Team (Hard) - #1383
Maximize team performance with constraints.

---

## Problem-Solving Tips

1. **When greedy works:**
   - Local optimum leads to global optimum
   - Problem has optimal substructure
   - Sorting often helps

2. **Common patterns:**
   - Sort by one dimension
   - Two-pointer approach
   - Track max/min so far
   - Two-pass (left-right, right-left)

3. **Proving correctness:**
   - Exchange argument
   - Greedy stays ahead
   - Contradiction

4. **Edge cases:**
   - Empty input
   - Single element
   - All same values
   - Already sorted/reverse sorted
