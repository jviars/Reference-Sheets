# Graph Theory Reference Sheet

## Basic Concepts

### Graph Definitions
1. **Undirected Graph**
   ```
   G = (V,E) where:
   V = {v₁, v₂, ..., vₙ}  // vertex set
   E = {{u,v} : u,v ∈ V}  // edge set
   ```

2. **Directed Graph (Digraph)**
   ```
   G = (V,E) where:
   E = {(u,v) : u,v ∈ V}  // ordered pairs
   ```

3. **Weighted Graph**
   ```
   G = (V,E,w) where:
   w: E → ℝ  // weight function
   ```

### Graph Properties
1. **Degree**
   ```
   deg(v) = |{e ∈ E : v ∈ e}|
   For digraphs:
   in-deg(v) = |{(u,v) ∈ E}|
   out-deg(v) = |{(v,u) ∈ E}|
   ```

2. **Handshaking Lemma**
   ```
   Σv∈V deg(v) = 2|E|
   ```

3. **Path and Cycle**
   - Path: (v₁, v₂, ..., vₖ) where {vᵢ,vᵢ₊₁} ∈ E
   - Simple path: no repeated vertices
   - Cycle: v₁ = vₖ
   - Simple cycle: no repeated vertices except v₁ = vₖ

## Graph Types

### Special Graphs
1. **Complete Graph (Kₙ)**
   ```
   |V| = n
   |E| = n(n-1)/2
   deg(v) = n-1 for all v ∈ V
   ```

2. **Bipartite Graph**
   ```
   V = V₁ ∪ V₂, V₁ ∩ V₂ = ∅
   E ⊆ {{u,v} : u ∈ V₁, v ∈ V₂}
   ```

3. **Trees**
   ```
   |E| = |V| - 1
   Connected, acyclic
   ```

4. **Planar Graphs**
   ```
   Euler's formula: V - E + F = 2
   |E| ≤ 3|V| - 6 (for |V| ≥ 3)
   ```

## Graph Traversals

### Depth-First Search (DFS)
1. **Properties**
   ```
   Time complexity: O(|V| + |E|)
   Space complexity: O(|V|)
   Discovery time: d[v]
   Finish time: f[v]
   ```

2. **DFS Forest**
   - Tree edges
   - Back edges
   - Forward edges
   - Cross edges

### Breadth-First Search (BFS)
1. **Properties**
   ```
   Time complexity: O(|V| + |E|)
   Space complexity: O(|V|)
   Level structure: L₀, L₁, ..., Lₖ
   ```

2. **BFS Tree**
   - Shortest paths in unweighted graphs
   - Level structure
   - Parent-child relationships

## Shortest Paths

### Dijkstra's Algorithm
1. **Properties**
   ```
   Time: O((|V| + |E|)log|V|)
   Non-negative weights
   d[v] = shortest path weight
   π[v] = parent in shortest path
   ```

2. **Invariant**
   ```
   d[v] ≥ d[u] + w(u,v)
   for all edges (u,v)
   ```

### Bellman-Ford Algorithm
1. **Properties**
   ```
   Time: O(|V|·|E|)
   Handles negative weights
   Detects negative cycles
   ```

2. **Relaxation**
   ```
   d[v] ← min(d[v], d[u] + w(u,v))
   ```

### Floyd-Warshall Algorithm
1. **Properties**
   ```
   Time: O(|V|³)
   All pairs shortest paths
   D[i,j] = shortest path i to j
   ```

2. **Recurrence**
   ```
   D[i,j]ᵏ = min(D[i,j]ᵏ⁻¹, D[i,k]ᵏ⁻¹ + D[k,j]ᵏ⁻¹)
   ```

## Minimum Spanning Trees

### Kruskal's Algorithm
1. **Properties**
   ```
   Time: O(|E|log|E|)
   Greedy approach
   Uses disjoint sets
   ```

2. **MST Properties**
   ```
   |E| = |V| - 1
   Minimum total weight
   Cut property
   ```

### Prim's Algorithm
1. **Properties**
   ```
   Time: O((|V| + |E|)log|V|)
   Grows single tree
   Uses priority queue
   ```

2. **Key Property**
   ```
   A ⊆ E is part of MST if A can be extended to MST
   ```

## Network Flow

### Ford-Fulkerson Algorithm
1. **Properties**
   ```
   Time: O(|E|·f) where f is max flow
   Augmenting paths
   Residual graph
   ```

2. **Max-Flow Min-Cut Theorem**
   ```
   Maximum flow = Minimum cut capacity
   ```

### Maximum Bipartite Matching
1. **Properties**
   ```
   Special case of max flow
   Unit capacities
   Perfect matching if |M| = min(|V₁|,|V₂|)
   ```

2. **Hall's Marriage Theorem**
   ```
   Perfect matching exists iff
   |N(S)| ≥ |S| for all S ⊆ V₁
   ```

## Graph Coloring

### Vertex Coloring
1. **Properties**
   ```
   χ(G) = chromatic number
   χ(G) ≤ Δ(G) + 1
   χ(G) ≤ 2 for bipartite
   ```

2. **Special Cases**
   ```
   χ(Kₙ) = n
   χ(Cₙ) = 2 if n even, 3 if n odd
   ```

### Edge Coloring
1. **Properties**
   ```
   χ'(G) = edge chromatic number
   χ'(G) ≥ Δ(G)
   ```

2. **Vizing's Theorem**
   ```
   Δ(G) ≤ χ'(G) ≤ Δ(G) + 1
   ```

## Graph Properties

### Connectivity
1. **Vertex Connectivity**
   ```
   κ(G) = min |S| where S disconnects G
   G is k-connected if κ(G) ≥ k
   ```

2. **Edge Connectivity**
   ```
   λ(G) = min |F| where F disconnects G
   κ(G) ≤ λ(G) ≤ δ(G)
   ```

### Cycles
1. **Euler Circuits**
   ```
   Exists iff all vertices have even degree
   Euler path: exactly 0 or 2 odd degree vertices
   ```

2. **Hamilton Cycles**
   ```
   NP-complete problem
   Dirac's theorem: deg(v) ≥ |V|/2
   ```

### Planarity
1. **Kuratowski's Theorem**
   ```
   G planar iff no subdivision of K₅ or K₃,₃
   ```

2. **Face Counting**
   ```
   For maximal planar graphs:
   |E| = 3|V| - 6
   |F| = 2|V| - 4
   ```

## Applications

### Network Analysis
1. **Centrality Measures**
   ```
   Degree centrality: CD(v) = deg(v)/(|V|-1)
   Closeness: CC(v) = (|V|-1)/Σd(v,u)
   Betweenness: CB(v) = Σ(σst(v)/σst)
   ```

2. **Network Flow Applications**
   ```
   Maximum matching
   Minimum cut
   Assignment problems
   ```

### Path Problems
1. **Shortest Paths**
   ```
   Single source
   All pairs
   k-shortest paths
   ```

2. **Traveling Salesman Problem**
   ```
   NP-hard
   Approximation algorithms
   Branch and bound
   ```
