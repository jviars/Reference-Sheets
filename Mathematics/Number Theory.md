# Number Theory Reference Sheet

## Divisibility and Prime Numbers

### Basic Divisibility
1. **Definition**
   - a|b means a divides b
   - ∃k ∈ ℤ such that b = ak

2. **Properties**
   - If a|b and b|c, then a|c (transitivity)
   - If a|b and a|c, then a|(bx + cy) for any x,y ∈ ℤ
   - If a|b and b|a, then a = ±b

### Prime Numbers
1. **Definition**
   - p > 1 with exactly two divisors: 1 and p

2. **Properties**
   - Infinite number of primes (Euclid's proof)
   - If p|ab, then p|a or p|b (prime divisor property)

3. **Primality Tests**
   ```python
   def is_prime(n):
       if n < 2:
           return False
       for i in range(2, int(n**0.5) + 1):
           if n % i == 0:
               return False
       return True
   ```

### Fundamental Theorem of Arithmetic
1. **Statement**
   - Every positive integer > 1 can be uniquely factored into primes
   - n = p₁ᵃ¹p₂ᵃ²...pₖᵃᵏ

2. **Example**
   ```
   84 = 2² × 3 × 7
   ```

## Greatest Common Divisor (GCD)

### Definition and Properties
1. **GCD(a,b)**
   - Largest d such that d|a and d|b
   - gcd(a,b) = gcd(b,a)
   - gcd(a,0) = |a|

2. **Linear Combination Property**
   - gcd(a,b) = ax + by for some x,y ∈ ℤ (Bézout's Identity)

### Euclidean Algorithm
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return abs(a)
```

### Extended Euclidean Algorithm
```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    d, x, y = extended_gcd(b, a % b)
    return d, y, x - (a // b) * y
```

## Congruences

### Basic Properties
1. **Definition**
   - a ≡ b (mod m) if m|(a-b)
   - a ≡ b (mod m) ⟺ a = b + km for some k ∈ ℤ

2. **Properties**
   - If a ≡ b (mod m) and c ≡ d (mod m), then:
     * a + c ≡ b + d (mod m)
     * ac ≡ bd (mod m)

### Linear Congruences
1. **ax ≡ b (mod m)**
   - Solutions exist iff gcd(a,m)|b
   - If solution exists, there are gcd(a,m) solutions

2. **Chinese Remainder Theorem (CRT)**
   ```
   x ≡ a₁ (mod m₁)
   x ≡ a₂ (mod m₂)
   ...
   x ≡ aₖ (mod mₖ)
   ```
   - Solution exists if gcd(mᵢ,mⱼ) = 1 for i ≠ j
   - Solution is unique modulo M = m₁m₂...mₖ

## Euler's Function and Theorems

### Euler's Totient Function φ(n)
1. **Definition**
   - φ(n) = number of integers k, 1 ≤ k ≤ n, with gcd(k,n) = 1

2. **Properties**
   - For prime p: φ(p) = p - 1
   - For prime power pᵏ: φ(pᵏ) = pᵏ - pᵏ⁻¹
   - For coprime m,n: φ(mn) = φ(m)φ(n)

3. **Formula**
   - For n = p₁ᵃ¹p₂ᵃ²...pₖᵃᵏ:
   - φ(n) = n∏(1 - 1/pᵢ)

### Euler's Theorem
1. **Statement**
   - If gcd(a,n) = 1, then aᶠ⁽ⁿ⁾ ≡ 1 (mod n)

2. **Fermat's Little Theorem**
   - If p is prime and p∤a, then aᵖ⁻¹ ≡ 1 (mod p)
   - For any a: aᵖ ≡ a (mod p)

## Primitive Roots and Indices

### Primitive Roots
1. **Definition**
   - g is primitive root modulo n if:
   - {g¹,g²,...,gᶠ⁽ⁿ⁾} ≡ {a: gcd(a,n) = 1} (mod n)

2. **Properties**
   - Not all numbers have primitive roots
   - Primitive roots exist for:
     * Odd prime powers
     * 2, 4
     * 2 times odd prime power

### Discrete Logarithm
1. **Definition**
   - If g is primitive root mod p:
   - ind_g(a) = k where gᵏ ≡ a (mod p)

2. **Properties**
   - ind_g(ab) ≡ ind_g(a) + ind_g(b) (mod φ(p))
   - ind_g(aⁿ) ≡ n·ind_g(a) (mod φ(p))

## Quadratic Residues

### Legendre Symbol
1. **Definition**
   - (a/p) = 1 if a is QR mod p
   - (a/p) = -1 if a is NQR mod p
   - (a/p) = 0 if p|a

2. **Properties**
   - (a/p)(b/p) = (ab/p)
   - If a ≡ b (mod p), then (a/p) = (b/p)

### Law of Quadratic Reciprocity
1. **Statement**
   - For odd primes p,q:
   - (p/q)(q/p) = (-1)⁽ᵖ⁻¹⁾⁽ᵍ⁻¹⁾/⁴

2. **Supplementary Laws**
   - (−1/p) = (−1)⁽ᵖ⁻¹⁾/²
   - (2/p) = (−1)⁽ᵖ²⁻¹⁾/⁸

## Diophantine Equations

### Linear Diophantine Equations
1. **ax + by = c**
   - Solutions exist iff gcd(a,b)|c
   - If (x₀,y₀) is a solution:
     * x = x₀ + (b/d)t
     * y = y₀ - (a/d)t
     where d = gcd(a,b), t ∈ ℤ

2. **Implementation**
```python
def diophantine(a, b, c):
    d, x, y = extended_gcd(a, b)
    if c % d != 0:
        return None  # No solution
    x *= c // d
    y *= c // d
    return (x, y, d)
```

### Pythagorean Triples
1. **Primitive Triples**
   - a = m² - n²
   - b = 2mn
   - c = m² + n²
   where m > n > 0, gcd(m,n) = 1, m-n odd

2. **All Triples**
   - Multiply primitive triple by k ∈ ℤ⁺

## Special Numbers and Sequences

### Perfect Numbers
1. **Definition**
   - n equals sum of proper divisors
   - Example: 6 = 1 + 2 + 3

2. **Properties**
   - Even perfect numbers have form:
   - n = 2ᵖ⁻¹(2ᵖ-1) where 2ᵖ-1 is prime

### Mersenne Primes
1. **Definition**
   - Prime numbers of form 2ᵖ-1
   - p must be prime for 2ᵖ-1 to be prime

2. **Known Values**
   - M₂ = 3
   - M₃ = 7
   - M₅ = 31
   - M₇ = 127

### Fibonacci Numbers
1. **Definition**
   - F₀ = 0, F₁ = 1
   - Fₙ = Fₙ₋₁ + Fₙ₋₂

2. **Properties**
   - gcd(Fₙ,Fₘ) = Fgcd(n,m)
   - F²ₙ₊₁ - Fₙ₊₁Fₙ = (-1)ⁿ

## Applications

### Cryptography
1. **RSA Algorithm**
   ```
   1. Choose primes p, q
   2. n = pq
   3. φ(n) = (p-1)(q-1)
   4. Choose e with gcd(e,φ(n)) = 1
   5. Find d where ed ≡ 1 (mod φ(n))
   Public key: (n,e)
   Private key: d
   ```

2. **Diffie-Hellman Key Exchange**
   ```
   1. Choose prime p and primitive root g
   2. Alice chooses a, sends gᵃ mod p
   3. Bob chooses b, sends gᵇ mod p
   4. Shared key: gᵃᵇ mod p
   ```

### Error Detection
1. **Check Digits**
   - ISBN-10
   - UPC
   - Credit card numbers

2. **Properties**
   - Based on modular arithmetic
   - Can detect common errors
