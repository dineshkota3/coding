# Dynamic Programming - Key Concepts to Master

## 1. Overlapping Subproblems

### Definition
Same subproblems are solved multiple times.

### Example: Fibonacci
```python
# Naive recursion - exponential
def fib_naive(n):
    if n <= 1:
        return n
    return fib_naive(n-1) + fib_naive(n-2)

# With memoization - linear
def fib_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo)
    return memo[n]
```

## 2. Optimal Substructure

### Definition
Optimal solution contains optimal solutions to subproblems.

### Example: Shortest Path
If shortest path from A to C goes through B, then:
- A to B must be shortest path
- B to C must be shortest path

## 3. Memoization (Top-Down)

### Using Dictionary
```python
def climb_stairs_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 2:
        return n
    memo[n] = climb_stairs_memo(n-1, memo) + climb_stairs_memo(n-2, memo)
    return memo[n]
```

### Using functools.lru_cache
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def climb_stairs(n):
    if n <= 2:
        return n
    return climb_stairs(n-1) + climb_stairs(n-2)
```

## 4. Tabulation (Bottom-Up)

### 1D DP Array
```python
def climb_stairs_dp(n):
    if n <= 2:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2

    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]

    return dp[n]
```

### Space Optimized
```python
def climb_stairs_optimized(n):
    if n <= 2:
        return n

    prev, curr = 1, 2
    for i in range(3, n + 1):
        prev, curr = curr, prev + curr

    return curr
```

## 5. State Definition and Transition

### State Definition
What does dp[i] or dp[i][j] represent?

### Common State Definitions
```python
# dp[i] = result for subproblem of size i
# dp[i] = maximum/minimum up to index i
# dp[i] = number of ways to reach state i
# dp[i][j] = result considering first i items with limit j
```

### State Transition
How does dp[i] relate to dp[i-1], dp[i-2], etc.?

```python
# Fibonacci: dp[i] = dp[i-1] + dp[i-2]
# LIS: dp[i] = max(dp[j] + 1) for all j < i where nums[j] < nums[i]
# Knapsack: dp[i][w] = max(dp[i-1][w], dp[i-1][w-weight[i]] + value[i])
```

## 6. 2D DP

### Grid Path Problems
```python
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]
```

### String Matching
```python
def edit_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Base cases
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j

    # Fill table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])

    return dp[m][n]
```

## 7. Space Optimization

### 2D to 1D
```python
# Original: dp[i][j] uses dp[i-1][j] and dp[i-1][j-1]
# Optimized: use single row, iterate backwards

def knapsack_1d(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for w, v in zip(weights, values):
        for j in range(capacity, w - 1, -1):
            dp[j] = max(dp[j], dp[j - w] + v)

    return dp[capacity]
```

## 8. DP Patterns

| Pattern | Example Problems |
|---------|------------------|
| Linear | Fibonacci, Climbing Stairs, House Robber |
| Grid | Unique Paths, Minimum Path Sum |
| Subsequence | LIS, LCS |
| Knapsack | 0/1 Knapsack, Unbounded Knapsack |
| String | Edit Distance, Palindrome |
| Interval | Matrix Chain, Burst Balloons |

## Time & Space Complexity

| Pattern | Time | Space |
|---------|------|-------|
| 1D DP | O(n) | O(n) or O(1) |
| 2D DP | O(mn) | O(mn) or O(min(m,n)) |
| Knapsack | O(nW) | O(nW) or O(W) |

## DP Problem Solving Framework

1. **Define state:** What does dp[i] represent?
2. **Find recurrence:** How does dp[i] relate to previous states?
3. **Base cases:** What are the initial values?
4. **Order of computation:** In what order to fill the table?
5. **Final answer:** Which state(s) give the answer?
6. **Optimize:** Can space be reduced?
