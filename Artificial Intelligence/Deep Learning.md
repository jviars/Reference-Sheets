# Deep Learning Reference Sheet

## Neural Network Fundamentals

### Basic Components
1. **Neuron**
   ```
   output = activation(Σ(wᵢxᵢ) + b)
   where:
   wᵢ = weights
   xᵢ = inputs
   b = bias
   ```

2. **Layer Types**
   ```
   Input Layer: Raw data input
   Hidden Layers: Internal processing
   Output Layer: Final predictions
   ```

### Activation Functions
1. **ReLU**
   ```
   f(x) = max(0, x)
   f'(x) = {1 if x > 0, 0 otherwise}
   ```

2. **Sigmoid**
   ```
   f(x) = 1/(1 + e⁻ˣ)
   f'(x) = f(x)(1 - f(x))
   ```

3. **Tanh**
   ```
   f(x) = (e^x - e^(-x))/(e^x + e^(-x))
   f'(x) = 1 - f(x)²
   ```

4. **Softmax**
   ```
   f(x)ᵢ = e^xᵢ/Σe^xⱼ
   Used for multi-class classification
   ```

## Network Architectures

### Feedforward Neural Networks
1. **Architecture**
   ```
   Input → Dense Layers → Output
   Each layer fully connected to next
   ```

2. **Common Configurations**
   ```
   Binary Classification: Dense → ReLU → Dense → Sigmoid
   Multi-class: Dense → ReLU → Dense → Softmax
   Regression: Dense → ReLU → Dense → Linear
   ```

### Convolutional Neural Networks (CNN)
1. **Layer Types**
   ```
   Convolutional: Feature extraction
   Pooling: Dimensionality reduction
   Fully Connected: Classification
   ```

2. **Common Operations**
   ```
   Conv2D: filters, kernel_size, stride, padding
   MaxPooling: pool_size, stride
   Global Average Pooling
   ```

3. **Popular Architectures**
   ```
   VGG: Stacked 3x3 convolutions
   ResNet: Skip connections
   Inception: Multi-scale processing
   ```

### Recurrent Neural Networks (RNN)
1. **Basic RNN**
   ```
   hₜ = tanh(Wₕhₜ₋₁ + Wₓxₜ + b)
   ```

2. **LSTM**
   ```
   Forget gate: fₜ = σ(Wf·[hₜ₋₁, xₜ] + bf)
   Input gate: iₜ = σ(Wi·[hₜ₋₁, xₜ] + bi)
   Cell state: Cₜ = fₜ * Cₜ₋₁ + iₜ * tanh(Wc·[hₜ₋₁, xₜ] + bc)
   Output gate: oₜ = σ(Wo·[hₜ₋₁, xₜ] + bo)
   ```

3. **GRU**
   ```
   Update gate: zₜ = σ(Wz·[hₜ₋₁, xₜ] + bz)
   Reset gate: rₜ = σ(Wr·[hₜ₋₁, xₜ] + br)
   New memory: h̃ₜ = tanh(W·[rₜ * hₜ₋₁, xₜ] + b)
   Final memory: hₜ = (1-zₜ) * hₜ₋₁ + zₜ * h̃ₜ
   ```

### Transformer Architecture
1. **Components**
   ```
   Self-Attention
   Multi-Head Attention
   Position-wise Feed-Forward
   Layer Normalization
   ```

2. **Attention Mechanism**
   ```
   Attention(Q,K,V) = softmax(QKᵀ/√dk)V
   Multi-Head = Concat(head₁, ..., headₕ)W^O
   ```

## Training Process

### Loss Functions
1. **Classification**
   ```
   Binary Cross-Entropy:
   -Σ(y log(p) + (1-y)log(1-p))

   Categorical Cross-Entropy:
   -Σy log(p)
   ```

2. **Regression**
   ```
   MSE: (1/n)Σ(y - ŷ)²
   MAE: (1/n)Σ|y - ŷ|
   Huber: Combination of MSE and MAE
   ```

### Optimization
1. **Gradient Descent Variants**
   ```
   SGD: w = w - η∇L
   Momentum: v = βv - η∇L, w = w + v
   Adam: Combines momentum and RMSprop
   ```

2. **Learning Rate Schedules**
   ```
   Step decay: η = η₀ × 0.1^(epoch/step)
   Exponential decay: η = η₀ × e^(-kt)
   Cosine annealing: η = η₀/2(1 + cos(πt/T))
   ```

### Regularization
1. **Weight Regularization**
   ```
   L1: λΣ|w|
   L2: λΣw²
   ```

2. **Dropout**
   ```
   Training: Randomly zero out units
   Testing: Scale activations by dropout rate
   ```

3. **Batch Normalization**
   ```
   μ_B = (1/m)Σxᵢ
   σ²_B = (1/m)Σ(xᵢ - μ_B)²
   x̂ᵢ = (xᵢ - μ_B)/√(σ²_B + ε)
   yᵢ = γx̂ᵢ + β
   ```

## Model Evaluation

### Metrics
1. **Classification**
   ```
   Accuracy
   Precision
   Recall
   F1-Score
   AUC-ROC
   ```

2. **Regression**
   ```
   MSE
   RMSE
   MAE
   R²
   ```

### Monitoring
1. **Learning Curves**
   ```
   Training vs. Validation Loss
   Training vs. Validation Accuracy
   ```

2. **Gradient Monitoring**
   ```
   Gradient norms
   Weight updates
   Layer activations
   ```

## Advanced Techniques

### Transfer Learning
1. **Approaches**
   ```
   Feature Extraction: Freeze pre-trained layers
   Fine-Tuning: Update some/all layers
   ```

2. **Common Practices**
   ```
   Start with frozen layers
   Gradually unfreeze
   Use smaller learning rate
   ```

### Data Augmentation
1. **Image**
   ```
   Rotation
   Scaling
   Flipping
   Color jittering
   Random cropping
   ```

2. **Text**
   ```
   Synonym replacement
   Back-translation
   Random insertion/deletion
   Sentence shuffling
   ```

### Model Compression
1. **Pruning**
   ```
   Weight pruning
   Unit pruning
   Filter pruning
   ```

2. **Quantization**
   ```
   Post-training quantization
   Quantization-aware training
   Mixed precision training
   ```

## Best Practices

### Initialization
1. **Weight Initialization**
   ```
   Xavier/Glorot: U(-√(6/n), √(6/n))
   He: N(0, √(2/n))
   ```

2. **Bias Initialization**
   ```
   Usually zero
   Small positive values for ReLU
   ```

### Hyperparameter Tuning
1. **Key Parameters**
   ```
   Learning rate
   Batch size
   Number of layers/units
   Regularization strength
   ```

2. **Search Strategies**
   ```
   Grid search
   Random search
   Bayesian optimization
   ```

### Model Architecture Design
1. **Guidelines**
   ```
   Start simple
   Gradual complexity
   Skip connections
   Bottleneck layers
   ```

2. **Common Patterns**
   ```
   Residual blocks
   Dense blocks
   Inception modules
   ```

## Troubleshooting

### Common Issues
1. **Vanishing Gradients**
   ```
   Solutions:
   - Residual connections
   - Batch normalization
   - Proper initialization
   ```

2. **Exploding Gradients**
   ```
   Solutions:
   - Gradient clipping
   - Layer normalization
   - Learning rate reduction
   ```

### Performance Optimization
1. **Memory Usage**
   ```
   Gradient accumulation
   Mixed precision training
   Model parallelism
   ```

2. **Training Speed**
   ```
   Data parallelism
   Pipeline parallelism
   Efficient data loading
   ```
