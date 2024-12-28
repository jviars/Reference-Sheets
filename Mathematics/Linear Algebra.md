# Linear Algebra Reference Sheet

## Vector Spaces

### Basic Definitions
1. **Vector Space Axioms**
   - Closure under addition: u + v ∈ V
   - Commutativity: u + v = v + u
   - Associativity: (u + v) + w = u + (v + w)
   - Zero vector: ∃0 ∈ V such that v + 0 = v
   - Additive inverse: ∀v ∈ V, ∃(-v) such that v + (-v) = 0
   - Closure under scalar multiplication: cv ∈ V
   - Scalar multiplication properties:
     * c(dv) = (cd)v
     * (c + d)v = cv + dv
     * c(u + v) = cu + cv
     * 1v = v

2. **Subspaces**
   - Must contain zero vector
   - Closed under addition
   - Closed under scalar multiplication

### Vector Operations
1. **Basic Operations**
   ```
   Addition: u + v = (u₁ + v₁, u₂ + v₂, ..., uₙ + vₙ)
   Scalar multiplication: cu = (cu₁, cu₂, ..., cuₙ)
   Dot product: u·v = u₁v₁ + u₂v₂ + ... + uₙvₙ
   ```

2. **Properties**
   - ‖v‖ = √(v·v)
   - Cauchy-Schwarz: |u·v| ≤ ‖u‖‖v‖
   - Triangle inequality: ‖u + v‖ ≤ ‖u‖ + ‖v‖

### Span and Linear Independence
1. **Span**
   - span{v₁, ..., vₖ} = {c₁v₁ + ... + cₖvₖ | cᵢ ∈ ℝ}

2. **Linear Independence**
   - {v₁, ..., vₖ} is linearly independent if:
   - c₁v₁ + ... + cₖvₖ = 0 implies c₁ = ... = cₖ = 0

## Matrices

### Matrix Operations
1. **Addition and Scalar Multiplication**
   ```
   [a b] + [e f] = [a+e b+f]
   [c d]   [g h]   [c+g d+h]

   k[a b] = [ka kb]
   [c d]    [kc kd]
   ```

2. **Matrix Multiplication**
   ```
   [a b] [e f] = [ae+bg af+bh]
   [c d] [g h]   [ce+dg cf+dh]
   ```

3. **Properties**
   - (AB)C = A(BC)
   - A(B + C) = AB + AC
   - (A + B)C = AC + BC
   - Generally, AB ≠ BA

### Special Matrices
1. **Identity Matrix**
   ```
   [1 0]
   [0 1]
   ```

2. **Diagonal Matrix**
   ```
   [d₁ 0  0 ]
   [0  d₂ 0 ]
   [0  0  d₃]
   ```

3. **Triangular Matrices**
   ```
   Upper:     Lower:
   [a b c]    [a 0 0]
   [0 d e]    [b d 0]
   [0 0 f]    [c e f]
   ```

### Determinant
1. **2×2 Matrix**
   ```
   |a b| = ad - bc
   |c d|
   ```

2. **Properties**
   - det(AB) = det(A)det(B)
   - det(Aᵀ) = det(A)
   - det(A⁻¹) = 1/det(A)
   - A is invertible iff det(A) ≠ 0

### Matrix Inverse
1. **2×2 Matrix**
   ```
   [a b]⁻¹ = 1   [ d -b]
   [c d]     det [-c  a]
   where det = ad - bc
   ```

2. **Properties**
   - AA⁻¹ = A⁻¹A = I
   - (AB)⁻¹ = B⁻¹A⁻¹
   - (A⁻¹)⁻¹ = A

## Linear Transformations

### Basic Concepts
1. **Definition**
   - T(cu + v) = cT(u) + T(v)
   - T: V → W is linear

2. **Matrix Representation**
   - [T]ᵦ = matrix of T relative to basis β

### Eigenvalues and Eigenvectors
1. **Definitions**
   - Av = λv
   - v is eigenvector
   - λ is eigenvalue

2. **Characteristic Equation**
   - det(A - λI) = 0

3. **Diagonalization**
   - A = PDP⁻¹
   - D is diagonal matrix of eigenvalues
   - P columns are eigenvectors

## Inner Product Spaces

### Inner Products
1. **Properties**
   - ⟨u,v⟩ = ⟨v,u⟩* (conjugate symmetry)
   - ⟨u + v,w⟩ = ⟨u,w⟩ + ⟨v,w⟩
   - ⟨cu,v⟩ = c⟨u,v⟩
   - ⟨u,u⟩ > 0 if u ≠ 0

2. **Standard Inner Product**
   - ⟨u,v⟩ = u₁v₁ + u₂v₂ + ... + uₙvₙ

### Orthogonality
1. **Orthogonal Vectors**
   - u ⊥ v if ⟨u,v⟩ = 0

2. **Orthogonal Matrices**
   - Q is orthogonal if QᵀQ = QQᵀ = I
   - Q⁻¹ = Qᵀ

### Gram-Schmidt Process
1. **Algorithm**
   ```
   v₁ = u₁
   v₂ = u₂ - proj_v₁(u₂)
   v₃ = u₃ - proj_v₁(u₃) - proj_v₂(u₃)
   ```

2. **Projection Formula**
   - proj_v(u) = ⟨u,v⟩/‖v‖² · v

## Systems of Linear Equations

### Solution Methods
1. **Gaussian Elimination**
   - Forward elimination
   - Back substitution

2. **Matrix Method**
   - Ax = b
   - x = A⁻¹b (if A is invertible)

### Types of Solutions
1. **Unique Solution**
   - rank(A) = rank([A|b]) = n

2. **No Solution**
   - rank(A) < rank([A|b])

3. **Infinite Solutions**
   - rank(A) = rank([A|b]) < n

## Applications

### Linear Transformations
1. **Rotation**
   ```
   [cos θ -sin θ]
   [sin θ  cos θ]
   ```

2. **Reflection**
   ```
   [1  0 ]  // x-axis
   [0 -1 ]

   [-1 0]   // y-axis
   [0  1]
   ```

3. **Scaling**
   ```
   [sx 0 ]
   [0  sy]
   ```

### Least Squares
1. **Normal Equations**
   - AᵀAx = Aᵀb

2. **Solution**
   - x = (AᵀA)⁻¹Aᵀb

### Change of Basis
1. **Formula**
   - [v]ᵦ = P⁻¹[v]ᵧ
   - P is change of basis matrix

## Key Theorems

### Rank-Nullity Theorem
- dim(null(T)) + rank(T) = dim(domain(T))

### Fundamental Theorem of Linear Algebra
1. **For m×n matrix A:**
   - row(A) ⊕ null(A) = ℝⁿ
   - col(A) ⊕ null(Aᵀ) = ℝᵐ

### Spectral Theorem
- Symmetric matrices are orthogonally diagonalizable

### Cayley-Hamilton Theorem
- Every matrix satisfies its characteristic equation

## Computational Methods

### Matrix Decompositions
1. **LU Decomposition**
   ```
   A = LU
   L is lower triangular
   U is upper triangular
   ```

2. **QR Decomposition**
   ```
   A = QR
   Q is orthogonal
   R is upper triangular
   ```

3. **SVD (Singular Value Decomposition)**
   ```
   A = UΣVᵀ
   U, V are orthogonal
   Σ is diagonal with singular values
   ```

### Numerical Methods
1. **Power Method**
   - For finding dominant eigenvalue
   - Iterate: xₖ₊₁ = Axₖ/‖Axₖ‖

2. **QR Algorithm**
   - For finding all eigenvalues
   - Iterate: Aₖ₊₁ = RₖQₖ where Aₖ = QₖRₖ
