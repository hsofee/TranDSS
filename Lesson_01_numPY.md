# เอกสารประกอบการสอน NumPy
## สำหรับนักศึกษาปริญญาตรี หลักสูตรคอมพิวเตอร์ธุรกิจและเทคโนโลยีดิจิทัล
## อ.โซฟีร์ หะยียูโซ๊ะ

---

## 📚 สารบัญ
1. [บทนำ NumPy](#บทนำ-numpy)
2. [การติดตั้งและการ Import](#การติดตั้งและการ-import)
3. [NumPy Array พื้นฐาน](#numpy-array-พื้นฐาน)
4. [การสร้าง Array](#การสร้าง-array)
5. [Array Indexing และ Slicing](#array-indexing-และ-slicing)
6. [การดำเนินการทางคณิตศาสตร์](#การดำเนินการทางคณิตศาสตร์)
7. [Array Manipulation](#array-manipulation)
8. [Broadcasting](#broadcasting)
9. [ฟังก์ชันสำคัญ](#ฟังก์ชันสำคัญ)
10. [Linear Algebra](#linear-algebra)
11. [Random Numbers](#random-numbers)
12. [File I/O](#file-io)
13. [Performance และ Memory](#performance-และ-memory)
14. [แบบฝึกหัด](#แบบฝึกหัด)
15. [โครงงานปฏิบัติ](#โครงงานปฏิบัติ)

---

## บทนำ NumPy

### NumPy คืออะไร?
**NumPy** (Numerical Python) เป็น library พื้นฐานสำหรับการคำนวณเชิงวิทยาศาสตร์ใน Python ที่มีความสำคัญอย่างยิ่งในด้าน Data Science, Machine Learning และ Scientific Computing

### ทำไมต้องใช้ NumPy?

#### เปรียบเทียบ Python List vs NumPy Array

```python
# Python List - ช้า
python_list = [1, 2, 3, 4, 5]
result = [x * 2 for x in python_list]  # ต้องใช้ loop

# NumPy Array - เร็ว
import numpy as np
numpy_array = np.array([1, 2, 3, 4, 5])
result = numpy_array * 2  # Vectorized operation
```

### ข้อดีของ NumPy
- **Performance**: เร็วกว่า Python List ถึง 50-100 เท่า
- **Memory Efficient**: ใช้หน่วยความจำน้อยกว่า
- **Vectorization**: สามารถดำเนินการกับ array ทั้งหมดพร้อมกัน
- **Broadcasting**: การคำนวณระหว่าง array ขนาดต่างกัน
- **Integration**: ทำงานร่วมกับ library อื่นได้ดี (Pandas, Matplotlib, Scikit-learn)

### สถิติการใช้งาน
- ใช้ในงาน Data Science มากกว่า 95%
- Base library ของ Pandas, Scikit-learn, TensorFlow
- ประมาณ 15 ล้าน downloads ต่อเดือน

---

## การติดตั้งและการ Import

### การติดตั้ง
```bash
# ผ่าน pip
pip install numpy

# ผ่าน conda
conda install numpy

# ตรวจสอบ version
python -c "import numpy; print(numpy.__version__)"
```

### การ Import
```python
# Standard import
import numpy as np

# ตรวจสอบ version
print(f"NumPy version: {np.__version__}")

# Import เฉพาะฟังก์ชันที่ต้องการ
from numpy import array, zeros, ones
```

---

## NumPy Array พื้นฐาน

### ndarray คืออะไร?
**ndarray** (N-dimensional array) เป็นโครงสร้างข้อมูลหลักของ NumPy ที่เก็บข้อมูลแบบ homogeneous (ชนิดข้อมูลเดียวกัน)

### คุณสมบัติของ ndarray

```python
import numpy as np

# สร้าง array
arr = np.array([[1, 2, 3], [4, 5, 6]])

# คุณสมบัติสำคัญ
print(f"Shape: {arr.shape}")        # (2, 3)
print(f"Dimensions: {arr.ndim}")    # 2
print(f"Size: {arr.size}")          # 6
print(f"Data type: {arr.dtype}")    # int64
print(f"Item size: {arr.itemsize}") # 8 bytes
```

### Data Types ใน NumPy

```python
# Integer types
int8_arr = np.array([1, 2, 3], dtype=np.int8)     # 8-bit integer
int32_arr = np.array([1, 2, 3], dtype=np.int32)   # 32-bit integer
int64_arr = np.array([1, 2, 3], dtype=np.int64)   # 64-bit integer

# Float types
float32_arr = np.array([1.0, 2.0, 3.0], dtype=np.float32)
float64_arr = np.array([1.0, 2.0, 3.0], dtype=np.float64)

# Boolean type
bool_arr = np.array([True, False, True], dtype=bool)

# String type
str_arr = np.array(['a', 'b', 'c'], dtype='U1')

# แปลงชนิดข้อมูล
arr_int = np.array([1.1, 2.2, 3.3])
arr_converted = arr_int.astype(int)
print(arr_converted)  # [1 2 3]
```

---

## การสร้าง Array

### วิธีการสร้าง Array

#### 1. จาก Python List/Tuple
```python
# 1D Array
arr_1d = np.array([1, 2, 3, 4, 5])

# 2D Array
arr_2d = np.array([[1, 2, 3], [4, 5, 6]])

# 3D Array
arr_3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
```

#### 2. Built-in Functions
```python
# Zeros
zeros_arr = np.zeros((3, 4))           # Array ของ 0
zeros_int = np.zeros((2, 3), dtype=int) # ระบุ dtype

# Ones
ones_arr = np.ones((2, 3))             # Array ของ 1

# Empty
empty_arr = np.empty((2, 2))           # Array ว่าง (ค่า random)

# Full
full_arr = np.full((2, 3), 7)          # Array เต็มด้วยค่า 7

# Identity matrix
identity = np.eye(3)                   # Identity matrix 3x3

# Range arrays
range_arr = np.arange(0, 10, 2)        # [0 2 4 6 8]
linspace_arr = np.linspace(0, 1, 5)    # [0.   0.25 0.5  0.75 1.  ]

# Random arrays
random_arr = np.random.random((2, 3))  # Random floats [0,1)
randint_arr = np.random.randint(1, 10, size=(3, 3))  # Random integers
```

#### 3. การสร้างจาก Pattern
```python
# Diagonal array
diag_arr = np.diag([1, 2, 3, 4])

# Array จาก function
def my_func(i, j):
    return i + j

fromfunction_arr = np.fromfunction(my_func, (3, 3))
```

---

## Array Indexing และ Slicing

### 1D Array Indexing
```python
arr = np.array([10, 20, 30, 40, 50])

# Basic indexing
print(arr[0])     # 10 (first element)
print(arr[-1])    # 50 (last element)
print(arr[1:4])   # [20 30 40] (slicing)
print(arr[::2])   # [10 30 50] (step=2)
print(arr[::-1])  # [50 40 30 20 10] (reverse)
```

### 2D Array Indexing
```python
arr_2d = np.array([[1, 2, 3], 
                   [4, 5, 6], 
                   [7, 8, 9]])

# Basic indexing
print(arr_2d[0, 1])      # 2 (row 0, column 1)
print(arr_2d[1, :])      # [4 5 6] (entire row 1)
print(arr_2d[:, 2])      # [3 6 9] (entire column 2)
print(arr_2d[0:2, 1:3])  # [[2 3], [5 6]] (subarray)

# Negative indexing
print(arr_2d[-1, -1])    # 9 (last element)
```

### Boolean Indexing
```python
arr = np.array([1, 2, 3, 4, 5, 6])

# Boolean mask
mask = arr > 3
print(mask)              # [False False False True True True]
print(arr[mask])         # [4 5 6]

# Direct boolean indexing
print(arr[arr > 3])      # [4 5 6]
print(arr[(arr > 2) & (arr < 5)])  # [3 4] (multiple conditions)
```

### Fancy Indexing
```python
arr = np.array([10, 20, 30, 40, 50])

# Index array
indices = [0, 2, 4]
print(arr[indices])      # [10 30 50]

# 2D fancy indexing
arr_2d = np.array([[1, 2], [3, 4], [5, 6]])
print(arr_2d[[0, 2], [1, 0]])  # [2 5] (elements at (0,1) and (2,0))
```

---

## การดำเนินการทางคณิตศาสตร์

### Arithmetic Operations
```python
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([5, 6, 7, 8])

# Basic operations
print(arr1 + arr2)       # [ 6  8 10 12]
print(arr1 - arr2)       # [-4 -4 -4 -4]
print(arr1 * arr2)       # [ 5 12 21 32]
print(arr1 / arr2)       # [0.2 0.33 0.43 0.5]
print(arr1 ** 2)         # [ 1  4  9 16]
print(arr1 % 2)          # [1 0 1 0]

# กับ scalar
print(arr1 + 10)         # [11 12 13 14]
print(arr1 * 3)          # [ 3  6  9 12]
```

### Universal Functions (ufuncs)
```python
arr = np.array([0, np.pi/6, np.pi/4, np.pi/3, np.pi/2])

# Trigonometric functions
print(np.sin(arr))
print(np.cos(arr))
print(np.tan(arr))

# Exponential and logarithmic
arr_pos = np.array([1, 2, 3, 4, 5])
print(np.exp(arr_pos))        # e^x
print(np.log(arr_pos))        # natural log
print(np.log10(arr_pos))      # log base 10
print(np.sqrt(arr_pos))       # square root

# Other useful functions
arr_mixed = np.array([-2, -1, 0, 1, 2])
print(np.abs(arr_mixed))      # absolute value
print(np.sign(arr_mixed))     # sign function
print(np.round(np.array([1.2, 1.7, 2.3]), 0))  # rounding
```

### Comparison Operations
```python
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([1, 3, 2, 4])

print(arr1 == arr2)      # [ True False False  True]
print(arr1 > arr2)       # [False False  True False]
print(arr1 < 3)          # [ True  True False False]

# Logical operations
print(np.logical_and(arr1 > 1, arr1 < 4))  # [False  True  True False]
print(np.logical_or(arr1 == 1, arr1 == 4)) # [ True False False  True]
print(np.logical_not(arr1 > 2))             # [ True  True False False]
```

---

## Array Manipulation

### เปลี่ยนรูปร่าง (Reshaping)
```python
arr = np.arange(12)
print(arr)                           # [ 0  1  2  3  4  5  6  7  8  9 10 11]

# Reshape
arr_2d = arr.reshape(3, 4)
print(arr_2d)
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]

# Reshape กับ -1 (automatic calculation)
arr_auto = arr.reshape(4, -1)        # รูปร่าง (4, 3)
arr_flat = arr_2d.reshape(-1)        # Flatten to 1D

# Transpose
arr_t = arr_2d.T                     # หรือ arr_2d.transpose()
print(arr_t.shape)                   # (4, 3)
```

### การรวม Array (Concatenation)
```python
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])

# Concatenate along axis
concat_0 = np.concatenate([arr1, arr2], axis=0)  # รวมตามแนวตั้ง
print(concat_0)
# [[1 2]
#  [3 4]
#  [5 6]
#  [7 8]]

concat_1 = np.concatenate([arr1, arr2], axis=1)  # รวมตามแนวนอน
print(concat_1)
# [[1 2 5 6]
#  [3 4 7 8]]

# Stack functions
vstack_arr = np.vstack([arr1, arr2])    # เหมือน axis=0
hstack_arr = np.hstack([arr1, arr2])    # เหมือน axis=1
```

### การแยก Array (Splitting)
```python
arr = np.arange(12).reshape(3, 4)

# Split along axis
split_0 = np.split(arr, 3, axis=0)      # แยกเป็น 3 ส่วนตามแนวตั้ง
split_1 = np.split(arr, 2, axis=1)      # แยกเป็น 2 ส่วนตามแนวนอน

# Vertical and horizontal split
vsplit_arr = np.vsplit(arr, 3)          # แยกตามแนวตั้ง
hsplit_arr = np.hsplit(arr, 2)          # แยกตามแนวนอน
```

### การเพิ่ม/ลบ elements
```python
arr = np.array([1, 2, 3, 4, 5])

# Append
new_arr = np.append(arr, [6, 7])
print(new_arr)                          # [1 2 3 4 5 6 7]

# Insert
inserted = np.insert(arr, 2, [10, 11])  # แทรกที่ index 2
print(inserted)                         # [ 1  2 10 11  3  4  5]

# Delete
deleted = np.delete(arr, [1, 3])        # ลบ index 1 และ 3
print(deleted)                          # [1 3 5]
```

---

## Broadcasting

Broadcasting เป็นความสามารถของ NumPy ในการดำเนินการระหว่าง arrays ที่มีขนาดต่างกัน

### กฎของ Broadcasting
1. Arrays จะถูกจัดแนว (align) จากขวาไปซ้าย
2. ถ้า dimension ไม่เท่ากัน จะเติม 1 ทางซ้าย
3. Arrays จะ compatible ถ้า dimension แต่ละอันเท่ากันหรือเป็น 1


### Broadcasing
ข้อแตกต่างระหว่าง Numpy Array กับ List คือ Numpy Array สามารถ assign ค่าพร้อม ๆ กัน ครั้งละหลาย ๆ องค์ประกอบได้ ตัวอย่างเช่น การตั้งค่าโดยใช้ช่วงของ index


```python
arr[0:5]=100
arr
```




    array([100, 100, 100, 100, 100,   5,   6,   7,   8,   9,  10])



การ reset ค่า array ใหม่


```python
arr = np.arange(0,11)
arr
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])



สร้าง Array ใหม่ ด้วยการ Slices


```python
slice_of_arr = arr[0:6]
slice_of_arr
```




    array([0, 1, 2, 3, 4, 5])


### ตัวอย่าง Broadcasting
```python
# ตัวอย่างที่ 1: Scalar กับ Array
arr = np.array([1, 2, 3, 4])
result = arr + 10                # Broadcasting scalar
print(result)                    # [11 12 13 14]

# ตัวอย่างที่ 2: 1D กับ 2D
arr_2d = np.array([[1, 2, 3], 
                   [4, 5, 6]])
arr_1d = np.array([10, 20, 30])

result = arr_2d + arr_1d         # (2,3) + (3,) = (2,3)
print(result)
# [[11 22 33]
#  [14 25 36]]

# ตัวอย่างที่ 3: Column vector กับ Row vector
col_vector = np.array([[1], [2], [3]])      # (3,1)
row_vector = np.array([10, 20])             # (2,)

result = col_vector + row_vector            # (3,1) + (2,) = (3,2)
print(result)
# [[11 21]
#  [12 22]
#  [13 23]]
```

### การใช้ Broadcasting ใน Real-world
```python
# Normalize data (subtract mean, divide by std)
data = np.random.randn(100, 5)              # 100 samples, 5 features
mean = np.mean(data, axis=0)                # Mean of each feature
std = np.std(data, axis=0)                  # Std of each feature
normalized = (data - mean) / std            # Broadcasting!

# Distance calculation
points = np.array([[1, 2], [3, 4], [5, 6]])
center = np.array([0, 0])
distances = np.sqrt(np.sum((points - center)**2, axis=1))
```

---

## ฟังก์ชันสำคัญ

### Aggregation Functions
```python
arr = np.array([[1, 2, 3], 
                [4, 5, 6], 
                [7, 8, 9]])

# Basic statistics
print(np.sum(arr))              # 45
print(np.mean(arr))             # 5.0
print(np.std(arr))              # 2.58
print(np.var(arr))              # 6.67
print(np.min(arr))              # 1
print(np.max(arr))              # 9

# Along axis
print(np.sum(arr, axis=0))      # [12 15 18] (sum columns)
print(np.sum(arr, axis=1))      # [ 6 15 24] (sum rows)
print(np.mean(arr, axis=0))     # [4. 5. 6.] (mean columns)

# Percentiles
print(np.median(arr))           # 5.0
print(np.percentile(arr, 25))   # 3.0
print(np.percentile(arr, 75))   # 7.0
```

### Sorting Functions
```python
arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])

# Sort
sorted_arr = np.sort(arr)
print(sorted_arr)               # [1 1 2 3 4 5 6 9]

# Argsort (indices of sorted elements)
indices = np.argsort(arr)
print(indices)                  # [1 3 6 0 2 4 7 5]
print(arr[indices])             # [1 1 2 3 4 5 6 9]

# 2D sorting
arr_2d = np.array([[3, 2, 1], [6, 5, 4]])
print(np.sort(arr_2d, axis=1))  # Sort each row
# [[1 2 3]
#  [4 5 6]]
```

### Unique and Set Operations
```python
arr = np.array([1, 2, 2, 3, 3, 3, 4])

# Unique values
unique_vals = np.unique(arr)
print(unique_vals)              # [1 2 3 4]

# Unique with counts
unique_vals, counts = np.unique(arr, return_counts=True)
print(unique_vals)              # [1 2 3 4]
print(counts)                   # [1 2 3 1]

# Set operations
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([3, 4, 5, 6])

print(np.intersect1d(arr1, arr2))  # [3 4] (intersection)
print(np.union1d(arr1, arr2))      # [1 2 3 4 5 6] (union)
print(np.setdiff1d(arr1, arr2))    # [1 2] (difference)
```

### Conditional Functions
```python
arr = np.array([-2, -1, 0, 1, 2])

# Where function
result = np.where(arr > 0, arr, 0)  # ถ้า > 0 ใช้ค่าเดิม ไม่งั้นใช้ 0
print(result)                       # [0 0 0 1 2]

# Select function
conditions = [arr < -1, arr > 1]
choices = ['negative', 'positive']
result = np.select(conditions, choices, default='zero')
print(result)                       # ['negative' 'zero' 'zero' 'zero' 'positive']

# Any and All
bool_arr = np.array([True, False, True])
print(np.any(bool_arr))            # True
print(np.all(bool_arr))            # False
```

---



### Matrix Properties
```python
A = np.array([[1, 2], [3, 4]])

# Determinant
det_A = np.linalg.det(A)
print(f"Determinant: {det_A}")   # -2.0

# Inverse
inv_A = np.linalg.inv(A)
print(f"Inverse:\n{inv_A}")

# Eigenvalues and eigenvectors
eigenvals, eigenvecs = np.linalg.eig(A)
print(f"Eigenvalues: {eigenvals}")
print(f"Eigenvectors:\n{eigenvecs}")

# Matrix rank
rank_A = np.linalg.matrix_rank(A)
print(f"Rank: {rank_A}")         # 2
```

### Solving Linear Systems
```python
# Solve Ax = b
A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])

x = np.linalg.solve(A, b)
print(f"Solution: {x}")          # [2. 3.]

# Verify
print(f"Verification: {A @ x}")  # [9. 8.]
```

### Decompositions
```python
A = np.array([[4, 2], [1, 3]])

# QR decomposition
Q, R = np.linalg.qr(A)
print(f"Q:\n{Q}")
print(f"R:\n{R}")

# SVD (Singular Value Decomposition)
U, s, Vt = np.linalg.svd(A)
print(f"U:\n{U}")
print(f"Singular values: {s}")
print(f"Vt:\n{Vt}")
```

---

## Random Numbers

### Random Number Generation
```python
# Set seed for reproducibility
np.random.seed(42)

# Basic random numbers
random_floats = np.random.random(5)        # [0, 1)
random_ints = np.random.randint(1, 10, 5)  # integers [1, 10)

# Random from distributions
normal_dist = np.random.normal(0, 1, 100)      # Normal(μ=0, σ=1)
uniform_dist = np.random.uniform(-1, 1, 50)    # Uniform[-1, 1)
exponential_dist = np.random.exponential(2, 30) # Exponential(λ=2)

# Random choice
arr = np.array([1, 2, 3, 4, 5])
choices = np.random.choice(arr, size=10, replace=True)

# Shuffle
data = np.arange(10)
np.random.shuffle(data)
print(data)
```

### Random Sampling
```python
# Random sampling without replacement
population = np.arange(100)
sample = np.random.choice(population, size=10, replace=False)

# Probability-based sampling
values = [1, 2, 3, 4]
probabilities = [0.4, 0.3, 0.2, 0.1]
samples = np.random.choice(values, size=1000, p=probabilities)
```

---

## File I/O

### การบันทึกและโหลด Array
```python
# Save and load single array
arr = np.array([1, 2, 3, 4, 5])

# Save as .npy file
np.save('my_array.npy', arr)

# Load .npy file
loaded_arr = np.load('my_array.npy')

# Save multiple arrays
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
np.savez('multiple_arrays.npz', first=arr1, second=arr2)

# Load multiple arrays
data = np.load('multiple_arrays.npz')
print(data['first'])
print(data['second'])
```

### Text Files
```python
# Save to text file
arr = np.array([[1, 2, 3], [4, 5, 6]])
np.savetxt('data.txt', arr, delimiter=',', fmt='%d')

# Load from text file
loaded_data = np.loadtxt('data.txt', delimiter=',')

# Load CSV with headers
data = np.genfromtxt('data.csv', delimiter=',', names=True, dtype=None)
```

---

## Performance และ Memory

### Memory Layout
```python
# Row-major (C-style) vs Column-major (Fortran-style)
arr_c = np.array([[1, 2, 3], [4, 5, 6]], order='C')
arr_f = np.array([[1, 2, 3], [4, 5, 6]], order='F')

print(f"C-order flags: {arr_c.flags}")
print(f"F-order flags: {arr_f.flags}")
```

### Views vs Copies
```python
arr = np.array([1, 2, 3, 4, 5])

# View (shares memory)
view_arr = arr[1:4]
view_arr[0] = 100
print(arr)                    # [  1 100   3   4   5] - original changed!

# Copy (separate memory)
copy_arr = arr[1:4].copy()
copy_arr[0] = 200
print(arr)                    # [  1 100   3   4   5] - original unchanged
```

### Performance Tips
```python
import time

# ใช้ vectorized operations แทน loops
n = 1000000
arr1 = np.random.random(n)
arr2 = np.random.random(n)

# Slow: Python loop
start = time.time()
result_slow = []
for i in range(n):
    result_slow.append(arr1[i] + arr2[i])
time_slow = time.time() - start

# Fast: Vectorized
start = time.time()
result_fast = arr1 + arr2
time_fast = time.time() - start

print(f"Loop time: {time_slow:.4f}s")
print(f"Vectorized time: {time_fast:.4f}s")
print(f"Speedup: {time_slow/time_fast:.1f}x")
```

---

## แบบฝึกหัด

### แบบฝึกหัดที่ 1: พื้นฐาน Array (10 คะแนน)

#### ข้อ 1.1 (2 คะแนน)
สร้าง NumPy array ต่อไปนี้:
```python
# TODO: เขียนโค้ดสร้าง array
# a) 1D array ที่มีค่า [0, 2, 4, 6, 8, 10]
# b) 2D array รูปแบบ:
#    [[1, 0, 0],
#     [0, 1, 0], 
#     [0, 0, 1]]
# c) 3x4 array ที่เต็มไปด้วยเลข 7


#### ข้อ 1.2 (3 คะแนน)
จากการสำรวจ array ต่อไปนี้:
```python
mystery_array = np.random.randint(1, 100, size=(5, 6))
```
เขียนโค้ดหาข้อมูลต่อไปนี้:
- Shape, dimensions, size, และ data type
- ค่าต่ำสุด, สูงสุด, ค่าเฉลี่ย
- ค่าเฉลี่ยของแต่ละแถวและแต่ละคอลัมน์

#### ข้อ 1.3 (5 คะแนน)
เขียนโค้ดสร้าง checkerboard pattern (รูปแบบหมากรุก) ขนาด 8x8 โดยใช้ 0 และ 1



### แบบฝึกหัดที่ 2: Indexing และ Slicing (15 คะแนน)

#### ข้อ 2.1 (5 คะแนน)
จาก array ต่อไปนี้:
```python
data = np.arange(1, 26).reshape(5, 5)
```
เขียนโค้ดดึงข้อมูลต่อไปนี้:
- แถวที่ 2 และ 4
- คอลัมน์ที่ 1, 3, 5
- subarray ตรงกลาง 3x3
- ทุก element ที่มีค่ามากกว่า 15

#### ข้อ 2.2 (10 คะแนน)
เขียนฟังก์ชันที่รับ 2D array และส่งกลับ:
- Border elements (elements ที่อยู่ขอบ)
- Corner elements (elements ที่อยู่มุม)
- Center region (กำจัดขอบออก 1 ชั้น)

### แบบฝึกหัดที่ 3: การคำนวณ (20 คะแนน)

#### ข้อ 3.1 (10 คะแนน)
เขียนโค้ดคำนวณ:
1. Euclidean distance ระหว่างจุด 2 จุดใน n-dimensional space
2. Cosine similarity ระหว่าง vector 2 ตัว
3. Standard score (z-score) ของ array

#### ข้อ 3.2 (10 คะแนน)
จำลอง Monte Carlo method เพื่อหาค่า π:
1. สุ่มจุด N จุดใน square [-1, 1] x [-1, 1]
2. นับจุดที่อยู่ใน unit circle
3. ประมาณค่า π = 4 × (จุดใน circle / จุดทั้งหมด)

### แบบฝึกหัดที่ 4: Array Manipulation (15 คะแนน)

#### ข้อ 4.1 (8 คะแนน)
เขียนฟังก์ชันที่:
1. หมุน 2D array 90 องศาตามเข็มนาฬิกา
2. Flip array ตามแนวนอนและแนวตั้ง
3. สร้าง spiral array (เลขเรียงแบบเกลียว)

#### ข้อ 4.2 (7 คะแนน)
จาก image data (2D array), เขียนฟังก์ชัน:
1. Crop ภาพตรงกลาง
2. Resize ภาพโดยการ sampling
3. Apply simple blur filter (3x3 averaging)

### แบบฝึกหัดที่ 5: Linear Algebra (20 คะแนน)

#### ข้อ 5.1 (10 คะแนน)
เขียนโค้ดแก้ระบบสมการเชิงเส้น:
```
3x + 2y - z = 1
2x - 2y + 4z = 0
-x + 0.5y - z = 0
```

และตรวจสอบคำตอบ

#### ข้อ 5.2 (10 คะแนน)
Implement Principal Component Analysis (PCA) algorithm:
1. Center the data (subtract mean)
2. Calculate covariance matrix
3. Find eigenvalues and eigenvectors
4. Transform data to principal components



### แบบฝึกหัดที่ 6: Performance และ Memory (10 คะแนน)

#### ข้อ 6.1 (5 คะแนน)
เปรียบเทียบ performance ของการคำนวณ:
1. Matrix multiplication ด้วย loop vs np.dot
2. Element-wise operations ด้วย loop vs vectorization
3. Sum calculation ด้วย loop vs np.sum

#### ข้อ 6.2 (5 คะแนน)
เขียนโค้ดวิเคราะห์ memory usage:
1. เปรียบเทียบขนาด memory ของ Python list vs NumPy array
2. ทดสอบ view vs copy behavior
3. วัด memory footprint ของ arrays ขนาดต่างๆ

### แบบฝึกหัดที่ 7: Practical Applications (10 คะแนน)

#### ข้อ 7.1 (5 คะแนน)
สร้าง data preprocessing pipeline:
```python
def preprocess_data(data):
    """
    Preprocess numerical data:
    1. Handle missing values (replace with mean)
    2. Remove outliers (beyond 3 standard deviations)
    3. Normalize to [0, 1] range
    4. Add polynomial features (degree 2)
    
    Parameters:
    data: np.array of shape (n_samples, n_features)
    
    Returns:
    processed_data: preprocessed data
    """
    # TODO: implement
    pass
```

#### ข้อ 7.2 (5 คะแนน)
สร้าง simple image filters:
1. Edge detection filter
2. Sharpening filter  
3. Gaussian blur

---

## โครงงานปฏิบัติ

### โครงงานที่ 1: Weather Data Analysis (25 คะแนน)

**เป้าหมาย**: วิเคราะห์ข้อมูลสภาพอากาศรายวันเป็นเวลา 1 ปี

**ข้อมูล**: สร้าง synthetic weather data หรือใช้ข้อมูลจริง
- Temperature (°C)
- Humidity (%)
- Pressure (hPa)
- Rainfall (mm)

**งานที่ต้องทำ**:
1. **Data Generation/Loading** (5 คะแนน)
   - สร้างข้อมูลสุ่มแบบ realistic หรือโหลดข้อมูลจริง
   - จำลอง seasonal patterns และ noise

2. **Data Analysis** (10 คะแนน)
   - หาค่าสถิติพื้นฐาน (mean, std, min, max) ของแต่ละเดือน
   - หา correlation ระหว่างตัวแปรต่างๆ
   - ตรวจหา outliers และจัดการ

3. **Trend Analysis** (5 คะแนน)
   - คำนวณ moving average (7-day, 30-day)
   - หา seasonal trends
   - ตรวจสอบ long-term trends

4. **Reporting** (5 คะแนน)
   - สร้างรายงานสรุปผลการวิเคราะห์
   - แสดงผลด้วยตัวเลขและ basic visualization

**Template Code**:
```python
import numpy as np
import matplotlib.pyplot as plt
from datetime import datetime, timedelta

def generate_weather_data(days=365):
    """Generate synthetic weather data"""
    # TODO: implement realistic weather simulation
    pass

def analyze_monthly_stats(data, dates):
    """Analyze monthly statistics"""
    # TODO: implement monthly analysis
    pass

def detect_outliers(data, threshold=3):
    """Detect outliers using z-score method"""
    # TODO: implement outlier detection
    pass

def calculate_moving_average(data, window):
    """Calculate moving average"""
    # TODO: implement moving average
    pass

# Main analysis
if __name__ == "__main__":
    # Generate or load data
    weather_data = generate_weather_data()
    
    # Perform analysis
    monthly_stats = analyze_monthly_stats(weather_data)
    outliers = detect_outliers(weather_data)
    trends = calculate_moving_average(weather_data, 30)
    
    # Generate report
    print("Weather Data Analysis Report")
    print("=" * 40)
    # TODO: implement reporting
```

### โครงงานที่ 2: Simple Recommendation System (30 คะแนน)

**เป้าหมาย**: สร้างระบบแนะนำสินค้าแบบง่ายโดยใช้ collaborative filtering

**ข้อมูล**: User-Item rating matrix
- Users: 1000 คน
- Items: 500 รายการ  
- Ratings: 1-5 (sparse matrix ~5% filled)

**งานที่ต้องทำ**:
1. **Data Generation** (5 คะแนน)
   - สร้าง user-item rating matrix แบบ sparse
   - จำลอง user preferences และ item characteristics

2. **Similarity Calculation** (10 คะแนน)
   - คำนวณ user-user similarity (cosine similarity)
   - คำนวณ item-item similarity
   - Handle missing values ใน sparse matrix

3. **Recommendation Algorithm** (10 คะแนน)
   - Implement user-based collaborative filtering
   - Implement item-based collaborative filtering
   - Predict ratings สำหรับ unrated items

4. **Evaluation** (5 คะแนน)
   - Split data เป็น train/test
   - คำนวณ RMSE (Root Mean Square Error)
   - เปรียบเทียบ performance ของ algorithms ต่างๆ

**Template Code**:
```python
import numpy as np
from scipy.sparse import random
from sklearn.metrics.pairwise import cosine_similarity

class RecommendationSystem:
    def __init__(self, n_users=1000, n_items=500, density=0.05):
        self.n_users = n_users
        self.n_items = n_items
        self.density = density
        self.ratings = None
        
    def generate_data(self):
        """Generate synthetic user-item rating matrix"""
        # TODO: implement data generation
        pass
    
    def calculate_user_similarity(self):
        """Calculate user-user similarity matrix"""
        # TODO: implement user similarity calculation
        pass
    
    def calculate_item_similarity(self):
        """Calculate item-item similarity matrix"""
        # TODO: implement item similarity calculation
        pass
    
    def predict_user_based(self, user_id, item_id, k=50):
        """Predict rating using user-based collaborative filtering"""
        # TODO: implement user-based prediction
        pass
    
    def predict_item_based(self, user_id, item_id, k=50):
        """Predict rating using item-based collaborative filtering"""
        # TODO: implement item-based prediction
        pass
    
    def recommend_items(self, user_id, n_recommendations=10):
        """Recommend top N items for a user"""
        # TODO: implement recommendation generation
        pass
    
    def evaluate(self, test_data):
        """Evaluate recommendation system using RMSE"""
        # TODO: implement evaluation
        pass

# Example usage
if __name__ == "__main__":
    # Initialize system
    rec_sys = RecommendationSystem()
    rec_sys.generate_data()
    
    # Train model
    rec_sys.calculate_user_similarity()
    rec_sys.calculate_item_similarity()
    
    # Make recommendations
    user_id = 0
    recommendations = rec_sys.recommend_items(user_id)
    
    # Evaluate system
    rmse = rec_sys.evaluate(test_data)
    print(f"System RMSE: {rmse:.4f}")
```

### โครงงานที่ 3: Image Processing Pipeline (35 คะแนน)

**เป้าหมาย**: สร้าง image processing pipeline สำหรับการประมวลผลภาพพื้นฐาน

**งานที่ต้องทำ**:
1. **Image I/O และ Basic Operations** (10 คะแนน)
   - สร้างฟังก์ชันโหลดภาพเป็น NumPy array
   - Implement basic operations: crop, resize, rotate
   - Color space conversion (RGB to Grayscale)

2. **Filters และ Enhancement** (15 คะแนน)
   - Implement convolution operation
   - สร้าง filters: blur, sharpen, edge detection
   - Histogram equalization สำหรับ contrast enhancement
   - Noise reduction filters

3. **Feature Extraction** (10 คะแนน)
   - Calculate image statistics (mean, std, histogram)
   - Extract simple features: edges, corners
   - Implement simple template matching

**Template Code**:
```python
import numpy as np

class ImageProcessor:
    def __init__(self):
        pass
    
    def load_image(self, filename):
        """Load image as NumPy array"""
        # For this exercise, generate synthetic image
        # In real application, use PIL or opencv
        return np.random.randint(0, 256, (100, 100, 3), dtype=np.uint8)
    
    def rgb_to_grayscale(self, image):
        """Convert RGB image to grayscale"""
        # TODO: implement RGB to grayscale conversion
        # Formula: 0.299*R + 0.587*G + 0.114*B
        pass
    
    def crop_image(self, image, x, y, width, height):
        """Crop image to specified region"""
        # TODO: implement image cropping
        pass
    
    def resize_image(self, image, new_width, new_height):
        """Resize image using nearest neighbor interpolation"""
        # TODO: implement image resizing
        pass
    
    def apply_convolution(self, image, kernel):
        """Apply convolution filter to image"""
        # TODO: implement 2D convolution
        pass
    
    def create_blur_kernel(self, size):
        """Create averaging (blur) kernel"""
        # TODO: create blur kernel
        pass
    
    def create_edge_kernel(self):
        """Create edge detection kernel (e.g., Sobel)"""
        # TODO: create edge detection kernel
        pass
    
    def histogram_equalization(self, image):
        """Apply histogram equalization"""
        # TODO: implement histogram equalization
        pass
    
    def calculate_histogram(self, image, bins=256):
        """Calculate image histogram"""
        # TODO: implement histogram calculation
        pass
    
    def template_matching(self, image, template):
        """Find template in image using normalized cross-correlation"""
        # TODO: implement template matching
        pass

# Example pipeline
if __name__ == "__main__":
    processor = ImageProcessor()
    
    # Load and process image
    image = processor.load_image("sample.jpg")
    gray_image = processor.rgb_to_grayscale(image)
    
    # Apply filters
    blur_kernel = processor.create_blur_kernel(5)
    blurred = processor.apply_convolution(gray_image, blur_kernel)
    
    edge_kernel = processor.create_edge_kernel()
    edges = processor.apply_convolution(gray_image, edge_kernel)
    
    # Enhancement
    enhanced = processor.histogram_equalization(gray_image)
    
    # Analysis
    histogram = processor.calculate_histogram(gray_image)
    
    print("Image processing pipeline completed!")
    print(f"Original image shape: {image.shape}")
    print(f"Histogram range: {np.min(histogram)} to {np.max(histogram)}")
```

---

## แนวทางการให้คะแนน

### เกณฑ์การประเมิน

#### แบบฝึกหัด (70%)
- **Correctness (40%)**: โค้ดทำงานถูกต้องและให้ผลลัพธ์ที่ถูกต้อง
- **Code Quality (20%)**: โค้ดเขียนได้ดี มี comments เหมาะสม
- **Efficiency (10%)**: ใช้ NumPy operations อย่างมีประสิทธิภาพ

#### โครงงาน (30%)
- **Implementation (50%)**: implement algorithm ถูกต้องครบถ้วน
- **Analysis (25%)**: วิเคราะห์ผลลัพธ์และอธิบายได้ดี
- **Documentation (15%)**: มี documentation และ comments ดี
- **Innovation (10%)**: มีการปรับปรุงหรือเพิ่มเติมฟีเจอร์

### คะแนนเต็ม: 100 คะแนน
- แบบฝึกหัดที่ 1-7: 70 คะแนน
- โครงงานเลือก 1 จาก 3: 30 คะแนน

---

## ทรัพยากรเพิ่มเติม

### เอกสารอ้างอิง
1. **NumPy Official Documentation**: https://numpy.org/doc/
2. **NumPy User Guide**: https://numpy.org/doc/stable/user/
3. **NumPy API Reference**: https://numpy.org/doc/stable/reference/

### หนังสือแนะนำ
1. "Python for Data Analysis" โดย Wes McKinney
2. "Effective Python" โดย Brett Slatkin  
3. "High Performance Python" โดย Micha Gorelick

### Online Courses
1. Coursera: "Introduction to Data Science in Python"
2. edX: "MIT Introduction to Computer Science and Programming"
3. Udacity: "Data Science Nanodegree"

### Practice Platforms
1. **LeetCode**: Array และ Matrix problems
2. **HackerRank**: Python และ Data Science tracks
3. **Kaggle Learn**: Micro-courses ฟรี

---

## สรุป

NumPy เป็น foundation ที่สำคัญของ Data Science ecosystem ใน Python การเรียนรู้ NumPy อย่างถ่องแท้จะช่วยให้นักศึกษา:

1. **เข้าใจพื้นฐานการคำนวณเชิงวิทยาศาสตร์**
2. **เตรียมพร้อมสำหรับ libraries ขั้นสูง** (Pandas, Scikit-learn, TensorFlow)
3. **พัฒนาทักษะการเขียนโปรแกรมที่มีประสิทธิภาพ**
4. **สร้างพื้นฐานสำหรับ Machine Learning และ Data Science**

### จุดสำคัญที่ต้องจำ
- **Vectorization**: ใช้ array operations แทน loops
- **Broadcasting**: การคำนวณระหว่าง arrays ขนาดต่างกัน
- **Memory efficiency**: เข้าใจ views vs copies
- **Performance**: รู้เมื่อไหร่ควรใช้ NumPy vs Python built-ins

### การพัฒนาต่อ
หลังจากเรียน NumPy แล้ว แนะนำให้ศึกษาต่อใน:
1. **Pandas**: สำหรับการจัดการข้อมูลแบบ structured
2. **Matplotlib/Seaborn**: สำหรับการ visualization
3. **Scikit-learn**: สำหรับ Machine Learning
4. **TensorFlow/PyTorch**: สำหรับ Deep Learning

---

**Good luck กับการเรียนรู้ NumPy! 🚀**
