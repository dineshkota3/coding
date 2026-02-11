# Sorting - Learning Objectives

## Overview
Sorting is fundamental to computer science. Understanding sorting algorithms helps in problem-solving and optimizing solutions.

## Learning Objectives

### 1. Sorting Paradigms
- Understand comparison-based vs non-comparison sorting
- Learn divide and conquer approach (merge sort, quick sort)
- Master in-place vs out-of-place sorting
- Understand stable vs unstable sorting

### 2. Algorithm Selection
- Learn when to use specific sorting algorithms
- Understand time-space tradeoffs
- Master choosing optimal sort for given constraints
- Practice custom comparator implementations

### 3. Comparison-Based Sorting
- Master merge sort (stable, O(n log n))
- Master quick sort (in-place, average O(n log n))
- Understand heap sort (in-place, guaranteed O(n log n))
- Learn insertion sort for small/nearly sorted arrays

### 4. Non-Comparison Sorting
- Learn counting sort for integers with small range
- Master radix sort for integers
- Understand bucket sort for uniform distribution
- Know when linear-time sorting is possible

## Python-Specific Notes
- Built-in `sorted()` returns new list, uses Timsort
- `list.sort()` sorts in-place
- Use `key` parameter for custom sorting: `sorted(arr, key=lambda x: x[1])`
- `functools.cmp_to_key()` for custom comparators

## Success Criteria
- [ ] Implement merge sort and quick sort from scratch
- [ ] Understand when each sorting algorithm is optimal
- [ ] Apply sorting as preprocessing for other problems
- [ ] Implement counting sort and radix sort
- [ ] Design custom comparators for complex sorting
