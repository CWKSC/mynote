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

If A, B is independent
P(A | B) = P(A)
P(B | A) = P(B)

Multiplication Rule
P(AB) = P(B) P(A | B)
```

### Law of total probability

```
P(A) = P(AB) + P(AB')
```

### Bayesian Method

```
Let H is Hypotheses

Prior probability of hypotheses
P(H) : P(H')

Likelihood ratio of evidence under different hypotheses
P(E | H) : P(E | H')

Posterior probability of hypotheses = Prior probability * Likelihood ratio 
P(H | E) = P(H)  P(E | H)
P(H'| E) = P(H') P(E | H')
P(H | E) : P(H' | E) = P(H) P(E | H) : P(H') P(E | H')
```

https://brohrer.mcknote.com/zh-Hant/statistics/how_bayesian_inference_works.html
