
## Python for Data Analysis

#### Pandas
Pandas คือ open source library ใน ภาษา Python ที่ใช้กันอย่างกว้างขวางในงานด้าน Data Science/Data Analysis และ Machine Learning โดยมีโครงสร้างพื้นฐานเป็น Numpy library ซึ่งสามารถสร้าง array ที่มีหลายมิติได้ Pandas จะถูกนำมาใช้ในการจัดการข้อมูลด้านต่าง ๆ เช่น
- Data Cleanising
- Data Fill
- Data Normalization
- Merges and Joins
- Data Visualization
- Loading and Saving Data
- ฯลฯ

ในหัวข้อนี้ เราจะเริ่มต้นเรียนรู้พื้นฐานของ Pandas จนไปถึงวิธีการใช้ Pandas ในการทำ Data Analysis

####### Pandas Installation
### 🛠 Installation

- conda install pandas (Window/Mac)
- pip install pandas (Window/Mac)
- python3.8 -m pip install pandas (for Mac M1)

#### **Pandas Series
Series เป็นชนิดของข้อมูลหลักสำหรับ Pandas ซึ่งชนิดของข้อมูลที่มีพื้นฐานมาจาก Numpy Array มีคุณสมบันที่คล้ายคลึงกัน แต่มีข้อแตกต่างกันตรงที่ Pandas Series สามารถมี index เป็น Label หรือคือค่าอย่างอื่นที่เป็น Python object ที่ไม่ใช่ตัวเลขได้ด้วย

โดยจะทำการเรียนรู้ผ่านตัวอย่างต่าง ๆ เริ่มต้นจากการ import Numpy และ Pandas Library เข้าสู่ Notebook



```python
import numpy as np
import pandas as pd
```

##### Creating a Series
เราสามารถสร้าง Series จาก List, Numpy Array หรือ Dictionary ได้

```python
labels = ['a','b','c']
my_list = [10,20,30]
arr = np.array([10,20,30])
d = {'a':10,'b':20,'c':30}
```

######## สร้าง Series จาก List

```python
pd.Series(data=my_list)
```

```python
pd.Series(data=my_list,index=labels)
```

```python
pd.Series(my_list,labels)
```

######## สร้าง Series จาก Numpy Arrays

```python
pd.Series(arr)
```

```python
pd.Series(arr,labels)
```

######## สร้าง Series จาก Dictionary

```python
pd.Series(d)
```

##### Data in a Series
Pandas Series สามารถสร้างขึ้นมาจากองค์ประกอบที่เป็น Python Object ชนิดต่าง ๆ ได้ตัวอย่างเช่น

######## มีองค์ประกอบเป็น String

```python
pd.Series(data=labels)
```

######## มีองค์ประกอบเป็น Function

```python
pd.Series([sum,print,len])
```

##### Using an Index
หัวใจหลักในการใช้งาน Series เริ่มต้นจากการเข้าใจ index โดย Pandas ได้ถูกออกแบบมาให้สามารถใช้ชื่อ หรือตัวเลขเป็น index ได้ เพื่อความสะดวกในการเรียกใช้งานข้อมูล

เริ่มต้นเรียนรู้จากการสร้าง Series "ser1" และ "ser2"

```python
ser1 = pd.Series([1,2,3,4],
                 index = ['USA', 'Germany',
                          'USSR', 'Japan'])
```

```python
ser1
```

```python
ser2 = pd.Series([1,2,5,4],
                 index = ['USA', 'Germany',
                          'Italy', 'Japan'])
```

```python
ser2
```

######## ตัวอย่างการเรียกค่าภายใน series ผ่าน index

```python
ser1['USA']
```

######## ตัวอย่างการทำ Operation ระหว่าง Series
Operation ระหว่าง series จะกระทำต่อกันผ่านค่า index ที่เหมือนกัน

```python
ser1 + ser2
```

```python
ser2+ser1
```

#### **Pandas DataFrame
DataFrame คือ เครื่องมือหลักที่ใช้ในการทำงานของ Library Pandas โดยได้สร้างขึ้นเลียนแบบการทำงานของภาษา R

DataFrame สามารถมองได้ว่าเป็นกลุ่มกันของ Series หลาย ๆ Series เพื่อใช้งานผ่าน index ชุดเดียวกัน

เริ่มต้นทำการศึกษา Pandas DataFrame จากการ import Pandas และ Numpy เข้าสู่ Notebook และสร้าง DataFrame “df”

```python
import pandas as pd
import numpy as np
```

```python
from numpy.random import randn
np.random.seed(101)
```

```python
df = pd.DataFrame(randn(5,4),
                  index='A B C D E'.split(),
                  columns='W X Y Z'.split())
```

```python
df
```

```python

```

##### Selection and Indexing
เราสามารถเรียกข้อมูลภายใน DataFrame ได้หลากหลายวิธี เช่น

######## การเรียกผ่าน column name

```python
df['W']
```

######## การเรียกข้อมูลเป็น list ของ column name

```python

```

```python
df[['W','Z']]
```

######## การเรียกข้อมูลแบบใช้ SQL Syntax (ไม่แนะนำให้ใช้)

```python
df.W
```

######## DataFrame Columns คือ Pandas Series

```python
type(df['W'])
```

####### การสร้าง Column ใหม่ให้ DataFrame:

```python
df['new1'] = df['W'] + df['Y']
```

```python
df['new2'] = df['X'] + df['Z']
```

```python
df
```

```python

```

ให้นกศึกษาทำการสร้าง new3,new4,new5 โดยมีรูปแบบ ดังนี้
new3 (x/z) , new4(z+w) , new5(ค่า AVG (w,x,y,z ) **ทำข้อความเป็นตัวหนา**

```python

```



ให้นักนักศึกษา ทำการสร้าง DF: ขนาด ึ7 * 4 โดยมีข้อมูลด้านในบรรจุ ตัวเลขจำนวนเต็มแบบ วันในเดือน โดยทำการกำหนด หัว เป็น อาทิตย์ จันทร์ อังคาร .... เสาร์  ส่วนของ แถวกำหนดให้ week1 , week2, week3 ,week4

####### "drop"
"drop" คือ การลบ Column ออกจาก DataFrame ด้วยคำสั่ง

การ drop ยังไม่ได้ลบ column new1 ออกไปจาก df หากไม่มีการระบุให้แทนค่าใหม่ใน df

```python
df.drop('new1',axis=1)
df
```

การ drop โดยการะบุให้แทนค่าใหม่ใน df จะลบ column new1 ออกไปทันที

```python
df.drop('new1',axis=1,inplace=True)
df
```

นอกจากนี้ยังมีวิธีการลบ column แบบง่าย ๆ โดยใช้คำสั่ง "del" ซึ่งจะลบ column นั้นออกจาก DataFrame ทันที

```python
del df['new2']
```

```python
df
```

```python

```

```python

```

 lab :: ให้สร้าง col  new1(x+w)  new2(y*z)  new(x+y+z) new4 (w-z)

การ drop ยังใช้ได้กับการลบ row ตัวอย่างเช่น

```python
df.drop('E',axis=0)
```

แต่จะยังไม่แทนค่ากลับเข้าไปใน df หากไม่มีการระบุให้ "inplace = True"

####### Selecting Rows
เลือกแถวที่ index เป็น "A"

```python
df.loc['A']
```

หรือเลือกแถวตมตำแหน่งที่มันจัดวาง แทนที่การเลือกผ่าน index เช่นการเลือกแถวที่อยู่ในลำดับที่ 2 (ลำดับที่จะเริ่มต้นจาก 0) จะได้ค่าในแถวที่มี index เป็น "C" ออกมา

```python
df.iloc[2]
```

####### Selecting Subset of rows and columns
เลือกแถวที่ index เป็น “B” column เป็น “Y”

```python
df.loc['B','Y']
```

เลือกแถวที่ index เป็น “A” และ “B” column เป็น “W” และ “Y”

```python
df.loc[['A','B'],['W','Y']]
```

```python
df
```

1)ต้องการแสดงผล ข้อมูล
ให้เลือก C,X และ D,Z <BR>
2) ให้ทำการ บวกตำแหน่ง ของ A +X = New1 และ B-Y = New2

// เฉลย 2

```python
df
df['new2']= df.loc['B'] + df.loc['Z']

df
```

##### Conditional Selection
คุณสมบัติที่สำคัญของ Pandas DataFrame คือ ความสามารถในการเลือกข้อมูลภายใน DataFrame โดยการใช้เงื่อนไข ที่สามารถคัดกรองข้อมูลโดยใส่เงื่อนไขไว้ภายใน \[ \] ด้านหลังชื่อ DataFrame

คุณสมบัตินี้มีความคล้ายคลึงกับ Numpy Array

จาก DataFrame "df"

```python
df
```

```python
df>0.1
```

ใส่เงื่อนไข df>0 ภายใน \[ \] ด้านหลัง df

```python
df[df>0]
```

เลือกเฉพาะข้อมูลที่ column "W" ที่มีค่า >0

```python
df[df['W']>0]
```

เลือกเฉพาะข้อมูลที่ column "W" ที่มีค่า >0 และเลือกเฉพาะค่าใน column "Y"

```python
df[df['W']>0]['Y']
```

เลือกเฉพาะข้อมูลที่ column "W" ที่มีค่า >0 และเลือกเฉพาะค่าใน column "Y" และ "X"

```python
df[df['W']>0][['Y','X']]
```

การเลือกข้อมูลโดยใช้ 2 เงื่อนไข ทำได้โดยใช้ตัวเชื่อมเงื่อนไข
- "|" สำหรับ "or"
- "&" สำหรับ "and"

```python
df[(df['W']>1) | (df['Y'] > 1)]
```

```python
df[(df['W']>0) & (df['Y'] > 1)]
```

โจทย์ x <0  หรือ  z >= 0

```python
df[(df['X']<0)&(df['Z'] >= 0)][['Y','X']]
```

```python

```

**โจทย์  1** <BR>
import pandas as pd

## สร้าง DataFrame ตัวอย่าง
data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
        'Age': [24, 27, 22, 32, 29],
        'City': ['New York', 'Los Angeles', 'Chicago', 'Houston', 'Phoenix']}
df = pd.DataFrame(data)

## เลือกคอลัมน์ 'Name' และ 'Age'
## เลือกแถวที่มีค่า 'Age' มากกว่า 25


โจทย์ 2: จาก DataFrame ที่กำหนดให้ ให้เลือกและแสดงเฉพาะข้อมูลของแถวที่ 2 ถึงแถวที่ 4 (นับจาก 0) และคอลัมน์ 'Name' ถึง 'City'

import pandas as pd

## สร้าง DataFrame ตัวอย่าง
data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
        'Age': [24, 27, 22, 32, 29],
        'City': ['New York', 'Los Angeles', 'Chicago', 'Houston', 'Phoenix']}
df = pd.DataFrame(data)

## เปลี่ยนค่าในคอลัมน์ 'City' เป็น 'San Francisco' สำหรับแถวที่มีค่า 'Age' น้อยกว่า 25


##### More Index Details
คุณสมบัติเพิ่มเติมของ index ตัวอย่างเช่น
- การ reset ค่า index
- การตั้งค่า index เป็นค่าใหม่

จาก DataFrame "df"

```python
df
```

สามารถ reset ค่า index ได้โดย

```python
df.reset_index()
```

สามารถตั้งค่า index เป็นค่าใหม่จาก column ภายใน DataFrame ได้โดย

```python
newind = 'CA NY WY OR CO'.split()
df['States'] = newind
df
```

City  Y P N S Su

```python
df.set_index('States')
```

ซึ่งจะยังไม่แทนค่าใหม่เข้าไปใน "df" หากไม่ได้สั่งให้ "inplace = True"

```python
df.set_index('States',inplace=True)
df
```

##### Multi-Index and Index Hierarchy
DataFrame สามารถมี index ได้มากกว่าหนึ่งชั้น เราสามารถเรียนรู้ได้จากตัวอย่างต่อไปนี้

```python
# Index Levels
outside = ['G1','G1','G1','G2','G2','G2']
inside = [1,2,3,1,2,3]
hier_index = list(zip(outside,inside))
hier_index = pd.MultiIndex.\
             from_tuples(hier_index)
```

```python
hier_index
```

```python
df = pd.DataFrame(np.random.randn(6,2),
                  index=hier_index,
                  columns=['A','B'])
df
```

เราสามารถเรียกข้อมูลจาก index ที่มีหลายชั้นได้จาก df.loc\[ \]

ในกรณีที่ต้องการเรียก column เราสามารถใช้เพียงแค่ df\['columns name'\] ได้เหมือนเดิม

การเรียกข้อมูลโดยการใช้ index เพียงแค่ 1 ชั้น จะส่งค่าที่เป็น sub-dataframe กลับออกมา ตัวอย่างเช่น

```python
df.loc['G1']
```

เรียกค่าโดยใช้ index ทั้ง 2 ชั้น

```python
df.loc['G1'].loc[1]
```

เราสามารถเรียกดูชื่อชั้นของ index ได้โดย ซึ่งตอนนี้ยังไม่มีชื่อ

```python
df.index.names
```

เราสามารถตั้งชื่อชั้นของ index ได้

```python
df.index.names = ['Group','Num']
df
```

เรียกค่าจาก df ที่มี index ชั้นใดชั้นหนึ่งเป็น "G1"

```python
df.xs('G1')
```

เรียกค่าจาก df ที่มี index ชั้นแรกเป็น "G1" และชั้นที่ 2 เป็น 1

```python
df.xs(['G1',2])
```

เรียกค่าจาก df โดยระบุชั้นของ index เป็น "Num" และมาค่าเป็น 1

```python
df.xs(1,level='Num')
```

#### ** Missing Data
เรียนรู้การใช้ Pandas ในการจัดการ Missing Data

เริ่มต้นจาก import Numpy และ Pandas เข้าสู้ Notebook และสร้าง DataFrame "df"

```python
import numpy as np
import pandas as pd
```

```python
df = pd.DataFrame({'A':[1,2,np.nan],
                  'B':[5,np.nan,np.nan],
                  'C':[1,2,3]})
df
```

df มีค่าภายใน เป็น NaN (Not a Number)

เราสามารถกำจัด row ที่มีค่า NaN ทั้งหมด ออกจาก df ได้โดย

```python
df.dropna()
```

สามารถกำจัด column ที่มีค่า NaN ทั้งหมด ออกจาก df ได้โดย

```python
df.dropna(axis=1)
```

กำจัดแถวที่มีค่าเป็น NaN ตั้งแต่ 2 ค่าขึ้นไป

```python
df.dropna(thresh=2)
```

เปลี่ยนค่า NaN เป็นค่าอื่น

```python
df.fillna(value='FILL VALUE')
```

เปลี่ยนค่า NaN ใน column "A" เป็นค่าเฉลี่ยของ column "A"

```python
df['A'].fillna(value=df['A'].mean())
```

#### ** Groupby
Groupby เป็นคำสั่งที่ช่วยในการจัดกลุ่มแถวของข้อมูลที่มีค่าเหมือนกัน แล้วสรุปค่าออกมาด้วย aggregate methods

เริ่มต้นจาก import Pandas และสร้าง DataFrame จาก Dictionary

```python
import pandas as pd
# Create dataframe
data = {'Company':['GOOG','GOOG','MSFT',
                   'MSFT','FB','FB'],
       'Person':['Sam','Charlie','Amy',
                 'Vanessa','Carl','Sarah'],
       'Sales':[200,120,340,124,243,350]}
```

```python
df = pd.DataFrame(data)
df
```

จากนั้นลองใช้ df.groupby() เพื่อจัดกลุ่มของ row ตามค่าใน column ตัวอย่างเช่น จัดกลุ่มของค่าใน column "Company"

```python
df.groupby('Company')
```

```python
df['Sales'] = df['Sales'].str.replace('$', '', regex=False).astype(float)
```



df.groupby() จะมีค่าเป็น object หนึ่ง ซึ่งสามารถสร้างตัวแปรขึ้นมารับค่าเก็บไว้ได้

```python
by_comp = df.groupby("Company")
```

```python

```

จากนั้นสามารถนำ aggregate methods มาคำนวณค่าออกมา เช่น การคำนวณค่าเฉลี่ย

```python
#by_comp.mean()

by_comp = df.groupby("Company")
by_comp.mean()
```

ซึ่งมีค่าเหมือนกับ

```python
df.groupby('Company').mean()
```

**ตัวอย่างการใช้ aggregate methods อื่น**

การคำนวนค่า Standard Deviation

```python
by_comp.std()
```

การคำนวนค่าที่น้อยที่สุด

```python
by_comp.min()
```

การคำนวนค่าที่มากที่สุด

```python
by_comp.max()
```

การนับจำนวน (Count)

```python
by_comp.count()
```

การคำนวณค่าทางสถิติ ต่าง ๆ ออกมาแสดง พร้อม ๆ กัน

```python
by_comp.describe()
```

การแสดงค่าโดยใช้ transpose

```python
by_comp.describe().transpose()
```

การแสดงค่าโดยใช้ transpose และเลือกเฉพาะ column 'GOOG'

```python
by_comp.describe().transpose()['GOOG']
```

#### ** Merging, Joining, and Concatenating
การรวม DataFrame เข้าด้วยกัน มีวิธีการหลักอยู่ 3 วิธี ได้แก่
- Merging
- Joining
- Concatenating

เริ่มต้นการเรียนรู้จากการสร้างตัวอย่าง DataFrame 3 ตัวอย่าง

```python
import pandas as pd
```

```python
df1 = pd.DataFrame({'A': ['A0', 'A1',
                          'A2', 'A3'],
                    'B': ['B0', 'B1',
                          'B2', 'B3'],
                    'C': ['C0', 'C1',
                          'C2', 'C3'],
                    'D': ['D0', 'D1',
                          'D2', 'D3']},
                    index=[0, 1, 2, 3])
df1
```

```python
df2 = pd.DataFrame({'A': ['A4', 'A5',
                          'A6', 'A7'],
                    'B': ['B4', 'B5',
                          'B6', 'B7'],
                    'C': ['C4', 'C5',
                          'C6', 'C7'],
                    'D': ['D4', 'D5',
                          'D6', 'D7']},
                    index=[4, 5, 6, 7])
df2
```

```python
df3 = pd.DataFrame({'A': ['A8', 'A9',
                          'A10', 'A11'],
                    'B': ['B8', 'B9',
                          'B10', 'B11'],
                    'C': ['C8', 'C9',
                          'C10', 'C11'],
                    'D': ['D8', 'D9',
                          'D10', 'D11']},
                    index=[8, 9, 10, 11])
df3
```

##### Concatenation
Concatenation เป็นการนำข้อมูลมาเรียงต่อกัน โดยจะต่อกันจะยึดตามคุณสมบัติ (columns หรือ index) คุณสมบัติเดียวกัน จึงจะเรียงต่อกันได้

โดยเราสามารถใช้คำสั่ง "pd.concat( )" แล้วใส่ list ของ DataFrame ที่ต้องการจะนำมาต่อกันเข้าไปใน ( ) ดังตัวอย่าง

```python
pd.concat([df1,df2,df3])
```

มีค่าเท่ากับคำสั่ง pd.concat([df1,df2,df3],axis=0)

“axis=0” คือคำสั่งให้ต่อกันโดยยึดคุณสมบัติตาม columns

```python
pd.concat([df1,df2,df3],axis=0)
```

“axis=1” คือคำสั่งให้ต่อกันโดยยึดคุณสมบัติตาม rows

```python
pd.concat([df1,df2,df3],axis=1)
```

##### Merging
Merge คือ การเชื่อมต่อข้อมูล โดยใช้เงื่อนไขที่เหมือนกันมาช่วยในการเชื่อมต่อ คล้าย ๆ กับการ merge ใน SQL

เรียนรู้การ merge โดยการสมมติ DataFrame ขึ้นมา 2 ตัวอย่าง

```python
left = pd.DataFrame({'key': ['K0', 'K1',
                             'K2', 'K3'],
                     'A': ['A0', 'A1',
                           'A2', 'A3'],
                     'B': ['B0', 'B1',
                           'B2', 'B3']})

right = pd.DataFrame({'key': ['K0', 'K1',
                              'K2', 'K3'],
                      'C': ['C0', 'C1',
                            'C2', 'C3'],
                      'D': ['D0', 'D1',
                            'D2', 'D3']})
```

```python
left
```

```python
right
```

ใช้คำสั่ง pd.merge( ) สำหรับ merge 2 DataFrame เข้าด้วยกัน ตามเงื่อนไขที่กำหดไว้ ดังแสดงในตัวอย่าง

```python
pd.merge(left,right,how='inner',on='key')
```

สร้างตัวอย่างข้อมูลสำหรับการ merge ที่ซับซ้อนมากขึ้น

```python
left = pd.DataFrame({'key1': ['K0', 'K0',
                              'K1', 'K2'],
                     'key2': ['K0', 'K1',
                              'K0', 'K1'],
                        'A': ['A0', 'A1',
                              'A2', 'A3'],
                        'B': ['B0', 'B1',
                              'B2', 'B3']})

right = pd.DataFrame({'key1': ['K0', 'K1',
                               'K1', 'K2'],
                      'key2': ['K0', 'K0',
                               'K0', 'K0'],
                         'C': ['C0', 'C1',
                               'C2', 'C3'],
                         'D': ['D0', 'D1',
                               'D2', 'D3']})
```

ตัวอย่าง DataFrame ชุดใหม่

```python
left
```

```python
right
```

merge โดยใช้เงื่อนไขจาก 2 columns

```python
pd.merge(left, right, on=['key1', 'key2'])
```

มีค่าเท่ากับการทำ inner merge

```python
pd.merge(left, right,
         how='inner', on=['key1', 'key2'])
```

การทำ outer merge

```python
pd.merge(left, right,
         how='outer', on=['key1', 'key2'])
```

การทำ right merge

```python
pd.merge(left, right,
         how='right', on=['key1', 'key2'])
```

การทำ left merge

```python
pd.merge(left, right,
         how='left', on=['key1', 'key2'])
```

##### Joining
Join เป็นคำสั่งสำหรับการรวม 2 DataFrame ที่มี index ที่แตกต่างกันให้กลายเป็น DataFrame เดียวกัน

สร้างตัวอย่าง DataFrame 2 ตัวอย่าง สำหรับเพื่อเรียนรู้การใช้คำสั่ง Join

```python
left = pd.DataFrame({'A': ['A0', 'A1',
                           'A2'],
                     'B': ['B0', 'B1',
                           'B2']},
                      index=['K0', 'K1',
                             'K2'])

right = pd.DataFrame({'C': ['C0', 'C2',
                            'C3'],
                      'D': ['D0', 'D2',
                            'D3']},
                      index=['K0', 'K2',
                             'K3'])
```

```python
left
```

```python
right
```

การ join แบบไม่ใส่เงื่อนไขใด จะยึดเอา index ของตัวตั้งต้น (ตัวด้านซ้าย) เป็นหลัก ให้ผลเหมือนการให้ how = 'left'

```python
left.join(right)
```

```python
left.join(right, how = 'left')
```

การ join แบบ outer จะรวมทุกค่าที่มีในทั้ง 2 DataFrame เข้าไปเป็น DataFrame เดียวกัน

```python
left.join(right, how='outer')
```

การ join แบบ right จะยึดเอา index ของตัวที่เอามา join (ตัวด้านขวา) เป็นหลัก

```python
left.join(right, how='right')
```

#### ** Operations
มีตัวดำเนินการ (Operators) มากมายใน Pandas ที่ใช้งานในการตรวจสอบและวิเคราะห์ข้อมูลภายใน DataFrame ดังตัวอย่างด้านล่าง

สร้าง DataFrame เพื่อเป็นตัวอย่างในการเรียนรู้

```python
import pandas as pd
df = pd.DataFrame({'col1':[1,2,3,4],
                   'col2':[444,555,
                           666,444],
                   'col3':['abc','def',
                           'ghi','xyz']})
df.head()
```

##### Info on Unique Values
**unique** เป็น คำสั่งสำหรับตรวจสอบข้อมูลที่ไม่ซ้ำกันใน column เดียวกัน

```python
df['col2'].unique()
```

**nunique** เป็นคำสั่งสำหรับนับจำนวนข้อมูลที่ไม่ซ้ำกันใน column เดียวกัน

```python
df['col2'].nunique()
```

**value_counts** เป็นคำสั่งสำหรับนับจำนวนข้อมูลครั้งที่แต่ละ unique ค่าเกิดขึ้น

```python
df['col2'].value_counts()
```

##### Selecting Data
ใช้เงื่อนไขในการเลือกข้อมูลจาก DataFrame สามารถใช้ได้มากกว่า 1 เงื่อนไข ดังได้กล่าวไปแล้วข้างต้น

```python
newdf = df[(df['col1']>2)
           & (df['col2']==444)]
newdf
```

##### Applying Functions
**apply** เป็นคำสั่งที่ใช้ในการส่งค่าแต่ละค่าใน DataFrame ไปแทนค่าใน Function

```python
def times2(x):
    return x*2
```

ส่งค่าใน col1 ไปผ่าน function "time2"

```python
df['col1'].apply(times2)
```

ส่งค่าใน col3 ไปผ่าน function "len"

```python
df['col3'].apply(len)
```

##### Satistical Calculation Functions
ประกอบ function ในการคำนวณหาค่าทางสถิติต่าง ๆ ในแต่ละ columns

คำนวณผลรวมใน column col1

```python
df['col1'].sum()
```

คำนวณค่าเฉลี่ยใน column col1

```python
df['col1'].mean()
```

คำนวณค่าที่น้อยที่สุดใน column col1

```python
df['col1'].min()
```

คำนวณค่าที่มากที่สุดใน column col1

```python
df['col1'].max()
```

คำนวณค่า Standard Deviation ใน column col1

```python
df['col1'].std()
```

นับจำนวนข้อมูลที่อยู่ใน column col1

```python
df['col1'].count()
```

คำนวณค่าสถิติต่าง ๆ ใน column col1

```python
df['col1'].describe()
```

```python
df.describe()
```

##### Permanently Removing a Column
การลบ column ใน DataFrame แบบถาวร

```python
del df['col1']
```

```python
df
```

##### Get Column and Index Names
การเรียกดูชื่อ column

```python
df.columns
```

การเรียกดูชื่อ index

```python
df.index
```

##### Sorting and Ordering a DataFrame
จัดลำดับค่าใน DataFrame

เรียงลำดับค่าใน df ตามค่าใน column col2 โดยยังไม่มีการแทนค่ากลับเข้าไปในตัวแปร df

หากต้องการให้แทนค่ากลับเข้าไปในตัวแปร df ให้กำหนด  “inplace = True” ไว้ในคำสั่งด้วย

```python
df.sort_values(by='col2')
```

##### Check Null Values
เป็นการตรวจสอบว่ามีค่า Missing Value ใน DataFrame หรือไม่

ตรวจสอบโดยใช้คำสั่ง df.isnull( )

```python
df.isnull()
```

ใช้คำสั่ง df.isnull().sum() เพื่อตรวจสอบมี missing value ในแต่ละ column เป็นจำนวนเท่าไหร่

```python
df.isnull().sum()
```

```python
df.dropna()
```

##### Filling in NaN values with something else
แทนค่า NaN ใน DataFrame ด้วยค่าอย่างอื่น

สร้าง DataFrame ที่มีค่า NaN ขึ้นมา 1 ตัวอย่าง

```python
import numpy as np
df = pd.DataFrame({'col1':[1,2,
                           3,np.nan],
                   'col2':[np.nan,555,
                           666,444],
                   'col3':['abc','def',
                           'ghi','xyz']})
df.head()
```

แทนค่า NaN ด้วยคำสั่ง df.fillna( )

```python
df.fillna('FILL')
```

##### Create Pivot Table
สร้างตัวอย่าง DataFrame เพื่อใช้เรียนรู้การสร้าง Pivot Table

```python
data = {'A':['foo','foo','foo',
             'bar','bar','bar'],
        'B':['one','one','two',
             'two','one','one'],
        'C':['x','y','x','y','x','y'],
        'D':[1,3,2,5,4,1]}

df = pd.DataFrame(data)
df
```

สร้าง Pivot Table โดยใช้คำสั่ง df.pivot_table( )

```python
df.pivot_table(values='D',
               index=['A', 'B'],
               columns=['C'])
```

#### ** Data Input and Output
Pandas สามารถอ่านข้อมูลได้หลายประเภท โดยการใช้คำสั่ง pd.read_methods เช่น
- pd.read_csv()
- pd.read_excel()

### 📂 Reading Data

```python
from google.colab import drive
drive.mount('/content/drive')
```

```python
import csv
```

```python

```

##### CSV
####### CSV Input
pd.read_csv() เป็นการใช้ pandas อ่านไฟล์ CSV เพื่อดึงข้อมูลเข้ามาเป็น DataFrame
import pandas as pd
df = pd.read_csv('dataset/1500000SalesRecords.csv')

```python
import csv
```

```python
df = pd.read_csv('/content/sample_data/california_housing_train.csv')
df
```

```python

```

####### CSV Output
df.to_csv() เป็นการ export DataFrame ออกไปเป็นไฟล์ CSV

```python
#path = '/content/dataset/'
path = '/content/drive/MyDrive/Colab Notebooks/dataset'
df.to_csv(path+'example3',index=False)
```



##### Excel
Pandas สามารถใช้ในการอ่าน และเขียนไฟล์ excel ได้ แต่เป็นเพียงการดึงข้อมูลภายในตารางเท่านั้น ไม่เกี่ยวข้องกับรูปภาพ หรือ สูตรที่อยู่ภายในไฟล์

####### Excel Input
pd.read_excel( ) เป็นการอ่านไฟล์ excel

โดยในตัวอย่างได้อ่านไฟล์ชื่อ 'Excel_Sample.xlsx" Sheet ชื่อ "Sheet1

```python
#path ='/dataset/Excel_Sample.xlsx'
/content/sample_data/SPU training.xlsx
```

```python
pd.read_excel('/content/sample_data/Excel_Sample.xlsx',sheet_name='Sheet1')
```

####### Excel Output
df.to_excel() เป็นการ export DataFrame ออกไปเป็นไฟล์ excel

โดยในตัวอย่างได้ export ไปยังไฟล์ชื่อ "Excel_sample.xlsx" และ sheet ชื่อ "Sheet1"

```python
path2='/content/drive/MyDrive/dataset/Excel_Sample1.xlsx'
df.to_excel(path2,
            sheet_name='Sheet1',
            index = False)
```

```python

```
