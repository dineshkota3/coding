# Stack - Algorithms to Learn

## 1. Valid Parentheses

### Problem
Given a string containing brackets, determine if input is valid.

### Algorithm
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

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 2. Min Stack

### Problem
Design a stack that supports push, pop, top, and getMin in O(1).

### Algorithm
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

### Complexity
- **Time:** O(1) for all operations
- **Space:** O(n)

---

## 3. Evaluate Reverse Polish Notation

### Problem
Evaluate postfix expression.

### Algorithm
```python
def eval_rpn(tokens):
    stack = []

    for token in tokens:
        if token in '+-*/':
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            else:
                stack.append(int(a / b))
        else:
            stack.append(int(token))

    return stack[0]
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 4. Daily Temperatures (Next Greater Element)

### Problem
For each day, find how many days until a warmer temperature.

### Algorithm
```python
def daily_temperatures(temperatures):
    n = len(temperatures)
    result = [0] * n
    stack = []  # Stores indices

    for i in range(n):
        while stack and temperatures[stack[-1]] < temperatures[i]:
            prev_idx = stack.pop()
            result[prev_idx] = i - prev_idx
        stack.append(i)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 5. Largest Rectangle in Histogram

### Problem
Find largest rectangular area in histogram.

### Algorithm
```python
def largest_rectangle_area(heights):
    stack = []  # Stores indices
    max_area = 0
    heights.append(0)  # Sentinel

    for i, h in enumerate(heights):
        while stack and heights[stack[-1]] > h:
            height = heights[stack.pop()]
            width = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)

    return max_area
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 6. Simplify Path

### Problem
Simplify Unix-style file path.

### Algorithm
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

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 7. Basic Calculator

### Problem
Evaluate expression with +, -, (, ).

### Algorithm
```python
def calculate(s):
    stack = []
    result = 0
    num = 0
    sign = 1

    for char in s:
        if char.isdigit():
            num = num * 10 + int(char)
        elif char == '+':
            result += sign * num
            num = 0
            sign = 1
        elif char == '-':
            result += sign * num
            num = 0
            sign = -1
        elif char == '(':
            stack.append(result)
            stack.append(sign)
            result = 0
            sign = 1
        elif char == ')':
            result += sign * num
            num = 0
            result *= stack.pop()  # sign
            result += stack.pop()  # previous result

    result += sign * num
    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 8. Implement Queue using Stacks

### Problem
Implement queue using only stacks.

### Algorithm
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

### Complexity
- **Time:** O(1) amortized
- **Space:** O(n)

---

## 9. Next Greater Element I

### Problem
Find next greater element for each element in subset.

### Algorithm
```python
def next_greater_element(nums1, nums2):
    next_greater = {}
    stack = []

    for num in nums2:
        while stack and stack[-1] < num:
            next_greater[stack.pop()] = num
        stack.append(num)

    return [next_greater.get(num, -1) for num in nums1]
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 10. Next Greater Element II (Circular Array)

### Problem
Find next greater in circular array.

### Algorithm
```python
def next_greater_elements(nums):
    n = len(nums)
    result = [-1] * n
    stack = []

    for i in range(2 * n):
        while stack and nums[stack[-1]] < nums[i % n]:
            result[stack.pop()] = nums[i % n]
        if i < n:
            stack.append(i)

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 11. Car Fleet

### Problem
Count car fleets reaching target.

### Algorithm
```python
def car_fleet(target, position, speed):
    cars = sorted(zip(position, speed), reverse=True)
    stack = []

    for pos, sp in cars:
        time = (target - pos) / sp
        if not stack or time > stack[-1]:
            stack.append(time)

    return len(stack)
```

### Complexity
- **Time:** O(n log n)
- **Space:** O(n)

---

## 12. Remove K Digits

### Problem
Remove k digits to form smallest number.

### Algorithm
```python
def remove_k_digits(num, k):
    stack = []

    for digit in num:
        while k > 0 and stack and stack[-1] > digit:
            stack.pop()
            k -= 1
        stack.append(digit)

    # Remove remaining k digits
    while k > 0:
        stack.pop()
        k -= 1

    # Build result
    result = ''.join(stack).lstrip('0')
    return result if result else '0'
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 13. Remove Duplicate Letters

### Problem
Remove duplicates to form smallest lexicographical result.

### Algorithm
```python
def remove_duplicate_letters(s):
    last_occurrence = {c: i for i, c in enumerate(s)}
    visited = set()
    stack = []

    for i, c in enumerate(s):
        if c not in visited:
            while stack and c < stack[-1] and i < last_occurrence[stack[-1]]:
                visited.remove(stack.pop())
            stack.append(c)
            visited.add(c)

    return ''.join(stack)
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) - limited to 26 letters

---

## 14. Online Stock Span

### Problem
Return span of stock price (consecutive days with price <= today).

### Algorithm
```python
class StockSpanner:
    def __init__(self):
        self.stack = []  # (price, span)

    def next(self, price):
        span = 1
        while self.stack and self.stack[-1][0] <= price:
            span += self.stack.pop()[1]
        self.stack.append((price, span))
        return span
```

### Complexity
- **Time:** O(1) amortized
- **Space:** O(n)

---

## 15. Asteroid Collision

### Problem
Simulate asteroid collisions (positive moves right, negative moves left).

### Algorithm
```python
def asteroid_collision(asteroids):
    stack = []

    for asteroid in asteroids:
        while stack and asteroid < 0 < stack[-1]:
            if stack[-1] < -asteroid:
                stack.pop()
                continue
            elif stack[-1] == -asteroid:
                stack.pop()
            break
        else:
            stack.append(asteroid)

    return stack
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 16. Basic Calculator II

### Problem
Evaluate expression with +, -, *, /.

### Algorithm
```python
def calculate(s):
    stack = []
    num = 0
    op = '+'

    for i, char in enumerate(s):
        if char.isdigit():
            num = num * 10 + int(char)

        if char in '+-*/' or i == len(s) - 1:
            if op == '+':
                stack.append(num)
            elif op == '-':
                stack.append(-num)
            elif op == '*':
                stack.append(stack.pop() * num)
            else:
                stack.append(int(stack.pop() / num))

            op = char
            num = 0

    return sum(stack)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 17. Decode String

### Problem
Decode string with nested brackets (e.g., "3[a2[c]]" → "accaccacc").

### Algorithm
```python
def decode_string(s):
    stack = []
    current_num = 0
    current_str = ""

    for char in s:
        if char.isdigit():
            current_num = current_num * 10 + int(char)
        elif char == '[':
            stack.append((current_str, current_num))
            current_str = ""
            current_num = 0
        elif char == ']':
            prev_str, num = stack.pop()
            current_str = prev_str + current_str * num
        else:
            current_str += char

    return current_str
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 18. Evaluate Bracket Pairs

### Problem
Replace bracket pairs with values from knowledge array.

### Algorithm
```python
def evaluate(s, knowledge):
    knowledge = dict(knowledge)
    result = []
    i = 0

    while i < len(s):
        if s[i] == '(':
            j = s.find(')', i)
            key = s[i + 1:j]
            result.append(knowledge.get(key, '?'))
            i = j + 1
        else:
            result.append(s[i])
            i += 1

    return ''.join(result)
```

### Complexity
- **Time:** O(n + k)
- **Space:** O(k)

---

## 19. Maximum Width Ramp

### Problem
Find maximum width ramp (i < j and A[i] <= A[j]).

### Algorithm
```python
def max_width_ramp(nums):
    stack = []
    # Build decreasing stack of indices
    for i, num in enumerate(nums):
        if not stack or nums[stack[-1]] > num:
            stack.append(i)

    max_width = 0
    # Traverse from right
    for j in range(len(nums) - 1, -1, -1):
        while stack and nums[stack[-1]] <= nums[j]:
            max_width = max(max_width, j - stack.pop())

    return max_width
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 20. Score of Parentheses

### Problem
Calculate score: () = 1, AB = A + B, (A) = 2 * A.

### Algorithm
```python
def score_of_parentheses(s):
    stack = [0]  # Score at current depth

    for char in s:
        if char == '(':
            stack.append(0)
        else:
            score = stack.pop()
            stack[-1] += max(2 * score, 1)

    return stack[0]
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 21. Trapping Rain Water (Stack Approach)

### Problem
Calculate trapped rainwater using stack.

### Algorithm
```python
def trap(height):
    stack = []
    water = 0

    for i, h in enumerate(height):
        while stack and height[stack[-1]] < h:
            mid = stack.pop()
            if stack:
                left = stack[-1]
                width = i - left - 1
                min_height = min(height[left], h) - height[mid]
                water += width * min_height
        stack.append(i)

    return water
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 22. Exclusive Time of Functions

### Problem
Calculate exclusive time of each function.

### Algorithm
```python
def exclusive_time(n, logs):
    result = [0] * n
    stack = []
    prev_time = 0

    for log in logs:
        fid, typ, time = log.split(':')
        fid, time = int(fid), int(time)

        if typ == 'start':
            if stack:
                result[stack[-1]] += time - prev_time
            stack.append(fid)
            prev_time = time
        else:
            result[stack.pop()] += time - prev_time + 1
            prev_time = time + 1

    return result
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 23. Baseball Game

### Problem
Calculate total score with special operations.

### Algorithm
```python
def cal_points(ops):
    stack = []

    for op in ops:
        if op == '+':
            stack.append(stack[-1] + stack[-2])
        elif op == 'D':
            stack.append(2 * stack[-1])
        elif op == 'C':
            stack.pop()
        else:
            stack.append(int(op))

    return sum(stack)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 24. Remove Outermost Parentheses

### Problem
Remove outermost parentheses of every primitive string.

### Algorithm
```python
def remove_outer_parentheses(s):
    result = []
    opened = 0

    for char in s:
        if char == '(':
            if opened > 0:
                result.append(char)
            opened += 1
        else:
            opened -= 1
            if opened > 0:
                result.append(char)

    return ''.join(result)
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)
