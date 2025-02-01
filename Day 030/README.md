# Challenge Day 30

## 📝 Topik
**Review dan Mini-Project**

Menerapkan seluruh konsep yang telah dipelajari dalam **Exploratory Data Analysis (EDA)** lengkap untuk mendapatkan insight dari dataset.

---

## 🎯 Learning Objectives
1. **Mengulang kembali konsep utama** dari data preprocessing, analisis, visualisasi, dan machine learning dasar.
2. **Melakukan EDA** yang mencakup pembersihan data, visualisasi, dan analisis statistik.
3. **Menginterpretasikan hasil analisis** dan menarik kesimpulan dari dataset yang dipilih.
4. **Menyusun laporan ringkas** berdasarkan hasil EDA.

---

## 🏆 Aktivitas/Tantangan

### Reflection
Selamat! Anda telah menyelesaikan perjalanan 30 hari belajar tentang analisis data dan machine learning dasar.
Hari ini adalah waktu untuk mempraktikkan semua yang telah dipelajari dengan melakukan **Exploratory Data Analysis (EDA) lengkap** pada dataset pilihan Anda.

### Deskripsi
EDA adalah proses eksplorasi awal untuk memahami struktur data, membersihkan data, menemukan pola, dan mendapatkan insight sebelum membanguun model machine learning.
Tahapan:
1. Memilih datase
2. Membersihkan data
3. Melakukan eksplorasi statistik
4. Memvisualisasikan data
5. Merangkum insight utama

---
## 🚀 Langkah-Langkah

### Import Library dan Load Dataset
Gunakan dataset Titanic sebagai contoh.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = sns.load_dataset("titanic")

df.head()
```
Output:
```bash
survived	pclass	sex	age	sibsp	parch	fare	embarked	class	who	adult_male	deck	embark_town	alive	alone
0	0	3	male	22.0	1	0	7.2500	S	Third	man	True	NaN	Southampton	no	False
1	1	1	female	38.0	1	0	71.2833	C	First	woman	False	C	Cherbourg	yes	False
2	1	3	female	26.0	0	0	7.9250	S	Third	woman	False	NaN	Southampton	yes	True
3	1	1	female	35.0	1	0	53.1000	S	First	woman	False	C	Southampton	yes	False
4	0	3	male	35.0	0	0	8.0500	S	Third	man	True	NaN	Southampton	no	True
```

### Eksplorasi Awal Dataset
Lihat informasi dasar dataset.
```python
df.info()
```
Output:
```bash
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 891 entries, 0 to 890
Data columns (total 15 columns):
 #   Column       Non-Null Count  Dtype   
---  ------       --------------  -----   
 0   survived     891 non-null    int64   
 1   pclass       891 non-null    int64   
 2   sex          891 non-null    object  
 3   age          714 non-null    float64 
 4   sibsp        891 non-null    int64   
 5   parch        891 non-null    int64   
 6   fare         891 non-null    float64 
 7   embarked     889 non-null    object  
 8   class        891 non-null    category
 9   who          891 non-null    object  
 10  adult_male   891 non-null    bool    
 11  deck         203 non-null    category
 12  embark_town  889 non-null    object  
 13  alive        891 non-null    object  
 14  alone        891 non-null    bool    
dtypes: bool(2), category(2), float64(2), int64(4), object(5)
memory usage: 80.7+ KB
```
```python
df.describe(include="all")
```
Output:
```bash
survived	pclass	sex	age	sibsp	parch	fare	embarked	class	who	adult_male	deck	embark_town	alive	alone
count	891.000000	891.000000	891	714.000000	891.000000	891.000000	891.000000	889	891	891	891	203	889	891	891
unique	NaN	NaN	2	NaN	NaN	NaN	NaN	3	3	3	2	7	3	2	2
top	NaN	NaN	male	NaN	NaN	NaN	NaN	S	Third	man	True	C	Southampton	no	True
freq	NaN	NaN	577	NaN	NaN	NaN	NaN	644	491	537	537	59	644	549	537
mean	0.383838	2.308642	NaN	29.699118	0.523008	0.381594	32.204208	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
std	0.486592	0.836071	NaN	14.526497	1.102743	0.806057	49.693429	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
min	0.000000	1.000000	NaN	0.420000	0.000000	0.000000	0.000000	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
25%	0.000000	2.000000	NaN	20.125000	0.000000	0.000000	7.910400	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
50%	0.000000	3.000000	NaN	28.000000	0.000000	0.000000	14.454200	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
75%	1.000000	3.000000	NaN	38.000000	1.000000	0.000000	31.000000	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
max	1.000000	3.000000	NaN	80.000000	8.000000	6.000000	512.329200	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN
```

Cek apakah ada missing values.
```python
print("Missing Values: ")
print(df.isnull().sum())
```
Output:
```bash
Missing Values: 
survived         0
pclass           0
sex              0
age            177
sibsp            0
parch            0
fare             0
embarked         2
class            0
who              0
adult_male       0
deck           688
embark_town      2
alive            0
alone            0
dtype: int64
```

### Membersihkan Data
Tangani nilai yang hilang pada kolom **age** dengan imputasi median.
```python
df[“age”].fillna(df[“age”].median(), inplace=True)
```
Hapus kolom yang kurang relevan seperti **deck** (banyak missing values).
```python
df.drop(columns=[“deck”, “embark_town”], inplace=True)
```

Transformasi data object menjadi data numerik
```python
df["sex"] = df["sex"].map({"male": 0, "female": 1})
df = pd.get_dummies(df, columns=["embarked"], drop_first=True)
df["class"] = df["class"].map({"First": 1, "Second": 2, "Third": 3})
df["who"] = df["who"].map({"man": 0, "woman": 1, "child": 2})
df["alive"] = df["alive"].map({"yes": 1, "no": 0})
```

### Visualisasi Distribusi Data
Distribusi usia penumpang.
```python
plt.figure(figsize=(8, 5))
sns.histplot(df["age"], bins=30, kde=True, color="blue")
plt.title("Distribusi Usia Penumpang")
plt.xlabel("Usia")
plt.ylabel("Jumlah")
plt.savefig('Day_030_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20030/Day_030_01.png" width=”500”>

### Analisis Korelasi Antar Fitur
Cek korelasi antara fitur numerik.
```python
plt.figure(figsize=(10, 6))
sns.heatmap(df.corr(), annot=True, cmap="coolwarm", linewidths=0.5)
plt.title("Korelasi Antar Fitur")
plt.savefig('Day_030_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20030/Day_030_02.png" width=”500”>

### Analisis Kelangsungan Hidup Berdasarkan Faktor-Faktor Tertentu
Survival rate berdasarkan jenis kelamin.
```python
plt.figure(figsize=(6, 4))
sns.barplot(x="sex", y="survived", data=df, palette="coolwarm")
plt.title("Survival Rate Berdasarkan Jenis Kelamin")
plt.savefig('Day_030_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20030/Day_030_03.png" width=”500”>

### Analisis Kelangsungan Hidup Berdasarkan Faktor-Faktor Tertentu
Survival rate berdasarkan kelas tiket.
```python
plt.figure(figsize=(6, 4))
sns.barplot(x="pclass", y="survived", data=df, palette="viridis")
plt.title("Survival Rate Berdasarkan Kelas Tiket")
plt.savefig('Day_030_04.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20030/Day_030_04.png" width=”500”>

### Visualisasi Outliers pada Fare
Cek apakah ada outliers pada harga tiket.
```python
plt.figure(figsize=(8, 5))
sns.boxplot(x=df["fare"], color="red")
plt.title("Distribusi Harga Tiket (Fare)")
plt.savefig('Day_030_05.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20030/Day_030_05.png" width=”500”>


### Rangkum Insight dari EDA
Dari hasil analisis yang telah dilakukan, berikut beberapa temuan utama:
- Wanita memiliki tingkat kelangsungan hidup lebih tinggi dibanding pria.
- Penumpang kelas pertama memiliki peluang lebih besar untuk selamat dibanding kelas lainnya.
- Sebagian besar penumpang berada dalam rentang usia 20-40 tahun.
- Terdapat beberapa outliers pada harga tiket yang mungkin perlu ditangani sebelum pemodelan lebih lanjut.

### Kesimpulan 
Hari ini, Anda telah berhasil melakukan EDA menyeluruh pada dataset dan merangkum insight penting dari data! 🎉

Selamat menyelesaikan tantangan 30 hari! 🚀🔥
