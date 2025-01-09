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

```

#### b. Membaca file Excel
```python
import pandas as pd

df_excel = pd.read_excel('iris.xlsx')  # Ganti dengan path file Excel Anda
print(df_excel.head())
```
Output:
```bash

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

```

#### b. Menyimpan DataFrame ke Excel
```python
df_excel.to_excel('output_data.xlsx', index=False)
print("Data berhasil disimpan ke output_data.xlsx")
```
Output:
```bash

```

#### c. Menyimpan DataFrame ke JSON
```python
df_csv.to_json('output_data.json', orient='records')
print("Data berhasil disimpan ke output_data.json")
```
Output:
```bash

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

```
#### b. Melihat Statistik Dasar
```python

```
Output:
```bash

```
📂 File dan Format Output
Input File: 'iris.csv, 'iris.xlsx'
Output File:
- 'output_data.csv'
- 'output_data.xlsx'
- 'output_data.json'
