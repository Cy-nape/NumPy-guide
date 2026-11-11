# Frequently Asked Questions & Common Pitfalls

A collection of the most critical conceptual questions, debugging tips, and pitfalls encountered when working with NumPy.

---

### Q1: Why did modifying my sliced array change my original array? (View vs. Copy)

**Answer:**  
In NumPy, standard slicing (`arr[1:4]`) creates a **view** of the original memory buffer, NOT a new copy. Modifying elements in the view directly mutates the original array!

```python
original = np.array([10, 20, 30, 40])
slice_view = original[1:3]
slice_view[0] = 999

print(original)  # Output: [ 10 999  30  40 ] -> Original changed!
```

**How to avoid this:**  
If you want an independent copy, explicitly call `.copy()`:
```python
independent_copy = original[1:3].copy()
independent_copy[0] = 555
# original remains untouched
```

> **Rule of Thumb:**
> - Basic slicing (`arr[::2]`, `arr[1:5]`) returns a **view**.
> - Advanced / Fancy indexing (`arr[[0, 2]]`, boolean mask `arr[arr > 2]`) returns a **copy**.

---

### Q2: How do I intuitively understand `axis=0` vs. `axis=1`?

**Answer:**  
Think of `axis` as **the dimension that gets collapsed (summed/averaged away)**:

For a 2D array of shape `(rows, columns)`:
- `axis=0`: Collapses down the **rows** (moves vertically across each column). Result shape is `(columns,)`.
- `axis=1`: Collapses across the **columns** (moves horizontally along each row). Result shape is `(rows,)`.

```python
M = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(np.sum(M, axis=0))  # [1+4, 2+5, 3+6] -> [5, 7, 9] (per column total)
print(np.sum(M, axis=1))  # [1+2+3, 4+5+6] -> [6, 15]   (per row total)
```

---

### Q3: What is the difference between `*`, `np.dot()`, and `@`?

**Answer:**  
- `*` is **element-wise multiplication** (Hadamard product). Both operands must have matching shapes or broadcastable dimensions.
- `@` is the standard Python matrix multiplication operator (equivalent to `np.matmul()`).
- `np.dot()` performs the inner product for 1D vectors, and matrix multiplication for 2D arrays (with slightly different behavior for 3D+ tensors compared to `matmul`).

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[2, 0], [1, 2]])

# Element-wise:
print(A * B)
# [[ 2  0]
#  [ 3  8]]

# Matrix Multiplication:
print(A @ B)
# [[ 4  4]
#  [10  8]]
```

---

### Q4: Why is NumPy so much faster than native Python lists?

**Answer:**  
1. **Contiguous C Memory:** NumPy arrays store homogeneous data types in single, continuous blocks of memory. Python lists store pointers to scattered objects.
2. **Cache Locality:** Modern CPU caches can preload sequential memory blocks efficiently.
3. **No Dynamic Type Dispatch:** In a Python list, the interpreter must check the type of every element at runtime. In NumPy, the `dtype` is fixed, allowing compiled C/Fortran SIMD vector instructions to run without per-element checks.

---

### Q5: How does NumPy Broadcasting work, and how do I fix `ValueError: operands could not be broadcast together`?

**Answer:**  
Broadcasting matches dimensions starting from the **trailing (rightmost)** dimension and moves leftward.

Two dimensions are compatible if:
1. They are equal, OR
2. One of them is `1`.

If a dimension doesn't exist for one array, it is assumed to be `1`.

**Example:**
- Array A: `(5, 1, 4)`
- Array B: `   (3, 4)`
- Comparison:
  - Dim 3: 4 == 4 (OK)
  - Dim 2: 1 vs 3 (One is 1 -> OK, stretches to 3)
  - Dim 1: 5 vs None (Assumed 1 -> stretches to 5)
- Result shape: `(5, 3, 4)`

If dimensions mismatch without either being 1, e.g., shape `(3, 4)` and `(3,)`, use `np.newaxis` or `.reshape()` to align:
```python
A = np.ones((3, 4))
b = np.array([10, 20, 30])  # Shape (3,)

# b[:, np.newaxis] changes shape to (3, 1), allowing broadcast across 4 columns
result = A + b[:, np.newaxis]
```

---

### Q6: How do I handle missing values (`NaN`) in NumPy calculations?

**Answer:**  
Standard functions like `np.sum()` or `np.mean()` return `nan` if the array contains even a single `NaN`.

Use the **nan-safe** equivalents:
```python
data = np.array([10, np.nan, 20, 30])

print(np.mean(data))      # Returns: nan
print(np.nanmean(data))   # Returns: 20.0 (ignores NaNs)
print(np.nansum(data))    # Returns: 60.0

# Detecting & replacing NaNs
clean_data = np.nan_to_num(data, nan=0.0)
mask = ~np.isnan(data)
filtered_data = data[mask]
```

---

### Q7: `ravel()` vs. `flatten()` – which should I use?

- `ravel()`: Returns a **flattened view** if possible (fast, no memory duplication). Use this by default for performance.
- `flatten()`: Always allocates and returns an **independent copy**. Use this only if you explicitly need to modify the flattened array without affecting the original.
