# Chart Building สำหรับนักศึกษา
## การสร้างกราฟและการนำเสนอข้อมูลด้วย Python

---

## 📊 สารบัญ
1. [บทนำ Data Visualization](#บทนำ-data-visualization)
2. [การติดตั้งและเตรียม Environment](#การติดตั้งและเตรียม-environment)
3. [Matplotlib พื้นฐาน](#matplotlib-พื้นฐาน)
4. [Seaborn สำหรับ Statistical Plots](#seaborn-สำหรับ-statistical-plots)
5. [Plotly สำหรับ Interactive Charts](#plotly-สำหรับ-interactive-charts)
6. [Pandas Plotting](#pandas-plotting)
7. [Chart Types และการเลือกใช้](#chart-types-และการเลือกใช้)
8. [การออกแบบกราฟที่มีประสิทธิภาพ](#การออกแบบกราฟที่มีประสิทธิภาพ)
9. [Dashboard และ Multi-plot Layouts](#dashboard-และ-multi-plot-layouts)
10. [การ Export และ Sharing](#การ-export-และ-sharing)
11. [แบบฝึกหัด](#แบบฝึกหัด)
12. [โครงงานปฏิบัติ](#โครงงานปฏิบัติ)

---

## บทนำ Data Visualization

### Data Visualization คืออะไร?
Data Visualization คือการแสดงข้อมูลในรูปแบบกราฟิก เช่น กราฟ แผนภูมิ แผนที่ เพื่อให้เข้าใจข้อมูลได้ง่ายและรวดเร็วขึ้น

### ทำไมต้องทำ Data Visualization?

#### เปรียบเทียบการเข้าใจข้อมูล

```python
# ข้อมูลในรูปแบบตาราง - ยากต่อการเข้าใจ
import pandas as pd
import numpy as np

sales_data = pd.DataFrame({
    'Month': ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    'Sales': [10000, 12000, 15000, 11000, 18000, 20000],
    'Profit': [2000, 2500, 3200, 2100, 3800, 4200]
})
print("ข้อมูลในรูปแบบตาราง:")
print(sales_data)

# ข้อมูลในรูปแบบกราฟ - เข้าใจได้ในพริบตา
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))
plt.plot(sales_data['Month'], sales_data['Sales'], marker='o', label='Sales')
plt.plot(sales_data['Month'], sales_data['Profit'], marker='s', label='Profit')
plt.title('Sales และ Profit แต่ละเดือน')
plt.xlabel('เดือน')
plt.ylabel('จำนวนเงิน (บาท)')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

### ประโยชน์ของ Data Visualization
- **เข้าใจเร็ว**: สมองประมวลผลภาพได้เร็วกว่าตัวเลข 60,000 เท่า
- **ค้นหา Pattern**: เห็น trends, patterns, outliers ได้ชัดเจน
- **การสื่อสาร**: นำเสนอข้อมูลได้น่าสนใจและเข้าใจง่าย
- **การตัดสินใจ**: ช่วยในการตัดสินใจที่รวดเร็วและถูกต้อง

### หลักการพื้นฐาน
1. **Choose the Right Chart**: เลือกประเภทกราฟที่เหมาะกับข้อมูล
2. **Keep it Simple**: ความเรียบง่ายชนะความซับซ้อน
3. **Tell a Story**: กราฟควรเล่าเรื่องราวของข้อมูล
4. **Consider the Audience**: ปรับให้เหมาะกับผู้ดู

---

## การติดตั้งและเตรียม Environment

### การติดตั้ง Libraries

```bash
# การติดตั้งพื้นฐาน
pip install matplotlib seaborn plotly pandas numpy

# การติดตั้งเพิ่มเติม
pip install plotly-dash jupyter ipywidgets

# สำหรับ geographic plots
pip install geopandas folium

# สำหรับ advanced styling
pip install matplotlib-style-library
```

### การ Setup Environment

```python
# Import libraries หลัก
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.graph_objects as go
import plotly.express as px
from plotly.subplots import make_subplots
import warnings
warnings.filterwarnings('ignore')

# การตั้งค่า matplotlib
plt.style.use('default')  # หรือ 'seaborn', 'ggplot'
plt.rcParams['figure.figsize'] = (10, 6)
plt.rcParams['font.size'] = 12
plt.rcParams['axes.grid'] = True
plt.rcParams['grid.alpha'] = 0.3

# การตั้งค่า seaborn
sns.set_theme(style="whitegrid")
sns.set_palette("husl")

# สำหรับ Jupyter Notebook
%matplotlib inline

# ตรวจสอบ versions
print(f"Matplotlib: {plt.__version__}")
print(f"Seaborn: {sns.__version__}")
print(f"Plotly: {px.__version__}")
print(f"Pandas: {pd.__version__}")
```

### การสร้างข้อมูลตัวอย่าง

```python
# ฟังก์ชันสำหรับสร้างข้อมูลตัวอย่าง
def generate_sample_data():
    """สร้างข้อมูลตัวอย่างสำหรับการฝึกทำกราฟ"""
    
    np.random.seed(42)
    
    # ข้อมูลการขาย
    dates = pd.date_range('2023-01-01', periods=365, freq='D')
    sales_data = pd.DataFrame({
        'Date': dates,
        'Sales': np.random.normal(1000, 200, 365) + 
                np.sin(np.arange(365) * 2 * np.pi / 365) * 100,  # seasonal pattern
        'Product': np.random.choice(['A', 'B', 'C', 'D'], 365),
        'Region': np.random.choice(['North', 'South', 'East', 'West'], 365),
        'Customer_Type': np.random.choice(['New', 'Returning'], 365, p=[0.3, 0.7])
    })
    sales_data['Profit'] = sales_data['Sales'] * np.random.uniform(0.1, 0.3, 365)
    
    # ข้อมูลพนักงาน
    employees_data = pd.DataFrame({
        'Employee_ID': range(1, 101),
        'Department': np.random.choice(['IT', 'Sales', 'Marketing', 'HR', 'Finance'], 100),
        'Age': np.random.randint(22, 65, 100),
        'Salary': np.random.normal(50000, 15000, 100),
        'Experience': np.random.randint(0, 20, 100),
        'Gender': np.random.choice(['Male', 'Female'], 100),
        'Education': np.random.choice(['Bachelor', 'Master', 'PhD'], 100, p=[0.6, 0.3, 0.1])
    })
    
    # ข้อมูลสต็อค
    stock_data = pd.DataFrame({
        'Date': pd.date_range('2023-01-01', periods=252, freq='B'),  # Business days
        'AAPL': np.random.randn(252).cumsum() + 150,
        'GOOGL': np.random.randn(252).cumsum() + 2500,
        'MSFT': np.random.randn(252).cumsum() + 250,
        'TSLA': np.random.randn(252).cumsum() + 200
    })
    
    return sales_data, employees_data, stock_data

# สร้างข้อมูลตัวอย่าง
sales_df, employees_df, stock_df = generate_sample_data()

print("ข้อมูลตัวอย่างสร้างเสร็จแล้ว!")
print(f"Sales data shape: {sales_df.shape}")
print(f"Employees data shape: {employees_df.shape}")
print(f"Stock data shape: {stock_df.shape}")
```

---

## Matplotlib พื้นฐาน

### พื้นฐานการใช้ Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

# สร้างกราฟพื้นฐาน
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.title('กราฟ Sine Function')
plt.xlabel('x')
plt.ylabel('sin(x)')
plt.grid(True)
plt.show()
```

### Figure และ Axes Concept

```python
# วิธีที่ 1: pyplot interface (ง่าย)
plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.plot(x, np.sin(x))
plt.title('Sin(x)')

plt.subplot(1, 2, 2)
plt.plot(x, np.cos(x))
plt.title('Cos(x)')

plt.tight_layout()
plt.show()

# วิธีที่ 2: Object-oriented interface (ควบคุมได้มากกว่า)
fig, axes = plt.subplots(1, 2, figsize=(12, 4))

axes[0].plot(x, np.sin(x))
axes[0].set_title('Sin(x)')
axes[0].grid(True)

axes[1].plot(x, np.cos(x), color='red')
axes[1].set_title('Cos(x)')
axes[1].grid(True)

plt.tight_layout()
plt.show()
```

### ประเภทกราฟพื้นฐาน

#### Line Plot

```python
# Line plot พื้นฐาน
plt.figure(figsize=(12, 6))

# Single line
plt.subplot(1, 2, 1)
plt.plot(sales_df['Date'][:30], sales_df['Sales'][:30])
plt.title('Sales Trend (30 days)')
plt.xticks(rotation=45)
plt.ylabel('Sales Amount')

# Multiple lines
plt.subplot(1, 2, 2)
plt.plot(sales_df['Date'][:30], sales_df['Sales'][:30], 
         label='Sales', marker='o', linewidth=2)
plt.plot(sales_df['Date'][:30], sales_df['Profit'][:30], 
         label='Profit', marker='s', linewidth=2)
plt.title('Sales vs Profit')
plt.legend()
plt.xticks(rotation=45)
plt.ylabel('Amount')

plt.tight_layout()
plt.show()
```

#### Bar Plot

```python
# Bar plot
dept_counts = employees_df['Department'].value_counts()

plt.figure(figsize=(12, 6))

# Vertical bar chart
plt.subplot(1, 2, 1)
plt.bar(dept_counts.index, dept_counts.values, color='skyblue', edgecolor='navy')
plt.title('จำนวนพนักงานแต่ละแผนก')
plt.ylabel('จำนวนคน')
plt.xticks(rotation=45)

# Horizontal bar chart
plt.subplot(1, 2, 2)
plt.barh(dept_counts.index, dept_counts.values, color='lightcoral', edgecolor='darkred')
plt.title('จำนวนพนักงานแต่ละแผนก (แนวนอน)')
plt.xlabel('จำนวนคน')

plt.tight_layout()
plt.show()
```

#### Scatter Plot

```python
plt.figure(figsize=(12, 6))

# Basic scatter plot
plt.subplot(1, 2, 1)
plt.scatter(employees_df['Age'], employees_df['Salary'], alpha=0.6)
plt.title('Age vs Salary')
plt.xlabel('Age')
plt.ylabel('Salary')

# Colored scatter plot
plt.subplot(1, 2, 2)
colors = {'IT': 'red', 'Sales': 'blue', 'Marketing': 'green', 
          'HR': 'orange', 'Finance': 'purple'}
for dept in employees_df['Department'].unique():
    dept_data = employees_df[employees_df['Department'] == dept]
    plt.scatter(dept_data['Age'], dept_data['Salary'], 
               label=dept, color=colors[dept], alpha=0.6)
plt.title('Age vs Salary by Department')
plt.xlabel('Age')
plt.ylabel('Salary')
plt.legend()

plt.tight_layout()
plt.show()
```

#### Histogram

```python
plt.figure(figsize=(12, 6))

# Basic histogram
plt.subplot(1, 2, 1)
plt.hist(employees_df['Salary'], bins=20, color='lightblue', 
         edgecolor='black', alpha=0.7)
plt.title('การกระจายของเงินเดือน')
plt.xlabel('Salary')
plt.ylabel('Frequency')

# Multiple histograms
plt.subplot(1, 2, 2)
for dept in ['IT', 'Sales', 'Marketing']:
    dept_salaries = employees_df[employees_df['Department'] == dept]['Salary']
    plt.hist(dept_salaries, alpha=0.5, label=dept, bins=15)
plt.title('การกระจายเงินเดือนตามแผนก')
plt.xlabel('Salary')
plt.ylabel('Frequency')
plt.legend()

plt.tight_layout()
plt.show()
```

### การปรับแต่งกราฟ

```python
# กราฟที่ปรับแต่งครบถ้วน
plt.figure(figsize=(12, 8))

# สร้างข้อมูล
monthly_sales = sales_df.groupby(sales_df['Date'].dt.month)['Sales'].mean()
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
          'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']

# กราฟหลัก
bars = plt.bar(range(len(monthly_sales)), monthly_sales.values, 
               color=plt.cm.viridis(np.linspace(0, 1, len(monthly_sales))),
               edgecolor='black', linewidth=1.2)

# เพิ่มค่าบนแท่ง
for i, bar in enumerate(bars):
    height = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2., height,
             f'{height:.0f}',
             ha='center', va='bottom', fontweight='bold')

# ปรับแต่งรายละเอียด
plt.title('Average Monthly Sales 2023', fontsize=16, fontweight='bold', pad=20)
plt.xlabel('Month', fontsize=14, fontweight='bold')
plt.ylabel('Average Sales (THB)', fontsize=14, fontweight='bold')
plt.xticks(range(len(months)), months)

# Grid และ style
plt.grid(axis='y', alpha=0.3, linestyle='--')
plt.ylim(0, max(monthly_sales.values) * 1.1)

# เพิ่มคำอธิบาย
plt.figtext(0.5, 0.02, 'Data Source: Company Sales Database', 
            ha='center', fontsize=10, style='italic')

plt.tight_layout()
plt.show()
```

---

## Seaborn สำหรับ Statistical Plots

### พื้นฐาน Seaborn

```python
import seaborn as sns

# ตั้งค่า theme
sns.set_theme(style="whitegrid", palette="husl")

# สีและ palette
print("Available palettes:")
palettes = ['deep', 'muted', 'bright', 'pastel', 'dark', 'colorblind']
fig, axes = plt.subplots(len(palettes), 1, figsize=(10, 8))
for i, palette in enumerate(palettes):
    sns.palplot(sns.color_palette(palette), ax=axes[i])
    axes[i].set_title(f'Palette: {palette}')
plt.tight_layout()
plt.show()
```

### Distribution Plots

```python
plt.figure(figsize=(15, 10))

# Histogram with KDE
plt.subplot(2, 3, 1)
sns.histplot(employees_df['Salary'], kde=True, bins=20)
plt.title('Salary Distribution')

# Distribution plot
plt.subplot(2, 3, 2)
sns.distplot(employees_df['Age'], hist=True, kde=True, 
             bins=20, color='skyblue')
plt.title('Age Distribution')

# Box plot
plt.subplot(2, 3, 3)
sns.boxplot(x='Department', y='Salary', data=employees_df)
plt.title('Salary by Department')
plt.xticks(rotation=45)

# Violin plot
plt.subplot(2, 3, 4)
sns.violinplot(x='Department', y='Age', data=employees_df)
plt.title('Age Distribution by Department')
plt.xticks(rotation=45)

# Strip plot
plt.subplot(2, 3, 5)
sns.stripplot(x='Department', y='Salary', data=employees_df, 
              size=4, jitter=True)
plt.title('Salary Points by Department')
plt.xticks(rotation=45)

# Swarm plot
plt.subplot(2, 3, 6)
# ใช้ sample เพื่อไม่ให้กราฟแน่นเกินไป
sample_data = employees_df.sample(50)
sns.swarmplot(x='Gender', y='Salary', data=sample_data)
plt.title('Salary by Gender (Sample)')

plt.tight_layout()
plt.show()
```

### Relationship Plots

```python
plt.figure(figsize=(15, 10))

# Scatter plot with regression
plt.subplot(2, 3, 1)
sns.scatterplot(x='Age', y='Salary', hue='Department', 
                size='Experience', data=employees_df)
plt.title('Age vs Salary by Department')

# Regression plot
plt.subplot(2, 3, 2)
sns.regplot(x='Experience', y='Salary', data=employees_df, 
            scatter_kws={'alpha':0.6})
plt.title('Experience vs Salary (with regression)')

# Joint plot (ในหน้าต่างแยก)
# sns.jointplot(x='Age', y='Salary', data=employees_df, kind='reg')

# Pair plot สำหรับ numeric columns
numeric_cols = ['Age', 'Salary', 'Experience']
plt.subplot(2, 3, 3)
# สำหรับ subplot เราจะใช้ correlation heatmap แทน
correlation_matrix = employees_df[numeric_cols].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Matrix')

# Count plot
plt.subplot(2, 3, 4)
sns.countplot(x='Education', hue='Gender', data=employees_df)
plt.title('Education Level by Gender')

# Bar plot
plt.subplot(2, 3, 5)
sns.barplot(x='Department', y='Salary', hue='Gender', data=employees_df)
plt.title('Average Salary by Department and Gender')
plt.xticks(rotation=45)

# Point plot
plt.subplot(2, 3, 6)
sns.pointplot(x='Experience', y='Salary', hue='Department', 
              data=employees_df.groupby(['Experience', 'Department'])['Salary'].mean().reset_index())
plt.title('Salary Trend by Experience')
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

### Heatmaps

```python
plt.figure(figsize=(15, 6))

# Correlation heatmap
plt.subplot(1, 2, 1)
numeric_data = employees_df.select_dtypes(include=[np.number])
correlation_matrix = numeric_data.corr()
sns.heatmap(correlation_matrix, annot=True, cmap='RdYlBu_r', 
            center=0, square=True, linewidths=0.5)
plt.title('Correlation Heatmap')

# Pivot table heatmap
plt.subplot(1, 2, 2)
pivot_data = employees_df.pivot_table(values='Salary', 
                                     index='Department', 
                                     columns='Education', 
                                     aggfunc='mean')
sns.heatmap(pivot_data, annot=True, fmt='.0f', cmap='YlOrRd')
plt.title('Average Salary: Department vs Education')

plt.tight_layout()
plt.show()
```

### Advanced Seaborn Plots

```python
# FacetGrid สำหรับ multiple subplots
g = sns.FacetGrid(sales_df.sample(1000), col='Product', hue='Customer_Type', 
                  col_wrap=2, height=4)
g.map(plt.scatter, 'Sales', 'Profit', alpha=0.7)
g.add_legend()
plt.show()

# Pair plot
sample_employees = employees_df.sample(100)  # ใช้ sample เพื่อความเร็ว
sns.pairplot(sample_employees[['Age', 'Salary', 'Experience', 'Department']], 
             hue='Department', height=2.5)
plt.show()

# Cluster map
numeric_cols = ['Age', 'Salary', 'Experience']
sample_data = employees_df[numeric_cols].sample(50)
sns.clustermap(sample_data.T, cmap='viridis', standard_scale=1, 
               figsize=(10, 8))
plt.show()
```

---

## Plotly สำหรับ Interactive Charts

### พื้นฐาน Plotly

```python
import plotly.graph_objects as go
import plotly.express as px
from plotly.subplots import make_subplots

# กราฟ interactive พื้นฐาน
fig = go.Figure()
fig.add_trace(go.Scatter(x=sales_df['Date'][:100], 
                         y=sales_df['Sales'][:100],
                         mode='lines+markers',
                         name='Sales',
                         hovertemplate='Date: %{x}<br>Sales: $%{y:,.0f}<extra></extra>'))

fig.update_layout(title='Interactive Sales Chart',
                  xaxis_title='Date',
                  yaxis_title='Sales Amount',
                  hovermode='x unified')
fig.show()
```

### Plotly Express - Quick Charts

```python
# Scatter plot
fig = px.scatter(employees_df, x='Age', y='Salary', 
                 color='Department', size='Experience',
                 hover_data=['Education'],
                 title='Employee Age vs Salary',
                 labels={'Age': 'Age (years)', 
                        'Salary': 'Annual Salary (USD)'})
fig.show()

# Bar chart
dept_avg_salary = employees_df.groupby('Department')['Salary'].mean().reset_index()
fig = px.bar(dept_avg_salary, x='Department', y='Salary',
             color='Salary', color_continuous_scale='Viridis',
             title='Average Salary by Department')
fig.show()

# Box plot
fig = px.box(employees_df, x='Department', y='Salary', 
             color='Gender',
             title='Salary Distribution by Department and Gender')
fig.show()

# Line chart
monthly_sales = sales_df.groupby(sales_df['Date'].dt.month).agg({
    'Sales': 'mean',
    'Profit': 'mean'
}).reset_index()
monthly_sales['Month'] = monthly_sales['Date'].map({
    1: 'Jan', 2: 'Feb', 3: 'Mar', 4: 'Apr', 5: 'May', 6: 'Jun',
    7: 'Jul', 8: 'Aug', 9: 'Sep', 10: 'Oct', 11: 'Nov', 12: 'Dec'
})

fig = px.line(monthly_sales, x='Month', y=['Sales', 'Profit'],
              title='Monthly Sales and Profit Trends')
fig.show()
```

### Advanced Interactive Charts

```python
# Subplot combinations
fig = make_subplots(
    rows=2, cols=2,
    subplot_titles=('Sales Trend', 'Department Distribution', 
                   'Age vs Salary', 'Correlation Heatmap'),
    specs=[[{"secondary_y": True}, {"type": "pie"}],
           [{"type": "scatter"}, {"type": "heatmap"}]]
)

# Sales trend with dual axis
monthly_data = sales_df.groupby(sales_df['Date'].dt.month).agg({
    'Sales': 'mean',
    'Profit': 'mean'
}).reset_index()

fig.add_trace(go.Scatter(x=monthly_data['Date'], y=monthly_data['Sales'],
                         name='Sales', line=dict(color='blue')),
              row=1, col=1, secondary_y=False)
fig.add_trace(go.Scatter(x=monthly_data['Date'], y=monthly_data['Profit'],
                         name='Profit', line=dict(color='red')),
              row=1, col=1, secondary_y=True)

# Pie chart
dept_counts = employees_df['Department'].value_counts()
fig.add_trace(go.Pie(labels=dept_counts.index, values=dept_counts.values,
                     name="Department Distribution"),
              row=1, col=2)

# Scatter plot
fig.add_trace(go.Scatter(x=employees_df['Age'], y=employees_df['Salary'],
                         mode='markers', name='Age vs Salary',
                         marker=dict(color=employees_df['Experience'],
                                   colorscale='Viridis', showscale=True)),
              row=2, col=1)

# Correlation heatmap
numeric_data = employees_df.select_dtypes(include=[np.number])
corr_matrix = numeric_data.corr()
fig.add_trace(go.Heatmap(z=corr_matrix.values,
                         x=corr_matrix.columns,
                         y=corr_matrix.columns,
                         colorscale='RdBu', zmid=0),
              row=2, col=2)

# Update layout
fig.update_layout(height=800, showlegend=True,
                  title_text="Employee Analytics Dashboard")
fig.show()
```

### 3D Charts

```python
# 3D Scatter plot
fig = go.Figure(data=[go.Scatter3d(
    x=employees_df['Age'],
    y=employees_df['Experience'],
    z=employees_df['Salary'],
    mode='markers',
    marker=dict(
        size=5,
        color=employees_df['Salary'],
        colorscale='Viridis',
        opacity=0.8,
        colorbar=dict(title="Salary")
    ),
    text=employees_df['Department'],
    hovertemplate='Age: %{x}<br>Experience: %{y}<br>Salary: $%{z:,.0f}<br>Department: %{text}<extra></extra>'
)])

fig.update_layout(
    title='3D Employee Analysis: Age, Experience, and Salary',
    scene=dict(
        xaxis_title='Age',
        yaxis_title='Experience (years)',
        zaxis_title='Salary ($)',
        camera=dict(eye=dict(x=1.5, y=1.5, z=1.5))
    ),
    width=800,
    height=600
)
fig.show()

# Surface plot
x = np.linspace(-5, 5, 50)
y = np.linspace(-5, 5, 50)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

fig = go.Figure(data=[go.Surface(z=Z, x=X, y=Y, colorscale='Viridis')])
fig.update_layout(title='3D Surface Plot',
                  scene=dict(xaxis_title='X', yaxis_title='Y', zaxis_title='Z'),
                  width=700, height=500)
fig.show()
```

---

## Pandas Plotting

### การใช้ Pandas Built-in Plotting

```python
# Pandas plotting พื้นฐาน
sales_df.set_index('Date')['Sales'].plot(figsize=(12, 6), title='Daily Sales')
plt.show()

# Multiple columns
fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# Line plot
sales_df.set_index('Date')[['Sales', 'Profit']].plot(ax=axes[0,0], title='Sales & Profit Over Time')

# Bar plot
employees_df['Department'].value_counts().plot(kind='bar', ax=axes[0,1], 
                                              title='Employees by Department', rot=45)

# Histogram
employees_df['Salary'].plot(kind='hist', bins=20, ax=axes[1,0], 
                           title='Salary Distribution', alpha=0.7)

# Box plot
employees_df.boxplot(column='Salary', by='Department', ax=axes[1,1], rot=45)
axes[1,1].set_title('Salary by Department')

plt.tight_layout()
plt.show()

# Pandas plotting methods
print("Pandas plotting methods:")
methods = ['line', 'bar', 'barh', 'hist', 'box', 'kde', 'density', 
          'area', 'pie', 'scatter', 'hexbin']
for method in methods:
    print(f"df.plot(kind='{method}')")
```

### Time Series Plotting

```python
# Time series analysis plots
ts_data = sales_df.set_index('Date')

fig, axes = plt.subplots(3, 1, figsize=(15, 12))

# Original time series
ts_data['Sales'].plot(ax=axes[0], title='Daily Sales', alpha=0.7)
ts_data['Sales'].rolling(30).mean().plot(ax=axes[0], color='red', 
                                         label='30-day Moving Average')
axes[0].legend()

# Resampled data
monthly_data = ts_data.resample('M')[['Sales', 'Profit']].mean()
monthly_data.plot(ax=axes[1], title='Monthly Average Sales & Profit')

# Seasonal decomposition visualization
quarterly_data = ts_data.resample('Q')[['Sales', 'Profit']].sum()
quarterly_data.plot(kind='bar', ax=axes[2], title='Quarterly Sales & Profit')

plt.tight_layout()
plt.show()

# Correlation matrix with pandas
numeric_data = employees_df.select_dtypes(include=[np.number])
correlation_matrix = numeric_data.corr()

plt.figure(figsize=(10, 8))
plt.imshow(correlation_matrix, cmap='coolwarm', aspect='auto')
plt.colorbar()
plt.xticks(range(len(correlation_matrix.columns)), correlation_matrix.columns, rotation=45)
plt.yticks(range(len(correlation_matrix.columns)), correlation_matrix.columns)
plt.title('Correlation Matrix Heatmap')

# Add correlation values
for i in range(len(correlation_matrix.columns)):
    for j in range(len(correlation_matrix.columns)):
        plt.text(j, i, f'{correlation_matrix.iloc[i, j]:.2f}', 
                ha='center', va='center')

plt.tight_layout()
plt.show()
```

---

## Chart Types และการเลือกใช้

### Chart Selection Guide

```python
def chart_selection_guide():
    """คู่มือการเลือกประเภทกราฟ"""
    
    guide = {
        "เปรียบเทียบค่า": {
            "charts": ["Bar Chart", "Column Chart", "Radar Chart"],
            "use_case": "เปรียบเทียบค่าระหว่างหมวดหมู่ต่างๆ",
            "example": "ยอดขายแต่ละเดือน, จำนวนพนักงานแต่ละแผนก"
        },
        "แสดงแนวโน้ม": {
            "charts": ["Line Chart", "Area Chart"],
            "use_case": "แสดงการเปลี่ยนแปลงตามเวลา",
            "example": "ราคาหุ้น, อุณหภูมิรายวัน, ยอดขายรายเดือน"
        },
        "แสดงสัดส่วน": {
            "charts": ["Pie Chart", "Donut Chart", "Treemap"],
            "use_case": "แสดงสัดส่วนของส่วนต่างๆ ในภาพรวม",
            "example": "market share, การใช้งบประมาณ"
        },
        "แสดงความสัมพันธ์": {
            "charts": ["Scatter Plot", "Bubble Chart", "Heatmap"],
            "use_case": "แสดงความสัมพันธ์ระหว่างตัวแปร",
            "example": "อายุ vs เงินเดือน, อุณหภูมิ vs ยอดขาย"
        },
        "แสดงการกระจาย": {
            "charts": ["Histogram", "Box Plot", "Violin Plot"],
            "use_case": "แสดงการกระจายของข้อมูล",
            "example": "การกระจายของเงินเดือน, คะแนนสอบ"
        }
    }
    
    return guide

# แสดงคู่มือ
guide = chart_selection_guide()
for category, info in guide.items():
    print(f"\n=== {category} ===")
    print(f"Charts: {', '.join(info['charts'])}")
    print(f"Use case: {info['use_case']}")
    print(f"Example: {info['example']}")
```

### ตัวอย่างการเลือกใช้กราฟ

```python
# สาธิตการเลือกใช้กราฟที่เหมาะสม
fig, axes = plt.subplots(2, 3, figsize=(18, 12))

# 1. เปรียบเทียบหมวดหมู่ - Bar Chart
dept_salary = employees_df.groupby('Department')['Salary'].mean()
axes[0,0].bar(dept_salary.index, dept_salary.values, color='lightblue')
axes[0,0].set_title('1. เปรียบเทียบ: Average Salary by Department')
axes[0,0].tick_params(axis='x', rotation=45)

# 2. แนวโน้มตามเวลา - Line Chart
monthly_sales = sales_df.groupby(sales_df['Date'].dt.month)['Sales'].mean()
axes[0,1].plot(range(1, 13), monthly_sales.values, marker='o')
axes[0,1].set_title('2. แนวโน้ม: Monthly Sales Trend')
axes[0,1].set_xlabel('Month')

# 3. สัดส่วน - Pie Chart
dept_counts = employees_df['Department'].value_counts()
axes[0,2].pie(dept_counts.values, labels=dept_counts.index, autopct='%1.1f%%')
axes[0,2].set_title('3. สัดส่วน: Employee Distribution')

# 4. ความสัมพันธ์ - Scatter Plot
axes[1,0].scatter(employees_df['Age'], employees_df['Salary'], alpha=0.6)
axes[1,0].set_title('4. ความสัมพันธ์: Age vs Salary')
axes[1,0].set_xlabel('Age')
axes[1,0].set_ylabel('Salary')

# 5. การกระจาย - Histogram
axes[1,1].hist(employees_df['Salary'], bins=20, alpha=0.7, color='lightgreen')
axes[1,1].set_title('5. การกระจาย: Salary Distribution')
axes[1,1].set_xlabel('Salary')

# 6. การเปรียบเทียบกลุ่ม - Box Plot
dept_data = [employees_df[employees_df['Department'] == dept]['Salary'].values 
             for dept in employees_df['Department'].unique()]
axes[1,2].boxplot(dept_data, labels=employees_df['Department'].unique())
axes[1,2].set_title('6. เปรียบเทียบกลุ่ม: Salary by Department')
axes[1,2].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()
```

### Common Chart Mistakes และวิธีแก้ไข

```python
# ตัวอย่างกราฟที่ผิดและถูก
fig, axes = plt.subplots(2, 2, figsize=(16, 12))

# กราฟผิด: Pie chart กับข้อมูลมากเกินไป
product_sales = sales_df.groupby('Product')['Sales'].sum()
region_sales = sales_df.groupby('Region')['Sales'].sum()
all_categories = pd.concat([product_sales, region_sales])

axes[0,0].pie(all_categories.values, labels=all_categories.index, autopct='%1.1f%%')
axes[0,0].set_title('❌ ผิด: Pie Chart กับข้อมูลมากเกินไป')

# กราฟถูก: Bar chart สำหรับการเปรียบเทียบ
axes[0,1].bar(product_sales.index, product_sales.values, color='lightblue')
axes[0,1].set_title('✅ ถูก: Bar Chart สำหรับเปรียบเทียบ')

# กราฟผิด: Line chart กับ categorical data
dept_counts = employees_df['Department'].value_counts()
axes[1,0].plot(dept_counts.index, dept_counts.values, marker='o')
axes[1,0].set_title('❌ ผิด: Line Chart กับ Categorical Data')
axes[1,0].tick_params(axis='x', rotation=45)

# กราฟถูก: Bar chart กับ categorical data
axes[1,1].bar(dept_counts.index, dept_counts.values, color='lightcoral')
axes[1,1].set_title('✅ ถูก: Bar Chart กับ Categorical Data')
axes[1,1].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()

print("=== Common Chart Mistakes ===")
mistakes = [
    "1. ใช้ Pie Chart กับข้อมูลมากกว่า 5-7 หมวดหมู่",
    "2. ใช้ Line Chart กับ Categorical Data",
    "3. ใช้ 3D Charts โดยไม่จำเป็น",
    "4. สีที่ไม่เหมาะสม หรือ ตัดกันยาก",
    "5. ไม่มี Label หรือ Title ที่ชัดเจน",
    "6. Scale ที่ทำให้เข้าใจผิด (Misleading)",
    "7. เอาข้อมูลมาเปรียบเทียบกันไม่ได้"
]

for mistake in mistakes:
    print(mistake)
```

---

## การออกแบบกราฟที่มีประสิทธิภาพ

### Design Principles

```python
def demonstrate_design_principles():
    """สาธิตหลักการออกแบบกราฟ"""
    
    # สร้างข้อมูลตัวอย่าง
    monthly_data = sales_df.groupby(sales_df['Date'].dt.month).agg({
        'Sales': 'mean',
        'Profit': 'mean'
    }).reset_index()
    
    fig, axes = plt.subplots(2, 2, figsize=(16, 12))
    
    # 1. กราฟที่ไม่ดี - ขาด Design Principles
    axes[0,0].bar(monthly_data['Date'], monthly_data['Sales'], 
                  color=['red', 'blue', 'green', 'yellow', 'purple', 'orange'])
    axes[0,0].set_title('Bad Design: Too Many Colors, No Grid')
    
    # 2. กราฟที่ดี - ตามหลัก Design Principles
    bars = axes[0,1].bar(monthly_data['Date'], monthly_data['Sales'], 
                         color='steelblue', alpha=0.8, edgecolor='navy')
    axes[0,1].set_title('Good Design: Consistent Colors, Clean Layout', 
                        fontsize=14, fontweight='bold')
    axes[0,1].set_xlabel('Month', fontweight='bold')
    axes[0,1].set_ylabel('Average Sales', fontweight='bold')
    axes[0,1].grid(axis='y', alpha=0.3)
    
    # เพิ่มค่าบนแท่ง
    for bar in bars:
        height = bar.get_height()
        axes[0,1].text(bar.get_x() + bar.get_width()/2., height,
                      f'{height:.0f}', ha='center', va='bottom')
    
    # 3. กราฎที่มีปัญหา Scale
    axes[1,0].bar(monthly_data['Date'], monthly_data['Sales'])
    axes[1,0].set_ylim(950, 1050)  # Scale ที่ทำให้เข้าใจผิด
    axes[1,0].set_title('Misleading: Wrong Y-axis Scale')
    
    # 4. กราฟที่มี Scale ถูกต้อง
    axes[1,1].bar(monthly_data['Date'], monthly_data['Sales'], color='darkgreen', alpha=0.7)
    axes[1,1].set_ylim(0, max(monthly_data['Sales']) * 1.1)
    axes[1,1].set_title('Correct: Proper Y-axis Scale', fontweight='bold')
    axes[1,1].grid(axis='y', alpha=0.3)
    
    plt.tight_layout()
    plt.show()

demonstrate_design_principles()
```

### Color Theory และ Accessibility

```python
# Color palettes และ accessibility
fig, axes = plt.subplots(3, 2, figsize=(15, 15))

# 1. Rainbow colors (ไม่ดี)
dept_data = employees_df['Department'].value_counts()
colors_bad = plt.cm.rainbow(np.linspace(0, 1, len(dept_data)))
axes[0,0].bar(dept_data.index, dept_data.values, color=colors_bad)
axes[0,0].set_title('❌ Poor: Rainbow Colors')
axes[0,0].tick_params(axis='x', rotation=45)

# 2. Sequential colors (ดี)
colors_good = plt.cm.Blues(np.linspace(0.4, 0.8, len(dept_data)))
axes[0,1].bar(dept_data.index, dept_data.values, color=colors_good)
axes[0,1].set_title('✅ Good: Sequential Colors')
axes[0,1].tick_params(axis='x', rotation=45)

# 3. High contrast (ดีสำหรับ accessibility)
colors_accessible = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd']
axes[1,0].bar(dept_data.index, dept_data.values, color=colors_accessible)
axes[1,0].set_title('✅ Accessible: High Contrast Colors')
axes[1,0].tick_params(axis='x', rotation=45)

# 4. Colorblind friendly
colors_cb = ['#E69F00', '#56B4E9', '#009E73', '#F0E442', '#0072B2']
axes[1,1].bar(dept_data.index, dept_data.values, color=colors_cb)
axes[1,1].set_title('✅ Colorblind Friendly Palette')
axes[1,1].tick_params(axis='x', rotation=45)

# 5. Monochromatic (ดีสำหรับการพิมพ์ขาว-ดำ)
colors_mono = plt.cm.Greys(np.linspace(0.3, 0.8, len(dept_data)))
axes[2,0].bar(dept_data.index, dept_data.values, color=colors_mono, edgecolor='black')
axes[2,0].set_title('✅ Print Friendly: Monochromatic')
axes[2,0].tick_params(axis='x', rotation=45)

# 6. Brand colors example
brand_colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FFEAA7']
axes[2,1].bar(dept_data.index, dept_data.values, color=brand_colors)
axes[2,1].set_title('✅ Brand Colors Example')
axes[2,1].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()

# Color accessibility tools
def check_color_contrast(color1, color2):
    """เช็ค contrast ratio ระหว่างสี (simplified)"""
    # นี่เป็นการจำลองอย่างง่าย
    # ในการใช้งานจริงควรใช้ library เฉพาะ
    import colorsys
    
    def luminance(hex_color):
        # แปลง hex เป็น RGB
        rgb = [int(hex_color[i:i+2], 16)/255.0 for i in (1, 3, 5)]
        # คำนวณ luminance
        return 0.299*rgb[0] + 0.587*rgb[1] + 0.114*rgb[2]
    
    lum1 = luminance(color1)
    lum2 = luminance(color2)
    
    if lum1 > lum2:
        contrast = (lum1 + 0.05) / (lum2 + 0.05)
    else:
        contrast = (lum2 + 0.05) / (lum1 + 0.05)
    
    return contrast

# ทดสอบ contrast
colors_test = [('#000000', '#FFFFFF', 'Black on White'),
               ('#0000FF', '#FFFFFF', 'Blue on White'),
               ('#FF0000', '#00FF00', 'Red on Green'),
               ('#333333', '#CCCCCC', 'Dark Grey on Light Grey')]

print("Color Contrast Analysis:")
print("(WCAG AA requires contrast ratio ≥ 4.5:1)")
for color1, color2, desc in colors_test:
    contrast = check_color_contrast(color1, color2)
    status = "✅ Pass" if contrast >= 4.5 else "❌ Fail"
    print(f"{desc}: {contrast:.2f}:1 {status}")
```

### Typography และ Layout

```python
# Typography และ layout best practices
fig = plt.figure(figsize=(16, 12))

# สร้างข้อมูล
monthly_sales = sales_df.groupby(sales_df['Date'].dt.month)['Sales'].mean()
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
          'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']

# Main chart area
ax_main = plt.subplot2grid((3, 3), (0, 0), colspan=2, rowspan=2)

# สร้างกราฟหลัก
bars = ax_main.bar(range(len(monthly_sales)), monthly_sales.values, 
                   color='#2E86AB', alpha=0.8, edgecolor='#1F5582', linewidth=1.5)

# Typography hierarchy
ax_main.set_title('Monthly Sales Performance 2023', 
                  fontsize=20, fontweight='bold', pad=20, color='#2C3E50')
ax_main.set_xlabel('Month', fontsize=14, fontweight='bold', color='#34495E')
ax_main.set_ylabel('Average Sales (THB)', fontsize=14, fontweight='bold', color='#34495E')

# เปลี่ยน font ของ ticks
ax_main.tick_params(axis='both', which='major', labelsize=12)
ax_main.set_xticks(range(len(months)))
ax_main.set_xticklabels(months)

# Grid styling
ax_main.grid(axis='y', alpha=0.3, linestyle='--', linewidth=0.8)
ax_main.set_axisbelow(True)

# เพิ่มค่าบนแท่งกราฟ
for i, bar in enumerate(bars):
    height = bar.get_height()
    ax_main.text(bar.get_x() + bar.get_width()/2., height + height*0.01,
                f'{height:.0f}', ha='center', va='bottom', 
                fontsize=10, fontweight='bold', color='#2C3E50')

# Highlight highest value
max_idx = monthly_sales.values.argmax()
bars[max_idx].set_color('#E74C3C')
bars[max_idx].set_alpha(0.9)

# เพิ่ม annotation
ax_main.annotate(f'Peak: {monthly_sales.values[max_idx]:.0f}',
                xy=(max_idx, monthly_sales.values[max_idx]),
                xytext=(max_idx+1, monthly_sales.values[max_idx]+50),
                arrowprops=dict(arrowstyle='->', color='#E74C3C', lw=2),
                fontsize=12, fontweight='bold', color='#E74C3C',
                bbox=dict(boxstyle="round,pad=0.3", facecolor='white', edgecolor='#E74C3C'))

# Side panel - Key metrics
ax_side = plt.subplot2grid((3, 3), (0, 2), rowspan=2)
ax_side.axis('off')

# Key metrics
total_sales = monthly_sales.sum()
avg_sales = monthly_sales.mean()
growth_rate = ((monthly_sales.iloc[-1] - monthly_sales.iloc[0]) / monthly_sales.iloc[0]) * 100

metrics_text = f"""
KEY METRICS

Total Sales
{total_sales:,.0f} THB

Monthly Average
{avg_sales:,.0f} THB

Growth Rate
{growth_rate:+.1f}%

Best Month
{months[max_idx]}
"""

ax_side.text(0.05, 0.95, metrics_text, transform=ax_side.transAxes,
            fontsize=12, verticalalignment='top',
            bbox=dict(boxstyle="round,pad=0.5", facecolor='#ECF0F1', edgecolor='#BDC3C7'),
            fontfamily='monospace')

# Bottom panel - Data source และ notes
ax_bottom = plt.subplot2grid((3, 3), (2, 0), colspan=3)
ax_bottom.axis('off')

footer_text = """
Data Source: Company Sales Database | Report Generated: 2023 | 
Note: Sales figures include all product categories and regions
"""

ax_bottom.text(0.5, 0.5, footer_text, transform=ax_bottom.transAxes,
              ha='center', va='center', fontsize=10, 
              style='italic', color='#7F8C8D')

# Overall layout adjustments
plt.subplots_adjust(left=0.08, right=0.95, top=0.92, bottom=0.08, 
                    wspace=0.3, hspace=0.4)

plt.show()
```

---

## Dashboard และ Multi-plot Layouts

### Creating Dashboards

```python
def create_employee_dashboard():
    """สร้าง dashboard ครอบคลุมสำหรับข้อมูลพนักงาน"""
    
    # Setup figure
    fig = plt.figure(figsize=(20, 16))
    fig.suptitle('Employee Analytics Dashboard 2023', fontsize=24, fontweight='bold', y=0.98)
    
    # Define color palette
    colors = {
        'primary': '#3498DB',
        'secondary': '#E74C3C', 
        'success': '#27AE60',
        'warning': '#F39C12',
        'info': '#9B59B6'
    }
    
    # 1. Department Distribution (Top Left)
    ax1 = plt.subplot2grid((4, 4), (0, 0), colspan=2)
    dept_counts = employees_df['Department'].value_counts()
    wedges, texts, autotexts = ax1.pie(dept_counts.values, labels=dept_counts.index, 
                                       autopct='%1.1f%%', startangle=90,
                                       colors=[colors['primary'], colors['secondary'], 
                                              colors['success'], colors['warning'], colors['info']])
    ax1.set_title('Employee Distribution by Department', fontsize=14, fontweight='bold', pad=20)
    
    # 2. Salary Distribution (Top Right)
    ax2 = plt.subplot2grid((4, 4), (0, 2), colspan=2)
    ax2.hist(employees_df['Salary'], bins=25, color=colors['primary'], alpha=0.7, edgecolor='white')
    ax2.axvline(employees_df['Salary'].mean(), color=colors['secondary'], 
                linestyle='--', linewidth=2, label=f'Mean: ${employees_df["Salary"].mean():.0f}')
    ax2.axvline(employees_df['Salary'].median(), color=colors['success'], 
                linestyle='--', linewidth=2, label=f'Median: ${employees_df["Salary"].median():.0f}')
    ax2.set_title('Salary Distribution', fontsize=14, fontweight='bold')
    ax2.set_xlabel('Salary ($)')
    ax2.set_ylabel('Frequency')
    ax2.legend()
    ax2.grid(alpha=0.3)
    
    # 3. Age vs Salary Scatter (Middle Left)
    ax3 = plt.subplot2grid((4, 4), (1, 0), colspan=2)
    dept_colors = {dept: color for dept, color in zip(employees_df['Department'].unique(), 
                                                     [colors['primary'], colors['secondary'], 
                                                      colors['success'], colors['warning'], colors['info']])}
    
    for dept in employees_df['Department'].unique():
        dept_data = employees_df[employees_df['Department'] == dept]
        ax3.scatter(dept_data['Age'], dept_data['Salary'], 
                   label=dept, alpha=0.7, s=60, color=dept_colors[dept])
    
    ax3.set_title('Age vs Salary by Department', fontsize=14, fontweight='bold')
    ax3.set_xlabel('Age')
    ax3.set_ylabel('Salary ($)')
    ax3.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
    ax3.grid(alpha=0.3)
    
    # 4. Department Salary Comparison (Middle Right)
    ax4 = plt.subplot2grid((4, 4), (1, 2), colspan=2)
    dept_salary_stats = employees_df.groupby('Department')['Salary'].agg(['mean', 'median', 'std']).round(0)
    
    x = np.arange(len(dept_salary_stats.index))
    width = 0.35
    
    bars1 = ax4.bar(x - width/2, dept_salary_stats['mean'], width, 
                    label='Mean', color=colors['primary'], alpha=0.8)
    bars2 = ax4.bar(x + width/2, dept_salary_stats['median'], width, 
                    label='Median', color=colors['secondary'], alpha=0.8)
    
    ax4.set_title('Average Salary by Department', fontsize=14, fontweight='bold')
    ax4.set_xlabel('Department')
    ax4.set_ylabel('Salary ($)')
    ax4.set_xticks(x)
    ax4.set_xticklabels(dept_salary_stats.index, rotation=45)
    ax4.legend()
    ax4.grid(axis='y', alpha=0.3)
    
    # เพิ่มค่าบนแท่ง
    for bars in [bars1, bars2]:
        for bar in bars:
            height = bar.get_height()
            ax4.text(bar.get_x() + bar.get_width()/2., height,
                    f'${height:.0f}', ha='center', va='bottom', fontsize=9)
    
    # 5. Experience vs Salary (Bottom Left)
    ax5 = plt.subplot2grid((4, 4), (2, 0), colspan=2)
    ax5.scatter(employees_df['Experience'], employees_df['Salary'], 
               alpha=0.6, color=colors['success'], s=40)
    
    # Add trend line
    z = np.polyfit(employees_df['Experience'], employees_df['Salary'], 1)
    p = np.poly1d(z)
    ax5.plot(employees_df['Experience'], p(employees_df['Experience']), 
             "r--", alpha=0.8, linewidth=2, color=colors['secondary'])
    
    ax5.set_title('Experience vs Salary', fontsize=14, fontweight='bold')
    ax5.set_xlabel('Years of Experience')
    ax5.set_ylabel('Salary ($)')
    ax5.grid(alpha=0.3)
    
    # 6. Gender Distribution by Department (Bottom Right)
    ax6 = plt.subplot2grid((4, 4), (2, 2), colspan=2)
    gender_dept = pd.crosstab(employees_df['Department'], employees_df['Gender'])
    gender_dept.plot(kind='bar', ax=ax6, color=[colors['primary'], colors['secondary']], alpha=0.8)
    ax6.set_title('Gender Distribution by Department', fontsize=14, fontweight='bold')
    ax6.set_xlabel('Department')
    ax6.set_ylabel('Count')
    ax6.legend(title='Gender')
    ax6.tick_params(axis='x', rotation=45)
    
    # 7. Key Metrics Summary (Bottom)
    ax7 = plt.subplot2grid((4, 4), (3,