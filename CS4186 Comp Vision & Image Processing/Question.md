### Number of operation when apply kernel

```
K is Kernel with k * k
I is image with N * N
K * I denoted as I_K
(x, y) is image pixel location

(a) Represent I_K with I, K, k, x, y

I_K(x, y) = ∑ u = -(k - 1) / 2 to (k - 1) / 2  ∑ v = -(k - 1) / 2 to (k - 1) / 2  K(u, v) I(x - u, y - v)


(b) Represent Number of operation in (a) with N and k

Multiplication: k^2 (N - k + 1)^2
Addition: (k^2 - 1) (N - k + 1)^2


(c) Let K = gh, I_K = (I * g) * h. Represent Number of operation with N and k

K = gh, g * h * I:
Multiplication: k (N - k + 1) (2N - k + 1)
Addition: (k - 1) (N - k + 1) (2N - k + 1)

Convolution divide into two 1d vector and apply to image will reduce number of operation
```

