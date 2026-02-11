# Heap & Priority Queue - Learning Objectives

## Overview
Heap is a complete binary tree satisfying heap property. Priority queue is typically implemented using heap for O(log n) operations.

## Learning Objectives

### 1. Heap Data Structure Mastery
- Understand complete binary tree property
- Master min-heap vs max-heap distinction
- Learn array representation of heap
- Understand heap operations complexity

### 2. Heap Operations
- Master insert operation (bubble up)
- Learn extract min/max (bubble down)
- Understand heapify process
- Master build heap from array

### 3. Priority Queue Applications
- Learn to use Python heapq module
- Understand top-k problems
- Master merge k sorted lists
- Practice median finding problems

### 4. Heap Sort
- Understand heap sort algorithm
- Learn in-place sorting with heap
- Compare with other sorting algorithms
- Master heap sort implementation

## Python-Specific Notes
- heapq is min-heap by default
- For max-heap: negate values
- heapq.heappush(), heapq.heappop()
- heapq.heapify() to build heap in O(n)

## Success Criteria
- [ ] Implement min-heap and max-heap from scratch
- [ ] Use heap to solve top-k problems
- [ ] Merge k sorted lists efficiently
- [ ] Find median from data stream
- [ ] Solve task scheduler using heap
