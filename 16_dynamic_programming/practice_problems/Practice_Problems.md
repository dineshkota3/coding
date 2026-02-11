# Dynamic Programming - Practice Problems

## Easy Problems

### 1. Climbing Stairs
**LeetCode:** #70

**Description:**
Count ways to climb n stairs (1 or 2 steps).

**Example:**
```
Input: n = 3
Output: 3 (1+1+1, 1+2, 2+1)
```

**Approach Hint:** dp[i] = dp[i-1] + dp[i-2]

---

### 2. House Robber
**LeetCode:** #198

**Description:**
Maximize money without robbing adjacent houses.

**Example:**
```
Input: nums = [1, 2, 3, 1]
Output: 4 (rob house 0 and 2)
```

**Approach Hint:** dp[i] = max(dp[i-1], dp[i-2] + nums[i])

---

### 3. Maximum Subarray
**LeetCode:** #53

**Description:**
Find contiguous subarray with largest sum.

**Example:**
```
Input: nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6 ([4, -1, 2, 1])
```

**Approach Hint:** Kadane's: dp[i] = max(nums[i], dp[i-1] + nums[i])

---

## Medium Problems

### 4. Longest Increasing Subsequence
**LeetCode:** #300

**Description:**
Find length of longest strictly increasing subsequence.

**Example:**
```
Input: nums = [10, 9, 2, 5, 3, 7, 101, 18]
Output: 4 ([2, 3, 7, 18] or [2, 5, 7, 101])
```

**Approach Hint:** O(n²) DP or O(n log n) with binary search.

---

### 5. Longest Common Subsequence
**LeetCode:** #1143

**Description:**
Find length of longest common subsequence.

**Example:**
```
Input: text1 = "abcde", text2 = "ace"
Output: 3 ("ace")
```

**Approach Hint:** 2D DP: if match, dp[i][j] = dp[i-1][j-1] + 1

---

### 6. 0/1 Knapsack
**Various platforms**

**Description:**
Maximize value with weight capacity, each item once.

**Example:**
```
Input: weights = [1, 3, 4, 5], values = [1, 4, 5, 7], capacity = 7
Output: 9 (items with weights 3 and 4)
```

**Approach Hint:** 2D or 1D DP: dp[j] = max(dp[j], dp[j-w] + v)

---

### 7. Coin Change
**LeetCode:** #322

**Description:**
Find minimum coins to make amount.

**Example:**
```
Input: coins = [1, 2, 5], amount = 11
Output: 3 (5 + 5 + 1)
```

**Approach Hint:** dp[i] = min(dp[i], dp[i-coin] + 1) for each coin.

---

### 8. Coin Change 2
**LeetCode:** #518

**Description:**
Count ways to make amount.

**Example:**
```
Input: amount = 5, coins = [1, 2, 5]
Output: 4 (5=5, 5=2+2+1, 5=2+1+1+1, 5=1+1+1+1+1)
```

**Approach Hint:** dp[i] += dp[i-coin] for each coin.

---

### 9. Edit Distance
**LeetCode:** #72

**Description:**
Minimum operations to convert word1 to word2.

**Example:**
```
Input: word1 = "horse", word2 = "ros"
Output: 3 (horse -> rorse -> rose -> ros)
```

**Approach Hint:** 2D DP with insert, delete, replace.

---

### 10. Unique Paths
**LeetCode:** #62

**Description:**
Count paths from top-left to bottom-right (only right/down).

**Example:**
```
Input: m = 3, n = 7
Output: 28
```

**Approach Hint:** dp[i][j] = dp[i-1][j] + dp[i][j-1]

---

### 11. Unique Paths II
**LeetCode:** #63

**Description:**
Unique paths with obstacles.

**Example:**
```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
```

**Approach Hint:** Skip cells with obstacles.

---

### 12. Minimum Path Sum
**LeetCode:** #64

**Description:**
Find path with minimum sum from top-left to bottom-right.

**Example:**
```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7 (1 → 3 → 1 → 1 → 1)
```

**Approach Hint:** dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])

---

### 13. Decode Ways
**LeetCode:** #91

**Description:**
Count ways to decode a numeric string (A=1, B=2, ..., Z=26).

**Example:**
```
Input: s = "12"
Output: 2 ("AB" or "L")
```

**Approach Hint:** Check single digit and two-digit combinations.

---

### 14. Partition Equal Subset Sum
**LeetCode:** #416

**Description:**
Determine if array can be partitioned into equal sum subsets.

**Example:**
```
Input: nums = [1, 5, 11, 5]
Output: true ([1, 5, 5] and [11])
```

**Approach Hint:** Subset sum DP with target = sum/2.

---

## Hard Problems

### 15. Word Break
**LeetCode:** #140

**Description:**
Return all possible sentences from segmenting string with dictionary words.

**Example:**
```
Input: s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
Output: ["cats and dog","cat sand dog"]
```

**Approach Hint:** DP + backtracking, or memoization.

---

### 16. Burst Balloons
**LeetCode:** #312

**Description:**
Maximize coins by bursting balloons in optimal order.

**Example:**
```
Input: nums = [3, 1, 5, 8]
Output: 167
```

**Approach Hint:** Interval DP: dp[i][j] = max coins for bursting (i, j).

---

## Additional Practice

### House Robber II (Medium) - #213
Circular houses.

### Best Time to Buy and Sell Stock with Cooldown (Medium) - #309
State machine DP.

### Palindromic Substrings (Medium) - #647
Count palindromes.

### Target Sum (Medium) - #494
Assign + or - to reach target.

### Counting Bits (Easy) - #338
Count 1s in binary for all numbers 0 to n.

### Triangle (Medium) - #120
Minimum path sum in triangle.

### Dungeon Game (Hard) - #174
Minimum HP to reach princess.

### Interleaving String (Hard) - #97
Check if s3 is interleaving of s1 and s2.

### Distinct Subsequences (Hard) - #115
Count distinct subsequences.

---

## Problem-Solving Tips

1. **DP Framework:**
   1. Define state
   2. Find recurrence relation
   3. Set base cases
   4. Determine order
   5. Return answer

2. **Common patterns:**
   - Linear: dp[i] from dp[i-1], dp[i-2]
   - Grid: dp[i][j] from dp[i-1][j], dp[i][j-1]
   - Subsequence: dp[i] = max(dp[j] + ...) for j < i

3. **Space optimization:**
   - 1D: Keep only previous
   - 2D to 1D: Iterate backwards

4. **Edge cases:**
   - Empty input
   - Single element
   - All same values
   - Negative numbers
