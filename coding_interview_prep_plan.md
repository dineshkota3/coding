# Coding Interview Preparation Plan (Python)

## Table of Contents
1. [Arrays & Matrix](#1-arrays--matrix)
2. [String](#2-string)
3. [Searching](#3-searching)
4. [Sorting](#4-sorting)
5. [Hashing](#5-hashing)
6. [Stack](#6-stack)
7. [Queue](#7-queue)
8. [Linked List](#8-linked-list)
9. [Recursion](#9-recursion)
10. [Backtracking](#10-backtracking)
11. [Tree](#11-tree)
12. [BST](#12-bst-binary-search-tree)
13. [Heap/Priority Queue](#13-heap--priority-queue)
14. [Graph](#14-graph)
15. [Greedy](#15-greedy)
16. [Dynamic Programming](#16-dynamic-programming)
17. [Trie](#17-trie)

---

## 1. ARRAYS & MATRIX

### Learning Objectives
- Understand array indexing and memory layout
- Master two pointers technique
- Learn sliding window technique (fixed and variable size)
- Practice matrix traversal patterns
- Understand in-place array modifications

### Key Concepts to Master
- Two pointers (opposite ends, fast-slow)
- Sliding window (fixed size, variable size)
- Matrix rotation (transpose + reverse)
- Spiral traversal
- Prefix sums
- Kadane's algorithm
- Merge intervals pattern

### Algorithms to Learn
- Two Sum (hash map approach)
- Maximum Subarray (Kadane's Algorithm)
- Merge Intervals
- Rotate Matrix (90 degrees clockwise and counter-clockwise)
- Spiral Matrix Traversal
- Sliding Window Maximum
- Container With Most Water
- Product of Array Except Self
- Find Minimum in Rotated Sorted Array
- Search in 2D Matrix

### Practice Problems (Easy to Hard)
- Two Sum
- Best Time to Buy and Sell Stock
- Contains Duplicate
- Maximum Subarray
- Move Zeros
- Product of Array Except Self
- Set Matrix Zeroes
- 3Sum
- 4Sum
- Merge Intervals
- Search a 2D Matrix II

---

## 2. STRING

### Learning Objectives
- Master string manipulation techniques
- Learn pattern matching algorithms
- Understand string encoding/decoding
- Practice palindrome problems

### Key Concepts to Master
- Two pointers for string manipulation
- Sliding window for substring problems
- KMP algorithm for pattern matching
- Palindrome expansion technique
- String hashing (Rabin-Karp)
- Trie prefix matching

### Algorithms to Learn
- Longest Substring Without Repeating Characters
- Longest Palindromic Substring (expand around center)
- Valid Anagram
- String to Integer (atoi)
- KMP Pattern Matching
- Rabin-Karp Algorithm
- Z Algorithm
- Manacher's Algorithm (longest palindromic substring)

### Practice Problems
- Valid Palindrome
- Longest Common Prefix
- Valid Parentheses
- Implement strStr()
- Count and Say
- Group Anagrams
- Longest Substring Without Repeating Characters
- Minimum Window Substring
- Encode and Decode Strings

---

## 3. SEARCHING

### Learning Objectives
- Master binary search and its variations
- Understand search space optimization
- Learn binary search on answer pattern

### Key Concepts to Master
- Binary search (standard implementation)
- Binary search variations (first/last position)
- Lower bound and upper bound
- Binary search on answer
- Search in rotated sorted arrays
- Ternary search
- Exponential search

### Algorithms to Learn
- Standard Binary Search
- Binary Search - First Occurrence
- Binary Search - Last Occurrence
- Binary Search - Lower Bound
- Binary Search - Upper Bound
- Search in Rotated Sorted Array
- Find Minimum in Rotated Sorted Array
- Search in 2D Matrix
- Median of Two Sorted Arrays
- Find Peak Element

### Practice Problems
- Binary Search
- Search Insert Position
- First Bad Version
- Search in Rotated Sorted Array
- Find Minimum in Rotated Sorted Array
- Search a 2D Matrix
- Find Peak Element
- Median of Two Sorted Arrays
- Sqrt(x)

---

## 4. SORTING

### Learning Objectives
- Understand different sorting paradigms
- Learn when to use specific sorting algorithms
- Master comparison-based vs non-comparison sorting

### Key Concepts to Master
- Comparison-based sorting limitations
- Divide and conquer approach
- Stable vs unstable sorting
- Time-space tradeoffs
- Counting sort (integer sorting)
- Radix sort (integer sorting)

### Algorithms to Learn
- Bubble Sort (basic understanding)
- Selection Sort (basic understanding)
- Insertion Sort (useful for small/nearly sorted)
- Merge Sort (stable, external sorting)
- Quick Sort (in-place, average case O(n log n))
- Heap Sort (in-place, guaranteed O(n log n))
- Counting Sort (linear time for integers)
- Radix Sort (linear time for integers)
- Bucket Sort (uniform distribution)

### Practice Problems
- Sort Colors (Dutch National Flag)
- Merge Intervals
- Sort List (linked list merge sort)
- Largest Number (custom comparator)
- Meeting Rooms II
- Wiggle Sort
- Pancake Sorting
- Merge Sorted Array
- Relative Sort Array

---

## 5. HASHING

### Learning Objectives
- Understand hash function design
- Master hash map and hash set usage
- Learn collision handling strategies
- Apply hashing to optimize solutions

### Key Concepts to Master
- Hash functions and properties
- Collision resolution (chaining, open addressing)
- Hash set vs hash map
- Time complexity analysis
- Using hashing for O(1) lookups
- Frequency counting
- Subarray sum problems using hashing

### Algorithms to Learn
- Two Sum using Hash Map
- Group Anagrams
- Longest Consecutive Sequence
- Subarray Sum Equals K
- Find Duplicate in Array
- Count Frequency of Elements
- LRU Cache Implementation
- LFU Cache Implementation

### Practice Problems
- Single Number
- Majority Element
- Valid Sudoku
- Copy List with Random Pointer
- Insert Delete GetRandom O(1)
- Logger Rate Limiter
- Design HashSet
- Design HashMap
- Subarray Sum Equals K
- Longest Consecutive Sequence

---

## 6. STACK

### Learning Objectives
- Understand LIFO property
- Master stack operations and applications
- Learn monotonic stack patterns

### Key Concepts to Master
- Stack operations (push, pop, peek, isEmpty)
- Stack using array vs linked list
- Monotonic stack (increasing/decreasing)
- Stack for expression evaluation
- Stack for parsing problems
- Two stack patterns

### Algorithms to Learn
- Valid Parentheses
- Min Stack (O(1) getMin)
- Evaluate Reverse Polish Notation
- Daily Temperatures (Next Greater Element)
- Largest Rectangle in Histogram
- Simplify Path
- Basic Calculator
- Implement Queue using Stacks

### Practice Problems
- Implement Stack using Queues
- Remove All Adjacent Duplicates In String
- Removing Stars From a String
- Asteroid Collision
- Online Stock Span
- Score of Parentheses
- Backspace String Compare
- Minimum Add to Make Parentheses Valid
- Min Stack
- Valid Parentheses

---

## 7. QUEUE

### Learning Objectives
- Understand FIFO property
- Master queue operations and applications
- Learn circular queue implementation

### Key Concepts to Master
- Queue operations (enqueue, dequeue, peek, isEmpty)
- Queue using array (circular)
- Queue using linked list
- Priority queue
- Deque (double-ended queue)
- BFS using queue
- Sliding window using deque

### Algorithms to Learn
- Queue Implementation (array and linked list)
- Circular Queue Implementation
- Implement Stack using Queues
- Sliding Window Maximum (using deque)
- Task Scheduler
- Design Circular Queue
- Design Circular Deque

### Practice Problems
- Design Circular Queue
- Design Circular Deque
- Implement Stack using Queues
- Sliding Window Maximum
- Design Bounded Blocking Queue
- Design Hit Counter
- Moving Average from Data Stream
- Task Scheduler
- Number of Islands (BFS approach)

---

## 8. LINKED LIST

### Learning Objectives
- Master linked list manipulation
- Learn fast and slow pointer technique
- Understand in-place list modifications

### Key Concepts to Master
- Node structure and pointers
- Singly vs doubly linked list
- Dummy node technique
- Fast and slow pointers
- Reversing linked lists
- Cycle detection (Floyd's algorithm)
- Merging sorted lists

### Algorithms to Learn
- Reverse Linked List (iterative and recursive)
- Detect Cycle (Floyd's Algorithm)
- Find Cycle Start Node
- Merge Two Sorted Lists
- Middle of Linked List (fast-slow pointers)
- Remove Nth Node From End
- Reorder Linked List
- Palindrome Linked List
- Intersection of Two Linked Lists

### Practice Problems
- Reverse Linked List
- Merge Two Sorted Lists
- Linked List Cycle
- Reorder List
- Remove Nth Node From End of List
- Add Two Numbers
- Reverse Nodes in k-Group
- Rotate List
- Sort List
- Palindrome Linked List

---

## 9. RECURSION

### Learning Objectives
- Understand recursive thinking
- Master base case and recursive case identification
- Learn recursion vs iteration tradeoffs

### Key Concepts to Master
- Base case definition
- Recursive case design
- Call stack behavior
- Tail recursion
- Recursion tree visualization
- Time complexity analysis (recurrence relations)
- Memoization introduction

### Algorithms to Learn
- Factorial (classic recursion)
- Fibonacci (naive and memoized)
- Power Function (fast exponentiation)
- Binary Search (recursive)
- Generate Subsets
- Generate Permutations
- Tower of Hanoi
- Greatest Common Divisor (Euclidean algorithm)
- Depth-First Search (recursive)

### Practice Problems
- Climbing Stairs
- Combination Sum
- Subsets
- Permutations
- Generate Parentheses
- Letter Combinations of a Phone Number
- Word Search
- Pow(x, n)
- Kth Symbol in Grammar

---

## 10. BACKTRACKING

### Learning Objectives
- Master depth-first search with pruning
- Learn constraint satisfaction problems
- Understand state space exploration

### Key Concepts to Master
- Decision tree traversal
- State space tree
- Pruning invalid branches
- Backtracking vs pure recursion
- Constraint propagation
- Optimization problems using backtracking

### Algorithms to Learn
- N-Queens Problem
- Sudoku Solver
- Generate Parentheses
- Combination Sum
- Subsets (Power Set)
- Permutations
- Word Search
- Palindrome Partitioning
- Letter Combinations of a Phone Number
- Combination Sum II

### Practice Problems
- Subsets
- Subsets II
- Permutations
- Permutations II
- Combination Sum
- Combination Sum II
- Palindrome Partitioning
- Generate Parentheses
- Letter Combinations of a Phone Number
- Word Search
- N-Queens
- Sudoku Solver

---

## 11. TREE

### Learning Objectives
- Master tree data structure
- Learn all tree traversal methods
- Understand tree properties and algorithms

### Key Concepts to Master
- Tree terminology (root, node, leaf, depth, height)
- Binary tree properties
- Tree traversals (inorder, preorder, postorder, level order)
- Recursive vs iterative traversal
- Tree construction from traversals
- Tree balancing concepts

### Algorithms to Learn
- Inorder Traversal (recursive and iterative)
- Preorder Traversal (recursive and iterative)
- Postorder Traversal (recursive and iterative)
- Level Order Traversal (BFS)
- Maximum Depth of Binary Tree
- Check if Binary Tree is Balanced
- Lowest Common Ancestor
- Serialize and Deserialize Binary Tree
- Path Sum
- Invert Binary Tree
- Symmetric Tree

### Practice Problems
- Maximum Depth of Binary Tree
- Invert Binary Tree
- Symmetric Tree
- Path Sum
- Sum Root to Leaf Numbers
- Binary Tree Right Side View
- Flatten Binary Tree to Linked List
- Construct Binary Tree from Preorder and Inorder
- Construct Binary Tree from Inorder and Postorder
- Lowest Common Ancestor of a Binary Tree
- Serialize and Deserialize Binary Tree

---

## 12. BST (BINARY SEARCH TREE)

### Learning Objectives
- Understand BST properties
- Master BST operations
- Learn BST applications

### Key Concepts to Master
- BST property (left < root < right)
- Search, insert, delete operations
- BST traversal gives sorted output
- Height balanced BST
- Floor and ceil in BST
- BST vs sorted array tradeoffs

### Algorithms to Learn
- Search in BST
- Insert into BST
- Delete from BST
- Validate BST
- Kth Smallest Element in BST
- Convert Sorted Array to BST
- Floor in BST
- Ceil in BST
- Lowest Common Ancestor of BST
- BST Iterator

### Practice Problems
- Validate Binary Search Tree
- Lowest Common Ancestor of a BST
- Balanced Binary Tree
- Binary Tree Maximum Path Sum
- Binary Tree Level Order Traversal
- Convert BST to Sorted Doubly Linked List
- Minimum Absolute Difference in BST
- Two Sum IV - Input is a BST
- Kth Smallest Element in a BST
- Convert Sorted Array to Binary Search Tree

---

## 13. HEAP & PRIORITY QUEUE

### Learning Objectives
- Master heap data structure
- Learn priority queue applications
- Understand heap operations and complexity

### Key Concepts to Master
- Complete binary tree property
- Min-heap vs max-heap
- Heap operations (insert, extract, peek)
- Heapify process (build heap)
- Heap sort
- Priority queue applications
- Python heapq module

### Algorithms to Learn
- Min Heap Implementation
- Max Heap Implementation
- Heapify (build heap from array)
- Heap Sort
- Kth Largest Element in Array
- Merge K Sorted Lists
- Top K Frequent Elements
- Find Median from Data Stream
- Task Scheduler (using heap)

### Practice Problems
- Kth Largest Element in an Array
- Top K Frequent Elements
- Merge K Sorted Lists
- Find Median from Data Stream
- Kth Smallest Element in a Sorted Matrix
- Reorganize String
- Last Stone Weight
- K Closest Points to Origin
- Sort Characters By Frequency
- Task Scheduler

---

## 14. GRAPH

### Learning Objectives
- Master graph representation and traversal
- Learn fundamental graph algorithms
- Understand shortest path algorithms

### Key Concepts to Master
- Graph representation (adjacency list, adjacency matrix)
- Graph types (directed, undirected, weighted, unweighted)
- Graph traversal (BFS, DFS)
- Connected components
- Topological sort
- Shortest path algorithms
- Minimum spanning tree

### Algorithms to Learn
- Breadth-First Search (BFS)
- Depth-First Search (DFS)
- Detect Cycle in Undirected Graph
- Detect Cycle in Directed Graph
- Topological Sort (Kahn's Algorithm)
- Dijkstra's Algorithm (single source shortest path)
- Bellman-Ford Algorithm
- Union-Find (Disjoint Set Union)
- Kruskal's Algorithm (MST)
- Prim's Algorithm (MST)

### Practice Problems
- Course Schedule (cycle detection)
- Course Schedule II (topological sort)
- Clone Graph
- Pacific Atlantic Water Flow
- Number of Islands
- Surrounded Regions
- Rotting Oranges
- Word Ladder (BFS)
- Graph Valid Tree
- Minimum Spanning Tree

---

## 15. GREEDY

### Learning Objectives
- Understand greedy choice property
- Learn when greedy approach works
- Master classic greedy problems

### Key Concepts to Master
- Greedy choice property
- Optimal substructure
- Local optimum → global optimum
- Greedy vs dynamic programming
- Activity selection
- Interval scheduling

### Algorithms to Learn
- Activity Selection Problem
- Jump Game (can reach end)
- Jump Game II (minimum jumps)
- Gas Station Problem
- Candy Distribution
- Partition Labels
- Minimum Number of Arrows to Burst Balloons
- Task Scheduler (greedy approach)
- Huffman Coding (concept)

### Practice Problems
- Maximum Subarray (Kadane's)
- Best Time to Buy and Sell Stock II
- Merge Intervals
- Non-overlapping Intervals
- Queue Reconstruction by Height
- Assign Cookies
- Boat to Save People
- Jump Game
- Jump Game II
- Gas Station
- Candy
- Partition Labels

---

## 16. DYNAMIC PROGRAMMING

### Learning Objectives
- Master DP problem-solving approach
- Learn to identify DP problems
- Understand memoization and tabulation

### Key Concepts to Master
- Overlapping subproblems
- Optimal substructure
- Memoization (top-down)
- Tabulation (bottom-up)
- State definition
- State transition
- 1D, 2D, and multi-dimensional DP
- Space optimization techniques

### Algorithms to Learn
- Fibonacci Series (DP approach)
- Climbing Stairs
- House Robber
- Longest Increasing Subsequence
- Longest Common Subsequence
- 0/1 Knapsack Problem
- Coin Change (minimum coins)
- Coin Change II (number of ways)
- Edit Distance
- Maximum Subarray Sum (Kadane's)
- Unique Paths
- Palindromic Substrings
- Decode Ways
- Partition Equal Subset Sum
- Matrix Chain Multiplication

### Practice Problems
- Climbing Stairs
- House Robber
- House Robber II
- Longest Increasing Subsequence
- Longest Common Subsequence
- 0/1 Knapsack
- Coin Change
- Coin Change 2
- Edit Distance
- Unique Paths
- Unique Paths II
- Minimum Path Sum
- Dungeon Game
- Interleaving String
- Decode Ways
- Partition Equal Subset Sum
- Target Sum
- Word Break
- Burst Balloons
- Best Time to Buy and Sell Stock with Cooldown
- Palindromic Substrings

---

## 17. TRIE

### Learning Objectives
- Master prefix tree structure
- Learn trie operations
- Understand trie applications

### Key Concepts to Master
- Trie node structure
- Trie properties
- Insert, search, delete operations
- Prefix search
- Memory optimization (compressed trie)
- Trie vs hash map for strings

### Algorithms to Learn
- Trie Implementation
- Insert Operation
- Search Operation
- Starts With (Prefix Search)
- Delete Operation
- Word Dictionary (add and search with wildcard)
- Implement Trie with Count
- Replace Words
- Longest Word in Dictionary

### Practice Problems
- Implement Trie (Prefix Tree)
- Design Add and Search Words Data Structure
- Word Search II
- Prefix and Suffix Search
- Stream of Characters
- Map Sum Pairs
- Implement Magic Dictionary
- Concatenated Words
- Replace Words
- Longest Word in Dictionary

---

## STUDY SCHEDULE RECOMMENDATION (14 WEEKS)

### Week 1-2: Foundations
- **Days 1-3**: Arrays & Matrix
  - Two pointers, sliding window, matrix operations
- **Days 4-6**: Strings
  - String manipulation, pattern matching
- **Days 7-8**: Searching
  - Binary search and variations
- **Days 9-10**: Sorting
  - Merge sort, quick sort, counting sort

### Week 3-4: Linear Data Structures
- **Days 1-2**: Hashing
  - Hash maps, hash sets, collision handling
- **Days 3-4**: Stack
  - Stack operations, monotonic stack
- **Days 5-6**: Queue
  - Queue operations, circular queue, deque
- **Days 7-10**: Linked List
  - List manipulation, fast-slow pointers, cycles

### Week 5-6: Recursion & Trees
- **Days 1-3**: Recursion
  - Recursive thinking, base cases, memoization intro
- **Days 4-6**: Backtracking
  - Decision trees, pruning, constraint satisfaction
- **Days 7-10**: Tree
  - Traversals, tree properties, tree algorithms

### Week 7-8: Advanced Trees & Heaps
- **Days 1-3**: BST
  - BST operations, validation, search
- **Days 4-6**: Heap/Priority Queue
  - Heap operations, heapify, priority queue apps
- **Days 7-10**: Graph Basics
  - Graph representation, BFS, DFS

### Week 9-10: Graph Algorithms
- **Days 1-2**: Graph Traversal
  - BFS, DFS applications
- **Days 3-4**: Cycle Detection
  - Undirected and directed graphs
- **Days 5-6**: Topological Sort
  - Kahn's algorithm, DAG problems
- **Days 7-8**: Shortest Path
  - Dijkstra, Bellman-Ford
- **Days 9-10**: MST & Union-Find
  - Kruskal's, Prim's algorithm

### Week 11-12: Algorithm Paradigms
- **Days 1-4**: Greedy
  - Activity selection, interval problems
- **Days 5-8**: Dynamic Programming - Basics
  - 1D DP, classic problems
- **Days 9-14**: Dynamic Programming - Advanced
  - 2D DP, optimization problems

### Week 13: Advanced Topics
- **Days 1-2**: Trie
  - Prefix tree, trie operations
- **Days 3-7**: Mixed Practice
  - Problems from all topics

### Week 14: Final Review
- **Days 1-3**: Mock Interviews
  - Timed problem-solving
- **Days 4-5**: Weak Area Focus
  - Targeted practice
- **Days 6-7**: Speed Practice
  - Quick problem-solving

---

## PRACTICE PROBLEMS BY DIFFICULTY

### Easy (Build Foundation)
- Two Sum
- Valid Parentheses
- Merge Two Sorted Lists
- Maximum Subarray
- Climbing Stairs
- Best Time to Buy and Sell Stock
- Contains Duplicate
- Valid Anagram
- Reverse Linked List
- Binary Search
- Invert Binary Tree
- Single Number
- Majority Element

### Medium (Core Practice)
- 3Sum
- Group Anagrams
- Validate BST
- Word Search
- Longest Increasing Subsequence
- Longest Common Subsequence
- Subsets
- Permutations
- Combination Sum
- Kth Largest Element
- Top K Frequent Elements
- Course Schedule
- Clone Graph
- Number of Islands
- Insert Interval
- Binary Tree Level Order Traversal
- Construct Binary Tree from Traversals
- Implement Trie
- Word Dictionary
- House Robber
- Coin Change

### Hard (Challenge Yourself)
- Median of Two Sorted Arrays
- Trapping Rain Water
- N-Queens
- Word Ladder II
- Regular Expression Matching
- Burst Balloons
- Merge K Sorted Lists
- LRUCache
- Sudoku Solver
- Serialize and Deserialize Binary Tree
- Binary Tree Maximum Path Sum
- Find Median from Data Stream
- Palindrome Pairs
- Word Search II
- Minimum Window Substring
- Edit Distance
- Distinct Subsequences

---

## RECOMMENDED LEARNING RESOURCES

### Books
- "Cracking the Coding Interview" by Gayle Laakmann McDowell
- "Elements of Programming Interviews" by Adnan Aziz et al.
- "Introduction to Algorithms" (CLRS) - for reference

### Online Platforms
- **LeetCode** (https://leetcode.com/) - Primary practice platform
- **HackerRank** (https://www.hackerrank.com/) - Skill-specific practice
- **Codeforces** (https://codeforces.com/) - Competitive programming
- **GeeksforGeeks** (https://www.geeksforgeeks.org/) - Tutorial and problems

### Video Resources
- NeetCode (YouTube)
- Tushar Roy (YouTube)
- WilliamFiset (YouTube)
- Abdul Bari (YouTube - algorithms)

### Visualization Tools
- Visualgo.net (algorithm visualization)
- USACO Guide (competitive programming)

---

## SUCCESS TIPS

### Daily Practice Routine
1. **Warm-up** (15 min): Review previous problems
2. **Learn** (30 min): Study new concept/algorithm
3. **Practice** (60 min): Solve 2-3 problems
4. **Review** (15 min): Analyze solutions and learnings

### Problem-Solving Strategy
1. **Understand**: Read problem carefully, identify input/output
2. **Analyze**: Identify patterns and possible approaches
3. **Plan**: Choose optimal approach, outline solution
4. **Implement**: Write clean, readable code
5. **Test**: Verify with examples and edge cases
6. **Optimize**: Review time and space complexity

### Common Mistakes to Avoid
- Jumping to solutions without thinking
- Not practicing edge cases
- Ignoring time/space complexity analysis
- Not revisiting problems after solving
- Focusing only on easy problems
- Memorizing instead of understanding

### Interview Day Tips
- Think aloud during the interview
- Start with brute force, then optimize
- Clarify assumptions before coding
- Test your code with examples
- Handle edge cases explicitly
- Communicate your thought process

---

**Remember: Consistency beats intensity. Practice regularly, focus on understanding, and don't be afraid to revisit problems multiple times. Good luck with your preparation!**
