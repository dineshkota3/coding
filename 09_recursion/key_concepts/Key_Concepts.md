# Recursion - Key Concepts to Master

## 1. Base Case Definition

### What is a Base Case?
The condition that stops recursion - the simplest instance of the problem.

### Types of Base Cases
```python
# Single base case
def factorial(n):
    if n <= 1:  # Base case
        return 1
    return n * factorial(n - 1)  # Recursive case

# Multiple base cases
def fibonacci(n):
    if n == 0:  # Base case 1
        return 0
    if n == 1:  # Base case 2
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)
```

## 2. Recursive Case Design

### Structure
1. **Identify:** How does problem relate to smaller subproblems?
2. **Combine:** How do subproblem solutions form full solution?
3. **Return:** What should the caller receive?

### Example: Sum of Array
```python
def sum_array(arr):
    # Base case
    if not arr:
        return 0
    # Recursive case: first + rest
    return arr[0] + sum_array(arr[1:])
```

## 3. Call Stack Behavior

### How Recursion Uses Stack
```
factorial(4)
  factorial(3)
    factorial(2)
      factorial(1) -> returns 1
    returns 2 * 1 = 2
  returns 3 * 2 = 6
returns 4 * 6 = 24
```

### Stack Overflow
```python
# Danger: No base case
def infinite_recursion():
    return infinite_recursion()  # RecursionError
```

### Python Recursion Limit
```python
import sys
print(sys.getrecursionlimit())  # Usually 1000
sys.setrecursionlimit(10000)    # Increase if needed
```

## 4. Tail Recursion

### Definition
Recursive call is the last operation - no work after return.

### Non-Tail Recursive
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)  # Multiplication after call
```

### Tail Recursive
```python
def factorial_tail(n, accumulator=1):
    if n <= 1:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)
```

**Note:** Python doesn't optimize tail recursion, but the pattern is useful for understanding.

## 5. Recursion Tree Visualization

### Fibonacci Tree
```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1) = 1
│   │   └── fib(0) = 0
│   └── fib(1) = 1
└── fib(2)
    ├── fib(1) = 1
    └── fib(0) = 0
```

### Time Complexity
Without memoization: O(2^n) for Fibonacci

## 6. Memoization Introduction

### Why Memoize?
Avoid recalculating same subproblems.

### Using Dictionary
```python
def fib_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
    return memo[n]
```

### Using functools.lru_cache
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib_cached(n):
    if n <= 1:
        return n
    return fib_cached(n - 1) + fib_cached(n - 2)
```

## 7. Time Complexity Analysis

### Recurrence Relations
```
T(n) = T(n-1) + O(1)  → O(n)
T(n) = 2T(n-1) + O(1) → O(2^n)
T(n) = T(n/2) + O(1)  → O(log n)
T(n) = 2T(n/2) + O(n) → O(n log n)
```

### Master Theorem (Simplified)
For T(n) = aT(n/b) + f(n):
- Compare f(n) with n^(log_b(a))

## Common Recursive Patterns

| Pattern | Example |
|---------|---------|
| Linear recursion | Factorial |
| Binary recursion | Fibonacci |
| Divide and conquer | Binary search |
| Tree recursion | Tree traversal |
| Backtracking | Permutations |

## Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Code clarity | Often cleaner | Can be verbose |
| Space | O(depth) stack | O(1) usually |
| Stack overflow | Possible | Not an issue |
| Performance | Function call overhead | Generally faster |

## When to Use Recursion

1. **Tree/Graph problems** - natural recursive structure
2. **Divide and conquer** - break into subproblems
3. **Backtracking** - explore all possibilities
4. **When code clarity matters** - recursive is more readable
5. **Problem is naturally recursive** - mathematical definitions
