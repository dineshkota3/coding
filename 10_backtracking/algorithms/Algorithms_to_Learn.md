# Backtracking - Algorithms to Learn

## 1. N-Queens Problem

### Problem
Place n queens on n×n board so no two queens attack each other.

### Algorithm
```python
def solve_n_queens(n):
    result = []

    def create_board(state):
        board = []
        for row in state:
            board.append('.' * row + 'Q' + '.' * (n - row - 1))
        return board

    def is_valid(state, row, col):
        for r, c in enumerate(state):
            if c == col:  # Same column
                return False
            if abs(row - r) == abs(col - c):  # Same diagonal
                return False
        return True

    def backtrack(row, state):
        if row == n:
            result.append(create_board(state))
            return

        for col in range(n):
            if is_valid(state, row, col):
                state.append(col)
                backtrack(row + 1, state)
                state.pop()

    backtrack(0, [])
    return result
```

### Complexity
- **Time:** O(n!)
- **Space:** O(n)

---

## 2. Sudoku Solver

### Problem
Solve a 9×9 Sudoku board.

### Algorithm
```python
def solve_sudoku(board):
    def is_valid(row, col, num):
        # Check row
        for c in range(9):
            if board[row][c] == num:
                return False

        # Check column
        for r in range(9):
            if board[r][col] == num:
                return False

        # Check 3x3 box
        box_row, box_col = 3 * (row // 3), 3 * (col // 3)
        for r in range(box_row, box_row + 3):
            for c in range(box_col, box_col + 3):
                if board[r][c] == num:
                    return False

        return True

    def solve():
        for row in range(9):
            for col in range(9):
                if board[row][col] == '.':
                    for num in '123456789':
                        if is_valid(row, col, num):
                            board[row][col] = num
                            if solve():
                                return True
                            board[row][col] = '.'
                    return False
        return True

    solve()
    return board
```

### Complexity
- **Time:** O(9^(n*n)) worst case
- **Space:** O(n*n)

---

## 3. Generate Parentheses

### Problem
Generate all valid combinations of n pairs of parentheses.

### Algorithm
```python
def generate_parentheses(n):
    result = []

    def backtrack(current, open_count, close_count):
        if len(current) == 2 * n:
            result.append(current)
            return

        if open_count < n:
            backtrack(current + '(', open_count + 1, close_count)

        if close_count < open_count:
            backtrack(current + ')', open_count, close_count + 1)

    backtrack('', 0, 0)
    return result
```

### Complexity
- **Time:** O(4^n / √n) - Catalan number
- **Space:** O(n)

---

## 4. Combination Sum

### Problem
Find all unique combinations that sum to target (can reuse elements).

### Algorithm
```python
def combination_sum(candidates, target):
    result = []

    def backtrack(start, current, remaining):
        if remaining == 0:
            result.append(current[:])
            return
        if remaining < 0:
            return

        for i in range(start, len(candidates)):
            current.append(candidates[i])
            backtrack(i, current, remaining - candidates[i])
            current.pop()

    backtrack(0, [], target)
    return result
```

### Complexity
- **Time:** O(2^(target/min))
- **Space:** O(target/min)

---

## 5. Subsets (Power Set)

### Problem
Generate all possible subsets.

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
```

### Complexity
- **Time:** O(n × 2^n)
- **Space:** O(n)

---

## 6. Permutations

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

## 7. Word Search

### Problem
Find if word exists in 2D board.

### Algorithm
```python
def exist(board, word):
    rows, cols = len(board), len(board[0])

    def backtrack(r, c, idx):
        if idx == len(word):
            return True

        if (r < 0 or r >= rows or c < 0 or c >= cols or
            board[r][c] != word[idx]):
            return False

        temp = board[r][c]
        board[r][c] = '#'

        found = (backtrack(r+1, c, idx+1) or
                 backtrack(r-1, c, idx+1) or
                 backtrack(r, c+1, idx+1) or
                 backtrack(r, c-1, idx+1))

        board[r][c] = temp
        return found

    for r in range(rows):
        for c in range(cols):
            if backtrack(r, c, 0):
                return True
    return False
```

### Complexity
- **Time:** O(n × m × 4^k) where k is word length
- **Space:** O(k)

---

## 8. Palindrome Partitioning

### Problem
Partition string such that every substring is a palindrome.

### Algorithm
```python
def partition(s):
    result = []

    def is_palindrome(sub):
        return sub == sub[::-1]

    def backtrack(start, current):
        if start == len(s):
            result.append(current[:])
            return

        for end in range(start + 1, len(s) + 1):
            substring = s[start:end]
            if is_palindrome(substring):
                current.append(substring)
                backtrack(end, current)
                current.pop()

    backtrack(0, [])
    return result
```

### Complexity
- **Time:** O(n × 2^n)
- **Space:** O(n)

---

## 9. Letter Combinations of a Phone Number

### Problem
Generate all letter combinations from phone digits.

### Algorithm
```python
def letter_combinations(digits):
    if not digits:
        return []

    mapping = {
        '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
        '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'
    }

    result = []

    def backtrack(idx, current):
        if idx == len(digits):
            result.append(current)
            return

        for letter in mapping[digits[idx]]:
            backtrack(idx + 1, current + letter)

    backtrack(0, '')
    return result
```

### Complexity
- **Time:** O(4^n)
- **Space:** O(n)

---

## 10. Combination Sum II

### Problem
Find combinations that sum to target (can't reuse, may have duplicates).

### Algorithm
```python
def combination_sum2(candidates, target):
    candidates.sort()
    result = []

    def backtrack(start, current, remaining):
        if remaining == 0:
            result.append(current[:])
            return
        if remaining < 0:
            return

        for i in range(start, len(candidates)):
            if i > start and candidates[i] == candidates[i-1]:
                continue  # Skip duplicates

            current.append(candidates[i])
            backtrack(i + 1, current, remaining - candidates[i])
            current.pop()

    backtrack(0, [], target)
    return result
```

### Complexity
- **Time:** O(2^n)
- **Space:** O(n)

---

## 11. Restore IP Addresses

### Problem
Generate all valid IP addresses from string.

### Algorithm
```python
def restore_ip_addresses(s):
    result = []

    def backtrack(start, parts):
        if len(parts) == 4:
            if start == len(s):
                result.append('.'.join(parts))
            return

        for length in range(1, 4):
            if start + length > len(s):
                break

            segment = s[start:start + length]

            # Check validity
            if (len(segment) > 1 and segment[0] == '0') or int(segment) > 255:
                continue

            backtrack(start + length, parts + [segment])

    backtrack(0, [])
    return result
```

### Complexity
- **Time:** O(3^4) = O(81)
- **Space:** O(1)

---

## 12. Expression Add Operators

### Problem
Add operators to form target.

### Algorithm
```python
def add_operators(num, target):
    result = []

    def backtrack(index, path, value, prev):
        if index == len(num):
            if value == target:
                result.append(path)
            return

        for i in range(index, len(num)):
            if i > index and num[index] == '0':
                break

            curr = int(num[index:i + 1])

            if index == 0:
                backtrack(i + 1, str(curr), curr, curr)
            else:
                backtrack(i + 1, path + '+' + str(curr), value + curr, curr)
                backtrack(i + 1, path + '-' + str(curr), value - curr, -curr)
                backtrack(i + 1, path + '*' + str(curr), value - prev + prev * curr, prev * curr)

    backtrack(0, '', 0, 0)
    return result
```

### Complexity
- **Time:** O(4^n)
- **Space:** O(n)

---

## 13. Split Array into Fibonacci Sequence

### Problem
Split string into Fibonacci sequence.

### Algorithm
```python
def split_into_fibonacci(num):
    result = []

    def backtrack(index):
        if index == len(num) and len(result) >= 3:
            return True

        for i in range(index, min(index + 10, len(num))):
            if i > index and num[index] == '0':
                break

            curr = int(num[index:i + 1])

            if curr > 2**31 - 1:
                break

            if len(result) < 2:
                result.append(curr)
                if backtrack(i + 1):
                    return True
                result.pop()
            else:
                if result[-1] + result[-2] == curr:
                    result.append(curr)
                    if backtrack(i + 1):
                        return True
                    result.pop()

        return False

    backtrack(0)
    return result
```

### Complexity
- **Time:** O(n²)
- **Space:** O(n)

---

## 14. Beautiful Arrangement

### Problem
Count beautiful arrangements (num divides position or position divides num).

### Algorithm
```python
def count_arrangement(n):
    count = 0
    visited = [False] * (n + 1)

    def backtrack(pos):
        nonlocal count
        if pos > n:
            count += 1
            return

        for num in range(1, n + 1):
            if not visited[num] and (num % pos == 0 or pos % num == 0):
                visited[num] = True
                backtrack(pos + 1)
                visited[num] = False

    backtrack(1)
    return count
```

### Complexity
- **Time:** O(k) where k is number of valid arrangements
- **Space:** O(n)

---

## 15. Increasing Subsequences

### Problem
Find all increasing subsequences of length >= 2.

### Algorithm
```python
def find_subsequences(nums):
    result = []

    def backtrack(start, path):
        if len(path) >= 2:
            result.append(path[:])

        used = set()
        for i in range(start, len(nums)):
            if nums[i] in used:
                continue
            if not path or nums[i] >= path[-1]:
                used.add(nums[i])
                path.append(nums[i])
                backtrack(i + 1, path)
                path.pop()

    backtrack(0, [])
    return result
```

### Complexity
- **Time:** O(2^n)
- **Space:** O(n)

---

## 16. Combinations

### Problem
Return all combinations of k numbers from 1 to n.

### Algorithm
```python
def combine(n, k):
    result = []

    def backtrack(start, path):
        if len(path) == k:
            result.append(path[:])
            return

        for i in range(start, n + 1):
            path.append(i)
            backtrack(i + 1, path)
            path.pop()

    backtrack(1, [])
    return result
```

### Complexity
- **Time:** O(C(n,k))
- **Space:** O(k)

---

## 17. Factor Combinations

### Problem
Return all possible combinations of factors.

### Algorithm
```python
def get_factors(n):
    result = []

    def backtrack(start, remaining, path):
        if remaining == 1:
            if len(path) > 1:
                result.append(path[:])
            return

        for i in range(start, remaining + 1):
            if remaining % i == 0:
                path.append(i)
                backtrack(i, remaining // i, path)
                path.pop()

    backtrack(2, n, [])
    return result
```

### Complexity
- **Time:** O(sqrt(n)^log n)
- **Space:** O(log n)

---

## 18. Generalized Abbreviation

### Problem
Generate all abbreviations of word.

### Algorithm
```python
def generate_abbreviations(word):
    result = []

    def backtrack(index, path, count):
        if index == len(word):
            result.append(path + (str(count) if count > 0 else ''))
            return

        # Abbreviate
        backtrack(index + 1, path, count + 1)

        # Keep character
        backtrack(index + 1, path + (str(count) if count > 0 else '') + word[index], 0)

    backtrack(0, '', 0)
    return result
```

### Complexity
- **Time:** O(2^n)
- **Space:** O(n)

---

## 19. Android Unlock Patterns

### Problem
Count unlock patterns of length m to n.

### Algorithm
```python
def number_of_patterns(m, n):
    skip = {}
    skip[(1, 3)] = skip[(3, 1)] = 2
    skip[(1, 7)] = skip[(7, 1)] = 4
    skip[(3, 9)] = skip[(9, 3)] = 6
    skip[(7, 9)] = skip[(9, 7)] = 8
    skip[(1, 9)] = skip[(9, 1)] = skip[(3, 7)] = skip[(7, 3)] = 5
    skip[(2, 8)] = skip[(8, 2)] = skip[(4, 6)] = skip[(6, 4)] = 5

    visited = [False] * 10

    def dfs(remaining, current):
        if remaining == 0:
            return 1

        count = 0
        for next_num in range(1, 10):
            if not visited[next_num]:
                jump = skip.get((current, next_num))
                if jump is None or visited[jump]:
                    visited[next_num] = True
                    count += dfs(remaining - 1, next_num)
                    visited[next_num] = False

        return count

    result = 0
    for length in range(m, n + 1):
        visited[1] = True
        result += dfs(length - 1, 1) * 4  # 1, 3, 7, 9 are symmetric
        visited[1] = False

        visited[2] = True
        result += dfs(length - 1, 2) * 4  # 2, 4, 6, 8 are symmetric
        visited[2] = False

        visited[5] = True
        result += dfs(length - 1, 5)
        visited[5] = False

    return result
```

### Complexity
- **Time:** O(9!)
- **Space:** O(9)
