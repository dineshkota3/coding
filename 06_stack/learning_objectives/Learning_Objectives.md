# Stack - Learning Objectives

## Overview
Stack is a Last-In-First-Out (LIFO) data structure essential for many algorithms and parsing problems.

## Learning Objectives

### 1. LIFO Property Understanding
- Understand Last-In-First-Out behavior
- Learn when LIFO is the natural approach
- Master stack visualization and mental model
- Recognize problems requiring stack

### 2. Stack Operations Mastery
- Master push, pop, peek, and isEmpty operations
- Understand time complexity O(1) for all operations
- Learn stack implementation using array and linked list
- Practice with Python list as stack

### 3. Monotonic Stack Patterns
- Learn increasing monotonic stack
- Learn decreasing monotonic stack
- Master next greater/smaller element problems
- Understand when to use monotonic stack

### 4. Expression Evaluation and Parsing
- Learn to evaluate arithmetic expressions
- Master parenthesis matching
- Understand expression conversion (infix to postfix)
- Practice calculator problems

## Python-Specific Notes
- Use list as stack: `append()` for push, `pop()` for pop
- `stack[-1]` for peek
- `len(stack) == 0` for isEmpty check
- `deque` can also be used but list is typically faster

## Success Criteria
- [ ] Implement stack from scratch using array and linked list
- [ ] Solve valid parentheses and similar problems
- [ ] Apply monotonic stack for next greater element
- [ ] Implement basic calculator
- [ ] Design min stack with O(1) getMin
