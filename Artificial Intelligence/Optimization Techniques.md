# Optimization Techniques Reference Sheet

## Gradient-Based Methods

### Gradient Descent Variants
1. **Basic Gradient Descent**
   ```
   θₜ₊₁ = θₜ - η∇J(θₜ)
   where:
   η = learning rate
   ∇J = gradient of objective function
   ```

2. **Stochastic Gradient Descent (SGD)**
   ```
   θₜ₊₁ = θₜ - η∇J(θₜ; xᵢ)
   Mini-batch: θₜ₊₁ = θₜ - η∇J(θₜ; Xᵢ)
   ```

3. **Momentum**
   ```
   vₜ₊₁ = γvₜ + η∇J(θₜ)
   θₜ₊₁ = θₜ - vₜ₊₁
   where γ = momentum coefficient
   ```

### Advanced Gradient Methods
1. **AdaGrad**
   ```
   gₜ = ∇J(θₜ)
   rₜ = rₜ₋₁ + gₜ² (element-wise)
   θₜ₊₁ = θₜ - η/√(rₜ + ε)·gₜ
   ```

2. **RMSprop**
   ```
   rₜ = βrₜ₋₁ + (1-β)gₜ²
   θₜ₊₁ = θₜ - η/√(rₜ + ε)·gₜ
   ```

3. **Adam**
   ```
   mₜ = β₁mₜ₋₁ + (1-β₁)gₜ
   vₜ = β₂vₜ₋₁ + (1-β₂)gₜ²
   m̂ₜ = mₜ/(1-β₁ᵗ)
   v̂ₜ = vₜ/(1-β₂ᵗ)
   θₜ₊₁ = θₜ - η·m̂ₜ/√(v̂ₜ + ε)
   ```

## Second-Order Methods

### Newton's Method
1. **Update Rule**
   ```
   θₜ₊₁ = θₜ - H⁻¹∇J(θₜ)
   where H = Hessian matrix
   ```

2. **Quasi-Newton Methods**
   ```
   BFGS: Approximate H⁻¹
   L-BFGS: Limited-memory version
   ```

### Trust Region Methods
1. **Subproblem**
   ```
   min mₖ(p) = fₖ + gₖᵀp + ½pᵀBₖp
   s.t. ‖p‖ ≤ Δₖ
   ```

2. **Region Update**
   ```
   ρₖ = (f(xₖ) - f(xₖ + pₖ))/(mₖ(0) - mₖ(pₖ))
   Update Δₖ based on ρₖ
   ```

## Constrained Optimization

### Lagrange Multipliers
1. **Equality Constraints**
   ```
   L(x,λ) = f(x) + Σᵢλᵢgᵢ(x)
   ∇ₓL = 0
   gᵢ(x) = 0
   ```

2. **KKT Conditions**
   ```
   ∇ₓL = 0
   gᵢ(x) ≤ 0
   hⱼ(x) = 0
   λᵢgᵢ(x) = 0
   λᵢ ≥ 0
   ```

### Interior Point Methods
1. **Barrier Function**
   ```
   B(x,μ) = f(x) - μΣᵢln(-gᵢ(x))
   ```

2. **Central Path**
   ```
   Follow path as μ → 0
   Newton steps for each μ
   ```

## Global Optimization

### Simulated Annealing
1. **Algorithm**
   ```
   Accept new state with probability:
   P = exp(-(E_new - E_old)/T)
   T = temperature (decreases over time)
   ```

2. **Cooling Schedule**
   ```
   Geometric: Tₖ₊₁ = αTₖ
   Linear: Tₖ₊₁ = Tₖ - β
   ```

### Genetic Algorithms
1. **Components**
   ```
   Selection
   Crossover
   Mutation
   Fitness evaluation
   ```

2. **Operations**
   ```
   Tournament selection
   Single/Multi-point crossover
   Bit-flip mutation
   Elitism
   ```

## Multi-Objective Optimization

### Pareto Optimization
1. **Pareto Front**
   ```
   Non-dominated solutions
   Trade-off surface
   ```

2. **Methods**
   ```
   NSGA-II
   MOEA/D
   SPEA2
   ```

### Scalarization
1. **Weighted Sum**
   ```
   f = Σᵢwᵢfᵢ(x)
   Σᵢwᵢ = 1
   wᵢ ≥ 0
   ```

2. **ε-Constraint**
   ```
   min f₁(x)
   s.t. fᵢ(x) ≤ εᵢ, i = 2,...,m
   ```

## Derivative-Free Optimization

### Pattern Search
1. **Mesh Adaptive Direct Search**
   ```
   Generate mesh points
   Poll points
   Update mesh size
   ```

2. **Nelder-Mead Simplex**
   ```
   Reflection
   Expansion
   Contraction
   Shrinkage
   ```

### Bayesian Optimization
1. **Components**
   ```
   Surrogate model (e.g., Gaussian Process)
   Acquisition function
   Sequential sampling
   ```

2. **Acquisition Functions**
   ```
   Expected Improvement
   Upper Confidence Bound
   Probability of Improvement
   ```

## Stochastic Optimization

### Random Search
1. **Basic Algorithm**
   ```
   Sample points randomly
   Keep best solution
   Update sampling distribution
   ```

2. **Adaptive Random Search**
   ```
   Adjust step size
   Focus on promising regions
   ```

### Particle Swarm Optimization
1. **Update Rules**
   ```
   vᵢ = ωvᵢ + c₁r₁(pᵢ - xᵢ) + c₂r₂(g - xᵢ)
   xᵢ = xᵢ + vᵢ
   ```

2. **Parameters**
   ```
   ω = inertia weight
   c₁,c₂ = acceleration coefficients
   r₁,r₂ = random numbers
   ```

## Optimization in Deep Learning

### Learning Rate Scheduling
1. **Step Decay**
   ```
   η = η₀ × γ^⌊epoch/step_size⌋
   ```

2. **Cosine Annealing**
   ```
   η = η_min + ½(η_max - η_min)(1 + cos(πt/T))
   ```

### Regularization
1. **Weight Decay**
   ```
   L = Loss + λ‖w‖²
   ```

2. **Early Stopping**
   ```
   Monitor validation loss
   Stop when no improvement
   ```

## Implementation Considerations

### Numerical Stability
1. **Gradient Clipping**
   ```
   Norm clipping
   Value clipping
   ```

2. **Scaling**
   ```
   Feature normalization
   Gradient normalization
   ```

### Parallelization
1. **Data Parallelism**
   ```
   Split data across devices
   Average gradients
   ```

2. **Model Parallelism**
   ```
   Split model across devices
   Pipeline parallelism
   ```

## Performance Metrics

### Convergence Analysis
1. **Convergence Rate**
   ```
   Linear: ‖xₖ₊₁ - x*‖ ≤ c‖xₖ - x*‖
   Superlinear: limₖ→∞‖xₖ₊₁ - x*‖/‖xₖ - x*‖ = 0
   Quadratic: ‖xₖ₊₁ - x*‖ ≤ c‖xₖ - x*‖²
   ```

2. **Stopping Criteria**
   ```
   Gradient norm
   Function value change
   Parameter change
   Maximum iterations
   ```

### Robustness Analysis
1. **Sensitivity**
   ```
   Parameter sensitivity
   Initial condition sensitivity
   ```

2. **Stability**
   ```
   Numerical stability
   Solution stability
   ```
