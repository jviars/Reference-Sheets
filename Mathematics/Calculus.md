# Calculus Reference Sheet

## Limits and Continuity

### Limit Properties
1. **Basic Properties**
   ```
   lim(f + g) = lim(f) + lim(g)
   lim(cf) = c·lim(f)
   lim(f·g) = lim(f)·lim(g)
   lim(f/g) = lim(f)/lim(g), if lim(g) ≠ 0
   ```

2. **Special Limits**
   ```
   lim(sin x)/x = 1 as x → 0
   lim(1 + 1/n)ⁿ = e as n → ∞
   lim(1 + x)¹/ˣ = e as x → 0
   ```

### Continuity
1. **Properties**
   - f is continuous at a if lim[x→a] f(x) = f(a)
   - Sum, product, quotient of continuous functions
   - Composition of continuous functions

2. **Types of Discontinuities**
   - Removable (point)
   - Jump
   - Infinite

## Derivatives

### Basic Rules
1. **Power Rule**
   ```
   d/dx(xⁿ) = n·xⁿ⁻¹
   ```

2. **Product Rule**
   ```
   d/dx(f·g) = f'g + fg'
   ```

3. **Quotient Rule**
   ```
   d/dx(f/g) = (f'g - fg')/g²
   ```

4. **Chain Rule**
   ```
   d/dx(f(g(x))) = f'(g(x))·g'(x)
   ```

### Derivatives of Common Functions
1. **Trigonometric**
   ```
   d/dx(sin x) = cos x
   d/dx(cos x) = -sin x
   d/dx(tan x) = sec² x
   d/dx(cot x) = -csc² x
   d/dx(sec x) = sec x·tan x
   d/dx(csc x) = -csc x·cot x
   ```

2. **Exponential and Logarithmic**
   ```
   d/dx(eˣ) = eˣ
   d/dx(aˣ) = aˣ·ln(a)
   d/dx(ln x) = 1/x
   d/dx(log_a x) = 1/(x·ln(a))
   ```

3. **Inverse Trigonometric**
   ```
   d/dx(arcsin x) = 1/√(1 - x²)
   d/dx(arccos x) = -1/√(1 - x²)
   d/dx(arctan x) = 1/(1 + x²)
   ```

### Applications of Derivatives
1. **Related Rates**
   - Chain rule with time derivatives
   - Geometric relationships

2. **Optimization**
   - Critical points: f'(x) = 0 or undefined
   - Second derivative test
   - Absolute extrema on closed interval

## Integration

### Basic Integrals
1. **Power Rule**
   ```
   ∫xⁿ dx = xⁿ⁺¹/(n+1) + C, n ≠ -1
   ∫(1/x) dx = ln|x| + C
   ```

2. **Exponential and Logarithmic**
   ```
   ∫eˣ dx = eˣ + C
   ∫aˣ dx = aˣ/ln(a) + C
   ```

3. **Trigonometric**
   ```
   ∫sin x dx = -cos x + C
   ∫cos x dx = sin x + C
   ∫sec² x dx = tan x + C
   ∫csc² x dx = -cot x + C
   ∫tan x dx = ln|sec x| + C
   ∫cot x dx = ln|sin x| + C
   ```

### Integration Techniques
1. **Substitution (u-substitution)**
   ```
   ∫f(g(x))g'(x) dx = ∫f(u) du
   where u = g(x)
   ```

2. **Integration by Parts**
   ```
   ∫u dv = uv - ∫v du
   ```

3. **Partial Fractions**
   ```
   Distinct linear factors: A/(x-a) + B/(x-b)
   Repeated linear factors: A/(x-a) + B/(x-a)²
   Quadratic factors: (Ax + B)/(x² + px + q)
   ```

4. **Trigonometric Substitution**
   ```
   √(a² - x²): x = a·sin θ
   √(a² + x²): x = a·tan θ
   √(x² - a²): x = a·sec θ
   ```

### Applications of Integration
1. **Area Between Curves**
   ```
   Area = ∫[f(x) - g(x)] dx
   ```

2. **Volume of Revolution**
   ```
   Disk method: V = π∫[f(x)]² dx
   Washer method: V = π∫[R(x)² - r(x)²] dx
   Shell method: V = 2π∫x·f(x) dx
   ```

3. **Arc Length**
   ```
   L = ∫√(1 + [f'(x)]²) dx
   ```

## Vector Calculus

### Vector Functions
1. **Derivatives**
   ```
   r'(t) = <x'(t), y'(t), z'(t)>
   ```

2. **Properties**
   ```
   d/dt(r₁ + r₂) = r₁' + r₂'
   d/dt(f·r) = f'r + fr'
   ```

### Multiple Integration
1. **Double Integrals**
   ```
   ∫∫f(x,y) dA = ∫ᵃᵇ∫ᵍ⁽ˣ⁾ʰ⁽ˣ⁾f(x,y) dy dx
   ```

2. **Triple Integrals**
   ```
   ∫∫∫f(x,y,z) dV
   ```

3. **Change of Variables**
   ```
   Double: |∂(x,y)/∂(u,v)|
   Triple: |∂(x,y,z)/∂(u,v,w)|
   ```

### Vector Fields
1. **Gradient**
   ```
   ∇f = <∂f/∂x, ∂f/∂y, ∂f/∂z>
   ```

2. **Divergence**
   ```
   div F = ∇·F = ∂P/∂x + ∂Q/∂y + ∂R/∂z
   ```

3. **Curl**
   ```
   curl F = ∇×F = <∂R/∂y - ∂Q/∂z, ∂P/∂z - ∂R/∂x, ∂Q/∂x - ∂P/∂y>
   ```

## Differential Equations

### First Order DEs
1. **Separable Equations**
   ```
   dy/dx = g(x)h(y)
   ∫(1/h(y))dy = ∫g(x)dx
   ```

2. **Linear Equations**
   ```
   dy/dx + P(x)y = Q(x)
   μ(x) = e^∫P(x)dx (integrating factor)
   ```

### Second Order Linear DEs
1. **Homogeneous**
   ```
   ay'' + by' + cy = 0
   Characteristic equation: ar² + br + c = 0
   ```

2. **Non-homogeneous**
   ```
   ay'' + by' + cy = f(x)
   Particular solution + Complementary solution
   ```

## Series

### Power Series
1. **Taylor Series**
   ```
   f(x) = Σ(f⁽ⁿ⁾(a)/n!)(x-a)ⁿ
   ```

2. **Maclaurin Series**
   ```
   eˣ = 1 + x + x²/2! + x³/3! + ...
   sin x = x - x³/3! + x⁵/5! - ...
   cos x = 1 - x²/2! + x⁴/4! - ...
   ```

### Tests for Convergence
1. **Ratio Test**
   ```
   lim|aₙ₊₁/aₙ| = L
   L < 1: converges
   L > 1: diverges
   L = 1: inconclusive
   ```

2. **Root Test**
   ```
   lim|aₙ|¹/ⁿ = L
   L < 1: converges
   L > 1: diverges
   L = 1: inconclusive
   ```

3. **Comparison Tests**
   - Direct comparison
   - Limit comparison

## Key Theorems

### Calculus Fundamentals
1. **Mean Value Theorem**
   ```
   f'(c) = [f(b) - f(a)]/(b-a)
   for some c in (a,b)
   ```

2. **Intermediate Value Theorem**
   ```
   For continuous f on [a,b],
   f takes on all values between f(a) and f(b)
   ```

3. **Extreme Value Theorem**
   ```
   Continuous f on [a,b] has
   absolute maximum and minimum
   ```

### Integration
1. **Fundamental Theorem of Calculus**
   ```
   Part 1: d/dx[∫ᵃˣf(t)dt] = f(x)
   Part 2: ∫ᵃᵇf(x)dx = F(b) - F(a)
   ```

2. **Green's Theorem**
   ```
   ∮_C(P dx + Q dy) = ∫∫_D(∂Q/∂x - ∂P/∂y)dA
   ```

3. **Stokes' Theorem**
   ```
   ∮_C F·dr = ∫∫_S(curl F)·n dS
   ```

4. **Divergence Theorem**
   ```
   ∫∫_S F·n dS = ∫∫∫_V div F dV
   ```
