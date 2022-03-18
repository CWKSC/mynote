### Combination and Permutation

```
P(n, r) = n! / (n - r)!
C(n, r) = P(n, r) / r! = n! / (r!(n - r)!)
```

### Star and bar 隔板法

https://zh.wikipedia.org/wiki/%E9%9A%94%E6%9D%BF%E6%B3%95

```
n object into k box
x1 + x2 + ... xk = n

Not allow empty box (at least 1)
C(n - 1, k - 1)

Allow empty box (at least 0)
C(n + k - 1, k - 1)

At least 2
C(n - k - 1, k - 1)

At least 3
C(n - 2 * k - 1, k - 1)

At least m
C(n + (1 - m) * k - 1, k - 1)

x1 + x2 + ... xk = n
where xi >= mi (at least mi)
C(n + sum of (1 - mi) - 1, k - 1)

Example:
x1 + x2 + x3 + x4 = 20
where x1 >= 0, x2 >= 1, x3 >= 2, x4 >= 3
How many integer solution?

C(20 - ((1 - 0) + (1 - 1) + (1 - 2) + (1 - 3)) - 1, 4 - 1)
= C(20 - (-1 + 0 + 1 + 2) - 1, 4 - 1)
= 680
```

### 插空法

https://zh.wikipedia.org/wiki/%E6%8F%92%E7%A9%BA%E6%B3%95

### Problem of points / Unfinished Game  / 賭金分配問題 The Problem of Division of the Stakes / 

```
money * win round of someone / all possible outcomes of remaining rounds
list of all the outcome and count

A remain x round to win
B remain y round to win
Max total remaining rounds = (x - 1) + (y - 1) + 1 = x + y - 1

Xi remain wi round to win, where i from 1 to n
Max total remaining rounds = sum of (wi - 1)  + 1 = sum of wi  - n + 1

(Out of Syllabus)
// https://en.wikipedia.org/wiki/Problem_of_points
ratio of A : ratio of B 
ratio of A = Sum of k = 0 to s - 1 ( C(r + s - 1, k) )
ratio of B = Sum of k = s to r + s - 1 ( C(r + s - 1, k) )
```

### False Positive

```
Test Always positive if have disease
Probability of false positive = fp
Probability of have disease = d

            Positive      Negative
Disease     d * 1 = d     0
No disease  d' * fp       Not given

P(disease | positive) = d / (d + d' * fp)
```

### Three Axioms of Probability

```
1. P(A) >= 0 for any event A
2. P(S) = 1, where S is sample space
3. P(A1 U A2 U A3 ...) = P(A1) + P(A2) + P(A3) + ...
```

### Notation

```
P(A U B) = P(A or B)
P(A ∩ B) = P(AB) = P(A and B)
Usually P(A ∩ B) will write as P(AB) in following
```

### Basic

```
P(A) <= 1
P(A') = 1 - P(A)

P(A - B) = P(AB')
P(A − B) = P(A) − P(AB)
```

### Union

```
P(A U B) = P(A) + P(B) - P(AB)

If A, B is disjoint
P(A U B) = P(A) + P(B)
```

### Intercept

```
P(AB) = P(A) P(B)

If A, B is disjoint
P(AB) = 0

If A, B is dependent
P(AB) = P(A) P(B | A) = P(B) P(A | B)

If A, B is independent
P(AB) = P(A) P(B)
P(A1 A2 A3 ...) = P(A1) P(A2) P(A3) ...
```

### Disjoint event

```
Disjoint mean A and B cannot occur at the same time
Disjoint != Independent

AB = ∅
P(AB) = P(∅) = 0
P(A U B) = P(A) + P(B)
P(A1 U A2 U A3 ...) = P(A1) + P(A2) + P(A3) + ...
```

### Dependent event

```
Dependent mean happen A or B will affect probability of other

P(AB) = P(A) P(B | A) = P(B) P(A | B)
```

### Independent event

```
Independent mean happen A or B not affect probability of other
Independent != Disjoint

P(AB) = P(A) P(B)
P(A | B) = P(A)

A and B' are also independent
A' and B are also independent
A' and B' are also independent

Use P(AB) != P(A) P(B) to prove A, B not Independent event

E(XY) = E(X) E(Y)
Var(X + Y) = Var(X) + Var(Y)
```

### Conditional probability

```
P(A | B) = P(A ∩ B) / P(B)

P(A | B) >= 0
P(A | A) = 1
P(A1 U A2 U A3 ... | B) = P(A1 | B) + P(A2 | B) + P(A2 | B) + ...

If A B are disjoint
P(A | B) = 0

If B is subset of A, i.e. B ⊂ A, A ∩ B = B
P(A | B) = 1

If A is subset of B, i.e. A ⊂ B, A ∩ B = A
P(A | B) = P(A) / P(B)
```

### Bayes' rule

```
P(A | B) = P(A) P(B | A) / P(B)
P(AB) = P(A | B) P(B) = P(B | A) P(A)
```

### Cumulative distribution function (CDF)

```
F(X) = P(X <= x)
```

### Binomial Distribution

```
X ~ B(n, p)
P(X = k) = C(n, k) p^k (1 - p)^(n - k)

E(X) = np
Var(X) = np(1 - p)
```

### Expectation Mean

```
E(X) = sum of  x P(X = x)
E(X) = sum of  (1 - P(X <= x)) = sum of P(X > x)
E(f(x)) = sum of  f(x) P(X = x)

E(X + Y) = E(X) + E(Y)
E(aX) = aE(x)

If X ~ B(n, p)
E(X) = np

If Independent
E(XY) = E(X)E(Y)
```

### Variance 

```
Var(X) = E([X - E(X)]^2)
Var(X) = E(X^2) - E(X)^2

Var(X + a) = Var(X)
Var(aX) = a^2 Var(X)

If Independent
Var(X + Y) = Var(X) + Var(Y)

If X ~ B(n, p)
Var(X) = np(1 - p)
```

### Standard Deviation

```
SD(X) = sqrt(Var(X))

SD(aX + b) = |a|SD(X)
```

### Markov’s Inequality

```
P(X >= a) <= E(X) / a  if X >= 0, a > 0
```

### Chebyshev’s Inequality

```
P(|X - E(X)| >= k * SD(x)) <= 1 / k^2
P(|X - E(X)| < k * SD(x)) >= 1 - 1 / k^2
```

### Bernoulli’s Utility

```
utility = log( wealth )
utility change of gain = log( wealth + gain ) – log( wealth )
```

