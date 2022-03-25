### Cross-correlation and Convolution

```
F is image, H is kernel of size 2k + 1 * 2k + 1
G is output

Cross-correlation:
G[i, j] = Σ u = -k to k  Σ v = -k to k  H[u, v] F[i + u, j + v]
G = H ⊗ F

Convolution:
G[i, j] = Σ u = -k to k  Σ v = -k to k  H[u, v] F[i - u, j - v]
G = H * F

Convolution is commutative and associative
F * G = G * F  (commutative)
F * (G * I) = (F * G) * I  (associative) 
```

### Mean filtering

```python
# Mean Kernal is all element with 1 / total number of element

import numpy as np

def genMeanKernal(k = 1):
    length = 2 * k + 1
    return np.full((length, length), 1 / (length * length))

print(genMeanKernal(1))
#[[0.11111111 0.11111111 0.11111111]
# [0.11111111 0.11111111 0.11111111]
# [0.11111111 0.11111111 0.11111111]]

print(genMeanKernal(2))
#[[0.04 0.04 0.04 0.04 0.04]
# [0.04 0.04 0.04 0.04 0.04]
# [0.04 0.04 0.04 0.04 0.04]
# [0.04 0.04 0.04 0.04 0.04]
# [0.04 0.04 0.04 0.04 0.04]]
```

### Sharpening filter

```
0 0 0       1 1 1
0 2 0 - 1/9 1 1 1
0 0 0       1 1 1
```

### Gaussian Kernel

```python
# Gσ = e^(- (x^2 + y^2) / (2σ^2)) / (2 pi σ^2)
# σ is Standard Deviation (SD)

import numpy as np

def gaussianFunc(x, y, sd=1):
    return np.exp(-(x ** 2 + y ** 2) / (2 * sd ** 2)) / (2 * np.pi * sd ** 2)

def genGaussianKernel(k=1, sd=1):
    x, y = np.mgrid[-k : k + 1, -k : k + 1]
    gaussian_kernel = gaussianFunc(x, y, sd)
    return gaussian_kernel / np.sum(gaussian_kernel)

print(genGaussianKernel(1))
# [[0.07511361 0.1238414  0.07511361]
#  [0.1238414  0.20417996 0.1238414 ]
#  [0.07511361 0.1238414  0.07511361]]

print(genGaussianKernel(2))
# [[0.00296902 0.01330621 0.02193823 0.01330621 0.00296902]
#  [0.01330621 0.0596343  0.09832033 0.0596343  0.01330621]
#  [0.02193823 0.09832033 0.16210282 0.09832033 0.02193823]
#  [0.01330621 0.0596343  0.09832033 0.0596343  0.01330621]
#  [0.00296902 0.01330621 0.02193823 0.01330621 0.00296902]]
```

### Thresholding Filters

```
threshold(x, y) = value  if f(x, y) > threshold 
                  0      otherwise
```

### Image derivatives

```
∂f / ∂x [x, y] ≈ F[x + 1, y] - F[x, y]

          /  /  /
∂f / ∂x : 1 -1  /
          /  /  /

          /  /  /
∂f / ∂y : / -1  /
          /  1  /

|| ∇ f || = [∂f / ∂x, ∂f / ∂y]
θ = tan^-1((∂f / ∂y) / (∂f / ∂x))
```

### Edge detection

```
Edge will appear in the place of value fast change
It mean value of image derivatives / scope is high

One of the problem is
Noise will make image derivatives be chaos

Apply mean or gaussian kernel to remove noise first

Since it is associative of convolution:
d / dx (f * h)
= f * dh / dx

Image can apply derivatives of kernal to get image derivatives
```

### Sobel operator

```
Common approximation of derivative of Gaussian

           -1  0  1
sx = 1 / 8 -2  0  1
           -1  0  1

            1  2  1
sy = 1 / 8  0  0  0
           -1 -2 -1
```

### 1D Gaussian

```
Gσ(x) = e^(-x^2 / (2σ^2)) / (sqrt(2 pi) σ^2)

Gσ'(x) = d / dx Gσ(x) = - 1 / σ (x / σ) Gσ(x) 
```

### Canny edge detector

```
// https://medium.com/@pomelyu5199/canny-edge-detector-%E5%AF%A6%E4%BD%9C-opencv-f7d1a0a57d19

1. Filter image with derivative of Gaussian
2. Find magnitude and orientation of gradient
3. Non-maximum suppression
4. Double Thresholding, divided strong edge and weak edge
5. Hysteresis, connect edge, start from strong edge pixel and connect with weak edge pixel
```

### Gaussian pyramid

```
Repeat smoothing and subsampling to get a set of image
```

### Histograms

```
y axis is number of pixel
x axis is value (gray / RGB / ...)

h(i) = Σ x  Σ y  1  if I(x, y) = value
                 0  otherwise

Sum of pixel with value as Histograms
```

### Histogram Matching

```
h(I) is image histogram
h(M) is model histogram

Intersection of image histogram and model histogram:
intersection(h(I), h(M)) = Σ i from 0 to number of bin  min(h(I)[i], h(M)[i])

Match score with normalized intersection:
match(h(I), h(M)) = intersection(h(I), h(M)) / Σ i from 0 to number of bin h(M)[i]
```

### Two Edge-based Texture Measures

```
Region R of N pixels
Mag(p) is gradient magnitude of p
T is threshold

F_edgeness = |{p | Mag(p) >= T}| / N

F_magfir = (H_mag(R), H_dir(R))

// Reference to 7.3.1 Edge Density and Direction
// https://courses.cs.washington.edu/courses/cse576/book/ch7.pdf 
```

### Local Binary Pattern Measure (very important)

```
b1 b2 b3
b8 X  b4  -> b1 b2 b3 b4 b5 b6 b7 b8    1 if bi >= X else 0 
b7 b6 b5

LBP_p,r(Nc) = Σ p from 0 to P - 1 g(Np - Nc) 2^p

Nc: center pixel
Np: neighbor pixel
r: radius
g(x): threshold function
g(x) = 1 if x >= 0
       0 if x <  0
```

### Co-occurrence Matrix

```
C_d(i, j) is a Co-occurrence Matrix by relationship d
d = (dr, dc)

d is a offset from origin
dc is right offset, offset of column
dr is down offset, offset of row
i is origin, j is location of origin after offset

C_d(i, j) = Σ row  Σ col  1 if I[row][col] == i && I[row + dr][col + dc] == j else 0

For example:
I:
1 1 0 0
1 1 0 0
0 0 2 2
0 0 2 2
0 0 2 2
0 0 2 2

if d = (1, 1)
C_d:
i\j 0 1 2
0   4 0 4
1   2 1 1
2   0 0 3

if d = (3, 1)
C_d:
i\j 0 1 2
0   1 0 3
1   2 0 2
2   0 0 1
```



