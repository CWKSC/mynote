### Perceptron

```
w1x1 + w2x2 + ... + c to binrary output (0/1)
1 if wx + b <= 0
0 if wx + b >  0
```

### Rectified Linear Unit (ReLU)

```
f(x) = max(0, x)

<= 0  -> 0
> 0   -> x
```

### Stride

```
Stride is number of number every time offset of stepping filter in image

filter is 3*3
image is 5*5

if stride = 1
output is 3*3

if stride = 2
output is 2*2
```

### Convolution Layer

```
Origin image multi by Feature Detector (filter/kernel)

There are multiple filter, so the output will be also multiple

Then apply by ReLU function
```

### Pool Layer

```
Mainly is using Max Pooling or Average Pooling

Max Pooling is Kernel with max function
Average Pooling is Kernal with average of all element

Reduce the resolution of feature map can speed up
```

### Unpooling

```
         1 1 2 2
1 2  ->  1 1 2 2
3 4      3 3 4 4
         3 3 4 4
```

### Max Unpooling

```
Remember position of max element
And use this position to Unpooling, all other value be 0
```

https://medium.com/cubo-ai/%E7%89%A9%E9%AB%94%E5%81%B5%E6%B8%AC-object-detection-740096ec4540

### R-CNN

```
1. Use selective Search to generate Region Proposals
2. Use CNN to get result for each Region Proposals
3. Use SVM to classication
4. Regulate bounding box

Improve version -> Fast R-CNN, Faster R-CNN
```

### Fast R-CNN

```
Use RoIPooling (Region of Interest Pooling) to merge the Region, and only need to do one times of apply CNN 
```

### Faster R-CNN

```
Use CNN to do Proposals
```

### YOLO

```
Divide image into grid
For each grid, output class probability and offset
```

### Harris corner detection

https://en.wikipedia.org/wiki/Harris_corner_detector

https://senitco.github.io/2017/06/18/image-feature-harris/

```
Ix = dI / dx
Iy = dI / dy

Find Ix^2, Iy^2, IxIy

M(x, y) = Σw [ Ix^2  IxIy ]
               IxIy  Iy^2

E(u, v) = [u v] M(x, y) [ u ]
                          v
        = Au^2 + 2Cuv + Bv^2
where
A = Σw Ix^2
B = Σw IY^2
C = Σw IxIy

[u v] M(x, y) [ u ] = 1
                v

M = [ λ1  0  ]
      0   λ2

R = det(M) - α trace(M)^2
det(M) = λ1λ2 = AB - C^2
trace(M) = λ1 + λ2 = A + B

Threshold with value T

Non-maximum suppression with a window (e.g. 5 * 5 window)
```

### Laplacian of Gaussian (LoG)

https://zhuanlan.zhihu.com/p/92143464

```
LoG(x, y) = - 1 / (pi σ^4) [1 - (x^2 + y^2) / (2σ^2)] e^(- (x^2 + y^2) / (2σ^2))
```

### Difference of Gaussian (DoG)

https://en.wikipedia.org/wiki/Difference_of_Gaussians

### Scale Invariant Feature Transform (SIFT)

https://zh.wikipedia.org/wiki/%E5%B0%BA%E5%BA%A6%E4%B8%8D%E8%AE%8A%E7%89%B9%E5%BE%B5%E8%BD%89%E6%8F%9B

https://zhuanlan.zhihu.com/p/261697473

https://zhuanlan.zhihu.com/p/43543527

https://medium.com/data-breach/introduction-to-sift-scale-invariant-feature-transform-65d7f3a72d40

```
```

### k-mean clustering

https://chih-sheng-huang821.medium.com/%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92-%E9%9B%86%E7%BE%A4%E5%88%86%E6%9E%90-k-means-clustering-e608a7fe1b43

```
```

