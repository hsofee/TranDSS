![image-3.png](attachment:image-3.png)
# Python for Data Analysis (lab2)
## Numpy
Numpy คือ Linear Algebra Library ในภาษา Python ซึ่งเป็น Library ที่เป็น main building block สำหรับ library อื่น ๆ ที่มีการใช้งานในสาขา Data Science

### Installation
การ Install "numpy" สามารถทำได้หลายวิธี วิธีที่แสดงในที่นี้ ทำได้โดย พิมพ์คำส่งใดคำสั่งหนึ่งเหล่านี้ใน Command Line (Window) หรือ Terminal (Mac) แล้ว Enter
- conda install numpy (Window/Mac)
- pip install numpy (Window/Mac)
- python3.8 -m pip install numpy (for Mac M1)

### Using Numpy

#### Import Numpy
เริ่มใช้งาน Numpy ได้โดยการ import numpy เข้ามา โดยใช้คำสั่ง


```python
import numpy as np
```

### Numpy Arrays
Numpy Arrays เป็นการสร้าง Array ซึ่งจะถูกใช้งานมากที่สุดในคอร์สนี้ โดย Numpy Arrays จะถูกใช้งานในรูปของปริมาณเวคเตอร์ (Vectors) หรือ เมตริกซ์ (Matrices)
- เวคเตอร์ (Vectors) คือ Array 1 มิติ
- เมตริกซ์ (Matrices) คือ Array 2 มิติ

#### Creating Numpy Arrays
##### From a Python List
เราสามารถสร้าง Array ได้โดยตรงจากการแปลงรูปแบบจาก List


```python
my_list = [1,2,3]
my_list
```


```python
np.array(my_list)
```




    array([1, 2, 3])




```python
my_matrix = [[1,2,3],[4,5,6],[7,8,9]]
my_matrix
```




    [[1, 2, 3], [4, 5, 6], [7, 8, 9]]




```python
np.array(my_matrix)
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



#### Built-in Methods
มี Built-in Methods ใน numpy อยู่หลายแบบที่สามารถใช้ในการสร้าง Array

##### arange


```python
np.arange(0,10)
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
np.arange(0,100,3)
```




    array([ 0,  3,  6,  9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48,
           51, 54, 57, 60, 63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99])




```python

```

lab 1 : สร้าง array เก็บข้อมูล เลขคู่ <BR> สร้าง Array เก็บเลขคี่ 0,100


```python
np.arange(1,100,2)
```




    array([ 1,  3,  5,  7,  9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33,
           35, 37, 39, 41, 43, 45, 47, 49, 51, 53, 55, 57, 59, 61, 63, 65, 67,
           69, 71, 73, 75, 77, 79, 81, 83, 85, 87, 89, 91, 93, 95, 97, 99])



##### zeros and ones
สร้าง array ของ 0 และ 1


```python
np.zeros(3)
```




    array([0., 0., 0.])




```python
np.zeros((5,5))
```




    array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])




```python
np.ones(3)
```




    array([1., 1., 1.])




```python
np.ones((3,3))
```




    array([[1., 1., 1.],
           [1., 1., 1.],
           [1., 1., 1.]])



##### linspace
จะคืนค่ามาเป็น array ชุดของตัวเลขที่อยู่ระหว่างช่วงตัวเลขที่กำหนด (ระหว่าง start กับ end) เป็นจำนวนกี่ช่วง (number of interval) // เป็นการเลือกค่า

###### np.linspace(\<start\>, \<end\>, \<number on interval\>)


```python
np.linspace(0,10,5)
```




    array([ 0. ,  2.5,  5. ,  7.5, 10. ])




```python
np.linspace(0,10,50)
```




    array([ 0.        ,  0.20408163,  0.40816327,  0.6122449 ,  0.81632653,
            1.02040816,  1.2244898 ,  1.42857143,  1.63265306,  1.83673469,
            2.04081633,  2.24489796,  2.44897959,  2.65306122,  2.85714286,
            3.06122449,  3.26530612,  3.46938776,  3.67346939,  3.87755102,
            4.08163265,  4.28571429,  4.48979592,  4.69387755,  4.89795918,
            5.10204082,  5.30612245,  5.51020408,  5.71428571,  5.91836735,
            6.12244898,  6.32653061,  6.53061224,  6.73469388,  6.93877551,
            7.14285714,  7.34693878,  7.55102041,  7.75510204,  7.95918367,
            8.16326531,  8.36734694,  8.57142857,  8.7755102 ,  8.97959184,
            9.18367347,  9.3877551 ,  9.59183673,  9.79591837, 10.        ])



##### eye
สร้าง identity matrix


```python
np.eye(4)
```




    array([[1., 0., 0., 0.],
           [0., 1., 0., 0.],
           [0., 0., 1., 0.],
           [0., 0., 0., 1.]])



##### Random
ใน Numpy มีวิธีการสุ่มค่าตัวเลขเพื่อสร้างองค์ประกอบภายใน array อยู่หลายวิธีด้วยกัน

###### rand
เป็นการสร้าง array ตามขนาดที่ต้องการ โดยมีองค์ประกอบเป็นตัวเลขที่สุ่มออกมา จากกลุ่มตัวอย่างระหว่าง \[0,1)


```python
np.random.rand(2)
```




    array([0.82299653, 0.3986578 ])




```python
np.random.rand(5,5)
```




    array([[0.05645273, 0.41729733, 0.31189252, 0.51424822, 0.68334367],
           [0.60697948, 0.58590954, 0.0153086 , 0.37426767, 0.47708962],
           [0.75210967, 0.51879086, 0.33050348, 0.37138147, 0.02202641],
           [0.76461512, 0.98392357, 0.98813082, 0.96692933, 0.79946321],
           [0.19126686, 0.13986107, 0.98920734, 0.04883403, 0.62556886]])



###### randn
เป็นการสร้าง array ตามขนาดที่ต้องการเช่นกัน แต่องค์ประกอบภายในเป็นตัวเลขที่สุ่มออกมา จากกลุ่มตัวอย่างที่กระจายตัวแบบ "Normal Distribution"


```python
np.random.randn(2)
```




    array([ 0.77605361, -0.13989479])




```python
np.random.randn(5,5)
```




    array([[ 0.98010381,  0.81384123,  1.95040817, -0.73842541,  0.26441898],
           [-0.69151858, -0.47302325, -0.33110371,  1.02410345, -1.3836574 ],
           [-0.29105804, -0.15802971, -1.61820332,  1.22363234,  0.20002531],
           [ 0.94820746,  0.94647865, -0.41150415, -1.05010113, -1.07454394],
           [-0.33171297, -0.47790996,  1.03144876, -0.70769961, -0.37865379]])



###### randint
เป็นการสุ่มตัวเลขที่เป็นจำนวนเต็ม (Integer) ที่อยู่ระหว่างช่วงที่กำหนด และจำนวนการสุ่มที่ต้องการ

###### np.random.randint(\<start\>, \<end\>, \<number of sample\>)


```python
np.random.randint(1,45)
```




    10




```python
np.random.randint(1,45,10)
```




    array([12, 11, 11,  5, 22, 41, 39, 26, 42, 22])



#### Array Attributes and Methods
คุณสมบัติ และวิธีการนำ Array ไปใช้งาน


```python
arr = np.arange(25)
ranarr = np.random.randint(0,550,20)
```


```python
arr
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23, 24])




```python
ranarr
```




    array([526, 538, 316, 295, 374, 199,  90, 253, 446, 475,  10, 345, 310,
           169, 440, 532, 183,   3, 153, 225])




```python

```

#### Reshape
เป็นการเปลี่ยนแปลงมิติของ array


```python
arr.reshape(5,5)
```




    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14],
           [15, 16, 17, 18, 19],
           [20, 21, 22, 23, 24]])



#### max, min, argmax, argmin
คำนวณค่า max, min และ หาตำแหน่งหรือ index ของค่า max, min


```python
ranarr
```




    array([526, 538, 316, 295, 374, 199,  90, 253, 446, 475,  10, 345, 310,
           169, 440, 532, 183,   3, 153, 225])




```python
ranarr.max()
```




    538




```python
ranarr.argmax()
```




    1




```python
ranarr.min()
```


```python
ranarr.argmin()
```

#### dtype
ใช้ตรวจสอบชนิดของข้อมูลที่อยู่ใน Array


```python
arr.dtype
```




    dtype('int64')



#### Shape
ใช้ตรวจสอบขนาด หรือ มิติ ของ Array


```python
# Vector
arr.shape
```




    (25,)




```python
# Notice the two sets of brackets
arr.reshape(1,25)
```




    array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15,
            16, 17, 18, 19, 20, 21, 22, 23, 24]])




```python
arr.reshape(1,25).shape
```




    (1, 25)




```python
arr.reshape(25,1)
```




    array([[ 0],
           [ 1],
           [ 2],
           [ 3],
           [ 4],
           [ 5],
           [ 6],
           [ 7],
           [ 8],
           [ 9],
           [10],
           [11],
           [12],
           [13],
           [14],
           [15],
           [16],
           [17],
           [18],
           [19],
           [20],
           [21],
           [22],
           [23],
           [24]])




```python
arr.reshape(25,1).shape
```

## Numpy Indexing and Selection
เป็นส่วนที่จะกล่าวถึงการเรียกแต่ละองค์ประกอบ หรือกลุ่มขององค์ประกอบที่อยู่ใน Array


```python
import numpy as np
```

การสร้าง Array แบบง่าย ๆ


```python
arr = np.arange(0,11)
```

การแสดงค่าของ Array


```python
arr
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])



### Bracket Indexing and Selection
การเลือกองค์ประกอบตัวใดตัวหนึ่ง หรือกลุ่มขององค์ประกอบใน Array มีลักษณะคล้ายกับการเลือกองค์ประกอบภายใน List

เรียกองค์ประกอบด้วย index


```python
arr[8]
```




    8



เรียกองค์ประกอบเป็นช่วงของ index


```python
arr[1:5]
```




    array([1, 2, 3, 4])




```python
arr[0:5]
```




    array([0, 1, 2, 3, 4])



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



LAB
1. ให้นักศึกษา ทำการสุ่มตัวเลข ตั้งแต่ 1 - 100 จำนวน 20 ตัวเลข ในรูปแบบของ Array แล้ว และจงแสดง ค่า ต่ำสุดและสูง
2. ให้แสดงข้อมูล 5 ตัวแรก <BR> 3. และทำการกำหนด ช่วงข้อมูล ตั้ง 6-10 เป็นค่า เท่ากับ 0


```python
#lab2
import numpy as np
alist = np.random.randint(1,45,10);
alist
print('max',alist.max());
print('max',alist.min());
print(alist[0:5]);
alist[6:10]=0
alist
```

    max 29
    max 4
    [20 22 13  7  4]





    array([20, 22, 13,  7,  4, 13,  0,  0,  0,  0])



เปลี่ยนแปลงค่าของ array ที่ได้จากการ slices


```python
slice_of_arr[:]=99
slice_of_arr
```




    array([99, 99, 99, 99, 99, 99])



การเปลี่ยนแปลงค่าของ array ที่สร้างจากการ slices จะไปเปลี่ยนแปลงค่าใน array ที่เป็นตัวตั้งต้นด้วยเช่นกัน


```python
arr
```




    array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])



เพื่อป้องกันปัญหาเกี่ยวกับหน่วยความจำ เราสามารถสร้าง array ใหม่ จาก array ตั้งต้นด้วยคำสั่ง


```python
arr_copy = arr.copy()
arr_copy
```




    array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])



### Indexing a 2D array (matrices)
รูปแบบโดยทั่วไปของ Matrices คือ "arr_2d\[row\]\[col\] หรือ arr_2d\[row,col\] ดังตัวอย่าง


```python
arr_2d = np.array(([5,10,15],
                   [20,25,30],
                   [35,40,45]))

arr_2d
```




    array([[ 5, 10, 15],
           [20, 25, 30],
           [35, 40, 45]])



เรียกองค์ประกอบแถวที่ 1


```python
arr_2d[0]
```




    array([ 5, 10, 15])



เรียกองค์ประกอบในแถวที่ 1 หลักที่ 0


```python
arr_2d[1][0]
```




    20




```python
arr_2d[2,2]
```




    45



##### การ slices แบบ 2D
เรียกองค์ประกอบด้านบนขวาของ Array


```python
arr_2d[1:2,:]
```




    array([[20, 25, 30]])



เรียกองค์ประกอบแถวที่ 2


```python
arr_2d[2]
```




    array([35, 40, 45])



เรียกองค์ประกอบแถวล่างสุด


```python
arr_2d[2,:]
```




    array([35, 40, 45])



### Fancy Indexing
สามารถเลือกแสดงค่าทั้งแถวหรือทั้งหลักได้โดยไม่ต้องเรียงลำดับ จากตัวอย่างด้านล่าง ได้ทำการสร้าง zero array ขนาด 10\*10 ขึ้นมา


```python
arr2d = np.zeros((10,10))
```

เก็บค่าขนาดของจำนวนหลักของ array ไว้ใน arr_length


```python
arr_length = arr2d.shape[1]
```

กำหนดค่าของ arr2d ใหม่โดยใช้ for loop


```python
for i in range(arr_length):
    arr2d[i] = i

arr2d
```




    array([[0., 0., 0., 0., 0., 0., 0., 0., 0., 0.],
           [1., 1., 1., 1., 1., 1., 1., 1., 1., 1.],
           [2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [3., 3., 3., 3., 3., 3., 3., 3., 3., 3.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [5., 5., 5., 5., 5., 5., 5., 5., 5., 5.],
           [6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [7., 7., 7., 7., 7., 7., 7., 7., 7., 7.],
           [8., 8., 8., 8., 8., 8., 8., 8., 8., 8.],
           [9., 9., 9., 9., 9., 9., 9., 9., 9., 9.]])



เลือกแสดงค่าขององค์ประกอบในแถวที่ 2, 4, 6, 8


```python
arr2d[[2,4,6,8]]
```




    array([[2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [8., 8., 8., 8., 8., 8., 8., 8., 8., 8.]])



เลือกแสดงค่าขององค์ประกอบในแถวที่ 6, 4, 2, 7 โดยไม่เรียงตามลำดับ


```python
arr2d[[6,4,2,7]]
```




    array([[6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [7., 7., 7., 7., 7., 7., 7., 7., 7., 7.]])



### Selection
การเลือกค่าโดยใช้ \[ \] ร่วมกับ comparison operators


```python
arr = np.arange(1,11)
arr
```




    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])




```python
arr > 4
```




    array([False, False, False, False,  True,  True,  True,  True,  True,
            True])




```python
bool_arr = arr > 4
```


```python
bool_arr
```




    array([False, False, False, False,  True,  True,  True,  True,  True,
            True])




```python
arr[bool_arr]
```




    array([ 5,  6,  7,  8,  9, 10])




```python
arr[arr>2]
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10])




```python
x = 2
arr[arr>x]
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10])



ให้แสดงค่า สุ้มต้วเลข 1- 100 จำนวน 50 ตัว  
1 ให้แสดงค่า (Ture) จริง ที่ตัวเลขมากกว่า 30
2. ให้แสดงค่า ตัวเลข ที่มีค่ามากว่า 65  


```python
import numpy as np
alist = np.random.randint(0,100,50);
print(alist)
alist > 30
print(alist>30 )
print(alist[alist > 65]);
```

    [57 78 18 18 24 69 46  7 43  0 40 53 76 86 35 27 47  3 30 53 14 80 38 97
      2 13 54 34 64 83 77 74  9 56 59 47 24 93 91 32 88 98 25 40 12 34 80 60
     73 51]
    [ True  True False False False  True  True False  True False  True  True
      True  True  True False  True False False  True False  True  True  True
     False False  True  True  True  True  True  True False  True  True  True
     False  True  True  True  True  True False  True False  True  True  True
      True  True]
    [78 69 76 86 80 97 83 77 74 93 91 88 98 80 73]


## Numpy Operations
### Arithmetic
การใช้ดำเนินการทางคณิตศาสตร์ กับ numpy array แสดงไว้ดังตัวอย่าง โดยจะนำองค์ประกอบที่มี index เดียวกัน มาทำการดำเนินการตามเครื่องหมายที่ได้กำหนดไว้


```python
import numpy as np
arr = np.arange(0,10)
```


```python
arr + arr + arr + arr
```




    array([ 0,  4,  8, 12, 16, 20, 24, 28, 32, 36])




```python
arr * arr
```




    array([ 0,  1,  4,  9, 16, 25, 36, 49, 64, 81])




```python
arr - arr
```




    array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])



การหารที่ตัวเศษ และตัวส่วนเป็น 0 จะมีข้อความเตือนเกิดขึ้น แต่ค่าจะถูกแทนค่าด้วย "nan"


```python
arr/arr
```

การหารที่ตัวส่วนเป็น 0 จะมีข้อความเตือนเกิดขึ้น แต่ค่าจะถูกแทนค่าด้วย "inf"


```python
1/arr
```


```python
arr**3
```

### Universal Array Functions
Universal Array Functions คือ ตัวดำเนินการทางคณิตศาสตร์จำเป็นที่อยู่ในรูปแบบของฟังก์ชัน ซึ่งสามารถนำมาใช้งานได้กับ numpy array ตัวอย่างที่นำมาแสดงในที่นี้ เป็นตัวดำเนิการทั่วไปที่มีการใช้งานเป็นประจำกัน

คำนวณค่ารากที่สอง (Squrt Root)


```python
np.sqrt(arr)
```




    array([0.        , 1.        , 1.41421356, 1.73205081, 2.        ,
           2.23606798, 2.44948974, 2.64575131, 2.82842712, 3.        ])



คำนวณค่า exponential (e^)


```python
np.exp(arr)
```




    array([1.00000000e+00, 2.71828183e+00, 7.38905610e+00, 2.00855369e+01,
           5.45981500e+01, 1.48413159e+02, 4.03428793e+02, 1.09663316e+03,
           2.98095799e+03, 8.10308393e+03])



หาค่าที่มากที่สุด และค่าที่น้อยที่สุด ใน array


```python
np.max(arr)
```


```python
np.min(arr)
```

คำนวณค่า Sine


```python
np.sin(arr)
```

คำนวณค่า Logarithm


```python
np.log(arr)
```


```python
np.log2(8)
```

### Statisitcal Calculation by Numpy
### 1D Array


```python
arr
```

#### Min


```python
arr.min(), np.min(arr)
```

#### Max


```python
arr.max(), np.max(arr)
```

#### Mean


```python
arr.mean(), np.mean(arr)
```

#### Median


```python
np.median(arr)
```

#### Standard Deviation


```python
arr.std()
```


```python

```

#### Interquartile range


```python
quartiles = np.quantile(arr, [0.25, 0.75])
quartiles[1] - quartiles[0]
```

### 2D Array


```python
a = np.array([[1, 1, 1],
              [2, 3, 1],
              [4, 9, 2],
              [8, 27, 4],
              [16, 1, 1]])
a
```




    array([[ 1,  1,  1],
           [ 2,  3,  1],
           [ 4,  9,  2],
           [ 8, 27,  4],
           [16,  1,  1]])



#### 2D Array Min


```python
np.min(a, axis=0)
```




    array([1, 1, 1])




```python
a.min(axis=1)
```

#### 2D Array Max


```python
np.max(a, axis=0)
```


```python
a.max(axis=1)
```

#### 2D Array Mean


```python
np.mean(a, axis=0)
```


```python
a.mean(axis=1)
```

#### 2D Array Median


```python
np.median(a, axis=0)
```


```python
np.median(a, axis=1)
```

#### 2D Array Standard Deviation


```python
a.std(axis=0)
```


```python
a.std(axis=1)
```

#### 2D Array Interquartile Range


```python
quartiles = np.quantile(a, [0.25, 0.75],
                        axis=0)
quartiles[1] - quartiles[0]
```


```python
quartiles = np.quantile(a, [0.25, 0.75],
                        axis=1)
quartiles[1] - quartiles[0]
```

จากชุดข้อมูล [1, 2, 3], [4, 5, 6], [7, 8, 9]  ให้นักศึกษา
1. แสดง ค่า ในตำแหน่งแถวที่ 2 คอลัมน์ที่ 3 และพิมพ์ค่าออกมา
2. พิ่มค่าใน array ทุกค่าด้วย 5 และพิมพ์ผลลัพธ์ออกม
3. ให้หาค่าเฉลี่ยในแถวที่ 1 และแสดงค่าออกมา


```python

```
