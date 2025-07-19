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
