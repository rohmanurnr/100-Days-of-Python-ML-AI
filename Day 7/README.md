# Challenge Day 7 

## 📝 Topik
**Membaca dan Menulis Data dengan Pandas**

---

## 🎯 Learning Objectives
1. Memahami cara membaca file data seperti CSV atau Excel menggunakan Pandas.
2. Menggunakan fungsi `read_csv()` dan `read_excel()` untuk memuat data ke dalam DataFrame.
3. Menyimpan DataFrame ke format lain seperti CSV, Excel, atau JSON menggunakan `to_csv()` dan `to_excel()`.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Kemampuan membaca dan menulis data adalah fondasi penting dalam analisis data. Pandas menyediakan fungsi yang sangat fleksibel untuk membaca berbagai jenis file, seperti CSV, Excel, JSON, dan banyak lagi. Dengan fungsi yang sama, kita juga dapat menyimpan hasil analisis ke format file yang sesuai untuk berbagi atau penyimpanan.

---
## 📂 File Input
Sebelum memulai, Anda memerlukan file **iris.csv** sebagai data input. Anda dapat mengunduh file ini melalui tautan berikut:
- [Unduh iris.csv](https://github.com/mwaskom/seaborn-data/blob/master/iris.csv)

Simpan file tersebut di direktori kerja yang sama dengan script Python Anda.

---
## 🛠️ Persyaratan
Python >= 3.7
Library yang diperlukan:
- pandas
- openpyxl (untuk membaca/menulis Excel)
Install library menggunakan pip:
```bash
pip install pandas openpyxl
```

---
## 🚀 Langkah-Langkah

### 1. Membaca File CSV/Excel
Gunakan Pandas untuk membaca file CSV atau Excel ke dalam DataFrame.

#### a. Membaca file CSV
```python
import pandas as pd

df_csv = pd.read_csv('iris.csv')  # Ganti dengan path file CSV Anda
print(df_csv.head())
```
Output:
```bash
   sepal.length  sepal.width  petal.length  petal.width variety
0           5.1          3.5           1.4          0.2  Setosa
1           4.9          3.0           1.4          0.2  Setosa
2           4.7          3.2           1.3          0.2  Setosa
3           4.6          3.1           1.5          0.2  Setosa
4           5.0          3.6           1.4          0.2  Setosa
```

#### b. Membaca file Excel
```python
import pandas as pd

df_excel = pd.read_excel('iris.xlsx')  # Ganti dengan path file Excel Anda
print(df_excel.head())
```
Output:
```bash
   sepal.length  sepal.width  petal.length  petal.width variety
0           5.1          3.5           1.4          0.2  Setosa
1           4.9          3.0           1.4          0.2  Setosa
2           4.7          3.2           1.3          0.2  Setosa
3           4.6          3.1           1.5          0.2  Setosa
4           5.0          3.6           1.4          0.2  Setosa
```

### 2. Menyimpan DataFrame ke Format Lain
Gunakan Pandas untuk menyimpan DataFrame ke format file lain.
#### a. Menyimpan DataFrame ke CSV
```python
df_csv.to_csv('output_data.csv', index=False)
print("Data berhasil disimpan ke output_data.csv")
```
Output:
```bash
Data berhasil disimpan ke output_data.csv
```

#### b. Menyimpan DataFrame ke Excel
```python
df_excel.to_excel('output_data.xlsx', index=False)
print("Data berhasil disimpan ke output_data.xlsx")
```
Output:
```bash
Data berhasil disimpan ke output_data.xlsx
```

#### c. Menyimpan DataFrame ke JSON
```python
df_csv.to_json('output_data.json', orient='records')
print("Data berhasil disimpan ke output_data.json")
```
Output:
```bash
Data berhasil disimpan ke output_data.json
```
### Eksplorasi Data
Tampilkan beberapa baris pertama dari data untuk memastikan data terbaca dengan benar. Lakukan eksplorasi dasar untuk memahami dataset.
#### a. Menampilkan Informasi Dataset
```python
print("\n=== Informasi Dataset CSV ===")
print(df_csv.info())
```
Output:
```bash
=== Informasi Dataset CSV ===
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 150 entries, 0 to 149
Data columns (total 5 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   sepal.length  150 non-null    float64
 1   sepal.width   150 non-null    float64
 2   petal.length  150 non-null    float64
 3   petal.width   150 non-null    float64
 4   variety       150 non-null    object 
dtypes: float64(4), object(1)
memory usage: 6.0+ KB
None
```
#### b. Melihat Statistik Dasar
```python
print("\n=== Statistik Dataset Excel ===")
print(df_excel.describe())
```
Output:
```bash
=== Statistik Dataset Excel ===
       sepal.length  sepal.width  petal.length  petal.width
count    150.000000   150.000000    150.000000   150.000000
mean       5.843333     3.057333      3.758000     1.199333
std        0.828066     0.435866      1.765298     0.762238
min        4.300000     2.000000      1.000000     0.100000
25%        5.100000     2.800000      1.600000     0.300000
50%        5.800000     3.000000      4.350000     1.300000
75%        6.400000     3.300000      5.100000     1.800000
max        7.900000     4.400000      6.900000     2.500000
```
📂 File dan Format Output
Input File: 'iris.csv, 'iris.xlsx'
Output File:
- 'output_data.csv'
- 'output_data.xlsx'
- 'output_data.json'
