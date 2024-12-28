# Probability Theory Reference Sheet

## Basic Concepts

### Sample Space and Events
1. **Sample Space (Ω)**
   - Set of all possible outcomes
   - Examples:
     * Coin flip: Ω = {H, T}
     * Die roll: Ω = {1, 2, 3, 4, 5, 6}

2. **Events**
   - Subsets of sample space
   - Operations:
     * Union: A ∪ B
     * Intersection: A ∩ B
     * Complement: A'

### Probability Axioms
1. **Non-negativity**
   ```
   P(A) ≥ 0 for all A ⊆ Ω
   ```

2. **Normalization**
   ```
   P(Ω) = 1
   ```

3. **Countable Additivity**
   ```
   P(∪Aᵢ) = ΣP(Aᵢ) for disjoint events
   ```

### Probability Properties
1. **Complement Rule**
   ```
   P(A') = 1 - P(A)
   ```

2. **Addition Rule**
   ```
   P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
   ```

3. **Monotonicity**
   ```
   If A ⊆ B, then P(A) ≤ P(B)
   ```

## Conditional Probability

### Basic Concepts
1. **Definition**
   ```
   P(A|B) = P(A ∩ B)/P(B), P(B) > 0
   ```

2. **Multiplication Rule**
   ```
   P(A ∩ B) = P(A|B)P(B) = P(B|A)P(A)
   ```

### Independence
1. **Events A and B are independent if:**
   ```
   P(A ∩ B) = P(A)P(B)
   P(A|B) = P(A)
   P(B|A) = P(B)
   ```

2. **Multiple Events**
   ```
   P(A₁ ∩ A₂ ∩ ... ∩ Aₙ) = P(A₁)P(A₂)...P(Aₙ)
   ```

### Bayes' Theorem
1. **Basic Form**
   ```
   P(A|B) = P(B|A)P(A)/P(B)
   ```

2. **Extended Form**
   ```
   P(Aᵢ|B) = P(B|Aᵢ)P(Aᵢ)/ΣP(B|Aⱼ)P(Aⱼ)
   ```

## Random Variables

### Types
1. **Discrete**
   - Countable range
   - Probability mass function (PMF)
   ```
   p(x) = P(X = x)
   Σp(x) = 1
   ```

2. **Continuous**
   - Uncountable range
   - Probability density function (PDF)
   ```
   P(a ≤ X ≤ b) = ∫ᵃᵇf(x)dx
   ∫f(x)dx = 1
   ```

### Expected Value
1. **Discrete**
   ```
   E[X] = Σx·p(x)
   ```

2. **Continuous**
   ```
   E[X] = ∫x·f(x)dx
   ```

3. **Properties**
   ```
   E[aX + b] = aE[X] + b
   E[X + Y] = E[X] + E[Y]
   E[XY] = E[X]E[Y] if independent
   ```

### Variance
1. **Definition**
   ```
   Var(X) = E[(X - μ)²] = E[X²] - (E[X])²
   ```

2. **Properties**
   ```
   Var(aX + b) = a²Var(X)
   Var(X + Y) = Var(X) + Var(Y) if independent
   ```

3. **Standard Deviation**
   ```
   σ = √Var(X)
   ```

## Common Distributions

### Discrete Distributions
1. **Bernoulli**
   ```
   P(X = 1) = p
   P(X = 0) = 1-p
   E[X] = p
   Var(X) = p(1-p)
   ```

2. **Binomial**
   ```
   P(X = k) = C(n,k)pᵏ(1-p)ⁿ⁻ᵏ
   E[X] = np
   Var(X) = np(1-p)
   ```

3. **Poisson**
   ```
   P(X = k) = λᵏe⁻λ/k!
   E[X] = λ
   Var(X) = λ
   ```

4. **Geometric**
   ```
   P(X = k) = p(1-p)ᵏ⁻¹
   E[X] = 1/p
   Var(X) = (1-p)/p²
   ```

### Continuous Distributions
1. **Uniform**
   ```
   f(x) = 1/(b-a) for a ≤ x ≤ b
   E[X] = (a+b)/2
   Var(X) = (b-a)²/12
   ```

2. **Normal**
   ```
   f(x) = (1/√(2πσ²))e^(-(x-μ)²/(2σ²))
   E[X] = μ
   Var(X) = σ²
   ```

3. **Exponential**
   ```
   f(x) = λe⁻λˣ for x ≥ 0
   E[X] = 1/λ
   Var(X) = 1/λ²
   ```

## Limit Theorems

### Law of Large Numbers
1. **Weak Law**
   ```
   X̄ₙ →ᵖ μ as n → ∞
   ```

2. **Strong Law**
   ```
   P(limₙ→∞ X̄ₙ = μ) = 1
   ```

### Central Limit Theorem
```
√n(X̄ₙ - μ)/σ →ᵈ N(0,1) as n → ∞
```

## Multivariate Distributions

### Joint Distributions
1. **Joint PMF/PDF**
   ```
   p(x,y) = P(X = x, Y = y)
   f(x,y) for continuous
   ```

2. **Marginal Distributions**
   ```
   p₁(x) = Σₖp(x,k)
   f₁(x) = ∫f(x,y)dy
   ```

### Covariance and Correlation
1. **Covariance**
   ```
   Cov(X,Y) = E[(X-μₓ)(Y-μᵧ)]
   ```

2. **Correlation**
   ```
   ρ = Cov(X,Y)/(σₓσᵧ)
   -1 ≤ ρ ≤ 1
   ```

## Transformations

### Univariate
1. **Discrete**
   ```
   P(Y = y) = ΣP(X = x) where g(x) = y
   ```

2. **Continuous**
   ```
   fᵧ(y) = fₓ(g⁻¹(y))|d/dy g⁻¹(y)|
   ```

### Multivariate
1. **Jacobian Transformation**
   ```
   |J| = |∂(u,v)/∂(x,y)|
   f(u,v) = f(x,y)|J|⁻¹
   ```

## Parameter Estimation

### Point Estimation
1. **Method of Moments**
   ```
   Sample moments = Population moments
   ```

2. **Maximum Likelihood**
   ```
   L(θ;x) = ∏f(xᵢ|θ)
   θ̂ = argmax L(θ;x)
   ```

### Interval Estimation
1. **Confidence Intervals**
   ```
   θ̂ ± z₍α/₂₎σ/√n
   ```

2. **Prediction Intervals**
   ```
   x̂ ± t₍α/₂₎s√(1 + 1/n)
   ```

## Hypothesis Testing

### Elements
1. **Hypotheses**
   ```
   H₀: null hypothesis
   H₁: alternative hypothesis
   ```

2. **Errors**
   ```
   Type I: reject H₀ when true
   Type II: fail to reject H₀ when false
   ```

### Test Statistics
1. **Z-test**
   ```
   Z = (X̄ - μ₀)/(σ/√n)
   ```

2. **T-test**
   ```
   T = (X̄ - μ₀)/(s/√n)
   ```
