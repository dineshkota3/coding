# Greedy - Key Concepts to Master

## 1. Greedy Choice Property

### Definition
A problem has the greedy choice property if a locally optimal choice leads to a globally optimal solution.

### Key Insight
At each step, make the choice that looks best right now, without reconsidering previous choices.

### When Greedy Works
1. **Greedy choice property:** Local optimum leads to global optimum
2. **Optimal substructure:** Optimal solution contains optimal solutions to subproblems

### When Greedy Fails
- Local choice might prevent better global solution
- Need to consider multiple possibilities
- Problem requires looking ahead

## 2. Greedy vs Dynamic Programming

| Greedy | Dynamic Programming |
|--------|---------------------|
| One choice per step | Consider all choices |
| Never backtracks | May reconsider |
| Faster (often O(n)) | Slower (often O(n²)) |
| May not find optimal | Guaranteed optimal |
| Harder to prove correct | Easier to verify |

## 3. Common Greedy Patterns

### Sort and Process
```python
# Activity selection
def activity_selection(activities):
    # Sort by end time
    activities.sort(key=lambda x: x[1])

    result = [activities[0]]
    last_end = activities[0][1]

    for start, end in activities[1:]:
        if start >= last_end:
            result.append((start, end))
            last_end = end

    return result
```

### Greedy with Heap
```python
# Meeting rooms II
import heapq

def min_meeting_rooms(intervals):
    if not intervals:
        return 0

    intervals.sort(key=lambda x: x[0])
    heap = [intervals[0][1]]  # Min-heap of end times

    for start, end in intervals[1:]:
        if start >= heap[0]:
            heapq.heappop(heap)
        heapq.heappush(heap, end)

    return len(heap)
```

### Two-Pointer Greedy
```python
# Container with most water
def max_area(height):
    left, right = 0, len(height) - 1
    max_water = 0

    while left < right:
        width = right - left
        container_height = min(height[left], height[right])
        max_water = max(max_water, width * container_height)

        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_water
```

## 4. Proving Greedy Correctness

### Exchange Argument
1. Assume optimal solution exists
2. Show greedy choice is always part of some optimal solution
3. Prove greedy choice + optimal subproblem = optimal solution

### Greedy Stays Ahead
1. Show greedy algorithm is never worse than optimal after each step
2. Prove by induction

## 5. Classic Problems

### Jump Game
```python
def can_jump(nums):
    max_reach = 0

    for i, num in enumerate(nums):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + num)

    return True
```

### Gas Station
```python
def can_complete_circuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1

    total = 0
    start = 0

    for i in range(len(gas)):
        total += gas[i] - cost[i]
        if total < 0:
            total = 0
            start = i + 1

    return start
```

### Candy Distribution
```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n

    # Left to right
    for i in range(1, n):
        if ratings[i] > ratings[i - 1]:
            candies[i] = candies[i - 1] + 1

    # Right to left
    for i in range(n - 2, -1, -1):
        if ratings[i] > ratings[i + 1]:
            candies[i] = max(candies[i], candies[i + 1] + 1)

    return sum(candies)
```

## 6. Interval Problems

### Merge Intervals
```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for interval in intervals[1:]:
        if interval[0] <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], interval[1])
        else:
            merged.append(interval)

    return merged
```

### Non-overlapping Intervals
```python
def erase_overlap_intervals(intervals):
    if not intervals:
        return 0

    intervals.sort(key=lambda x: x[1])
    count = 0
    prev_end = intervals[0][1]

    for i in range(1, len(intervals)):
        if intervals[i][0] < prev_end:
            count += 1
        else:
            prev_end = intervals[i][1]

    return count
```

## When to Use Greedy

| Problem Type | Greedy Works |
|--------------|--------------|
| Activity selection | Yes |
| Huffman coding | Yes |
| MST (Kruskal/Prim) | Yes |
| Shortest path (Dijkstra) | Yes |
| Knapsack (0/1) | No |
| Longest path | No |

## Time Complexity

| Algorithm | Time |
|-----------|------|
| Activity selection | O(n log n) |
| Jump game | O(n) |
| Gas station | O(n) |
| Candy | O(n) |
| Interval merge | O(n log n) |
