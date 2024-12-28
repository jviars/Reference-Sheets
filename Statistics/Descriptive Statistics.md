# Descriptive Statistics Reference Sheet

## Measures of Central Tendency

### Mean
1. **Arithmetic Mean**
   ```
   x̄ = (Σx)/n
   where:
   x̄ = sample mean
   Σx = sum of all values
   n = number of values
   ```

2. **Weighted Mean**
   ```
   x̄ᵤ = (Σwᵢxᵢ)/(Σwᵢ)
   where:
   wᵢ = weight for value i
   xᵢ = value i
   ```

3. **Geometric Mean**
   ```
   GM = (x₁ × x₂ × ... × xₙ)^(1/n)
   or
   GM = e^((Σln(x))/n)
   ```

4. **Harmonic Mean**
   ```
   HM = n/(Σ(1/xᵢ))
   ```

### Median
1. **Ordered Data**
   ```
   For odd n: median = x₍ₙ₊₁₎/₂
   For even n: median = (x₍ₙ/₂₎ + x₍ₙ/₂₊₁₎)/2
   ```

2. **Grouped Data**
   ```
   Md = L + ((n/2 - F)/f) × c
   where:
   L = lower boundary of median class
   F = cumulative frequency before median class
   f = frequency of median class
   c = class interval
   ```

### Mode
1. **Ungrouped Data**
   - Most frequently occurring value

2. **Grouped Data**
   ```
   Mo = L + ((d₁)/(d₁ + d₂)) × c
   where:
   L = lower boundary of modal class
   d₁ = frequency difference with previous class
   d₂ = frequency difference with next class
   c = class interval
   ```

## Measures of Dispersion

### Range
```
Range = Maximum value - Minimum value
```

### Variance
1. **Population Variance**
   ```
   σ² = Σ(x - μ)²/N
   where:
   μ = population mean
   N = population size
   ```

2. **Sample Variance**
   ```
   s² = Σ(x - x̄)²/(n-1)
   where:
   x̄ = sample mean
   n = sample size
   ```

### Standard Deviation
1. **Population**
   ```
   σ = √(σ²)
   ```

2. **Sample**
   ```
   s = √(s²)
   ```

### Coefficient of Variation
```
CV = (s/x̄) × 100%
```

### Quartiles and Percentiles
1. **Quartiles**
   ```
   Q₁ = 25th percentile
   Q₂ = Median (50th percentile)
   Q₃ = 75th percentile
   ```

2. **Interquartile Range (IQR)**
   ```
   IQR = Q₃ - Q₁
   ```

3. **Percentiles**
   ```
   Pₖ = L + ((k(n)/100 - F)/f) × c
   where:
   k = desired percentile
   Other terms same as median formula
   ```

## Measures of Shape

### Skewness
1. **Pearson's First Coefficient**
   ```
   SK₁ = 3(Mean - Median)/s
   ```

2. **Pearson's Second Coefficient**
   ```
   SK₂ = Σ(x - x̄)³/(n×s³)
   ```

### Kurtosis
```
K = [Σ(x - x̄)⁴/(n×s⁴)] - 3
where:
Mesokurtic: K = 0
Leptokurtic: K > 0
Platykurtic: K < 0
```

## Data Organization

### Frequency Distributions
1. **Class Interval**
   ```
   i = Range/k
   where k ≈ √n (Sturges' Rule)
   ```

2. **Frequency**
   - Absolute frequency (f)
   - Relative frequency (f/n)
   - Cumulative frequency (F)

3. **Class Boundaries**
   ```
   Lower boundary = Class lower limit - 0.5
   Upper boundary = Class upper limit + 0.5
   ```

### Graphical Representations

1. **Histogram**
   ```
   Area = Frequency
   Height = Frequency/Class interval
   ```

2. **Frequency Polygon**
   - Connect midpoints of histogram bars

3. **Ogive**
   - Cumulative frequency graph
   - Less-than and more-than ogives

4. **Box Plot**
   ```
   Lower fence = Q₁ - 1.5×IQR
   Upper fence = Q₃ + 1.5×IQR
   Outliers: Points beyond fences
   ```

## Statistical Sampling

### Types of Sampling
1. **Simple Random Sampling**
   - Each element has equal probability
   - With or without replacement

2. **Systematic Sampling**
   ```
   k = N/n (sampling interval)
   Select every kth item
   ```

3. **Stratified Sampling**
   - Population divided into strata
   - Sample from each stratum

4. **Cluster Sampling**
   - Population divided into clusters
   - Select entire clusters

### Sample Size Determination
1. **For Mean**
   ```
   n = (Z×σ/E)²
   where:
   Z = Z-score for confidence level
   σ = population standard deviation
   E = margin of error
   ```

2. **For Proportion**
   ```
   n = (Z²×p×q)/E²
   where:
   p = estimated proportion
   q = 1-p
   ```

## Data Quality

### Missing Data
1. **Types**
   - MCAR (Missing Completely at Random)
   - MAR (Missing at Random)
   - MNAR (Missing Not at Random)

2. **Handling Methods**
   - Listwise deletion
   - Pairwise deletion
   - Mean imputation
   - Regression imputation

### Outliers
1. **Detection**
   - Z-score method (|Z| > 3)
   - IQR method (beyond fences)
   - Modified Z-score
   ```
   M = 0.6745(x - x̃)/MAD
   where MAD = median absolute deviation
   ```

2. **Treatment**
   - Remove
   - Transform
   - Winsorize
   - Robust statistics

## Effect Size

### Standardized Mean Difference
```
Cohen's d = (x̄₁ - x̄₂)/s
where s = pooled standard deviation
```

### Correlation Coefficients
1. **Pearson's r**
   ```
   r = Σ((x - x̄)(y - ȳ))/(√(Σ(x - x̄)²)×√(Σ(y - ȳ)²))
   ```

2. **Spearman's ρ**
   ```
   ρ = 1 - (6Σd²)/(n(n² - 1))
   where d = difference in ranks
   ```

## Python Implementation
```python
import numpy as np
from scipy import stats

def descriptive_stats(data):
    return {
        'mean': np.mean(data),
        'median': np.median(data),
        'mode': stats.mode(data)[0],
        'std': np.std(data, ddof=1),
        'var': np.var(data, ddof=1),
        'range': np.ptp(data),
        'q1': np.percentile(data, 25),
        'q3': np.percentile(data, 75),
        'iqr': stats.iqr(data),
        'skew': stats.skew(data),
        'kurtosis': stats.kurtosis(data)
    }
```

## R Implementation
```r
descriptive_stats <- function(data) {
  list(
    mean = mean(data),
    median = median(data),
    mode = as.numeric(names(sort(table(data), decreasing=TRUE)[1])),
    sd = sd(data),
    var = var(data),
    range = range(data),
    q1 = quantile(data, 0.25),
    q3 = quantile(data, 0.75),
    iqr = IQR(data),
    skew = moments::skewness(data),
    kurtosis = moments::kurtosis(data)
  )
}
```
