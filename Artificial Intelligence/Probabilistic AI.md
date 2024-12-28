# Probabilistic AI Reference Sheet

## Probabilistic Graphical Models

### Bayesian Networks
1. **Structure**
   ```
   Directed Acyclic Graph (DAG)
   P(X₁,...,Xₙ) = ∏ᵢP(Xᵢ|parents(Xᵢ))
   ```

2. **Properties**
   ```
   Local Markov Property
   D-separation
   Factorization
   Conditional Independence
   ```

3. **Parameter Learning**
   ```
   Maximum Likelihood Estimation
   Maximum A Posteriori
   Bayesian Parameter Learning
   ```

### Markov Random Fields
1. **Structure**
   ```
   Undirected Graph
   P(X) = (1/Z)∏ᵩΨᵩ(xᵩ)
   Z = Σₓ∏ᵩΨᵩ(xᵩ)
   ```

2. **Clique Potentials**
   ```
   Maximal cliques
   Factor potentials
   Energy functions
   ```

3. **Applications**
   ```
   Image processing
   Social networks
   Natural language
   ```

## Probabilistic Inference

### Exact Inference
1. **Variable Elimination**
   ```
   Order: Eliminate variables
   Operations:
   - Factor multiplication
   - Factor marginalization
   ```

2. **Belief Propagation**
   ```
   Message passing:
   μₓ→ᵧ(y) = Σₓφ(x,y)∏ᵤ∈N(x)\y μᵤ→ₓ(x)
   ```

### Approximate Inference
1. **Monte Carlo Methods**
   ```
   Rejection Sampling
   Importance Sampling
   Markov Chain Monte Carlo (MCMC)
   ```

2. **Variational Inference**
   ```
   ELBO: L(q) = 𝔼q[log p(x,z)] - 𝔼q[log q(z)]
   KL divergence minimization
   Mean field approximation
   ```

## Probabilistic Programming

### Model Specification
1. **Variables**
   ```
   Random variables
   Deterministic variables
   Observed variables
   Latent variables
   ```

2. **Distributions**
   ```
   Prior distributions
   Likelihood functions
   Posterior distributions
   Conjugate pairs
   ```

### Inference Engines
1. **MCMC Samplers**
   ```
   Metropolis-Hastings
   Gibbs sampling
   Hamiltonian Monte Carlo
   No-U-Turn Sampler
   ```

2. **Variational Methods**
   ```
   Automatic Differentiation
   Variational Inference
   Stochastic Optimization
   ```

## Deep Probabilistic Models

### Variational Autoencoders
1. **Architecture**
   ```
   Encoder: q(z|x)
   Decoder: p(x|z)
   Latent space: z
   ```

2. **Loss Function**
   ```
   L = -KL(q(z|x)||p(z)) + 𝔼q(z|x)[log p(x|z)]
   ```

### Normalizing Flows
1. **Transformation**
   ```
   z = f(x) where f is invertible
   log p(x) = log p(z) + log|det(∂f/∂x)|
   ```

2. **Flow Types**
   ```
   Planar flows
   Radial flows
   Autoregressive flows
   Coupling layers
   ```

## Bayesian Deep Learning

### Bayesian Neural Networks
1. **Weight Uncertainty**
   ```
   Prior: p(w)
   Likelihood: p(D|w)
   Posterior: p(w|D)
   ```

2. **Inference Methods**
   ```
   Bayes by Backprop
   MC Dropout
   Ensemble methods
   ```

### Uncertainty Estimation
1. **Types of Uncertainty**
   ```
   Aleatoric uncertainty
   Epistemic uncertainty
   ```

2. **Calibration Methods**
   ```
   Temperature scaling
   Platt scaling
   Isotonic regression
   ```

## Time Series Models

### State Space Models
1. **Hidden Markov Models**
   ```
   P(x₁:ₜ,z₁:ₜ) = P(x₁)∏ₜP(xₜ|xₜ₋₁)P(zₜ|xₜ)
   ```

2. **Kalman Filters**
   ```
   Prediction: x̂ₜ|ₜ₋₁ = Fx̂ₜ₋₁|ₜ₋₁
   Update: x̂ₜ|ₜ = x̂ₜ|ₜ₋₁ + Kₜ(zₜ - Hx̂ₜ|ₜ₋₁)
   ```

### Sequential Monte Carlo
1. **Particle Filters**
   ```
   Importance sampling
   Resampling
   Proposal distributions
   ```

2. **Applications**
   ```
   Object tracking
   Robot localization
   Financial modeling
   ```

## Probabilistic Optimization

### Bayesian Optimization
1. **Components**
   ```
   Surrogate model (e.g., GP)
   Acquisition function
   Objective function
   ```

2. **Acquisition Functions**
   ```
   Expected Improvement
   Upper Confidence Bound
   Probability of Improvement
   ```

### Thompson Sampling
1. **Algorithm**
   ```
   Sample θ ~ p(θ|D)
   Choose action a = argmaxₐ𝔼[r|θ,a]
   Update posterior p(θ|D)
   ```

2. **Applications**
   ```
   Multi-armed bandits
   Contextual bandits
   Reinforcement learning
   ```

## Model Selection and Averaging

### Bayesian Model Selection
1. **Model Evidence**
   ```
   p(D) = ∫p(D|θ)p(θ)dθ
   ```

2. **Bayes Factors**
   ```
   BF₁₂ = p(D|M₁)/p(D|M₂)
   ```

### Bayesian Model Averaging
1. **Posterior Predictive**
   ```
   p(x̃|D) = ΣₖP(M_k|D)p(x̃|D,M_k)
   ```

2. **Weight Calculation**
   ```
   P(M_k|D) ∝ p(D|M_k)P(M_k)
   ```

## Implementation Considerations

### Computational Efficiency
1. **Parallel Computing**
   ```
   MCMC parallelization
   Distributed inference
   GPU acceleration
   ```

2. **Memory Management**
   ```
   Mini-batch processing
   Streaming algorithms
   Online learning
   ```

### Numerical Stability
1. **Log Space Computations**
   ```
   Log-sum-exp trick
   Stable gradients
   Numerical underflow prevention
   ```

2. **Optimization Techniques**
   ```
   Reparameterization
   Gradient clipping
   Adaptive step sizes
   ```

## Diagnostics and Validation

### MCMC Diagnostics
1. **Convergence Tests**
   ```
   Gelman-Rubin statistic
   Effective sample size
   Autocorrelation
   Trace plots
   ```

2. **Chain Analysis**
   ```
   Burn-in period
   Thinning
   Multiple chains
   ```

### Model Checking
1. **Posterior Predictive Checks**
   ```
   Simulated vs. observed data
   Test statistics
   Discrepancy measures
   ```

2. **Sensitivity Analysis**
   ```
   Prior sensitivity
   Model assumptions
   Parameter robustness
   ```
