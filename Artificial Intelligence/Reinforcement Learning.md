# Reinforcement Learning Reference Sheet

## Fundamental Concepts

### Markov Decision Process (MDP)
1. **Components**
   ```
   State space (S)
   Action space (A)
   Transition function P(s'|s,a)
   Reward function R(s,a,s')
   Discount factor γ ∈ [0,1]
   ```

2. **Properties**
   ```
   Markov Property: P(sₜ₊₁|sₜ,aₜ,sₜ₋₁,...,s₀) = P(sₜ₊₁|sₜ,aₜ)
   Stationarity: Transition probabilities don't change over time
   ```

### Value Functions
1. **State Value Function**
   ```
   V^π(s) = 𝔼π[Σₖγᵏrₜ₊ₖ₊₁|sₜ=s]
   ```

2. **Action Value Function**
   ```
   Q^π(s,a) = 𝔼π[Σₖγᵏrₜ₊ₖ₊₁|sₜ=s,aₜ=a]
   ```

3. **Optimal Value Functions**
   ```
   V*(s) = max_π V^π(s)
   Q*(s,a) = max_π Q^π(s,a)
   ```

### Bellman Equations
1. **Bellman Expectation**
   ```
   V^π(s) = Σₐπ(a|s)[R(s,a) + γΣₛ'P(s'|s,a)V^π(s')]
   Q^π(s,a) = R(s,a) + γΣₛ'P(s'|s,a)Σₐ'π(a'|s')Q^π(s',a')
   ```

2. **Bellman Optimality**
   ```
   V*(s) = maxₐ[R(s,a) + γΣₛ'P(s'|s,a)V*(s')]
   Q*(s,a) = R(s,a) + γΣₛ'P(s'|s,a)maxₐ'Q*(s',a')
   ```

## Classical Algorithms

### Dynamic Programming
1. **Policy Iteration**
   ```
   1. Policy Evaluation:
      Iterate V^π(s) = Σₐπ(a|s)[R(s,a) + γΣₛ'P(s'|s,a)V^π(s')]
   
   2. Policy Improvement:
      π'(s) = argmaxₐ[R(s,a) + γΣₛ'P(s'|s,a)V^π(s')]
   ```

2. **Value Iteration**
   ```
   Iterate:
   V(s) ← maxₐ[R(s,a) + γΣₛ'P(s'|s,a)V(s')]
   ```

### Monte Carlo Methods
1. **First Visit MC**
   ```
   For each state s:
   V(s) = average of returns following first visit to s
   ```

2. **Every Visit MC**
   ```
   For each state s:
   V(s) = average of returns following every visit to s
   ```

### Temporal Difference Learning
1. **TD(0)**
   ```
   V(sₜ) ← V(sₜ) + α[rₜ₊₁ + γV(sₜ₊₁) - V(sₜ)]
   ```

2. **Q-Learning**
   ```
   Q(sₜ,aₜ) ← Q(sₜ,aₜ) + α[rₜ₊₁ + γmaxₐQ(sₜ₊₁,a) - Q(sₜ,aₜ)]
   ```

3. **SARSA**
   ```
   Q(sₜ,aₜ) ← Q(sₜ,aₜ) + α[rₜ₊₁ + γQ(sₜ₊₁,aₜ₊₁) - Q(sₜ,aₜ)]
   ```

## Deep Reinforcement Learning

### Deep Q-Network (DQN)
1. **Key Components**
   ```
   Experience Replay Buffer
   Target Network
   Double DQN
   Dueling Architecture
   ```

2. **Loss Function**
   ```
   L = (r + γmaxₐ'Q(s',a';θ⁻) - Q(s,a;θ))²
   ```

### Policy Gradient Methods
1. **REINFORCE**
   ```
   ∇J(θ) = 𝔼π[∇log π(a|s;θ)G]
   where G = Σₖγᵏrₜ₊ₖ₊₁
   ```

2. **Actor-Critic**
   ```
   ∇J(θ) = 𝔼π[∇log π(a|s;θ)A^π(s,a)]
   where A^π(s,a) = Q^π(s,a) - V^π(s)
   ```

### Advanced Algorithms

1. **Proximal Policy Optimization (PPO)**
   ```
   L^CLIP(θ) = 𝔼ₜ[min(rₜ(θ)Aₜ, clip(rₜ(θ), 1-ε, 1+ε)Aₜ)]
   where rₜ(θ) = π(aₜ|sₜ;θ)/π(aₜ|sₜ;θ_old)
   ```

2. **Soft Actor-Critic (SAC)**
   ```
   π* = argmax_π 𝔼π[Σₜγᵗ(R(sₜ,aₜ) + αH(π(·|sₜ)))]
   ```

## Exploration Strategies

### Basic Strategies
1. **ε-greedy**
   ```
   With probability 1-ε: Choose argmaxₐQ(s,a)
   With probability ε: Choose random action
   ```

2. **Boltzmann Exploration**
   ```
   π(a|s) = exp(Q(s,a)/τ)/Σₐ'exp(Q(s,a')/τ)
   ```

### Advanced Exploration
1. **UCB**
   ```
   Select a = argmaxₐ[Q(s,a) + c√(ln t/N(s,a))]
   ```

2. **Intrinsic Motivation**
   ```
   R'(s,a,s') = R(s,a,s') + βI(s,a,s')
   where I is intrinsic reward
   ```

## Multi-Agent RL

### Types of Environments
1. **Cooperative**
   ```
   Shared reward function
   Team-based objectives
   ```

2. **Competitive**
   ```
   Zero-sum games
   Nash equilibrium
   ```

3. **Mixed**
   ```
   Partial cooperation
   Individual and shared rewards
   ```

### Algorithms
1. **Independent Learning**
   ```
   Each agent learns independently
   Treats other agents as part of environment
   ```

2. **Centralized Training**
   ```
   Joint action space
   Shared value function
   Decentralized execution
   ```

## Practical Considerations

### Implementation Tips
1. **Hyperparameter Tuning**
   ```
   Learning rate
   Discount factor
   Exploration parameters
   Network architecture
   ```

2. **Stability Improvements**
   ```
   Gradient clipping
   Reward scaling
   Action noise
   Learning rate scheduling
   ```

### Common Issues
1. **Credit Assignment**
   ```
   Sparse rewards
   Delayed rewards
   Multi-agent credit assignment
   ```

2. **Sample Efficiency**
   ```
   Off-policy learning
   Prioritized replay
   Model-based methods
   ```

## Advanced Topics

### Hierarchical RL
1. **Options Framework**
   ```
   Option = (I, π, β)
   I: Initiation set
   π: Option policy
   β: Termination condition
   ```

2. **Feudal Networks**
   ```
   Manager-worker hierarchy
   Goal-directed behavior
   ```

### Meta-Learning
1. **Algorithm Adaptation**
   ```
   Learn learning algorithms
   Rapid adaptation to new tasks
   ```

2. **Transfer Learning**
   ```
   Knowledge transfer between tasks
   Policy distillation
   ```

### Safety in RL
1. **Constrained RL**
   ```
   Safety constraints
   Risk-sensitive objectives
   ```

2. **Robust RL**
   ```
   Uncertainty handling
   Adversarial training
   ```

## Performance Metrics

### Training Metrics
1. **Learning Curves**
   ```
   Average return
   Episode length
   Success rate
   ```

2. **Efficiency Metrics**
   ```
   Sample efficiency
   Wall-clock time
   Memory usage
   ```

### Evaluation Metrics
1. **Policy Quality**
   ```
   Final performance
   Stability
   Generalization
   ```

2. **Robustness**
   ```
   Parameter sensitivity
   Environmental variations
   Noise tolerance
   ```
