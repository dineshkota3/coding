# Hashing - Learning Objectives

## Overview
Hashing provides O(1) average time for insert, delete, and lookup operations. It's essential for optimizing many algorithms.

## Learning Objectives

### 1. Hash Function Design
- Understand what makes a good hash function
- Learn properties: uniform distribution, deterministic, efficient
- Understand hash collisions and their impact
- Practice designing simple hash functions

### 2. Hash Map and Hash Set Mastery
- Master Python dict and set operations
- Understand time complexity analysis
- Learn when to use set vs map
- Practice common hash map patterns

### 3. Collision Handling
- Learn chaining (linked lists at each bucket)
- Understand open addressing (linear probing, quadratic probing)
- Know load factor and rehashing concepts
- Understand Python's collision resolution

### 4. Optimization with Hashing
- Learn to trade space for time using hashing
- Master frequency counting patterns
- Apply hashing to subarray problems
- Use hashing for duplicate detection

## Python-Specific Notes
- `dict`: Key-value pairs, O(1) average operations
- `set`: Unique values, O(1) average operations
- `collections.Counter`: Frequency counting
- `collections.defaultdict`: Auto-initialize values
- Dictionary comprehensions: `{k: v for k, v in items}`

## Success Criteria
- [ ] Implement a simple hash map from scratch
- [ ] Use hashing to optimize O(n²) to O(n)
- [ ] Solve frequency counting problems
- [ ] Apply hashing to subarray sum problems
- [ ] Design LRU Cache using hash map + doubly linked list
