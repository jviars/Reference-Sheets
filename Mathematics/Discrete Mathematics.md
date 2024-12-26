# Discrete Mathematics Cheat Sheet

## Set Theory

### Basic Set Operations
- Union: A ∪ B = {x | x ∈ A or x ∈ B}
- Intersection: A ∩ B = {x | x ∈ A and x ∈ B}
- Difference: A - B = {x | x ∈ A and x ∉ B}
- Symmetric Difference: A △ B = (A - B) ∪ (B - A)
- Complement: A' = {x ∈ U | x ∉ A}
- Cartesian Product: A × B = {(a,b) | a ∈ A and b ∈ B}

### Set Properties
1. Commutative Laws:
   - A ∪ B = B ∪ A
   - A ∩ B = B ∩ A

2. Associative Laws:
   - (A ∪ B) ∪ C = A ∪ (B ∪ C)
   - (A ∩ B) ∩ C = A ∩ (B ∩ C)

3. Distributive Laws:
   - A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)
   - A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)

4. DeMorgan's Laws:
   - (A ∪ B)' = A' ∩ B'
   - (A ∩ B)' = A' ∪ B'

### Set Cardinality
- |A| = number of elements in set A
- |A ∪ B| = |A| + |B| - |A ∩ B|
- |A × B| = |A| × |B|

## Logic

### Propositional Logic
- Conjunction (AND): p ∧ q
- Disjunction (OR): p ∨ q
- Negation (NOT): ¬p
- Implication: p → q
- Biconditional: p ↔ q
- Exclusive OR (XOR): p ⊕ q

### Truth Table Values
```
p  q  | p∧q | p∨q | p→q | p↔q | p⊕q
------------------------
T  T  |  T  |  T  |  T  |  T  |  F
T  F  |  F  |  T  |  F  |  F  |  T
F  T  |  F  |  T  |  T  |  F  |  T
F  F  |  F  |  F  |  T  |  T  |  F
```

### Logical Equivalences
1. Double Negation: ¬(¬p) ≡ p
2. DeMorgan's Laws:
   - ¬(p ∧ q) ≡ ¬p ∨ ¬q
   - ¬(p ∨ q) ≡ ¬p ∧ ¬q
3. Implication: p → q ≡ ¬p ∨ q
4. Contrapositive: (p → q) ≡ (¬q → ¬p)

## Functions

### Types of Functions
1. Injective (One-to-One):
   - ∀x₁,x₂ ∈ X, f(x₁) = f(x₂) → x₁ = x₂

2. Surjective (Onto):
   - ∀y ∈ Y, ∃x ∈ X such that f(x) = y

3. Bijective (One-to-One and Onto):
   - Both injective and surjective

### Function Properties
- Domain: Set of all possible input values
- Codomain: Set of all possible output values
- Range: Set of actual output values
- Image: f(A) = {f(x) | x ∈ A}
- Preimage: f⁻¹(B) = {x ∈ X | f(x) ∈ B}

## Relations

### Properties of Relations
1. Reflexive: ∀x ∈ A, xRx
2. Symmetric: ∀x,y ∈ A, xRy → yRx
3. Antisymmetric: ∀x,y ∈ A, (xRy ∧ yRx) → x = y
4. Transitive: ∀x,y,z ∈ A, (xRy ∧ yRz) → xRz

### Equivalence Relations
- Must be reflexive, symmetric, and transitive
- Partitions set into equivalence classes
- [a] = {x ∈ A | xRa}

### Partial Orders
- Must be reflexive, antisymmetric, and transitive
- Examples: ≤, ⊆, |

## Counting Principles

### Basic Counting
1. Sum Rule: |A ∪ B| = |A| + |B| (disjoint sets)
2. Product Rule: |A × B| = |A| × |B|
3. Subtraction Rule: |A ∪ B| = |A| + |B| - |A ∩ B|

### Permutations
1. Without Repetition:
   - P(n) = n!
   - P(n,r) = n!/(n-r)!

2. With Repetition:
   - n objects with n₁,...,nₖ types
   - P(n; n₁,...,nₖ) = n!/(n₁!×...×nₖ!)

### Combinations
1. Without Repetition:
   - C(n,r) = n!/(r!(n-r)!)
   - Also written as ⁿCᵣ or (n r)

2. With Repetition:
   - C(n+r-1,r) = (n+r-1)!/(r!(n-1)!)

## Graph Theory

### Basic Concepts
1. Graph: G = (V,E)
   - V: set of vertices
   - E: set of edges

2. Types of Graphs:
   - Simple Graph
   - Multigraph
   - Pseudograph
   - Directed Graph
   - Complete Graph

### Graph Properties
1. Degree:
   - deg(v) = number of edges incident to v
   - Handshaking Lemma: Σdeg(v) = 2|E|

2. Paths and Cycles:
   - Path: sequence of vertices connected by edges
   - Simple Path: no repeated vertices
   - Cycle: path that starts and ends at same vertex
   - Simple Cycle: no repeated vertices except first/last

3. Connectivity:
   - Connected Graph: path exists between any two vertices
   - Tree: connected graph with no cycles
   - Forest: collection of trees

### Graph Algorithms
1. Traversal:
   - Depth-First Search (DFS)
   - Breadth-First Search (BFS)

2. Shortest Path:
   - Dijkstra's Algorithm
   - Floyd-Warshall Algorithm

3. Minimum Spanning Tree:
   - Kruskal's Algorithm
   - Prim's Algorithm

## Number Theory

### Division Algorithm
- If a,b ∈ ℤ with b > 0, then ∃!q,r ∈ ℤ such that:
  a = bq + r, where 0 ≤ r < b

### Greatest Common Divisor (GCD)
1. Properties:
   - gcd(a,b) = gcd(b,a)
   - gcd(a,b) = gcd(a-b,b)
   - gcd(a,0) = |a|

2. Euclidean Algorithm:
   - gcd(a,b) = gcd(b,r) where a = bq + r

3. Bézout's Identity:
   - ∃x,y ∈ ℤ such that ax + by = gcd(a,b)

### Congruences
1. Basic Properties:
   - a ≡ b (mod n) ⟺ n|(a-b)
   - a ≡ b (mod n) → a + k ≡ b + k (mod n)
   - a ≡ b (mod n) → ak ≡ bk (mod n)

2. Chinese Remainder Theorem:
   - System of congruences with coprime moduli
   - Unique solution modulo product of moduli

## Recurrence Relations

### Linear Recurrence Relations
1. First-Order:
   - aₙ = caₙ₋₁ + b
   - General solution: aₙ = Ac^n + particular solution

2. Second-Order:
   - aₙ = paₙ₋₁ + qaₙ₋₂
   - Characteristic equation: r² - pr - q = 0

### Special Sequences
1. Arithmetic Sequence:
   - aₙ = a₁ + (n-1)d
   - Sum: Sₙ = n(a₁ + aₙ)/2

2. Geometric Sequence:
   - aₙ = a₁r^(n-1)
   - Sum: Sₙ = a₁(1-r^n)/(1-r)

3. Fibonacci Sequence:
   - Fₙ = Fₙ₋₁ + Fₙ₋₂
   - F₀ = 0, F₁ = 1

## Boolean Algebra

### Basic Operations
1. AND (∧):
   - 1 ∧ 1 = 1
   - 1 ∧ 0 = 0
   - 0 ∧ 1 = 0
   - 0 ∧ 0 = 0

2. OR (∨):
   - 1 ∨ 1 = 1
   - 1 ∨ 0 = 1
   - 0 ∨ 1 = 1
   - 0 ∨ 0 = 0

3. NOT (¬):
   - ¬1 = 0
   - ¬0 = 1

### Laws of Boolean Algebra
1. Identity Laws:
   - x ∨ 0 = x
   - x ∧ 1 = x

2. Complement Laws:
   - x ∨ ¬x = 1
   - x ∧ ¬x = 0

3. Idempotent Laws:
   - x ∨ x = x
   - x ∧ x = x

4. Absorption Laws:
   - x ∨ (x ∧ y) = x
   - x ∧ (x ∨ y) = x

## Discrete Probability

### Basic Probability
1. P(A) = |A|/|S| where S is sample space
2. P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
3. P(A') = 1 - P(A)

### Conditional Probability
1. P(A|B) = P(A ∩ B)/P(B)
2. Bayes' Theorem:
   P(A|B) = P(B|A)P(A)/P(B)

### Independence
1. Events A and B are independent if:
   P(A ∩ B) = P(A)P(B)

### Random Variables
1. Expected Value:
   E(X) = Σ xP(X = x)

2. Variance:
   Var(X) = E((X - μ)²) = E(X²) - [E(X)]²
