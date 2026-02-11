# Stack - Practice Problems

## Easy Problems

### 1. Implement Stack using Queues
**LeetCode:** #225

**Description:**
Implement a stack using only queues. The stack should support push, top, pop, and empty operations.

**Example:**
```
stack.push(1)
stack.push(2)
stack.top() -> 2
stack.pop() -> 2
stack.empty() -> false
```

**Approach Hint:** Use two queues or one queue with rotation.

---

### 2. Remove All Adjacent Duplicates In String
**LeetCode:** #1047

**Description:**
Given a string `s`, repeatedly remove adjacent duplicates until no more can be removed.

**Example:**
```
Input: s = "abbaca"
Output: "ca"
Explanation: "abbaca" -> "aaca" -> "ca"
```

**Approach Hint:** Use stack, pop when top equals current character.

---

### 3. Removing Stars From a String
**LeetCode:** #2390

**Description:**
Given a string with '*' characters, each '*' removes the closest non-'*' character to its left.

**Example:**
```
Input: s = "leet**cod*e"
Output: "lecoe"
```

**Approach Hint:** Use stack, pop on '*', push otherwise.

---

### 4. Backspace String Compare
**LeetCode:** #844

**Description:**
Given two strings with '#' representing backspace, determine if they are equal after processing.

**Example:**
```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both become "ac"
```

**Approach Hint:** Use stack to build final strings, then compare.

---

### 5. Minimum Add to Make Parentheses Valid
**LeetCode:** #921

**Description:**
Return the minimum number of parentheses to add to make the string valid.

**Example:**
```
Input: s = "())"
Output: 1
```

**Approach Hint:** Track unmatched open and close parentheses.

---

## Medium Problems

### 6. Asteroid Collision
**LeetCode:** #735

**Description:**
Asteroids moving in a line. Positive moves right, negative moves left. When they collide, smaller explodes. Equal both explode.

**Example:**
```
Input: asteroids = [5, 10, -5]
Output: [5, 10]
Explanation: 10 and -5 collide, -5 explodes.
```

**Approach Hint:** Use stack, handle collisions while top > 0 and current < 0.

---

### 7. Online Stock Span
**LeetCode:** #901

**Description:**
Design a class that returns the span of stock price (consecutive days with price <= today).

**Example:**
```
stockSpanner.next(100) -> 1
stockSpanner.next(80) -> 1
stockSpanner.next(60) -> 1
stockSpanner.next(70) -> 2
```

**Approach Hint:** Use monotonic decreasing stack storing (price, span).

---

### 8. Score of Parentheses
**LeetCode:** #856

**Description:**
Given balanced parentheses string, compute score: () = 1, AB = A + B, (A) = 2 * A.

**Example:**
```
Input: s = "(()(()))"
Output: 6
Explanation: ()()() = 1 + 2 * (1 + 1) = 6
```

**Approach Hint:** Use stack to track depth and scores.

---

### 9. Min Stack
**LeetCode:** #155

**Description:**
Design a stack that supports push, pop, top, and getMin in O(1) time.

**Example:**
```
minStack.push(-2)
minStack.push(0)
minStack.push(-3)
minStack.getMin() -> -3
minStack.pop()
minStack.top() -> 0
```

**Approach Hint:** Use auxiliary stack to track minimums.

---

### 10. Valid Parentheses
**LeetCode:** #20

**Description:**
Determine if input string with brackets is valid.

**Example:**
```
Input: s = "()[]{}"
Output: true
```

**Approach Hint:** Use stack to match opening and closing brackets.

---

## Hard Problems

### 11. Basic Calculator III
**LeetCode:** #772

**Description:**
Evaluate expression with +, -, *, /, (, ).

**Example:**
```
Input: s = "2*(5+5*2)/3+(6/2+8)"
Output: 21
```

**Approach Hint:** Use two stacks - one for numbers, one for operators. Handle precedence.

---

## Additional Practice

### Next Greater Element I (Easy) - #496
Find next greater element for elements in subset.

### Baseball Game (Easy) - #682
Calculate points based on operations.

### Make The String Great (Easy) - #1544
Remove adjacent characters that differ by 32.

### Daily Temperatures (Medium) - #739
Find days until warmer temperature.

### Evaluate Reverse Polish Notation (Medium) - #150
Evaluate postfix expression.

### Simplify Path (Medium) - #71
Simplify Unix file path.

### Decode String (Medium) - #394
Decode string with nested repetition.

### Car Fleet (Medium) - #853
Determine number of car fleets.

### Largest Rectangle in Histogram (Hard) - #84
Find largest rectangular area.

### Maximal Rectangle (Hard) - #85
Find maximal rectangle of 1s in matrix.

---

## Problem-Solving Tips

1. **When to use stack:**
   - Matching/pairing (parentheses, tags)
   - Expression evaluation
   - Next greater/smaller element
   - Undo/history operations
   - Depth-first operations

2. **Monotonic stack:**
   - Increasing: for next smaller element
   - Decreasing: for next greater element
   - Each element pushed/popped at most once

3. **Two stack patterns:**
   - Min stack: track minimum
   - Queue from stacks: amortized O(1)
   - Expression evaluation: values and operators

4. **Edge cases:**
   - Empty input
   - Single element
   - All same elements
   - Nested structures
