# NumPy Quick Reference & Cheat Sheet

A concise reference guide covering essential NumPy functions, syntax, and workflows for beginners and intermediate users.

---

## 1. Array Creation

```python
import numpy as np

# From Python collections
a = np.array([1, 2, 3])                # 1D array (vector)
b = np.array([[1, 2, 3], [4, 5, 6]])   # 2D array (matrix)
c = np.array([1, 2, 3], dtype=np.float32)  # Explicit data type

# Constant and filled arrays
np.zeros((3, 4))                       # 3x4 array of zeros (float64 by default)
np.ones((2, 3))                        # 2x3 array of ones
np.full((2, 2), 7)                     # 2x2 array filled with 7
np.eye(4)                              # 4x4 Identity matrix
np.empty((2, 3))                       # Uninitialized memory values

# Ranges and sequences
np.arange(0, 10, 2)                    # [0, 2, 4, 6, 8] (start, stop, step)
np.linspace(0, 1, 5)                   # 5 evenly spaced numbers from 0 to 1
np.logspace(0, 2, 3)                   # Logarithmically spaced: [1., 10., 100.]

# Random generation
np.random.seed(42)                     # Set seed for reproducibility
np.random.rand(2, 3)                   # Uniform distribution [0, 1)
np.random.randn(2, 3)                  # Standard normal distribution (mean=0, stdev=1)
np.random.randint(1, 100, size=(3, 3)) # Random integers between [low, high)
np.random.choice([10, 20, 30], size=5) # Random sampling with replacement
```

---

## 2. Array Attributes & Inspection

```python
arr = np.array([[1, 2, 3], [4, 5, 6]], dtype=np.int32)

arr.shape       # (2, 3) -> dimensions (rows, columns)
arr.ndim        # 2 -> number of dimensions
arr.size        # 6 -> total number of elements
arr.dtype       # dtype('int32') -> data type of elements
arr.itemsize    # 4 -> bytes per element
arr.nbytes      # 24 -> total bytes consumed in memory
```

---

## 3. Indexing & Slicing

### 1D Arrays
```python
x = np.array([10, 20, 30, 40, 50])
x[0]            # 10 (first item)
x[-1]           # 50 (last item)
x[1:4]          # array([20, 30, 40]) (slice [start:stop])
x[::2]          # array([10, 30, 50]) (step of 2)
x[::-1]         # Reversed array
```

### 2D Arrays (Matrices)
```python
M = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

M[0, 0]         # 1 -> element at row 0, col 0
M[1]            # array([4, 5, 6]) -> entire row 1
M[:, 1]         # array([2, 5, 8]) -> entire column 1
M[0:2, 1:3]     # Submatrix: rows 0-1, cols 1-2
```

### Boolean Masking & Filtering
```python
nums = np.array([12, 45, 67, 89, 34, 22])
mask = nums > 40              # [False, True, True, True, False, False]
nums[mask]                    # array([45, 67, 89])
nums[(nums > 20) & (nums < 70)]  # Logical AND (bitwise &)
nums[(nums < 20) | (nums > 80)]  # Logical OR (bitwise |)

# Conditional replacement
labels = np.where(nums >= 50, "Pass", "Fail")
```

---

## 4. Reshaping, Flattening & Dimensions

```python
a = np.arange(12)              # 1D array of 12 elements
b = a.reshape((3, 4))          # Reshape to 3 rows, 4 cols
c = a.reshape((3, -1))         # -1 automatically calculates dimension (4)

# Flattening
b.flatten()                    # Returns a 1D copy
b.ravel()                      # Returns a 1D view (faster, memory-efficient)

# Transposing
b.T                            # Transpose matrix (4x3)
np.transpose(b)

# Adding / Removing Axes
x = np.array([1, 2, 3])
x_col = x[:, np.newaxis]       # Shape (3, 1)
x_row = np.expand_dims(x, 0)   # Shape (1, 3)
squeezed = np.squeeze(x_col)   # Removes dimensions of length 1 -> Shape (3,)
```

---

## 5. Joining & Splitting Arrays

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

# Concatenation
np.concatenate((a, b), axis=0)  # Stack along rows (vertical) -> shape (4, 2)
np.concatenate((a, b), axis=1)  # Stack along cols (horizontal) -> shape (2, 4)

# Convenience stackers
np.vstack((a, b))               # Vertical stack
np.hstack((a, b))               # Horizontal stack
np.column_stack((a[:, 0], b[:, 0]))

# Splitting
upper, lower = np.vsplit(a, 2)
left, right = np.hsplit(a, 2)
```

---

## 6. Mathematical & Aggregation Operations

All operations are vectorized (element-wise) by default:

```python
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

# Element-wise arithmetic
x + y        # [5, 7, 9]
x * y        # [4, 10, 18]
x ** 2       # [1, 4, 9]
np.sqrt(x)   # Square root
np.exp(x)    # Exponential e^x
np.log(x)    # Natural log ln(x)

# Aggregations across axes
M = np.array([[10, 20], [30, 40]])
np.sum(M)               # 100 (total sum)
np.sum(M, axis=0)       # [40, 60] (sum down columns)
np.sum(M, axis=1)       # [30, 70] (sum across rows)
np.mean(M, axis=0)      # [20., 30.]
np.std(M)               # Standard deviation
np.min(M), np.max(M)    # 10, 40
np.argmin(M), np.argmax(M)  # Index of min/max

# Cumulative operations
np.cumsum(x)            # [1, 3, 6]
np.cumprod(x)           # [1, 2, 6]
```

---

## 7. Linear Algebra & Matrix Math

```python
u = np.array([1, 2, 3])
v = np.array([4, 5, 6])

# Dot product & Vector Norms
np.dot(u, v)            # 1*4 + 2*5 + 3*6 = 32
u @ v                   # Matrix multiplication operator (Python 3.5+)
np.linalg.norm(u)       # Euclidean length ||u|| = sqrt(1^2 + 2^2 + 3^2)

# Matrix Operations
A = np.array([[1, 2], [3, 4]])
B = np.array([[2, 0], [1, 2]])
C = A @ B               # Matrix product

np.linalg.inv(A)        # Matrix inverse
np.linalg.det(A)        # Determinant
np.linalg.eig(A)        # Eigenvalues and eigenvectors
```

---

## 8. Broadcasting Rules

Broadcasting allows arithmetic operations between arrays of different shapes without copying data.

Two dimensions are compatible when:
1. They are equal, OR
2. One of them is 1.

```python
# Example:
A = np.ones((3, 1))     # Shape: (3, 1)
B = np.ones((1, 4))     # Shape: (1, 4)
C = A + B               # Result Shape: (3, 4)
```

---

## 9. File Input & Output (I/O)

```python
# Binary format (.npy, .npz) - Fast & preserves exact data types
np.save("my_array.npy", arr)
loaded = np.load("my_array.npy")

# Multiple arrays compressed
np.savez_compressed("archive.npz", train=arr1, test=arr2)
data = np.load("archive.npz")
train_data = data["train"]

# Text / CSV format
np.savetxt("data.csv", arr, delimiter=",", fmt="%.2f", header="col1,col2")
csv_data = np.loadtxt("data.csv", delimiter=",", skiprows=1)
```
