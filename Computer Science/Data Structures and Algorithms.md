# Data Structures and Algorithms Reference Sheet

## Big O Notation

### Common Time Complexities
- O(1) - Constant time
- O(log n) - Logarithmic time
- O(n) - Linear time
- O(n log n) - Linearithmic time
- O(n²) - Quadratic time
- O(n³) - Cubic time
- O(2ⁿ) - Exponential time
- O(n!) - Factorial time

### Common Space Complexities
- O(1) - Constant space
- O(n) - Linear space
- O(n²) - Quadratic space

## Data Structures

### Arrays
```python
# Static Array
- Access: O(1)
- Search: O(n)
- Insert: O(n)
- Delete: O(n)

# Dynamic Array
- Access: O(1)
- Append: O(1) amortized
- Insert: O(n)
- Delete: O(n)
```

### Linked Lists
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Singly Linked List Operations
- Access: O(n)
- Search: O(n)
- Insert at head: O(1)
- Insert at tail: O(n)
- Delete: O(n)

# Doubly Linked List
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None
```

### Stacks
```python
class Stack:
    def __init__(self):
        self.items = []
    
    def push(self, item): # O(1)
        self.items.append(item)
    
    def pop(self): # O(1)
        return self.items.pop()
    
    def peek(self): # O(1)
        return self.items[-1]
```

### Queues
```python
class Queue:
    def __init__(self):
        self.items = []
    
    def enqueue(self, item): # O(1)
        self.items.append(item)
    
    def dequeue(self): # O(1)
        return self.items.pop(0)
```

### Hash Tables
```python
# Operations
- Insert: O(1) average
- Delete: O(1) average
- Search: O(1) average
- Worst case: O(n) for all

# Common Hash Functions
def simple_hash(key, size):
    return key % size

def string_hash(s, size):
    hash_value = 0
    for c in s:
        hash_value = (hash_value * 31 + ord(c)) % size
    return hash_value
```

### Trees
```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Binary Search Tree Operations
- Search: O(log n) average, O(n) worst
- Insert: O(log n) average, O(n) worst
- Delete: O(log n) average, O(n) worst

# AVL Tree
- All operations: O(log n) guaranteed
- Self-balancing
- Balance factor = |height(left) - height(right)| ≤ 1

# Red-Black Tree
- All operations: O(log n) guaranteed
- Self-balancing
- Properties:
  1. Every node is red or black
  2. Root is black
  3. Leaves (NIL) are black
  4. Red nodes have black children
  5. Same number of black nodes in all paths
```

### Heaps
```python
# Min-Heap Operations
- Insert: O(log n)
- Extract Min: O(log n)
- Get Min: O(1)
- Heapify: O(n)

# Implementation using array
parent = (i - 1) // 2
left_child = 2 * i + 1
right_child = 2 * i + 2
```

### Graphs
```python
# Representations

# Adjacency Matrix
graph = [
    [0, 1, 0],
    [1, 0, 1],
    [0, 1, 0]
]

# Adjacency List
graph = {
    'A': ['B'],
    'B': ['A', 'C'],
    'C': ['B']
}
```

## Algorithms

### Sorting Algorithms

#### Comparison-Based Sorts
```python
# Bubble Sort
- Time: O(n²)
- Space: O(1)
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

# Quick Sort
- Time: O(n log n) average, O(n²) worst
- Space: O(log n)
def quick_sort(arr, low, high):
    if low < high:
        pivot = partition(arr, low, high)
        quick_sort(arr, low, pivot-1)
        quick_sort(arr, pivot+1, high)

# Merge Sort
- Time: O(n log n)
- Space: O(n)
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]
        merge_sort(L)
        merge_sort(R)
        merge(arr, L, R)
```

#### Non-Comparison Sorts
```python
# Counting Sort
- Time: O(n + k)
- Space: O(k)
def counting_sort(arr, k):
    count = [0] * k
    for x in arr:
        count[x] += 1
    pos = 0
    for i in range(k):
        for j in range(count[i]):
            arr[pos] = i
            pos += 1

# Radix Sort
- Time: O(d * (n + k))
- Space: O(n + k)
```

### Searching Algorithms
```python
# Binary Search
- Time: O(log n)
- Space: O(1)
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

### Graph Algorithms

#### Graph Traversal
```python
# Breadth-First Search (BFS)
- Time: O(V + E)
- Space: O(V)
def bfs(graph, start):
    visited = set()
    queue = [start]
    while queue:
        vertex = queue.pop(0)
        if vertex not in visited:
            visited.add(vertex)
            queue.extend(graph[vertex] - visited)

# Depth-First Search (DFS)
- Time: O(V + E)
- Space: O(V)
def dfs(graph, vertex, visited=None):
    if visited is None:
        visited = set()
    visited.add(vertex)
    for neighbor in graph[vertex]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

#### Shortest Path Algorithms
```python
# Dijkstra's Algorithm
- Time: O((V + E) log V)
- Space: O(V)

# Bellman-Ford Algorithm
- Time: O(VE)
- Space: O(V)

# Floyd-Warshall Algorithm
- Time: O(V³)
- Space: O(V²)
```

#### Minimum Spanning Tree
```python
# Kruskal's Algorithm
- Time: O(E log E)
- Space: O(V)

# Prim's Algorithm
- Time: O((V + E) log V)
- Space: O(V)
```

### Dynamic Programming
```python
# Key Concepts
1. Overlapping subproblems
2. Optimal substructure
3. Memoization vs Tabulation

# Example: Fibonacci
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib(n-1) + fib(n-2)
    return memo[n]

# Common Problems
- Knapsack Problem
- Longest Common Subsequence
- Matrix Chain Multiplication
- Edit Distance
```

### String Algorithms
```python
# Pattern Matching
- Naive: O(mn)
- KMP: O(m + n)
- Rabin-Karp: O(m + n) average

# String Operations
- Substring
- Concatenation
- Pattern matching
- String manipulation
```

## Algorithm Design Techniques

### Divide and Conquer
1. Divide problem into subproblems
2. Solve subproblems recursively
3. Combine solutions
Example: Merge Sort, Quick Sort

### Greedy Algorithms
1. Make locally optimal choice
2. Hope for global optimum
Example: Dijkstra's Algorithm, Huffman Coding

### Dynamic Programming
1. Break down into subproblems
2. Store solutions to subproblems
3. Build up to larger solutions
Example: Fibonacci, Knapsack

### Backtracking
1. Build candidates incrementally
2. Abandon candidates ("backtrack")
Example: N-Queens, Sudoku Solver
