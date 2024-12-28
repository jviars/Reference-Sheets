# Graph Theory Reference Sheet

## Basic Concepts

### Graph Definitions
1. **Undirected Graph**
   - G = (V,E) where V is vertex set, E is edge set
   - E consists of unordered pairs {u,v}
   ```python
   class Graph:
       def __init__(self):
           self.adj_list = {}
           
       def add_edge(self, u, v):
           if u not in self.adj_list:
               self.adj_list[u] = []
           if v not in self.adj_list:
               self.adj_list[v] = []
           self.adj_list[u].append(v)
           self.adj_list[v].append(u)
   ```

2. **Directed Graph (Digraph)**
   - E consists of ordered pairs (u,v)
   - Edge (u,v) is different from (v,u)

3. **Weighted Graph**
   - Each edge has a weight/cost
   - G = (V,E,w) where w is weight function

### Graph Properties
1. **Degree**
   - deg(v) = number of edges incident to v
   - For digraphs:
     * in-degree = number of incoming edges
     * out-degree = number of outgoing edges

2. **Handshaking Lemma**
   - Σv∈V deg(v) = 2|E|
   - Sum of degrees equals twice number of edges

3. **Path and Cycle**
   - Path: sequence of vertices connected by edges
   - Simple path: no repeated vertices
   - Cycle: path starting and ending at same vertex
   - Simple cycle: no repeated vertices except start/end

## Graph Types

### Special Graphs
1. **Complete Graph (Kₙ)**
   - Every vertex connected to every other vertex
   - n vertices, n(n-1)/2 edges

2. **Bipartite Graph**
   - V can be partitioned into two sets
   - Edges only between sets, not within
   ```python
   def is_bipartite(graph):
       color = {}
       for node in graph:
           if node not in color:
               color[node] = 0
               stack = [node]
               while stack:
                   u = stack.pop()
                   for v in graph[u]:
                       if v not in color:
                           color[v] = 1 - color[u]
                           stack.append(v)
                       elif color[v] == color[u]:
                           return False
       return True
   ```

3. **Trees**
   - Connected graph with no cycles
   - n vertices, n-1 edges
   - Unique path between any two vertices

4. **Planar Graphs**
   - Can be drawn on plane without edge crossings
   - Euler's formula: V - E + F = 2
   - Maximum edges: 3V - 6 (V ≥ 3)

## Graph Traversal

### Depth-First Search (DFS)
```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    
    for next_vertex in graph[start]:
        if next_vertex not in visited:
            dfs(graph, next_vertex, visited)
    return visited
```

### Breadth-First Search (BFS)
```python
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    
    while queue:
        vertex = queue.popleft()
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return visited
```

## Shortest Paths

### Dijkstra's Algorithm
```python
def dijkstra(graph, start):
    distances = {vertex: float('infinity') for vertex in graph}
    distances[start] = 0
    unvisited = set(graph)
    
    while unvisited:
        current = min(unvisited, key=lambda x: distances[x])
        unvisited.remove(current)
        
        for neighbor, weight in graph[current].items():
            distance = distances[current] + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
    return distances
```

### Bellman-Ford Algorithm
```python
def bellman_ford(graph, start):
    distances = {vertex: float('infinity') for vertex in graph}
    distances[start] = 0
    
    for _ in range(len(graph) - 1):
        for u in graph:
            for v, weight in graph[u].items():
                if distances[u] + weight < distances[v]:
                    distances[v] = distances[u] + weight
    
    # Check for negative cycles
    for u in graph:
        for v, weight in graph[u].items():
            if distances[u] + weight < distances[v]:
                raise ValueError("Graph contains negative cycle")
    
    return distances
```

### Floyd-Warshall Algorithm
```python
def floyd_warshall(graph):
    dist = {v: {u: float('infinity') for u in graph} for v in graph}
    for v in graph:
        dist[v][v] = 0
        for u, weight in graph[v].items():
            dist[v][u] = weight
    
    for k in graph:
        for i in graph:
            for j in graph:
                dist[i][j] = min(dist[i][j],
                               dist[i][k] + dist[k][j])
    return dist
```

## Minimum Spanning Trees

### Kruskal's Algorithm
```python
def kruskal(graph):
    edges = [(w, u, v) for u in graph for v, w in graph[u].items()]
    edges.sort()
    parent = {v: v for v in graph}
    
    def find(v):
        if parent[v] != v:
            parent[v] = find(parent[v])
        return parent[v]
    
    def union(v1, v2):
        parent[find(v1)] = find(v2)
    
    mst = []
    for w, u, v in edges:
        if find(u) != find(v):
            union(u, v)
            mst.append((u, v, w))
    return mst
```

### Prim's Algorithm
```python
from heapq import heappush, heappop

def prim(graph):
    start_vertex = next(iter(graph))
    mst = []
    visited = {start_vertex}
    edges = [(w, start_vertex, v) for v, w in graph[start_vertex].items()]
    heapify(edges)
    
    while edges and len(visited) < len(graph):
        w, u, v = heappop(edges)
        if v not in visited:
            visited.add(v)
            mst.append((u, v, w))
            for next_vertex, weight in graph[v].items():
                if next_vertex not in visited:
                    heappush(edges, (weight, v, next_vertex))
    return mst
```

## Network Flow

### Ford-Fulkerson Algorithm
```python
def ford_fulkerson(graph, source, sink):
    def bfs(residual_graph, s, t, parent):
        visited = set([s])
        queue = deque([s])
        parent[s] = None
        
        while queue:
            u = queue.popleft()
            for v, capacity in residual_graph[u].items():
                if v not in visited and capacity > 0:
                    visited.add(v)
                    parent[v] = u
                    queue.append(v)
        return sink in visited
    
    max_flow = 0
    parent = {}
    residual_graph = {u: {v: cap for v, cap in edges.items()}
                     for u, edges in graph.items()}
    
    while bfs(residual_graph, source, sink, parent):
        path_flow = float('infinity')
        s = sink
        while s != source:
            path_flow = min(path_flow, residual_graph[parent[s]][s])
            s = parent[s]
        
        max_flow += path_flow
        v = sink
        while v != source:
            u = parent[v]
            residual_graph[u][v] -= path_flow
            residual_graph[v][u] += path_flow
            v = parent[v]
    
    return max_flow
```

## Graph Coloring

### Vertex Coloring
```python
def greedy_coloring(graph):
    colors = {}
    for vertex in graph:
        used_colors = {colors.get(neighbor)
                      for neighbor in graph[vertex]
                      if neighbor in colors}
        for color in range(len(graph)):
            if color not in used_colors:
                colors[vertex] = color
                break
    return colors
```

### Edge Coloring
```python
def edge_coloring(graph):
    edges = [(u, v) for u in graph for v in graph[u] if u < v]
    colors = {}
    
    for u, v in edges:
        used_colors = {colors.get((u, w)) for w in graph[u]}
        used_colors.update(colors.get((w, v)) for w in graph[v])
        
        for color in range(max(len(graph), 1)):
            if color not in used_colors:
                colors[(u, v)] = color
                colors[(v, u)] = color
                break
    
    return colors
```

## Graph Properties

### Connectivity
1. **Connected Components**
```python
def find_components(graph):
    visited = set()
    components = []
    
    for vertex in graph:
        if vertex not in visited:
            component = dfs(graph, vertex)
            components.append(component)
            visited.update(component)
    
    return components
```

2. **Articulation Points**
```python
def find_articulation_points(graph):
    disc = {}
    low = {}
    parent = {}
    ap = set()
    time = [0]
    
    def dfs(u):
        children = 0
        disc[u] = low[u] = time[0]
        time[0] += 1
        
        for v in graph[u]:
            if v not in disc:
                children += 1
                parent[v] = u
                dfs(v)
                low[u] = min(low[u], low[v])
                
                if parent[u] is None and children > 1:
                    ap.add(u)
                if parent[u] is not None and low[v] >= disc[u]:
                    ap.add(u)
            elif v != parent[u]:
                low[u] = min(low[u], disc[v])
    
    for vertex in graph:
        if vertex not in disc:
            parent[vertex] = None
            dfs(vertex)
    
    return ap
```

### Cycles
1. **Cycle Detection**
```python
def has_cycle(graph):
    visited = set()
    rec_stack = set()
    
    def dfs(vertex):
        visited.add(vertex)
        rec_stack.add(vertex)
        
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                if dfs(neighbor):
                    return True
            elif neighbor in rec_stack:
                return True
        
        rec_stack.remove(vertex)
        return False
    
    for vertex in graph:
        if vertex not in visited:
            if dfs(vertex):
                return True
    return False
```

2. **Eulerian Circuit**
```python
def is_eulerian(graph):
    # Check if all vertices have even degree
    return all(len(edges) % 2 == 0 for edges in graph.values())
```

### Matching
1. **Maximum Bipartite Matching**
```python
def max_bipartite_matching(graph, X, Y):
    matches = {}
    
    def bpm(u, seen):
        for v in graph[u]:
            if v not in seen:
                seen.add(v)
                if v not in matches or bpm(matches[v], seen):
                    matches[v] = u
                    return True
        return False
    
    for u in X:
        bpm(u, set())
    
    return matches
```

## Applications

### Social Networks
1. **Centrality Measures**
   - Degree centrality
   - Betweenness centrality
   - Closeness centrality
   - Eigenvector centrality

2. **Community Detection**
   - Modularity optimization
   - Hierarchical clustering
   - Label propagation

### Transportation Networks
1. **Route Planning**
   - Shortest path algorithms
   - Traffic flow optimization
   - Network capacity analysis

2. **Network Design**
   - Minimum spanning tree
   - Steiner tree problem
   - Facility location

### Computer Networks
1. **Network Topology**
   - Ring, Star, Mesh configurations
   - Redundancy and reliability
   - Cost optimization

2. **Routing Protocols**
   - Path finding algorithms
   - Flow control
   - Congestion management
