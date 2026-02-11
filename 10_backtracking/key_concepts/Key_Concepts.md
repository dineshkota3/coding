# Backtracking - Key Concepts to Master

## 1. Decision Tree Traversal

### Concept
At each step, make a decision, explore, then undo the decision.

### Template
```python
def backtrack(state, choices):
    if is_complete(state):
        save_solution(state)
        return

    for choice in choices:
        if is_valid(choice):
            make_choice(state, choice)
            backtrack(state, next_choices)
            undo_choice(state, choice)  # Backtrack
```

## 2. State Space Tree

### Definition
A tree where each node represents a partial solution and each edge represents a choice.

### Example: Subsets
```
                    []
           /        |        \
         [1]       [2]       [3]
        /   \       |
     [1,2] [1,3]  [2,3]
       |
    [1,2,3]
```

## 3. Pruning Invalid Branches

### Early Termination
```python
def backtrack(state, remaining):
    # Prune: stop if already invalid
    if not is_valid_so_far(state):
        return

    if is_complete(state):
        save(state)
        return

    for choice in remaining:
        make_choice(state, choice)
        backtrack(state, remaining_without_choice)
        undo_choice(state, choice)
```

### Key Insight
Pruning early saves exponential time.

## 4. Backtracking vs Pure Recursion

| Pure Recursion | Backtracking |
|----------------|--------------|
| Builds solution once | Explores all solutions |
| No undo needed | Must undo choices |
| Single path | Multiple paths with backtracking |
| Simple return | Save + backtrack |

## 5. Common Patterns

### Include/Exclude Pattern
```python
def subsets(nums):
    result = []

    def backtrack(i, current):
        if i == len(nums):
            result.append(current[:])
            return

        # Include nums[i]
        current.append(nums[i])
        backtrack(i + 1, current)
        current.pop()

        # Exclude nums[i]
        backtrack(i + 1, current)

    backtrack(0, [])
    return result
```

### Swap Pattern (Permutations)
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

### Grid Traversal Pattern
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
        board[r][c] = '#'  # Mark visited

        found = (backtrack(r+1, c, idx+1) or
                 backtrack(r-1, c, idx+1) or
                 backtrack(r, c+1, idx+1) or
                 backtrack(r, c-1, idx+1))

        board[r][c] = temp  # Restore
        return found
```

## 6. Constraint Propagation

### Valid Choice Check
```python
def is_valid(board, row, col, num):
    # Check row
    if num in board[row]:
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
```

## 7. Optimization Problems

### With Pruning
```python
def combination_sum(candidates, target):
    result = []

    def backtrack(start, current, remaining):
        if remaining == 0:
            result.append(current[:])
            return
        if remaining < 0:
            return  # Prune

        for i in range(start, len(candidates)):
            current.append(candidates[i])
            backtrack(i, current, remaining - candidates[i])
            current.pop()

    backtrack(0, [], target)
    return result
```

## When to Use Backtracking

| Problem Type | Example |
|--------------|---------|
| Find all solutions | Subsets, Permutations |
| Constraint satisfaction | N-Queens, Sudoku |
| Path finding | Word Search |
| Combinations | Combination Sum |
| Partitioning | Palindrome Partitioning |

## Time Complexity

| Problem | Complexity |
|---------|------------|
| Subsets | O(2^n) |
| Permutations | O(n!) |
| N-Queens | O(n!) |
| Combination Sum | O(2^n) |

## Space Complexity
- O(depth) for recursion stack
- O(n) for storing current state
- Additional for result storage
