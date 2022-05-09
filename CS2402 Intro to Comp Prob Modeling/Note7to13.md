### Sn and mean of Xn

```
X1, X2, ..., Xn is independent random variable with same distribution
Sn = X1 + X2 + ... + Xn

E(Sn) = n E(X)
Var(Sn) = n Var(X)
SD(Sn) = sqrt(n) SD(X)
SD(Sn) = sqrt(Var(X))

mean of Xn = Sn / n
E(mean of Xn) = E(X)
SD(mean of Xn) = SD(X) / sqrt(n)
```

### Normal Distribution (Out of Syllabus)

```
X ~ N(μ, σ^2)
E(X) = μ
Var(X) = σ^2
SD(X) = σ

f(x) = e^(- (x - μ)^2 / (2σ^2)) / (σ sqrt(2 pi))
F(x) = (1 + erf((x - μ) / (σ sqrt(2)))) / 2
erf(x) = 1 / sqrt(pi) Integral x to -x e^(-t^2) dt
```

### Standard Normal Distribution

```
X ~ N(0, 1)
E(X) = 0
Var(X) = 1
SD(X) = 1

P(X = x) = f(x)
f(x) = e^(- x^2 / 2) / sqrt(2 pi)
f(x) = f(-x)
f(x) = 0 if x -> +/-inf
Integral -inf to +inf f(x) dx = 1

P(X <= x) = F(x)
F(x) = Integral -inf to x  f(x) dx
F(0) = 0.5
Integral -1 to 1 f(x) dx = F(1) - F(-1) = 0.68
Integral -2 to 2 f(x) dx = F(2) - F(-2) = 0.95
Integral -3 to 3 f(x) dx = F(3) - F(-3) = 0.997

P(a < X < b) = Integral a to b  f(x) dx = F(b) - F(a)
```

### Normalization (standardized)

```
When E(X) = μ, SD(X) = σ
X* is standardized random variable of X
X* = (X - μ) / σ
```

### Central Limit Theorem

```
Central limit theorem mean sum of independent random variables will become normal distribution after normalization (standardized), even original variables not normal distribution

When E(X) = μ, SD(X) = σ
Sn* is standardized random variable of Sn
Sn* = (Sn - E(Sn)) / SD(Sn) = (Sn - nμ) / (sqrt(n)σ)
```

### Conditional Probability

```
P(A | B) = outcomes in AB / outcomes in B
P(A | B) = P(AB) / P(B)

Multiplication Rule
P(AB) = P(B) P(A | B) = P(A) P(B | A)

P(A | B) >= 0
P(A | A) = 1
P(A1 U A2 U A3 ... | B) = P(A1 | B) + P(A2 | B) + P(A2 | B) + ...

P(A' | B) = 1 - P(A | B)

If A B are disjoint
P(A | B) = 0

If A, B is independent
P(A | B) = P(A)
P(B | A) = P(B)
P(AB | C) = P(A | C) P(B | C)

If B is subset of A, i.e. B ⊂ A, A ∩ B = B
P(A | B) = 1

If A is subset of B, i.e. A ⊂ B, A ∩ B = A
P(A | B) = P(A) / P(B)
```

### Bayes' rule

```
P(A | B)
= P(AB) / P(B)
= P(B | A) P(A) / P(B)

P(AB) = P(A | B) P(B) = P(B | A) P(A)
```

### Law of total probability

```
P(A) = P(AB) + P(AB')
P(A) = P(A | B) P(B) + P(A | B') P(B')

// https://en.wikipedia.org/wiki/Law_of_total_probability
```

### Bayesian Method

```
Let H is Hypotheses

Prior probability of hypotheses
P(H) : P(H')

Likelihood ratio of evidence under different hypotheses
P(E | H) : P(E | H')

Posterior probability of hypotheses = Prior probability * Likelihood ratio 
P(H | E) : P(H' | E) = P(H) P(E | H) : P(H') P(E | H')
```

https://brohrer.mcknote.com/zh-Hant/statistics/how_bayesian_inference_works.html

### Linear Regression

```
y = mx + c

find
x
y
x - mean x
y - mean y
(x - mean x) (y - mean y)
(x - mean x)^2
Sxy
Sxx

m = Sxy / Sxx
c = mean y - m mean x
```

### Correlation Coefficient (r)

```
r = 1 / (n - 1) Σi=1 to n  ((xi - mean x) / Sx) ((yi - mean y) / Sy)
```

### Maximum Likelihood Estimation (MLE)

https://people.missouristate.edu/songfengzheng/Teaching/MTH541/Lecture%20notes/MLE.pdf

### Poisson Distribution

```
P(X = k) = λ^k e^(-λ) / k!

P(X = 0) = e^(-λ)
P(X = 1) = λ e^(-λ) 
P(X = 2) = λ^2 e^(-λ) / 2
P(X = 2) = λ^3 e^(-λ) / 6

E(X) = λ
Var(X) = λ
SD(X) = sqrt(λ)

If B(n, p) where n is very large and p is very small
B(n, p) ~= Poisson(np)
```

### Uniform Distribution

```
f(x) = 1 / (x_max - x_min) if x_min <= x <= x_max  else 0

E(x) = (x_min + x_max) / 2
Var(X) = (x_max - x_min)^2 / 12
```

