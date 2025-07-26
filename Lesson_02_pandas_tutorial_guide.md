# เอกสารประกอบการสอน Pandas
## สำหรับนักศึกษาปริญญาตรี

---

## 📊 สารบัญ
1. [บทนำ Pandas](#บทนำ-pandas)
2. [การติดตั้งและการ Import](#การติดตั้งและการ-import)
3. [Series พื้นฐาน](#series-พื้นฐาน)
4. [DataFrame พื้นฐาน](#dataframe-พื้นฐาน)
5. [การโหลดและบันทึกข้อมูล](#การโหลดและบันทึกข้อมูล)
6. [Data Selection และ Filtering](#data-selection-และ-filtering)
7. [แบบฝึกหัด](#แบบฝึกหัด)
8. [โครงงานปฏิบัติ](#โครงงานปฏิบัติ)

---

## บทนำ Pandas

### Pandas คืออะไร?
**Pandas** (Python Data Analysis Library) เป็น library ที่ทรงพลังสำหรับการจัดการและวิเคราะห์ข้อมูลใน Python โดยให้เครื่องมือที่เร็วและยืดหยุ่นสำหรับการทำงานกับข้อมูลแบบ structured

### ทำไมต้องใช้ Pandas?

#### เปรียบเทียบการทำงานกับข้อมูล

```python
# ไม่ใช้ Pandas - ยุ่งยาก
data = [
    ['Alice', 25, 50000],
    ['Bob', 30, 60000],
    ['Charlie', 35, 70000]
]

# หาค่าเฉลี่ยเงินเดือน
total_salary = sum(row[2] for row in data)
avg_salary = total_salary / len(data)

# ใช้ Pandas - ง่ายและชัดเจน
import pandas as pd
df = pd.DataFrame(data, columns=['Name', 'Age', 'Salary'])
avg_salary = df['Salary'].mean()
```

### ข้อดีของ Pandas
- **Easy Data Manipulation**: จัดการข้อมูลได้ง่าย
- **Multiple File Formats**: รองรับไฟล์หลายรูปแบบ (CSV, Excel, JSON, SQL)
- **Missing Data Handling**: จัดการข้อมูลที่หายได้ดี
- **Data Alignment**: จัดเรียงข้อมูลอัตโนมัติ
- **Flexible Grouping**: จัดกลุ่มข้อมูลได้หลากหลาย
- **Integration**: ทำงานร่วมกับ NumPy, Matplotlib ได้ดี

### สถิติการใช้งาน
- ใช้ในโครงการ Data Science มากกว่า 95%
- มีการ download มากกว่า 50 ล้านครั้งต่อเดือน
- Essential tool สำหรับ Data Scientists ทั่วโลก

---

## การติดตั้งและการ Import

### การติดตั้ง
```bash
# ผ่าน pip
pip install pandas

# ผ่าน conda
conda install pandas

# รวมกับ dependencies อื่นๆ
pip install pandas numpy matplotlib seaborn

# ตรวจสอบ version
python -c "import pandas as pd; print(pd.__version__)"
```

### การ Import
```python
# Standard import
import pandas as pd
import numpy as np

# ตรวจสอบ version
print(f"Pandas version: {pd.__version__}")

# Import เฉพาะที่ต้องการ
from pandas import DataFrame, Series, read_csv

# การตั้งค่า display options
pd.set_option('display.max_rows', 100)
pd.set_option('display.max_columns', 20)
pd.set_option('display.width', 1000)
```

### การตั้งค่าเพิ่มเติม
```python
# การแสดงผลทศนิยม
pd.set_option('display.float_format', '{:.2f}'.format)

# การแสดงผลขนาดใหญ่
pd.set_option('display.max_colwidth', 50)

# รีเซ็ตการตั้งค่า
pd.reset_option('all')

# ดูการตั้งค่าปัจจุบัน
print(pd.describe_option())
```

---

## Series พื้นฐาน

### Series คืออะไร?
**Series** เป็นโครงสร้างข้อมูล 1 มิติที่สามารถเก็บข้อมูลชนิดใดก็ได้ (integers, strings, floats, Python objects) พร้อมกับ labels (index)

### การสร้าง Series

```python
import pandas as pd
import numpy as np

# จาก Python list
s1 = pd.Series([1, 3, 5, np.nan, 6, 8])
print(s1)

# กำหนด index เอง
s2 = pd.Series([1, 3, 5, 6], index=['a', 'b', 'c', 'd'])
print(s2)

# จาก dictionary
data_dict = {'A': 1, 'B': 2, 'C': 3, 'D': 4}
s3 = pd.Series(data_dict)
print(s3)

# จาก NumPy array
arr = np.array([1, 2, 3, 4, 5])
s4 = pd.Series(arr, index=['x', 'y', 'z', 'w', 'v'])
print(s4)

# Series ที่มีค่าเดียวกันทั้งหมด
s5 = pd.Series(5, index=[0, 1, 2, 3])
print(s5)
```

### คุณสมบัติของ Series
```python
s = pd.Series([1, 3, 5, np.nan, 6, 8], index=['a', 'b', 'c', 'd', 'e', 'f'])

# คุณสมบัติพื้นฐาน
print(f"Values: {s.values}")          # NumPy array
print(f"Index: {s.index}")            # Index object
print(f"Data type: {s.dtype}")        # ชนิดข้อมูล
print(f"Shape: {s.shape}")            # รูปร่าง
print(f"Size: {s.size}")              # จำนวน elements
print(f"Name: {s.name}")              # ชื่อ Series

# ตั้งชื่อให้ Series และ index
s.name = 'My Series'
s.index.name = 'Labels'
print(s)
```

### การเข้าถึงข้อมูลใน Series
```python
s = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

# เข้าถึงด้วย label
print(s['b'])                    # 20
print(s[['a', 'c', 'e']])        # Multiple labels

# เข้าถึงด้วย position
print(s[1])                      # 20
print(s[0:3])                    # Slicing

# Boolean indexing
print(s[s > 25])                 # ค่าที่มากกว่า 25

# การตรวจสอบ
print('b' in s)                  # True
print(s.get('f', 'Not found'))   # Get with default value
```

### การดำเนินการกับ Series
```python
s1 = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
s2 = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])

# Arithmetic operations
print(s1 + s2)                   # Element-wise addition
print(s1 * 2)                    # Scalar multiplication
print(s1 ** 2)                   # Power

# Statistical operations
print(s1.sum())                  # ผลรวม
print(s1.mean())                 # ค่าเฉลี่ย
print(s1.std())                  # ส่วนเบี่ยงเบนมาตรฐาน
print(s1.describe())             # สถิติโดยรวม

# String operations (สำหรับ Series ที่มี string)
s_str = pd.Series(['apple', 'banana', 'cherry'])
print(s_str.str.upper())         # ตัวพิมพ์ใหญ่
print(s_str.str.len())           # ความยาว string
print(s_str.str.contains('a'))   # ตรวจสอบว่ามี 'a'
```

---

## DataFrame พื้นฐาน

### DataFrame คืออะไร?
**DataFrame** เป็นโครงสร้างข้อมูล 2 มิติที่เหมือน table ใน SQL หรือ spreadsheet ใน Excel โดยมี labeled axes (rows และ columns)

### การสร้าง DataFrame

```python
# จาก dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'City': ['New York', 'London', 'Tokyo', 'Paris'],
    'Salary': [50000, 60000, 70000, 55000]
}
df = pd.DataFrame(data)
print(df)

# จาก list of dictionaries
data_list = [
    {'Name': 'Alice', 'Age': 25, 'City': 'New York'},
    {'Name': 'Bob', 'Age': 30, 'City': 'London'},
    {'Name': 'Charlie', 'Age': 35, 'City': 'Tokyo'}
]
df2 = pd.DataFrame(data_list)
print(df2)

# จาก NumPy array
arr = np.random.randn(4, 3)
df3 = pd.DataFrame(arr, 
                   columns=['A', 'B', 'C'],
                   index=['Row1', 'Row2', 'Row3', 'Row4'])
print(df3)

# จาก Series
s1 = pd.Series([1, 2, 3], name='Col1')
s2 = pd.Series([4, 5, 6], name='Col2')
df4 = pd.DataFrame({'Col1': s1, 'Col2': s2})
print(df4)
```

### คุณสมบัติของ DataFrame
```python
df = pd.DataFrame({
    'A': [1, 2, 3, 4],
    'B': [5.0, 6.0, 7.0, 8.0],
    'C': ['foo', 'bar', 'baz', 'qux'],
    'D': [True, False, True, False]
})

# คุณสมบัติพื้นฐาน
print(f"Shape: {df.shape}")              # (rows, columns)
print(f"Size: {df.size}")                # total elements
print(f"Columns: {df.columns}")          # column names
print(f"Index: {df.index}")              # row indices
print(f"Data types:\n{df.dtypes}")       # data types
print(f"Memory usage:\n{df.memory_usage()}")

# ข้อมูลเบื้องต้น
print(df.head())                         # 5 แถวแรก
print(df.tail(3))                        # 3 แถวสุดท้าย
print(df.info())                         # ข้อมูลโดยรวม
print(df.describe())                     # สถิติสำหรับ numeric columns
```

### การเข้าถึงข้อมูลใน DataFrame

#### การเลือก Columns
```python
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# เลือก 1 column (ได้ Series)
print(df['Name'])

# เลือกหลาย columns (ได้ DataFrame)
print(df[['Name', 'Salary']])

# เข้าถึงด้วย attribute (ถ้าชื่อ column ไม่มีช่องว่าง)
print(df.Name)
```

#### การเลือก Rows
```python
# เลือกด้วย position
print(df.iloc[0])              # แถวแรก (Series)
print(df.iloc[0:2])            # แถวที่ 0-1 (DataFrame)

# เลือกด้วย label
df_indexed = df.set_index('Name')
print(df_indexed.loc['Alice'])  # แถวของ Alice

# Boolean indexing
print(df[df['Age'] > 30])       # คนที่อายุมากกว่า 30
print(df[df['Name'].isin(['Alice', 'Charlie'])])  # เลือกชื่อเฉพาะ
```

#### การเลือก Cells เฉพาะ
```python
# เลือก cell เฉพาะ
print(df.iloc[0, 1])           # แถว 0, column 1
print(df.loc[0, 'Age'])        # แถว 0, column 'Age'

# เลือกช่วง
print(df.iloc[0:2, 1:3])       # แถว 0-1, column 1-2
print(df.loc[0:1, 'Age':'Salary'])  # แถว 0-1, column Age-Salary
```

---

## การโหลดและบันทึกข้อมูล

### การอ่านไฟล์ต่างๆ

#### CSV Files
```python
# อ่าน CSV พื้นฐาน
df = pd.read_csv('data.csv')

# พร้อม parameters ต่างๆ
df = pd.read_csv(
    'data.csv',
    sep=',',                    # ตัวแบ่ง
    header=0,                   # แถวที่เป็น header
    index_col=0,                # column ที่เป็น index
    usecols=['Name', 'Age'],    # column ที่ต้องการ
    dtype={'Age': int},         # กำหนดชนิดข้อมูล
    parse_dates=['Date'],       # แปลงเป็น datetime
    na_values=['N/A', 'NULL']   # ค่า missing
)

# อ่านจาก URL
url = 'https://example.com/data.csv'
df = pd.read_csv(url)

# อ่านเฉพาะบางแถว
df = pd.read_csv('data.csv', nrows=100)  # อ่าน 100 แถวแรก
df = pd.read_csv('data.csv', skiprows=10)  # ข้าม 10 แถวแรก
```

#### Excel Files
```python
# อ่าน Excel
df = pd.read_excel('data.xlsx')

# อ่าน sheet เฉพาะ
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# อ่านหลาย sheets
dfs = pd.read_excel('data.xlsx', sheet_name=None)  # dictionary ของ DataFrames

# พร้อม parameters
df = pd.read_excel(
    'data.xlsx',
    sheet_name='Data',
    header=0,
    index_col=0,
    usecols='A:D',             # columns A ถึง D
    skiprows=2                 # ข้าม 2 แถวแรก
)
```

#### JSON Files
```python
# อ่าน JSON
df = pd.read_json('data.json')

# JSON รูปแบบต่างๆ
df = pd.read_json('data.json', orient='records')  # list of objects
df = pd.read_json('data.json', orient='index')    # object of objects
df = pd.read_json('data.json', lines=True)        # JSON Lines format
```

#### SQL Database
```python
import sqlite3

# เชื่อมต่อฐานข้อมูล
conn = sqlite3.connect('database.db')

# อ่านจาก SQL query
df = pd.read_sql_query('SELECT * FROM table_name', conn)

# อ่านทั้ง table
df = pd.read_sql_table('table_name', conn)

# ปิดการเชื่อมต่อ
conn.close()
```

### การบันทึกข้อมูล

```python
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

# บันทึกเป็น CSV
df.to_csv('output.csv', index=False)

# บันทึกเป็น Excel
df.to_excel('output.xlsx', sheet_name='Data', index=False)

# บันทึกเป็น JSON
df.to_json('output.json', orient='records', indent=2)

# บันทึกลงฐานข้อมูล
conn = sqlite3.connect('database.db')
df.to_sql('table_name', conn, if_exists='replace', index=False)
conn.close()

# บันทึกเฉพาะบางส่วน
df[['Name', 'Age']].to_csv('partial_data.csv', index=False)
```

---

## Data Selection และ Filtering

### เทคนิคการเลือกข้อมูล

#### Basic Selection
```python
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'City': ['NY', 'London', 'Tokyo', 'Paris', 'Berlin'],
    'Salary': [50000, 60000, 70000, 55000, 65000],
    'Department': ['IT', 'HR', 'IT', 'Finance', 'IT']
})

# เลือก columns
single_col = df['Name']                    # Series
multi_cols = df[['Name', 'Age', 'Salary']] # DataFrame

# เลือก rows ด้วย conditions
high_salary = df[df['Salary'] > 60000]
it_employees = df[df['Department'] == 'IT']
young_high_earners = df[(df['Age'] < 30) & (df['Salary'] > 50000)]
```

#### iloc และ loc
```python
# iloc - position-based selection
print(df.iloc[0])              # แถวแรก
print(df.iloc[0:3])            # แถว 0-2
print(df.iloc[:, 1:3])         # columns 1-2 ทุกแถว
print(df.iloc[0:2, 1:3])       # แถว 0-1, columns 1-2

# loc - label-based selection
df_with_index = df.set_index('Name')
print(df_with_index.loc['Alice'])           # แถวของ Alice
print(df_with_index.loc['Alice':'Charlie']) # แถว Alice ถึง Charlie
print(df_with_index.loc[:, 'Age':'Salary']) # columns Age ถึง Salary
```

#### Query Method
```python
# ใช้ query สำหรับ filtering ที่ซับซ้อน
result1 = df.query('Age > 30')
result2 = df.query('Age > 30 and Salary < 70000')
result3 = df.query('Department == "IT"')
result4 = df.query('City in ["NY", "Tokyo"]')

# ใช้ตัวแปร external
min_age = 30
result5 = df.query('Age > @min_age')
```

### Advanced Filtering

#### การใช้ isin()
```python
# เลือกหลายค่าพร้อมกัน
cities_of_interest = ['NY', 'Tokyo', 'Paris']
filtered = df[df['City'].isin(cities_of_interest)]

# ตรงข้ามของ isin
not_in_cities = df[~df['City'].isin(cities_of_interest)]
```

#### String Filtering
```python
# สร้างข้อมูลตัวอย่าง
df_str = pd.DataFrame({
    'Name': ['Alice Johnson', 'Bob Smith', 'Charlie Brown', 'Diana Wilson'],
    'Email': ['alice@gmail.com', 'bob@yahoo.com', 'charlie@gmail.com', 'diana@outlook.com']
})

# String methods
gmail_users = df_str[df_str['Email'].str.contains('gmail')]
starts_with_a = df_str[df_str['Name'].str.startswith('A')]
ends_with_son = df_str[df_str['Name'].str.endswith('son')]

# Case-insensitive search
contains_alice = df_str[df_str['Name'].str.contains('alice', case=False)]

# Regular expressions
pattern_match = df_str[df_str['Email'].str.match(r'\w+@gmail\.com')]
```

#### การจัดการ Missing Values ในการ Filter
```python
# สร้างข้อมูลที่มี missing values
df_missing = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': [np.nan, 2, 3, 4, np.nan],
    'C': [1, 2, 3, 4, 5]
})

# Filter ที่ไม่มี missing values
no_missing = df_missing[df_missing['A'].notna()]

# Filter ที่มี missing values
has_missing = df_missing[df_missing['A'].isna()]

# Filter หลาย columns
complete_rows = df_missing.dropna()  # แถวที่ไม่มี missing values
any_missing = df_missing[df_missing.isna().any(axis=1)]  # แถวที่มี missing values
```


## แบบฝึกหัด

### แบบฝึกหัดที่ 1: Series และ DataFrame พื้นฐาน (15 คะแนน)

#### ข้อ 1.1 (5 คะแนน)
สร้าง Series และ DataFrame ตามที่กำหนด:

```python
# TODO: เขียนโค้ดสร้าง
# a) Series ที่มี index เป็นชื่อเดือน และ values เป็นจำนวนวันในแต่ละเดือน
# b) DataFrame สำหรับข้อมูลนักเรียน 5 คน ประกอบด้วย:
#    - ชื่อ (Name)
#    - อายุ (Age) 
#    - เกรด (Grade)
#    - เมือง (City)
# c) แสดงข้อมูลเบื้องต้นของ DataFrame (shape, dtypes, info)
```

**เฉลย:**
```python
# a) Series เดือน
months_days = pd.Series(
    [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
    index=['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
           'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    name='Days_in_Month'
)

# b) DataFrame นักเรียน
students = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [20, 21, 19, 22, 20],
    'Grade': ['A', 'B', 'A', 'C', 'B'],
    'City': ['Bangkok', 'Chiang Mai', 'Phuket', 'Bangkok', 'Pattaya']
})

# c) ข้อมูลเบื้องต้น
print(f"Shape: {students.shape}")
print(f"Data types:\n{students.dtypes}")
print(f"Info:\n{students.info()}")
```

#### ข้อ 1.2 (5 คะแนน)
จากข้อมูลต่อไปนี้ ให้ทำการ selection และ filtering:

```python
sales_data = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=50, freq='D'),
    'Product': np.random.choice(['A', 'B', 'C'], 50),
    'Sales': np.random.randint(100, 1000, 50),
    'Region': np.random.choice(['North', 'South', 'East', 'West'], 50)
})

# TODO: เขียนโค้ด
# a) เลือกข้อมูลสินค้า 'A' ที่ขายได้มากกว่า 500
# b) หาค่าเฉลี่ยยอดขายของแต่ละภูมิภาค
# c) เลือกข้อมูล 10 วันแรกของเดือนมกราคม
# d) สร้าง column ใหม่ชื่อ 'Sales_Category' ที่แบ่งเป็น 'High' (>700), 'Medium' (400-700), 'Low' (<400)
```

#### ข้อ 1.3 (5 คะแนน)
เขียนฟังก์ชันวิเคราะห์ DataFrame:

```python
def analyze_dataframe(df, numeric_cols=None):
    """
    วิเคราะห์ DataFrame และส่งกลับสรุปผล
    
    Parameters:
    df: DataFrame ที่ต้องการวิเคราะห์
    numeric_cols: list ของ numeric columns (ถ้าไม่ระบุจะใช้ทุก numeric columns)
    
    Returns:
    dict ที่มีข้อมูล:
    - shape: รูปร่างของ DataFrame
    - missing_values: จำนวน missing values ในแต่ละ column
    - numeric_summary: สถิติของ numeric columns
    - categorical_summary: จำนวน unique values ในแต่ละ categorical column
    """
    # TODO: implement function
    pass

# ทดสอบฟังก์ชัน
test_data = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': ['x', 'y', 'x', 'z', 'y'],
    'C': [10.5, 20.3, 30.1, np.nan, 50.2]
})

result = analyze_dataframe(test_data)
```
