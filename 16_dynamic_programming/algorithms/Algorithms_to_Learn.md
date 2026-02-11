# Dynamic Programming - Algorithms to Learn

## 1. Fibonacci Series

### Problem
Calculate nth Fibonacci number.

### Algorithm
```python
# Memoization
@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

# Tabulation
def fib_dp(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# Space optimized
def fib_optimized(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b
```

### Complexity
- **Time:** O(n)
- **Space:** O(n) or O(1) optimized

---

## 2. Climbing Stairs

### Problem
Count ways to climb n stairs (1 or 2 steps at a time).

### Algorithm
```python
def climb_stairs(n):
    if n <= 2:
        return n

    prev, curr = 1, 2
    for i in range(3, n + 1):
        prev, curr = curr, prev + curr

    return curr
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 3. House Robber

### Problem
Maximum money without robbing adjacent houses.

### Algorithm
```python
def rob(nums):
    if not nums:
        return 0
    if len(nums) <= 2:
        return max(nums)

    prev, curr = nums[0], max(nums[0], nums[1])

    for i in range(2, len(nums)):
        prev, curr = curr, max(curr, prev + nums[i])

    return curr
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 4. Longest Increasing Subsequence

### Problem
Find length of longest increasing subsequence.

### Algorithm (O(n²))
```python
def length_of_lis(nums):
    if not nums:
        return 0

    dp = [1] * len(nums)

    for i in range(1, len(nums)):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)
```

### Algorithm (O(n log n))
```python
import bisect

def length_of_lis_optimized(nums):
    tails = []

    for num in nums:
        idx = bisect.bisect_left(tails, num)
        if idx == len(tails):
            tails.append(num)
        else:
            tails[idx] = num

    return len(tails)
```

### Complexity
- **O(n²):** Time O(n²), Space O(n)
- **Optimized:** Time O(n log n), Space O(n)

---

## 5. Longest Common Subsequence

### Problem
Find length of longest common subsequence.

### Algorithm
```python
def longest_common_subsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

### Complexity
- **Time:** O(mn)
- **Space:** O(mn)

---

## 6. 0/1 Knapsack Problem

### Problem
Maximize value with weight constraint (each item once).

### Algorithm
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            dp[i][w] = dp[i-1][w]  # Don't take item i
            if w >= weights[i-1]:
                dp[i][w] = max(dp[i][w], dp[i-1][w-weights[i-1]] + values[i-1])

    return dp[n][capacity]

# Space optimized
def knapsack_optimized(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for w, v in zip(weights, values):
        for j in range(capacity, w - 1, -1):
            dp[j] = max(dp[j], dp[j - w] + v)

    return dp[capacity]
```

### Complexity
- **Time:** O(n × capacity)
- **Space:** O(n × capacity) or O(capacity)

---

## 7. Coin Change (Minimum Coins)

### Problem
Find minimum coins to make amount.

### Algorithm
```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0

    for i in range(1, amount + 1):
        for coin in coins:
            if i >= coin:
                dp[i] = min(dp[i], dp[i - coin] + 1)

    return dp[amount] if dp[amount] != float('inf') else -1
```

### Complexity
- **Time:** O(amount × len(coins))
- **Space:** O(amount)

---

## 8. Coin Change II (Number of Ways)

### Problem
Count ways to make amount.

### Algorithm
```python
def change(amount, coins):
    dp = [0] * (amount + 1)
    dp[0] = 1

    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] += dp[i - coin]

    return dp[amount]
```

### Complexity
- **Time:** O(amount × len(coins))
- **Space:** O(amount)

---

## 9. Edit Distance

### Problem
Minimum operations to convert word1 to word2.

### Algorithm
```python
def edit_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])

    return dp[m][n]
```

### Complexity
- **Time:** O(mn)
- **Space:** O(mn)

---

## 10. Unique Paths

### Problem
Count paths from top-left to bottom-right.

### Algorithm
```python
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]

# Space optimized
def unique_paths_optimized(m, n):
    dp = [1] * n

    for i in range(1, m):
        for j in range(1, n):
            dp[j] += dp[j-1]

    return dp[n-1]
```

### Complexity
- **Time:** O(mn)
- **Space:** O(mn) or O(n)

---

## 11. House Robber II

### Problem
House robber with circular houses.

### Algorithm
```python
def rob_ii(nums):
    if len(nums) == 1:
        return nums[0]

    def rob_range(nums, start, end):
        prev = curr = 0
        for i in range(start, end):
            prev, curr = curr, max(curr, prev + nums[i])
        return curr

    return max(rob_range(nums, 0, len(nums) - 1), rob_range(nums, 1, len(nums)))
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 12. Maximum Product Subarray

### Problem
Find contiguous subarray with largest product.

### Algorithm
```python
def max_product(nums):
    max_prod = min_prod = result = nums[0]

    for num in nums[1:]:
        if num < 0:
            max_prod, min_prod = min_prod, max_prod

        max_prod = max(num, max_prod * num)
        min_prod = min(num, min_prod * num)
        result = max(result, max_prod)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 13. Word Break

### Problem
Determine if string can be segmented into dictionary words.

### Algorithm
```python
def word_break(s, word_dict):
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True

    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_dict:
                dp[i] = True
                break

    return dp[n]
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n)

---

## 14. Palindrome Partitioning II

### Problem
Minimum cuts to partition string into palindromes.

### Algorithm
```python
def min_cut(s):
    n = len(s)
    # is_palindrome[i][j] = True if s[i:j+1] is palindrome
    is_pal = [[False] * n for _ in range(n)]

    for i in range(n):
        is_pal[i][i] = True

    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            if s[i] == s[j]:
                if length == 2 or is_pal[i + 1][j - 1]:
                    is_pal[i][j] = True

    # dp[i] = min cuts for s[0:i+1]
    dp = [0] * n

    for i in range(n):
        if is_pal[0][i]:
            dp[i] = 0
        else:
            dp[i] = i  # Maximum cuts
            for j in range(i):
                if is_pal[j + 1][i]:
                    dp[i] = min(dp[i], dp[j] + 1)

    return dp[n - 1]
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n²)

---

## 15. Minimum Path Sum

### Problem
Find path with minimum sum from top-left to bottom-right.

### Algorithm
```python
def min_path_sum(grid):
    m, n = len(grid), len(grid[0])
    dp = [[0] * n for _ in range(m)]
    dp[0][0] = grid[0][0]

    for j in range(1, n):
        dp[0][j] = dp[0][j - 1] + grid[0][j]

    for i in range(1, m):
        dp[i][0] = dp[i - 1][0] + grid[i][0]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]

    return dp[m - 1][n - 1]
```

### Complexity
- **Time:** O(mn)
- **Space:** O(mn)

---

## 16. Triangle Minimum Path

### Problem
Find minimum path sum in triangle.

### Algorithm
```python
def minimum_total(triangle):
    dp = triangle[-1][:]

    for i in range(len(triangle) - 2, -1, -1):
        for j in range(len(triangle[i])):
            dp[j] = triangle[i][j] + min(dp[j], dp[j + 1])

    return dp[0]
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n)

---

## 17. Unique Paths II (with Obstacles)

### Problem
Count paths avoiding obstacles.

### Algorithm
```python
def unique_pathsWith_obstacles(obstacle_grid):
    m, n = len(obstacle_grid), len(obstacle_grid[0])

    if obstacle_grid[0][0] == 1:
        return 0

    dp = [[0] * n for _ in range(m)]
    dp[0][0] = 1

    for i in range(m):
        for j in range(n):
            if obstacle_grid[i][j] == 1:
                dp[i][j] = 0
            else:
                if i > 0:
                    dp[i][j] += dp[i - 1][j]
                if j > 0:
                    dp[i][j] += dp[i][j - 1]

    return dp[m - 1][n - 1]
```

### Complexity
- **Time:** O(mn)
- **Space:** O(mn)

---

## 18. Longest Palindromic Substring

### Problem
Find longest palindromic substring using DP.

### Algorithm
```python
def longest_palindrome(s):
    n = len(s)
    if n <= 1:
        return s

    dp = [[False] * n for _ in range(n)]
    start, max_len = 0, 1

    # All single characters are palindromes
    for i in range(n):
        dp[i][i] = True

    # Check for two character palindromes
    for i in range(n - 1):
        if s[i] == s[i + 1]:
            dp[i][i + 1] = True
            start, max_len = i, 2

    # Check for longer palindromes
    for length in range(3, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            if s[i] == s[j] and dp[i + 1][j - 1]:
                dp[i][j] = True
                start, max_len = i, length

    return s[start:start + max_len]
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n²)

---

## 19. Decode Ways

### Problem
Count ways to decode a numeric string.

### Algorithm
```python
def num_decodings(s):
    if not s or s[0] == '0':
        return 0

    n = len(s)
    dp = [0] * (n + 1)
    dp[0] = dp[1] = 1

    for i in range(2, n + 1):
        # Single digit
        if s[i - 1] != '0':
            dp[i] += dp[i - 1]

        # Two digits
        two_digit = int(s[i - 2:i])
        if 10 <= two_digit <= 26:
            dp[i] += dp[i - 2]

    return dp[n]
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 20. Perfect Squares

### Problem
Find minimum perfect squares that sum to n.

### Algorithm
```python
def num_squares(n):
    dp = [float('inf')] * (n + 1)
    dp[0] = 0

    for i in range(1, n + 1):
        j = 1
        while j * j <= i:
            dp[i] = min(dp[i], dp[i - j * j] + 1)
            j += 1

    return dp[n]
```

### Complexity
- **Time:** O(n√n)
- **Space:** O(n)

---

## 21. Jump Game II

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

    return jumps
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 22. Partition Equal Subset Sum

### Problem
Determine if array can be partitioned into equal sum subsets.

### Algorithm
```python
def can_partition(nums):
    total = sum(nums)
    if total % 2 != 0:
        return False

    target = total // 2
    dp = [False] * (target + 1)
    dp[0] = True

    for num in nums:
        for i in range(target, num - 1, -1):
            dp[i] = dp[i] or dp[i - num]

    return dp[target]
```

### Complexity
- **Time:** O(n × sum)
- **Space:** O(sum)

---

## 23. Target Sum

### Problem
Assign + or - to achieve target sum.

### Algorithm
```python
def find_target_sum_ways(nums, target):
    total = sum(nums)
    # (sum + target) must be even and non-negative
    if (total + target) % 2 != 0 or abs(target) > total:
        return 0

    subset_sum = (total + target) // 2
    dp = [0] * (subset_sum + 1)
    dp[0] = 1

    for num in nums:
        for i in range(subset_sum, num - 1, -1):
            dp[i] += dp[i - num]

    return dp[subset_sum]
```

### Complexity
- **Time:** O(n × sum)
- **Space:** O(sum)

---

## 24. Burst Balloons

### Problem
Maximize coins by bursting balloons in optimal order.

### Algorithm
```python
def max_coins(nums):
    nums = [1] + nums + [1]
    n = len(nums)
    dp = [[0] * n for _ in range(n)]

    for length in range(2, n):
        for left in range(n - length):
            right = left + length
            for k in range(left + 1, right):
                dp[left][right] = max(
                    dp[left][right],
                    nums[left] * nums[k] * nums[right] + dp[left][k] + dp[k][right]
                )

    return dp[0][n - 1]
```

### Complexity
- **Time:** O(n³)
- **Space:** O(n²)

---

## 25. Best Time to Buy and Sell Stock with Cooldown

### Problem
Maximize profit with cooldown after selling.

### Algorithm
```python
def max_profit(prices):
    if not prices:
        return 0

    n = len(prices)
    hold = [0] * n
    sold = [0] * n
    rest = [0] * n

    hold[0] = -prices[0]
    sold[0] = 0
    rest[0] = 0

    for i in range(1, n):
        hold[i] = max(hold[i - 1], rest[i - 1] - prices[i])
        sold[i] = hold[i - 1] + prices[i]
        rest[i] = max(rest[i - 1], sold[i - 1])

    return max(sold[-1], rest[-1])
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 26. Stone Game

### Problem
Determine if first player wins stone game.

### Algorithm
```python
def stone_game(piles):
    n = len(piles)
    dp = [[0] * n for _ in range(n)]

    for i in range(n):
        dp[i][i] = piles[i]

    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            dp[i][j] = max(piles[i] - dp[i + 1][j], piles[j] - dp[i][j - 1])

    return dp[0][n - 1] > 0
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n²)
