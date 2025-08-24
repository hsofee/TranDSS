
# Chart Building สำหรับนักศึกษา
## การสร้างกราฟและการนำเสนอข้อมูลด้วย Python

---

## 📊 สารบัญ
1. [บทนำ Data Visualization](#บทนำ-data-visualization)
2. [การติดตั้งและการเตรียม-environment](#การติดตั้งและการเตรียม-environment)
3. [Matplotlib พื้นฐาน](#matplotlib-พื้นฐาน)
4. [Seaborn สำหรับ Statistical Plots](#seaborn-สำหรับ-statistical-plots)
5. [Pandas Plotting](#pandas-plotting)
6. [Plotly สำหรับ Interactive Charts](#plotly-สำหรับ-interactive-charts)
7. [การออกแบบกราฟที่มีประสิทธิภาพ](#การออกแบบกราฟที่มีประสิทธิภาพ)
8. [การ Export และ Sharing](#การ-export-และ-sharing)
9. [แบบฝึกหัด](#แบบฝึกหัด)
10. [คำถามอภิปราย](#คำถามอภิปราย)

---

## บทนำ Data Visualization

### Data Visualization คืออะไร?
การแสดงข้อมูลในรูปแบบกราฟ ช่วยให้เข้าใจข้อมูลได้ง่ายขึ้น ค้นหา pattern และอธิบายผลได้อย่างชัดเจน

### ทำไมต้องทำ Data Visualization?
- เข้าใจง่ายกว่าการดูตัวเลขเพียงอย่างเดียว
- ทำให้เห็นแนวโน้ม (trend) และค่าผิดปกติ (outlier)
- ใช้สื่อสารกับผู้อื่นได้ดีกว่า

---

## การเตรียม Libraries

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```

📌 **อธิบายสำหรับนักศึกษา**
- `numpy` และ `pandas` ใช้จัดการข้อมูล
- `seaborn` และ `matplotlib` ใช้สร้างกราฟ
- `%matplotlib inline` ใช้ใน Jupyter Notebook เพื่อแสดงกราฟใน cell

---

## การโหลดข้อมูล

```python
# Read the CSV file
path = "/content/sample_data/california_housing_test.csv"
df = pd.read_csv(path)

# View the first 5 rows
df.head()
```

📌 **อธิบายสำหรับนักศึกษา**
- `pd.read_csv(path)` ใช้อ่านไฟล์ `.csv`
- `df.head()` แสดงตัวอย่างข้อมูล 5 แถวแรก
- Dataset นี้เป็น **California Housing Test Data**

---

## Matplotlib พื้นฐาน

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y)
plt.title("Sine Function")
plt.xlabel("x")
plt.ylabel("sin(x)")
plt.grid(True)
plt.show()
```

📌 **อธิบายสำหรับนักศึกษา**
- `plt.plot()` สร้างกราฟเส้น
- ใช้ใส่ title, xlabel, ylabel และ grid

---

## Seaborn สำหรับ Statistical Plots

```python
# โหลด dataset
data = sns.load_dataset("iris")

# draw lineplot
sns.lineplot(x="sepal_length", y="sepal_width", data=data)
```

📌 **อธิบายสำหรับนักศึกษา**
- `sns.load_dataset("iris")` โหลด dataset ดอกไม้ Iris
- `sns.lineplot()` สร้าง line chart พร้อมการจัดการ style อัตโนมัติ

---

## Pandas Plotting

```python
import pandas as pd

data = {
    'Year': [2018, 2019, 2020, 2021, 2022],
    'Sales': [250, 270, 300, 280, 320]
}
df = pd.DataFrame(data)

df.plot(x='Year', y='Sales', kind='bar', title='Annual Sales', legend=False)
plt.ylabel("Sales Amount")
plt.show()
```

📌 **อธิบายสำหรับนักศึกษา**
- Pandas มี built-in `.plot()` สำหรับวาดกราฟเร็ว ๆ
- เหมาะกับงานที่ต้องการ visualization จาก DataFrame โดยตรง

---

## Plotly สำหรับ Interactive Charts

### พื้นฐานการใช้ Plotly

```python
import plotly.express as px
import seaborn as sns

iris = sns.load_dataset("iris")

fig = px.scatter(iris, x="sepal_length", y="sepal_width",
                 color="species", size="petal_length",
                 hover_data=["petal_width"],
                 title="Iris Dataset: Sepal Length vs Width")
fig.show()
```

📌 **อธิบายสำหรับนักศึกษา**
- `plotly.express.scatter()` สร้าง scatter แบบ interactive
- สามารถ zoom, hover, และ pan ได้สะดวก

---

### ตัวอย่าง Bar Chart แบบ Interactive

```python
import pandas as pd
import plotly.express as px

sales_data = pd.DataFrame({
    "Month": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
    "Sales": [10000, 12000, 15000, 11000, 18000, 20000]
})

fig = px.bar(sales_data, x="Month", y="Sales", text="Sales",
             title="ยอดขายรายเดือน (Interactive)")
fig.update_traces(texttemplate='%{text:.0f}', textposition='outside')
fig.show()
```

---

### ตัวอย่าง Line Chart แบบ Interactive

```python
import numpy as np
import pandas as pd
import plotly.express as px

x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)

line_data = pd.DataFrame({"x": x, "sin(x)": y1, "cos(x)": y2})

fig = px.line(line_data, x="x", y=["sin(x)", "cos(x)"],
              title="Sine vs Cosine (Interactive)")
fig.show()
```

---

## การออกแบบกราฟที่มีประสิทธิภาพ

1. เลือกประเภทกราฟที่เหมาะสมกับข้อมูล
2. ใช้สีน้อยแต่สื่อความหมายชัด
3. ใส่ label และ legend ให้ครบถ้วน
4. หลีกเลี่ยงการใส่ข้อมูลเกินความจำเป็น

---

## การ Export และ Sharing

```python
# บันทึกกราฟเป็นไฟล์ภาพ
plt.savefig("output_chart.png", dpi=300)

# บันทึกกราฟเป็น PDF
plt.savefig("output_chart.pdf")
```

---

## แบบฝึกหัด

1. ใช้ Matplotlib วาดกราฟเส้นของ `sin(x)` และ `cos(x)` บนแกนเดียวกัน
2. ใช้ Seaborn วาดกราฟ histogram ของคอลัมน์ `petal_length` จาก dataset Iris
3. ใช้ Pandas Plotting วาด Bar Chart ของยอดขาย
4. ใช้ Plotly วาด Scatter Plot ที่ interactive ของ dataset `tips`

---

## คำถามอภิปราย

- เมื่อไรควรเลือกใช้ Matplotlib, Seaborn, Pandas หรือ Plotly?
- กราฟ interactive ช่วยให้นักศึกษานำเสนอข้อมูลได้ดีขึ้นอย่างไร?
- หากต้องทำ dashboard สำหรับผู้บริหาร ควรเลือกใช้ library ไหน?
