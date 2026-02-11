# Stack - Key Concepts to Master

## 1. Stack Operations

### Basic Operations
```python
stack = []

# Push
stack.append(1)
stack.append(2)

# Pop
top = stack.pop()  # Returns 2

# Peek
top = stack[-1]  # Returns 1 (doesn't remove)

# Check empty
is_empty = len(stack) == 0

# Size
size = len(stack)
```

### Time Complexity
| Operation | Time |
|-----------|------|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |
| isEmpty | O(1) |

## 2. Stack Implementation

### Using Array (Python List)
```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        raise IndexError("Pop from empty stack")

    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        raise IndexError("Peek from empty stack")

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)
```

### Using Linked List
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class StackLinkedList:
    def __init__(self):
        self.top = None
        self._size = 0

    def push(self, item):
        node = Node(item)
        node.next = self.top
        self.top = node
        self._size += 1

    def pop(self):
        if not self.top:
            raise IndexError("Pop from empty stack")
        value = self.top.value
        self.top = self.top.next
        self._size -= 1
        return value

    def peek(self):
        if not self.top:
            raise IndexError("Peek from empty stack")
        return self.top.value

    def is_empty(self):
        return self.top is None
```

## 3. Monotonic Stack

### Increasing Stack
Elements in stack are in increasing order (bottom to top).
```python
def increasing_stack(nums):
    stack = []
    for num in nums:
        while stack and stack[-1] > num:
            stack.pop()
        stack.append(num)
    return stack
```

### Decreasing Stack
Elements in stack are in decreasing order (bottom to top).
```python
def decreasing_stack(nums):
    stack = []
    for num in nums:
        while stack and stack[-1] < num:
            stack.pop()
        stack.append(num)
    return stack
```

### Next Greater Element
```python
def next_greater_element(nums):
    n = len(nums)
    result = [-1] * n
    stack = []  # Stores indices

    for i in range(n):
        while stack and nums[stack[-1]] < nums[i]:
            result[stack.pop()] = nums[i]
        stack.append(i)

    return result
```

## 4. Expression Evaluation

### Valid Parentheses
```python
def is_valid(s):
    mapping = {')': '(', '}': '{', ']': '['}
    stack = []

    for char in s:
        if char in mapping:
            if not stack or stack.pop() != mapping[char]:
                return False
        else:
            stack.append(char)

    return len(stack) == 0
```

### Evaluate RPN (Reverse Polish Notation)
```python
def eval_rpn(tokens):
    stack = []
    operators = {
        '+': lambda a, b: a + b,
        '-': lambda a, b: a - b,
        '*': lambda a, b: a * b,
        '/': lambda a, b: int(a / b)
    }

    for token in tokens:
        if token in operators:
            b = stack.pop()
            a = stack.pop()
            stack.append(operators[token](a, b))
        else:
            stack.append(int(token))

    return stack[0]
```

## 5. Stack for Parsing

### Simplify Path
```python
def simplify_path(path):
    stack = []
    components = path.split('/')

    for component in components:
        if component == '..':
            if stack:
                stack.pop()
        elif component and component != '.':
            stack.append(component)

    return '/' + '/'.join(stack)
```

## 6. Two Stack Patterns

### Min Stack
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val):
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self):
        if self.stack.pop() == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]
```

### Implement Queue using Stacks
```python
class MyQueue:
    def __init__(self):
        self.in_stack = []
        self.out_stack = []

    def push(self, x):
        self.in_stack.append(x)

    def pop(self):
        self._transfer()
        return self.out_stack.pop()

    def peek(self):
        self._transfer()
        return self.out_stack[-1]

    def empty(self):
        return not self.in_stack and not self.out_stack

    def _transfer(self):
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())
```

## When to Use Stack

| Problem Type | Example |
|--------------|---------|
| Matching/Validation | Valid Parentheses |
| Expression Evaluation | Basic Calculator |
| Next Greater/Smaller | Daily Temperatures |
| Undo/History | Browser History |
| Recursion Simulation | DFS Iterative |
| Parsing | Simplify Path |
| Histogram Problems | Largest Rectangle |
