# เอกสารประกอบการสอน Data Cleaning
## การทำความสะอาดข้อมูล

---

## 📋 สารบัญ
1. [ความหมายและความสำคัญ](#ความหมายและความสำคัญ)
2. [ประเภทของปัญหาข้อมูล](#ประเภทของปัญหาข้อมูล)
3. [ขั้นตอนการทำ Data Cleaning](#ขั้นตอนการทำ-data-cleaning)
4. [เครื่องมือและเทคนิค](#เครื่องมือและเทคนิค)
5. [ตัวอย่างการปฏิบัติ](#ตัวอย่างการปฏิบัติ)
6. [Best Practices](#best-practices)
7. [แบบฝึกหัด](#แบบฝึกหัด)

---

## ความหมายและความสำคัญ

### Data Cleaning คืออะไร?
Data Cleaning หรือ Data Cleansing คือ กระบวนการตรวจสอบ แก้ไข และปรับปรุงข้อมูลเพื่อให้ข้อมูลมีคุณภาพที่ดี พร้อมใช้งานสำหรับการวิเคราะห์

### ทำไมต้องทำ Data Cleaning?
- **ข้อมูลคุณภาพดี = ผลลัพธ์ที่เชื่อถือได้**
- ลดข้อผิดพลาดในการวิเคราะห์
- ประหยัดเวลาในการประมวลผล
- เพิ่มประสิทธิภาพของ Machine Learning Models
- สร้างความเชื่อมั่นในการตัดสินใจ

### สถิติที่น่าสนใจ
- นักวิเคราะห์ข้อมูลใช้เวลา 60-80% ในการทำ Data Cleaning
- ข้อมูลที่ไม่สะอาดสามารถลดประสิทธิภาพของโมเดลได้ถึง 25%

---

## ประเภทของปัญหาข้อมูล

### 1. Missing Data (ข้อมูลสูญหาย)
```
ตัวอย่าง:
Name     | Age | Salary
---------|-----|--------
John     | 25  | 50000
Mary     |     | 60000
Peter    | 30  |
```

### 2. Duplicate Data (ข้อมูลซ้ำ)
```
ตัวอย่าง:
ID | Name  | Email
---|-------|------------------
1  | John  | john@email.com
2  | Mary  | mary@email.com
3  | John  | john@email.com  ← ข้อมูลซ้ำ
```

### 3. Inconsistent Data (ข้อมูลไม่สอดคล้อง)
```
ตัวอย่าง:
Country
---------
Thailand
thailand
THAILAND
ประเทศไทย
```

### 4. Invalid Data (ข้อมูลไม่ถูกต้อง)
```
ตัวอย่าง:
Age: -5, 999, "abc"
Email: "notanemail"
Date: "2024-13-45"
```

### 5. Outliers (ข้อมูลผิดปกติ)
```
ตัวอย่าง:
Salary: 30000, 35000, 40000, 45000, 50000000
                                      ↑ Outlier
```

---

## ขั้นตอนการทำ Data Cleaning

### Phase 1: Data Profiling (การสำรวจข้อมูล)
1. **ตรวจสอบโครงสร้างข้อมูล**
   - จำนวนแถวและคอลัมน์
   - ประเภทของข้อมูล (Data Types)
   - ขนาดของไฟล์

2. **สำรวจคุณภาพข้อมูล**
   - หาข้อมูลที่สูญหาย
   - ตรวจสอบข้อมูลซ้ำ
   - วิเคราะห์การกระจายของข้อมูล

### Phase 2: Data Cleaning (การทำความสะอาด)
1. **จัดการ Missing Data**
2. **กำจัดข้อมูลซ้ำ**
3. **แก้ไขข้อมูลที่ไม่สอดคล้อง**
4. **กรองข้อมูลที่ไม่ถูกต้อง**
5. **จัดการ Outliers**

### Phase 3: Data Validation (การตรวจสอบ)
1. **ตรวจสอบผลลัพธ์**
2. **สร้างรายงานสรุป**
3. **บันทึกขั้นตอนการทำงาน**

---

## เครื่องมือและเทคนิค

### เครื่องมือยอดนิยม

#### Python Libraries
- **Pandas**: จัดการข้อมูลทั่วไป
- **NumPy**: คำนวณทางคณิตศาสตร์
- **Matplotlib/Seaborn**: สร้างกราฟ
- **Scikit-learn**: จัดการ Outliers

#### R Libraries
- **dplyr**: จัดการข้อมูล
- **tidyr**: จัดรูปแบบข้อมูล
- **VIM**: จัดการ Missing Data

#### SQL
- การใช้ SQL สำหรับทำความสะอาดข้อมูลในฐานข้อมูล

#### GUI Tools
- **OpenRefine**: เครื่องมือทำความสะอาดข้อมูลแบบ GUI
- **Tableau Prep**: สำหรับผู้ใช้ Tableau
- **Excel**: สำหรับข้อมูลขนาดเล็ก

### เทคนิคสำคัญ

#### การจัดการ Missing Data
1. **Deletion Methods**
   - Listwise deletion
   - Pairwise deletion

2. **Imputation Methods**
   - Mean/Median/Mode imputation
   - Forward/Backward fill
   - Interpolation
   - Machine Learning imputation

#### การตรวจหา Outliers
1. **Statistical Methods**
   - Z-score
   - IQR (Interquartile Range)
   - Modified Z-score

2. **Visual Methods**
   - Box plots
   - Scatter plots
   - Histograms


---

## Data Cleaning

### การจัดการ Missing Values

#### การตรวจสอบ Missing Values
```python
df = pd.DataFrame({
    'A': [1, 2, np.nan, 4, 5],
    'B': [np.nan, 2, 3, np.nan, 5],
    'C': [1, 2, 3, 4, 5],
    'D': ['a', 'b', None, 'd', 'e']
})

# ตรวจสอบ missing values
print(df.isnull().sum())           # จำนวน missing values ในแต่ละ column
print(df.isna().sum())             # เหมือนกับ isnull()
print(df.info())                   # ข้อมูลโดยรวมรวมถึง missing values

# ตรวจสอบแถวที่มี missing values
print(df[df.isnull().any(axis=1)])

# เปอร์เซ็นต์ของ missing values
missing_percent = (df.isnull().sum() / len(df)) * 100
print(missing_percent)
```

#### การลบ Missing Values
```python
# ลบแถวที่มี missing values
df_drop_rows = df.dropna()                    # ลบทุกแถวที่มี missing
df_drop_any = df.dropna(how='any')            # ลบถ้ามี missing อย่างน้อย 1 ค่า
df_drop_all = df.dropna(how='all')            # ลบถ้าทุกค่าเป็น missing

# ลบ columns ที่มี missing values
df_drop_cols = df.dropna(axis=1)              # ลบ columns ที่มี missing

# ลบถ้ามี missing values มากกว่าที่กำหนด
df_thresh = df.dropna(thresh=3)               # ต้องมีค่าที่ไม่ missing อย่างน้อย 3 ค่า

# ลบเฉพาะ columns เฉพาะ
df_subset = df.dropna(subset=['A', 'B'])      # ลบถ้า A หรือ B เป็น missing
```

#### การเติม Missing Values
```python
# เติมด้วยค่าคงที่
df_fill_zero = df.fillna(0)                   # เติมด้วย 0
df_fill_unknown = df.fillna('Unknown')        # เติมด้วย 'Unknown'

# เติมด้วยค่าสถิติ
df_fill_mean = df.fillna(df.mean())           # เติมด้วยค่าเฉลี่ย (numeric columns)
df_fill_median = df.fillna(df.median())       # เติมด้วย median

# เติมแต่ละ column ต่างกัน
fill_values = {'A': df['A'].mean(), 'B': df['B'].median(), 'D': 'Unknown'}
df_fill_dict = df.fillna(value=fill_values)

# Forward fill และ Backward fill
df_ffill = df.fillna(method='ffill')          # เติมด้วยค่าก่อนหน้า
df_bfill = df.fillna(method='bfill')          # เติมด้วยค่าถัดไป

# Interpolation
df_interp = df.interpolate()                  # interpolate สำหรับ numeric data
```

### การจัดการ Duplicates

```python
# สร้างข้อมูลที่มี duplicates
df_dup = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob'],
    'Age': [25, 30, 25, 35, 30],
    'City': ['NY', 'London', 'NY', 'Tokyo', 'London']
})

# ตรวจสอบ duplicates
print(df_dup.duplicated())                    # Boolean mask
print(df_dup.duplicated().sum())              # จำนวน duplicate rows

# ตรวจสอบ duplicates ใน column เฉพาะ
print(df_dup.duplicated(subset=['Name']))

# ลบ duplicates
df_no_dup = df_dup.drop_duplicates()          # ลบ duplicate rows
df_no_dup_name = df_dup.drop_duplicates(subset=['Name'])  # ลบ duplicate names

# เก็บ duplicate แรกหรือสุดท้าย
df_keep_first = df_dup.drop_duplicates(keep='first')
df_keep_last = df_dup.drop_duplicates(keep='last')
df_remove_all = df_dup.drop_duplicates(keep=False)  # ลบทุก duplicates
```

### Data Type Conversion

```python
df = pd.DataFrame({
    'A': ['1', '2', '3', '4'],           # string numbers
    'B': [1.0, 2.0, 3.0, 4.0],          # floats
    'C': ['2023-01-01', '2023-01-02'],   # date strings
    'D': ['True', 'False', 'True']       # boolean strings
})

# แปลง data types
df['A'] = df['A'].astype(int)             # string to int
df['B'] = df['B'].astype(int)             # float to int
df['C'] = pd.to_datetime(df['C'])         # string to datetime
df['D'] = df['D'].astype(bool)            # string to boolean

# แปลงหลาย columns พร้อมกัน
df = df.astype({
    'A': int,
    'B': float,
    'D': bool
})

# การจัดการ errors ในการแปลง
df_mixed = pd.DataFrame({'col': ['1', '2', 'text', '4']})
df_mixed['col_numeric'] = pd.to_numeric(df_mixed['col'], errors='coerce')  # NaN สำหรับ errors
```

### การทำความสะอาด String Data

```python
# สร้างข้อมูลที่ต้องทำความสะอาด
df_messy = pd.DataFrame({
    'Name': ['  Alice  ', 'BOB', 'charlie brown', 'DIANA'],
    'Email': ['ALICE@GMAIL.COM', 'bob@yahoo.com', 'Charlie@Gmail.com', 'diana@OUTLOOK.COM'],
    'Phone': ['123-456-7890', '(234) 567-8901', '345.678.9012', '456 789 0123']
})

# ทำความสะอาด strings
df_clean = df_messy.copy()

# ลบช่องว่างข้างหน้าและข้างหลัง
df_clean['Name'] = df_clean['Name'].str.strip()

# แปลงเป็นตัวพิมพ์เล็ก/ใหญ่
df_clean['Email'] = df_clean['Email'].str.lower()
df_clean['Name'] = df_clean['Name'].str.title()  # Title Case

# แทนที่ characters
df_clean['Phone'] = df_clean['Phone'].str.replace(r'[^\d]', '', regex=True)  # เก็บแต่ตัวเลข

# Split strings
name_parts = df_clean['Name'].str.split(' ', expand=True)
name_parts.columns = ['First_Name', 'Last_Name']

# Extract patterns ด้วย regex
email_domain = df_clean['Email'].str.extract(r'@(.+)')
email_domain.columns = ['Domain']

print(df_clean)
```

### การตรวจสอบและแก้ไข Outliers

```python
import matplotlib.pyplot as plt

# สร้างข้อมูลที่มี outliers
np.random.seed(42)
normal_data = np.random.normal(50, 10, 95)
outliers = [120, 130, -20, -10, 200]
data_with_outliers = np.concatenate([normal_data, outliers])

df_outliers = pd.DataFrame({'value': data_with_outliers})

# วิธีที่ 1: Z-Score Method
z_scores = np.abs((df_outliers['value'] - df_outliers['value'].mean()) / df_outliers['value'].std())
outlier_zscore = df_outliers[z_scores > 3]
print(f"Outliers by Z-score: {len(outlier_zscore)}")

# วิธีที่ 2: IQR Method
Q1 = df_outliers['value'].quantile(0.25)
Q3 = df_outliers['value'].quantile(0.75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outlier_iqr = df_outliers[(df_outliers['value'] < lower_bound) | 
                          (df_outliers['value'] > upper_bound)]
print(f"Outliers by IQR: {len(outlier_iqr)}")

# การจัดการ outliers
# 1. ลบ outliers
df_no_outliers = df_outliers[(df_outliers['value'] >= lower_bound) & 
                             (df_outliers['value'] <= upper_bound)]

# 2. Cap outliers (winsorizing)
df_capped = df_outliers.copy()
df_capped['value'] = df_capped['value'].clip(lower_bound, upper_bound)

# 3. Transform data
df_log = df_outliers.copy()
df_log['value_log'] = np.log1p(df_log['value'] - df_log['value'].min() + 1)
```

---

## Data Transformation

### การสร้าง Columns ใหม่

```python
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'Salary': [50000, 60000, 70000, 55000],
    'Years_Experience': [3, 8, 12, 5]
})

# สร้าง column ใหม่จากการคำนวณ
df['Salary_per_year_exp'] = df['Salary'] / df['Years_Experience']
df['Age_Group'] = df['Age'].apply(lambda x: 'Young' if x < 30 else 'Senior')

# ใช้ np.where สำหรับ conditional logic
df['Performance'] = np.where(df['Salary'] > 60000, 'High', 'Normal')

# ใช้ pd.cut สำหรับ binning
df['Age_Bin'] = pd.cut(df['Age'], bins=[0, 25, 30, 35, 100], 
                       labels=['Very Young', 'Young', 'Middle', 'Senior'])

# Multiple conditions
conditions = [
    (df['Age'] < 30) & (df['Salary'] > 55000),
    (df['Age'] >= 30) & (df['Salary'] > 65000),
    (df['Age'] >= 30) & (df['Salary'] <= 65000)
]
choices = ['High Potential', 'Senior High Performer', 'Senior Normal']
df['Category'] = np.select(conditions, choices, default='Other')

print(df)
```

### การใช้ Apply Functions

```python
# Apply function กับ Series
def categorize_salary(salary):
    if salary < 55000:
        return 'Low'
    elif salary < 65000:
        return 'Medium'
    else:
        return 'High'

df['Salary_Category'] = df['Salary'].apply(categorize_salary)

# Apply กับ lambda function
df['Name_Length'] = df['Name'].apply(lambda x: len(x))
df['Salary_K'] = df['Salary'].apply(lambda x: f"{x/1000:.0f}K")

# Apply กับ DataFrame (axis=1 สำหรับ rows)
def calculate_bonus(row):
    base_bonus = row['Salary'] * 0.1
    experience_bonus = row['Years_Experience'] * 1000
    return base_bonus + experience_bonus

df['Bonus'] = df.apply(calculate_bonus, axis=1)

# Apply กับหลาย columns
df['Salary_Age_Ratio'] = df.apply(lambda row: row['Salary'] / row['Age'], axis=1)
```

### Map และ Replace

```python
# Map ด้วย dictionary
age_mapping = {25: 'Young', 30: 'Middle', 35: 'Senior', 28: 'Young'}
df['Age_Category'] = df['Age'].map(age_mapping)

# Map ด้วย Series
salary_avg = df.groupby('Age_Group')['Salary'].mean()
df['Avg_Salary_for_Group'] = df['Age_Group'].map(salary_avg)

# Replace values
df_replace = df.copy()
df_replace['Name'] = df_replace['Name'].replace('Alice', 'Alicia')
df_replace['Performance'] = df_replace['Performance'].replace({'High': 'Excellent', 'Normal': 'Good'})

# Replace with regex
df_replace['Name'] = df_replace['Name'].str.replace(r'[aeiou]', 'X', regex=True)
```

### Pivot Tables และ Reshaping

```python
# สร้างข้อมูลตัวอย่างสำหรับ pivot
sales_data = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=12, freq='M'),
    'Product': ['A', 'B', 'A', 'B', 'A', 'B', 'A', 'B', 'A', 'B', 'A', 'B'],
    'Region': ['North', 'North', 'South', 'South', 'North', 'North', 
               'South', 'South', 'North', 'North', 'South', 'South'],
    'Sales': [100, 150, 120, 180, 110, 160, 130, 190, 105, 155, 125, 195]
})

# Pivot table
pivot_table = sales_data.pivot_table(
    values='Sales',
    index='Product',
    columns='Region',
    aggfunc='mean'
)
print(pivot_table)

# Melt (inverse of pivot)
melted = pivot_table.reset_index().melt(
    id_vars='Product',
    var_name='Region',
    value_name='Average_Sales'
)
print(melted)

# Stack และ Unstack
stacked = pivot_table.stack()
unstacked = stacked.unstack()
```

---

## Groupby Operations

### พื้นฐาน Groupby

```python
# สร้างข้อมูลตัวอย่าง
employees = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank'],
    'Department': ['IT', 'HR', 'IT', 'Finance', 'IT', 'HR'],
    'Age': [25, 30, 35, 28, 32, 27],
    'Salary': [50000, 60000, 70000, 55000, 65000, 58000],
    'Years_Experience': [3, 8, 12, 5, 9, 6]
})

# Basic groupby operations
dept_groups = employees.groupby('Department')

# Aggregation functions
print(dept_groups.mean())              # ค่าเฉลี่ย
print(dept_groups.sum())               # ผลรวม
print(dept_groups.count())             # จำนวน
print(dept_groups.std())               # ส่วนเบี่ยงเบนมาตรฐาน
print(dept_groups.describe())          # สถิติโดยรวม

# เลือก column เฉพาะ
print(dept_groups['Salary'].mean())
print(dept_groups[['Salary', 'Age']].mean())
```

### Advanced Groupby Operations

```python
# Multiple groupby columns
age_dept_groups = employees.groupby(['Department', 'Age'])
print(age_dept_groups.size())          # จำนวนใน group

# Custom aggregation functions
def salary_range(series):
    return series.max() - series.min()

custom_agg = employees.groupby('Department')['Salary'].agg([
    'mean',
    'median',
    'std',
    ('range', salary_range),
    ('count', 'count')
])
print(custom_agg)

# Different aggregations for different columns
multi_agg = employees.groupby('Department').agg({
    'Salary': ['mean', 'max', 'min'],
    'Age': ['mean', 'std'],
    'Years_Experience': 'mean'
})
print(multi_agg)

# Apply custom functions
def department_analysis(group):
    return pd.Series({
        'avg_salary': group['Salary'].mean(),
        'max_experience': group['Years_Experience'].max(),
        'avg_age': group['Age'].mean(),
        'salary_per_experience': group['Salary'].sum() / group['Years_Experience'].sum()
    })

dept_analysis = employees.groupby('Department').apply(department_analysis)
print(dept_analysis)
```

### Transform และ Filter

```python
# Transform - สร้างข้อมูลขนาดเดียวกับ original
employees['Dept_Avg_Salary'] = employees.groupby('Department')['Salary'].transform('mean')
employees['Salary_vs_Dept_Avg'] = employees['Salary'] - employees['Dept_Avg_Salary']
employees['Salary_Rank_in_Dept'] = employees.groupby('Department')['Salary'].rank(ascending=False)

# Filter - กรอง groups ที่ตรงเงื่อนไข
large_departments = employees.groupby('Department').filter(lambda x: len(x) >= 2)
high_avg_salary_depts = employees.groupby('Department').filter(lambda x: x['Salary'].mean() > 60000)

print(employees)
print("\nLarge departments:")
print(large_departments)
```

### Rolling และ Expanding Operations

```python
# สร้างข้อมูล time series
dates = pd.date_range('2023-01-01', periods=100, freq='D')
ts_data = pd.DataFrame({
    'Date': dates,
    'Value': np.random.randn(100).cumsum() + 100
})
ts_data.set_index('Date', inplace=True)

# Rolling operations
ts_data['Rolling_Mean_7'] = ts_data['Value'].rolling(window=7).mean()
ts_data['Rolling_Std_7'] = ts_data['Value'].rolling(window=7).std()
ts_data['Rolling_Max_7'] = ts_data['Value'].rolling(window=7).max()

# Expanding operations (ตั้งแต่เริ่มต้นถึงจุดปัจจุบัน)
ts_data['Expanding_Mean'] = ts_data['Value'].expanding().mean()
ts_data['Expanding_Std'] = ts_data['Value'].expanding().std()

# Rolling กับ groupby
grouped_employees = employees.copy()
grouped_employees['Salary_Rank_Overall'] = grouped_employees['Salary'].rank(ascending=False)

print(ts_data.head(10))
```

---

## Merging และ Joining

### การรวม DataFrames

```python
# สร้างข้อมูลตัวอย่าง
employees = pd.DataFrame({
    'EmployeeID': [1, 2, 3, 4, 5],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'DepartmentID': [101, 102, 101, 103, 102]
})

departments = pd.DataFrame({
    'DepartmentID': [101, 102, 103, 104],
    'Department': ['IT', 'HR', 'Finance', 'Marketing'],
    'Location': ['Building A', 'Building B', 'Building C', 'Building D']
})

salaries = pd.DataFrame({
    'EmployeeID': [1, 2, 3, 4, 6],
    'Salary': [50000, 60000, 70000, 55000, 48000],
    'Bonus': [5000, 6000, 7000, 5500, 4800]
})
```

#### Inner Join
```python
# Inner join - เก็บเฉพาะ records ที่มีใน table ทั้งสอง
emp_dept = pd.merge(employees, departments, on='DepartmentID', how='inner')
print("Inner Join:")
print(emp_dept)

emp_salary = pd.merge(employees, salaries, on='EmployeeID', how='inner')
print("\nEmployee-Salary Inner Join:")
print(emp_salary)
```

#### Left, Right, และ Outer Joins
```python
# Left join - เก็บทุก records จาก left table
left_join = pd.merge(employees, salaries, on='EmployeeID', how='left')
print("Left Join:")
print(left_join)

# Right join - เก็บทุก records จาก right table
right_join = pd.merge(employees, salaries, on='EmployeeID', how='right')
print("Right Join:")
print(right_join)

# Outer join - เก็บทุก records จากทั้งสอง tables
outer_join = pd.merge(employees, salaries, on='EmployeeID', how='outer')
print("Outer Join:")
print(outer_join)
```

#### Advanced Merging
```python
# Merge กับ different column names
emp_modified = employees.rename(columns={'EmployeeID': 'EmpID'})
merge_diff_names = pd.merge(emp_modified, salaries, 
                           left_on='EmpID', right_on='EmployeeID')

# Merge กับหลาย columns
combined_data = pd.merge(
    pd.merge(employees, departments, on='DepartmentID'),
    salaries, on='EmployeeID', how='left'
)
print("Complete Employee Data:")
print(combined_data)

# Merge กับ suffixes สำหรับ column ที่ชื่อซ้ำ
df1 = pd.DataFrame({'key': ['A', 'B', 'C'], 'value': [1, 2, 3]})
df2 = pd.DataFrame({'key': ['A', 'B', 'D'], 'value': [4, 5, 6]})
merged_suffix = pd.merge(df1, df2, on='key', how='outer', suffixes=('_left', '_right'))
print("Merge with suffixes:")
print(merged_suffix)
```

### Concatenation

```python
# สร้างข้อมูลตัวอย่าง
df1 = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6]
})

df2 = pd.DataFrame({
    'A': [7, 8, 9],
    'B': [10, 11, 12]
})

df3 = pd.DataFrame({
    'C': [13, 14, 15],
    'D': [16, 17, 18]
})

# Vertical concatenation (เพิ่มแถว)
vertical_concat = pd.concat([df1, df2], axis=0, ignore_index=True)
print("Vertical Concatenation:")
print(vertical_concat)

# Horizontal concatenation (เพิ่ม columns)
horizontal_concat = pd.concat([df1, df3], axis=1)
print("Horizontal Concatenation:")
print(horizontal_concat)

# Concatenation กับ keys
keyed_concat = pd.concat([df1, df2], keys=['Group1', 'Group2'])
print("Concatenation with keys:")
print(keyed_concat)
```

### Join Method

```python
# ใช้ join method (เหมาะกับ index-based joining)
df_indexed1 = employees.set_index('EmployeeID')
df_indexed2 = salaries.set_index('EmployeeID')

# Join (default เป็น left join)
joined = df_indexed1.join(df_indexed2)
print("Join result:")
print(joined)

# Join กับ different join types
inner_joined = df_indexed1.join(df_indexed2, how='inner')
outer_joined = df_indexed1.join(df_indexed2, how='outer')
```

---

## Time Series Analysis

### การจัดการ Datetime

```python
# สร้าง datetime data
dates = pd.date_range('2023-01-01', periods=100, freq='D')
ts_data = pd.DataFrame({
    'Date': dates,
    'Sales': np.random.randint(100, 1000, 100),
    'Temperature': np.random.normal(25, 5, 100)
})

# แปลง string เป็น datetime
date_strings = ['2023-01-01', '2023-01-02', '2023-01-03']
converted_dates = pd.to_datetime(date_strings)

# Parse datetime จาก format เฉพาะ
custom_dates = ['01/15/2023', '02/15/2023', '03/15/2023']
parsed_dates = pd.to_datetime(custom_dates, format='%m/%d/%Y')

# Set datetime เป็น index
ts_data.set_index('Date', inplace=True)
print(ts_data.head())
```

### Time-based Indexing และ Slicing

```python
# เลือกข้อมูลตาม date range
jan_data = ts_data['2023-01']                    # ข้อมูลเดือนมกราคม
first_week = ts_data['2023-01-01':'2023-01-07']  # สัปดาห์แรก
recent_data = ts_data.last('30D')                # 30 วันล่าสุด

# เลือกข้อมูลเฉพาะวัน
mondays = ts_data[ts_data.index.dayofweek == 0]  # วันจันทร์
weekends = ts_data[ts_data.index.dayofweek.isin([5, 6])]  # เสาร์-อาทิตย์

# เลือกข้อมูลเฉพาะเวลา (ถ้ามี time component)
ts_hourly = pd.DataFrame({
    'Datetime': pd.date_range('2023-01-01', periods=48, freq='H'),
    'Value': np.random.randn(48)
}).set_index('Datetime')

business_hours = ts_hourly.between_time('09:00', '17:00')
```

### Resampling และ Frequency Conversion

```python
# สร้างข้อมูลรายวัน
daily_data = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=365, freq='D'),
    'Sales': np.random.randint(100, 1000, 365),
    'Visitors': np.random.randint(50, 500, 365)
}).set_index('Date')

# Upsample (เพิ่มความถี่)
hourly_upsampled = daily_data.resample('H').interpolate()

# Downsample (ลดความถี่)
weekly_data = daily_data.resample('W').agg({
    'Sales': 'sum',
    'Visitors': 'mean'
})

monthly_data = daily_data.resample('M').agg({
    'Sales': ['sum', 'mean', 'std'],
    'Visitors': ['mean', 'max', 'min']
})

quarterly_data = daily_data.resample('Q').sum()

print("Weekly aggregated data:")
print(weekly_data.head())
```

### Time-based Calculations

```python
# Shift operations
daily_data['Sales_Previous_Day'] = daily_data['Sales'].shift(1)
daily_data['Sales_Next_Day'] = daily_data['Sales'].shift(-1)
daily_data['Sales_Weekly_Lag'] = daily_data['Sales'].shift(7)

# Percentage change
daily_data['Sales_Pct_Change'] = daily_data['Sales'].pct_change()
daily_data['Sales_Pct_Change_Weekly'] = daily_data['Sales'].pct_change(periods=7)

# Cumulative operations
daily_data['Sales_Cumsum'] = daily_data['Sales'].cumsum()
daily_data['Sales_Cummax'] = daily_data['Sales'].cummax()

# Rolling statistics
daily_data['Sales_MA_7'] = daily_data['Sales'].rolling(window=7).mean()
daily_data['Sales_MA_30'] = daily_data['Sales'].rolling(window=30).mean()
daily_data['Sales_Std_7'] = daily_data['Sales'].rolling(window=7).std()

# Expanding statistics
daily_data['Sales_Expanding_Mean'] = daily_data['Sales'].expanding().mean()

print(daily_data[['Sales', 'Sales_MA_7', 'Sales_MA_30']].head(10))
```

### Time Zone Handling

```python
# สร้างข้อมูลกับ timezone
utc_data = pd.DataFrame({
    'Datetime': pd.date_range('2023-01-01', periods=24, freq='H', tz='UTC'),
    'Value': np.random.randn(24)
}).set_index('Datetime')

# แปลง timezone
bkk_data = utc_data.tz_convert('Asia/Bangkok')
ny_data = utc_data.tz_convert('America/New_York')

# Localize timezone (สำหรับข้อมูลที่ไม่มี timezone)
naive_data = pd.DataFrame({
    'Datetime': pd.date_range('2023-01-01', periods=24, freq='H'),
    'Value': np.random.randn(24)
}).set_index('Datetime')

localized_data = naive_data.tz_localize('Asia/Bangkok')
```

---

## Visualization

### การใช้ Pandas Plot

```python
import matplotlib.pyplot as plt

# สร้างข้อมูลตัวอย่าง
data = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=100, freq='D'),
    'Sales': np.random.randint(100, 1000, 100),
    'Profit': np.random.randint(10, 100, 100),
    'Category': np.random.choice(['A', 'B', 'C'], 100)
}).set_index('Date')

# Line plot
data['Sales'].plot(kind='line', title='Sales Over Time', figsize=(10, 6))
plt.show()

# Multiple lines
data[['Sales', 'Profit']].plot(kind='line', title='Sales and Profit', figsize=(10, 6))
plt.show()

# Bar plot
monthly_sales = data.resample('M')['Sales'].sum()
monthly_sales.plot(kind='bar', title='Monthly Sales', figsize=(10, 6))
plt.show()

# Histogram
data['Sales'].plot(kind='hist', bins=20, title='Sales Distribution', figsize=(8, 6))
plt.show()

# Box plot
data.boxplot(column=['Sales', 'Profit'], figsize=(8, 6))
plt.show()

# Scatter plot
data.plot(kind='scatter', x='Sales', y='Profit', title='Sales vs Profit', figsize=(8, 6))
plt.show()
```

### Advanced Plotting

```python
# Group by plots
category_data = data.groupby('Category')['Sales'].sum()
category_data.plot(kind='pie', title='Sales by Category', figsize=(8, 8))
plt.show()

# Subplots
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

data['Sales'].plot(ax=axes[0,0], title='Sales')
data['Profit'].plot(ax=axes[0,1], title='Profit')
data['Sales'].hist(ax=axes[1,0], bins=20, title='Sales Distribution')
data.plot(kind='scatter', x='Sales', y='Profit', ax=axes[1,1], title='Sales vs Profit')

plt.tight_layout()
plt.show()

# Rolling average plot
data['Sales_MA'] = data['Sales'].rolling(window=10).mean()
data[['Sales', 'Sales_MA']].plot(title='Sales with Moving Average', figsize=(12, 6))
plt.show()
```

---

## Performance Optimization

### Memory Optimization

```python
# ตรวจสอบการใช้ memory
def memory_usage(df):
    return df.memory_usage(deep=True).sum() / 1024 / 1024  # MB

# สร้างข้อมูลตัวอย่าง
large_df = pd.DataFrame({
    'int_col': np.random.randint(0, 100, 1000000),
    'float_col': np.random.random(1000000),
    'str_col': np.random.choice(['A', 'B', 'C', 'D'], 1000000)
})

print(f"Original memory usage: {memory_usage(large_df):.2f} MB")

# Optimize data types
optimized_df = large_df.copy()

# Integer optimization
optimized_df['int_col'] = pd.to_numeric(optimized_df['int_col'], downcast='integer')

# Float optimization
optimized_df['float_col'] = pd.to_numeric(optimized_df['float_col'], downcast='float')

# Category optimization สำหรับ string ที่มีค่าซ้ำๆ
optimized_df['str_col'] = optimized_df['str_col'].astype('category')

print(f"Optimized memory usage: {memory_usage(optimized_df):.2f} MB")
print(f"Memory reduction: {(memory_usage(large_df) - memory_usage(optimized_df))/memory_usage(large_df)*100:.1f}%")

# ตรวจสอบ data types
print("\nOriginal dtypes:")
print(large_df.dtypes)
print("\nOptimized dtypes:")
print(optimized_df.dtypes)
```

### Vectorization vs Loops

```python
import time

# สร้างข้อมูลขนาดใหญ่
df_large = pd.DataFrame({
    'A': np.random.randint(1, 100, 100000),
    'B': np.random.randint(1, 100, 100000)
})

# Method 1: Loop (ช้า)
start_time = time.time()
result_loop = []
for i in range(len(df_large)):
    result_loop.append(df_large.iloc[i]['A'] * df_large.iloc[i]['B'])
df_large['Result_Loop'] = result_loop
loop_time = time.time() - start_time

# Method 2: Vectorization (เร็ว)
start_time = time.time()
df_large['Result_Vectorized'] = df_large['A'] * df_large['B']
vectorized_time = time.time() - start_time

# Method 3: Apply (กลาง)
start_time = time.time()
df_large['Result_Apply'] = df_large.apply(lambda row: row['A'] * row['B'], axis=1)
apply_time = time.time() - start_time

print(f"Loop time: {loop_time:.4f} seconds")
print(f"Vectorized time: {vectorized_time:.4f} seconds")
print(f"Apply time: {apply_time:.4f} seconds")
print(f"Vectorization speedup: {loop_time/vectorized_time:.1f}x")
```

### Efficient Data Loading

```python
# การอ่านไฟล์อย่างมีประสิทธิภาพ
def efficient_csv_reading():
    # อ่านเฉพาะ columns ที่ต้องการ
    df = pd.read_csv('large_file.csv', usecols=['col1', 'col2', 'col3'])
    
    # กำหนด data types ล่วงหน้า
    dtypes = {
        'col1': 'int32',
        'col2': 'category',
        'col3': 'float32'
    }
    df = pd.read_csv('large_file.csv', dtype=dtypes)
    
    # อ่านทีละ chunk สำหรับไฟล์ขนาดใหญ่
    chunk_size = 10000
    chunks = []
    for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
        # ประมวลผล chunk
        processed_chunk = chunk.groupby('category').sum()
        chunks.append(processed_chunk)
    
    # รวม chunks
    result = pd.concat(chunks, ignore_index=True)
    return result

# การใช้ compression
df = pd.read_csv('data.csv.gz', compression='gzip')  # อ่านไฟล์ที่ compress
df.to_csv('output.csv.gz', compression='gzip', index=False)  # บันทึกแบบ compress
```

### Query Optimization

```python
# ใช้ query แทน boolean indexing สำหรับ performance ที่ดีกว่า
large_df = pd.DataFrame({
    'A': np.random.randint(1, 1000, 1000000),
    'B': np.random.randint(1, 1000, 1000000),
    'C': np.random.choice(['X', 'Y', 'Z'], 1000000)
})

# Slow: boolean indexing
start_time = time.time()
result1 = large_df[(large_df['A'] > 500) & (large_df['B'] < 300) & (large_df['C'] == 'X')]
boolean_time = time.time() - start_time

# Fast: query method
start_time = time.time()
result2 = large_df.query('A > 500 and B < 300 and C == "X"')
query_time = time.time() - start_time

print(f"Boolean indexing: {boolean_time:.4f} seconds")
print(f"Query method: {query_time:.4f} seconds")
```

---

---

## ตัวอย่างการปฏิบัติ

### ตัวอย่างที่ 1: การใช้ Python Pandas

```python
import pandas as pd
import numpy as np

# โหลดข้อมูล
df = pd.read_csv('data.csv')

# 1. ตรวจสอบข้อมูลเบื้องต้น
print(df.info())
print(df.describe())
print(df.isnull().sum())

# 2. จัดการ Missing Data
# ลบแถวที่มี missing values
df_clean = df.dropna()

# หรือเติมด้วย mean
df['age'].fillna(df['age'].mean(), inplace=True)

# 3. กำจัดข้อมูลซ้ำ
df_clean = df.drop_duplicates()

# 4. แก้ไขข้อมูลไม่สอดคล้อง
df['country'] = df['country'].str.lower().str.strip()

# 5. จัดการ Outliers (ใช้ IQR method)
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

df_clean = df[(df['salary'] >= lower_bound) & 
              (df['salary'] <= upper_bound)]

# 6. บันทึกข้อมูลที่สะอาดแล้ว
df_clean.to_csv('cleaned_data.csv', index=False)
```

### ตัวอย่างที่ 2: การใช้ SQL

```sql
-- ลบข้อมูลซ้ำ
DELETE t1 FROM customers t1
INNER JOIN customers t2 
WHERE t1.id > t2.id 
AND t1.email = t2.email;

-- แก้ไขข้อมูลไม่สอดคล้อง
UPDATE customers 
SET country = UPPER(TRIM(country));

-- ลบข้อมูลที่ไม่ถูกต้อง
DELETE FROM customers 
WHERE age < 0 OR age > 150;
```

---

## Best Practices

### หลักการสำคัญ
1. **สำรองข้อมูลต้นฉบับ**: อย่าลืมสำรองข้อมูลเดิมก่อนทำการแก้ไข
2. **บันทึกขั้นตอน**: จดบันทึกทุกขั้นตอนที่ทำเพื่อให้สามารถย้อนกลับได้
3. **ตรวจสอบผลลัพธ์**: ตรวจสอบผลลัพธ์หลังจากแต่ละขั้นตอน
4. **ใช้เครื่องมือที่เหมาะสม**: เลือกเครื่องมือที่เหมาะกับข้อมูลและงาน

### Checklist สำหรับ Data Cleaning
- [ ] ตรวจสอบ Data Types
- [ ] หา Missing Values
- [ ] ตรวจสอบข้อมูลซ้ำ
- [ ] ตรวจสอบความสอดคล้องของข้อมูล
- [ ] หา Outliers
- [ ] ตรวจสอบ Range ของข้อมูล
- [ ] ตรวจสอบ Format ของข้อมูล
- [ ] สร้างรายงานสรุป

### ข้อผิดพลาดที่ควรหลีกเลี่ยง
1. **ลบข้อมูลมากเกินไป**: อาจทำให้เสียข้อมูลสำคัญ
2. **ไม่ตรวจสอบ Business Logic**: การแก้ไขควรสอดคล้องกับความหมายทางธุรกิจ
3. **ไม่สำรองข้อมูลเดิม**: อาจไม่สามารถย้อนกลับได้
4. **ใช้วิธีเดียวกันกับทุกปัญหา**: แต่ละปัญหาต้องใช้วิธีที่เหมาะสม

---

## แบบฝึกหัด

### แบบฝึกหัดที่ 1: ระบุปัญหา
ให้ระบุปัญหาในข้อมูลต่อไปนี้:

```
ID | Name     | Age | Email           | Salary
---|----------|-----|-----------------|--------
1  | John Doe | 25  | john@email.com  | 50000
2  | Mary     |     | mary@email.com  | 60000
3  | JOHN DOE | 25  | john@email.com  | 50000
4  | Peter    | -5  | notanemail      | 999999999
5  | Sarah    | 30  | sarah@email.com |
```

### แบบฝึกหัดที่ 2: เขียน Code
เขียน Python code เพื่อ:
1. โหลดข้อมูลจากไฟล์ CSV
2. ตรวจสอบ Missing Values
3. กำจัดข้อมูลซ้ำ
4. แก้ไขข้อมูลที่ไม่ถูกต้อง

### แบบฝึกหัดที่ 3: Case Study
ให้นักเรียนวิเคราะห์ชุดข้อมูลจริงและเสนอแผนการทำ Data Cleaning

---

## สรุป

Data Cleaning เป็นขั้นตอนสำคัญที่สุดในกระบวนการวิเคราะห์ข้อมูล การมีข้อมูลที่สะอาดและมีคุณภาพจะนำไปสู่ผลลัพธ์การวิเคราะห์ที่เชื่อถือได้และการตัดสินใจที่ถูกต้อง

### จุดสำคัญที่ต้องจำ
- Data Cleaning ใช้เวลามากที่สุดในกระบวนการวิเคราะห์ข้อมูล
- ต้องเข้าใจปัญหาก่อนเลือกวิธีแก้ไข
- การสำรองข้อมูลและบันทึกขั้นตอนเป็นสิ่งสำคัญ
- ไม่มีวิธีการเดียวที่เหมาะกับทุกสถานการณ์

---

**หมายเหตุ**: เอกสารนี้เป็นคู่มือเบื้องต้น สำหรับการเรียนรู้เพิ่มเติม แนะนำให้ฝึกปฏิบัติกับข้อมูลจริงและศึกษาเทคนิคขั้นสูงเพิ่มเติม


### แบบฝึกหัดที่ 2: Data Cleaning (20 คะแนน)

#### ข้อ 2.1 (10 คะแนน)
จากข้อมูลที่มีปัญหาต่อไปนี้ ให้ทำความสะอาด:

```python
messy_data = pd.DataFrame({
    'Name': ['  Alice  ', 'BOB', 'charlie brown', '  DIANA', 'Eve'],
    'Age': [25, 'thirty', 35, np.nan, '28'],
    'Email': ['alice@gmail.com', 'BOB@YAHOO.COM', 'charlie@gmail.com', 'diana@', 'eve@outlook.com'],
    'Salary': ['50,000', '60000', 'sixty thousand', '55,000', np.nan],
    'Phone': ['123-456-7890', '(234) 567-8901', '345.678.9012', '456 789 0123', '567-890-1234'],
    'Date_Joined': ['2023-01-01', '2023/02/15', '01-03-2023', '2023.04.10', '2023-05-20']
})

# TODO: ทำความสะอาดข้อมูล
# 1. ทำความสะอาด Name column (trim, proper case)
# 2. แปลง Age เป็น numeric (handle text values)
# 3. ทำความสะอาด Email (lowercase, validate format)
# 4. แปลง Salary เป็น numeric (remove commas, handle text)
# 5. จัดรูปแบบ Phone ให้เป็น xxx-xxx-xxxx
# 6. แปลง Date_Joined เป็น datetime
# 7. จัดการ missing values ด้วยวิธีที่เหมาะสม
```

#### ข้อ 2.2 (10 คะแนน)
เขียนฟังก์ชัน data cleaning pipeline:

```python
def clean_employee_data(df):
    """
    Data cleaning pipeline สำหรับข้อมูลพนักงาน
    
    Parameters:
    df: DataFrame ที่มี columns: Name, Age, Email, Salary, Phone, Date_Joined
    
    Returns:
    DataFrame ที่ทำความสะอาดแล้ว
    
    Cleaning steps:
    1. Remove leading/trailing spaces from string columns
    2. Convert text ages to numeric
    3. Standardize email format (lowercase)
    4. Convert salary strings to numeric
    5. Standardize phone format
    6. Convert date strings to datetime
    7. Handle missing values appropriately
    8. Remove duplicates
    9. Add validation flags for invalid data
    """
    # TODO: implement cleaning pipeline
    pass

# ทดสอบ pipeline
cleaned_data = clean_employee_data(messy_data)
print("Cleaned data:")
print(cleaned_data)
print(f"\nData types after cleaning:\n{cleaned_data.dtypes}")
```

### แบบฝึกหัดที่ 3: Groupby และ Aggregation (20 คะแนน)

#### ข้อ 3.1 (10 คะแนน)
วิเคราะห์ข้อมูลการขายต่อไปนี้:

```python
sales_analysis = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=365, freq='D'),
    'Product': np.random.choice(['Laptop', 'Phone', 'Tablet', 'Watch'], 365),
    'Category': np.random.choice(['Electronics', 'Accessories'], 365),
    'Region': np.random.choice(['North', 'South', 'East', 'West'], 365),
    'Salesperson': np.random.choice(['Alice', 'Bob', 'Charlie', 'Diana'], 365),
    'Units_Sold': np.random.randint(1, 20, 365),
    'Unit_Price': np.random.randint(100, 2000, 365)
})
sales_analysis['Total_Sales'] = sales_analysis['Units_Sold'] * sales_analysis['Unit_Price']

# TODO: วิเคราะห์ข้อมูล
# 1. ยอดขายรวมและเฉลี่ยของแต่ละสินค้า
# 2. Top 3 salesperson ที่มียอดขายสูงสุด
# 3. เปรียบเทียบยอดขายระหว่างภูมิภาคในแต่ละเดือน
# 4. ผลิตภัณฑ์ที่ขายดีที่สุดในแต่ละไตรมาส
# 5. Seasonal analysis: ยอดขายเฉลี่ยในแต่ละเดือน
```

#### ข้อ 3.2 (10 คะแนน)
สร้าง advanced aggregation functions:

```python
def sales_metrics(group):
    """
    คำนวณ metrics สำหรับยอดขาย
    
    Returns:
    Series ที่มี:
    - total_sales: ยอดขายรวม
    - avg_sales: ยอดขายเฉลี่ย
    - sales_std: ส่วนเบี่ยงเบนมาตรฐาน
    - max_sales: ยอดขายสูงสุด
    - min_sales: ยอดขายต่ำสุด
    - sales_range: ความแตกต่างระหว่างสูงสุดและต่ำสุด
    - coefficient_of_variation: CV
    """
    # TODO: implement metrics calculation
    pass

def product_performance_analysis(df, date_col, product_col, sales_col):
    """
    วิเคราะห์ performance ของสินค้า
    
    Parameters:
    df: DataFrame
    date_col: ชื่อ column ที่เป็น date
    product_col: ชื่อ column ที่เป็น product
    sales_col: ชื่อ column ที่เป็น sales
    
    Returns:
    DataFrame ที่มี analysis results สำหรับแต่ละสินค้า
    """
    # TODO: implement product analysis
    pass

# ทดสอบฟังก์ชัน
metrics_result = sales_analysis.groupby('Product').apply(sales_metrics)
performance_result = product_performance_analysis(sales_analysis, 'Date', 'Product', 'Total_Sales')
```

### แบบฝึกหัดที่ 4: Time Series และ Merging (25 คะแนน)

#### ข้อ 4.1 (15 คะแนน)
วิเคราะห์ time series data:

```python
# สร้างข้อมูล stock prices
stock_data = pd.DataFrame({
    'Date': pd.date_range('2023-01-01', periods=252, freq='B'),  # Business days
    'AAPL': np.random.randn(252).cumsum() + 150,
    'GOOGL': np.random.randn(252).cumsum() + 2500,
    'MSFT': np.random.randn(252).cumsum() + 250,
    'TSLA': np.random.randn(252).cumsum() + 200
}).set_index('Date')

# TODO: Time series analysis
# 1. คำนวณ daily returns สำหรับแต่ละหุ้น
# 2. คำนวณ 20-day และ 50-day moving averages
# 3. หา correlation matrix ระหว่างหุ้นต่างๆ
# 4. คำนวณ monthly returns โดยใช้ resampling
# 5. หาวันที่มี volatility สูงสุด (ใช้ rolling standard deviation)
# 6. สร้าง simple trading signal: ซื้อเมื่อ 20-day MA > 50-day MA
```

#### ข้อ 4.2 (10 คะแนน)
Merging และ joining exercises:

```python
# ข้อมูลตาราง
customers = pd.DataFrame({
    'CustomerID': [1, 2, 3, 4, 5],
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'City': ['Bangkok', 'Chiang Mai', 'Phuket', 'Bangkok', 'Pattaya'],
    'Age': [25, 30, 35, 28, 32]
})

orders = pd.DataFrame({
    'OrderID': [101, 102, 103, 104, 105, 106],
    'CustomerID': [1, 2, 1, 3, 2, 6],
    'Product': ['Laptop', 'Phone', 'Tablet', 'Watch', 'Laptop', 'Phone'],
    'Amount': [50000, 25000, 15000, 8000, 52000, 26000],
    'Order_Date': pd.date_range('2023-01-01', periods=6, freq='10D')
})

products = pd.DataFrame({
    'Product': ['Laptop', 'Phone', 'Tablet', 'Watch', 'Headphones'],
    'Category': ['Computer', 'Mobile', 'Computer', 'Wearable', 'Audio'],
    'Cost': [40000, 20000, 12000, 6000, 3000]
})

# TODO: Merging exercises
# 1. รวม customers และ orders (แสดงลูกค้าทั้งหมดรวมถึงคนที่ไม่เคยสั่งซื้อ)
# 2. รวม orders และ products เพื่อหา profit ของแต่ละ order
# 3. สร้าง comprehensive report ที่รวมข้อมูลทั้งสามตาราง
# 4. หาลูกค้าที่ใช้จ่ายมากที่สุดในแต่ละเมือง
# 5. วิเคราะห์ยอดขายตาม category และ customer demographics
```

### แบบฝึกหัดที่ 5: Advanced Operations (20 คะแนน)

#### ข้อ 5.1 (10 คะแนน)
การใช้ pivot tables และ reshaping:

```python
# สร้างข้อมูล survey
survey_data = pd.DataFrame({
    'RespondentID': range(1, 101),
    'Age_Group': np.random.choice(['18-25', '26-35', '36-45', '46-55', '55+'], 100),
    'Gender': np.random.choice(['Male', 'Female', 'Other'], 100),
    'Region': np.random.choice(['Bangkok', 'North', 'Northeast', 'Central', 'South'], 100),
    'Product_A_Rating': np.random.randint(1, 6, 100),
    'Product_B_Rating': np.random.randint(1, 6, 100),
    'Product_C_Rating': np.random.randint(1, 6, 100),
    'Overall_Satisfaction': np.random.randint(1, 6, 100)
})

# TODO: Pivot และ reshape operations
# 1. สร้าง pivot table แสดง average rating ของแต่ละ product ตาม age group และ gender
# 2. Melt data เพื่อแปลง product ratings เป็น long format
# 3. สร้าง cross-tabulation ระหว่าง region และ age group
# 4. คำนวณ correlation ระหว่าง product ratings และ overall satisfaction
# 5. สร้าง summary report ที่แสดงถึง insights สำคัญ
```

#### ข้อ 5.2 (10 คะแนน)
Performance optimization exercise:

```python
# สร้างข้อมูลขนาดใหญ่
large_dataset = pd.DataFrame({
    'ID': range(1000000),
    'Category': np.random.choice(['A', 'B', 'C', 'D', 'E'], 1000000),
    'Value1': np.random.randn(1000000),
    'Value2': np.random.randint(1, 1000, 1000000),
    'Date': pd.date_range('2020-01-01', periods=1000000, freq='min')
})

# TODO: Optimization exercises
# 1. เปรียบเทียบ performance ระหว่าง iterrows(), apply(), และ vectorization
# 2. Optimize memory usage โดยการเปลี่ยน data types
# 3. ใช้ categorical data type สำหรับ Category column
# 4. เปรียบเทียบ performance ของ groupby operations กับข้อมูลขนาดใหญ่
# 5. สร้างฟังก์ชันที่ process ข้อมูลอย่างมีประสิทธิภาพ

def optimize_dataframe(df):
    """
    Optimize DataFrame สำหรับ memory และ performance
    
    Returns:
    optimized DataFrame และ report การประหยัด memory
    """
    # TODO: implement optimization
    pass
```


