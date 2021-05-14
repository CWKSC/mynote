## Disjoint Set

Equivalence Relation

- Reflexive, Symmetric and Transitive

Reflexive: for every a, a R a is exist

Symmetric: a R b -> b R a, b R a -> a R b

Transitive: a R b and b R c -> a R c

### Array Implementation

```c++
class DisjointSet<T> {
    T name[Size];
    int Find(int);
    void Union(int, int)
}
```

### Tree Implementation

smaller tree connect to large tree

low height tree connect to deeper tree

if height of tree is equal, height will increase after union

## Sorting

### Heapsort

build heap, delete min n times

### Merge Sort

Spilt to smaller, and Merge sorted array

### Bucket Sort

### Radix Sort