# Recursion - Algorithms to Learn

## 1. Factorial (Classic Recursion)

### Problem
Calculate n! = n × (n-1) × ... × 1

### Algorithm
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# Iterative version
def factorial_iterative(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n) recursive, O(1) iterative

---

## 2. Fibonacci (Naive and Memoized)

### Problem
Calculate nth Fibonacci number where F(n) = F(n-1) + F(n-2)

### Algorithm (Naive)
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### Algorithm (Memoized)
```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n - 1, memo) + fibonacci_memo(n - 2, memo)
    return memo[n]
```

### Algorithm (DP)
```python
def fibonacci_dp(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b
```

### Complexity
- **Naive:** Time O(2^n), Space O(n)
- **Memoized:** Time O(n), Space O(n)
- **DP:** Time O(n), Space O(1)

---

## 3. Power Function (Fast Exponentiation)

### Problem
Calculate x^n efficiently.

### Algorithm (Naive)
```python
def power_naive(x, n):
    if n == 0:
        return 1
    return x * power_naive(x, n - 1)
```

### Algorithm (Fast)
```python
def power(x, n):
    if n == 0:
        return 1
    if n < 0:
        return 1 / power(x, -n)

    half = power(x, n // 2)
    if n % 2 == 0:
        return half * half
    else:
        return x * half * half
```

### Complexity
- **Naive:** O(n)
- **Fast:** O(log n)

---

## 4. Binary Search (Recursive)

### Problem
Search for target in sorted array.

### Algorithm
```python
def binary_search(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1

    if left > right:
        return -1

    mid = (left + right) // 2

    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, right)
    else:
        return binary_search(arr, target, left, mid - 1)
```

### Complexity
- **Time:** O(log n)
- **Space:** O(log n)

---

## 5. Generate Subsets (Power Set)

### Problem
Generate all subsets of a set.

### Algorithm
```python
def subsets(nums):
    result = []

    def backtrack(start, current):
        result.append(current[:])

        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()

    backtrack(0, [])
    return result

# Alternative: Bit manipulation
def subsets_bit(nums):
    n = len(nums)
    result = []
    for mask in range(1 << n):
        subset = []
        for i in range(n):
            if mask & (1 << i):
                subset.append(nums[i])
        result.append(subset)
    return result
```

### Complexity
- **Time:** O(n × 2^n)
- **Space:** O(n)

---

## 6. Generate Permutations

### Problem
Generate all permutations of array.

### Algorithm
```python
def permutations(nums):
    result = []

    def backtrack(start):
        if start == len(nums):
            result.append(nums[:])
            return

        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]

    backtrack(0)
    return result
```

### Complexity
- **Time:** O(n × n!)
- **Space:** O(n)

---

## 7. Tower of Hanoi

### Problem
Move n disks from source to destination using auxiliary peg.

### Algorithm
```python
def tower_of_hanoi(n, source, auxiliary, destination):
    if n == 1:
        print(f"Move disk 1 from {source} to {destination}")
        return

    tower_of_hanoi(n - 1, source, destination, auxiliary)
    print(f"Move disk {n} from {source} to {destination}")
    tower_of_hanoi(n - 1, auxiliary, source, destination)
```

### Complexity
- **Time:** O(2^n)
- **Space:** O(n)

---

## 8. Greatest Common Divisor (Euclidean)

### Problem
Find GCD of two numbers.

### Algorithm
```python
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

# Iterative version
def gcd_iterative(a, b):
    while b:
        a, b = b, a % b
    return a
```

### Complexity
- **Time:** O(log(min(a, b)))
- **Space:** O(log(min(a, b))) recursive

---

## 9. Depth-First Search (Recursive)

### Problem
DFS traversal of graph/tree.

### Algorithm (Tree)
```python
def dfs_tree(root):
    if not root:
        return

    print(root.val)  # Process
    dfs_tree(root.left)
    dfs_tree(root.right)

# Tree traversals
def inorder(root):
    if root:
        inorder(root.left)
        print(root.val)
        inorder(root.right)

def preorder(root):
    if root:
        print(root.val)
        preorder(root.left)
        preorder(root.right)

def postorder(root):
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.val)
```

### Algorithm (Graph)
```python
def dfs_graph(graph, node, visited=None):
    if visited is None:
        visited = set()

    visited.add(node)
    print(node)

    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs_graph(graph, neighbor, visited)

    return visited
```

### Complexity
- **Tree:** Time O(n), Space O(h) where h is height
- **Graph:** Time O(V + E), Space O(V)
