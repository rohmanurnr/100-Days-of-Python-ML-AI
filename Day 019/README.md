# Challenge Day 19

## 📝 Topik
**Analisis Data Temporal**

Menganalisis dataset berbasis waktu menggunakan Pandas, termasuk ekstraksi komponen waktu, visualisasi tren, dan agregasi berbasis periode.

---

## 🎯 Learning Objectives
1. Memahami konsep data temporal dan peranannya dalam analisis data.
2. Menggunakan Pandas untuk memanipulasi data berbasis waktu, seperti parsing datetime dan ekstraksi komponen waktu.
3. Menganalisis tren temporal dengan agregasi berbasis waktu (harian, bulanan, tahunan).
4. Membuat visualisasi tren waktu untuk menemukan pola.
5. Menerapkan fungsi rolling window untuk analisis tren musiman.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Data temporal adalah data yang dikaitkan dengan dimensi waktu, seperti penjualan harian, suhu bulanan, atau aktivitas pengguna berdasarkan waktu. Analisis data temporal memungkinkan kita untuk memahami tren, pola musiman, dan hubungan berbasis waktu. Dengan menggunakan Pandas, kita dapat dengan mudah memanipulasi dan menganalisis dataset berbasis waktu.

Contoh penggunaan:

- Analisis penjualan bulanan.
- Perhitungan rata-rata suhu tahunan.
- Identifikasi puncak aktivitas pengguna berdasarkan hari.

---
## 🚀 Langkah-Langkah

### Persiapan Dataset
Gunakan dataset berbasis waktu (misalnya, penjualan harian).
```python
import pandas as pd
import numpy as np

np.random.seed(42)
date_range = pd.date_range(start="2023-01-01", end="2023-12-31", freq="D")
sales = np.random.randint(50, 500, size=len(date_range))

data = {
    'Tanggal': date_range,
    'Penjualan': sales
}

df = pd.DataFrame(data)
print("Dataset:")
print(df.head())
```
Output:
```bash

Dataset:
     Tanggal  Penjualan
0 2023-01-01        152
1 2023-01-02        485
2 2023-01-03        398
3 2023-01-04        320
4 2023-01-05        156
```

### Parsing dan Manipulasi Waktu
Konversi kolom waktu ke format datetime dan ekstraksi komponen waktu, seperti tahun, bulan, dan hari.
```python
df['Tanggal'] = pd.to_datetime(df['Tanggal'])

df['Tahun'] = df['Tanggal'].dt.year
df['Bulan'] = df['Tanggal'].dt.month
df['Hari'] = df['Tanggal'].dt.day

print("\nDataset dengan Komponen Waktu:")
print(df.head())
```
Output:
```bash
Dataset dengan Komponen Waktu:
     Tanggal  Penjualan  Tahun  Bulan  Hari
0 2023-01-01        152   2023      1     1
1 2023-01-02        485   2023      1     2
2 2023-01-03        398   2023      1     3
3 2023-01-04        320   2023      1     4
4 2023-01-05        156   2023      1     5
```

### Agregasi Temporal
Lakukan agregasi berdasarkan waktu (misalnya, total penjualan bulanan atau mingguan).
```python
monthly_sales = df.groupby('Bulan')['Penjualan'].sum()

print("\nTotal Penjualan Bulanan:")
print(monthly_sales)
```
Output:
```bash
Total Penjualan Bulanan:
Bulan
1      8607
2      7405
3      9058
4      8812
5      8008
6      8360
7      7724
8      9274
9      7597
10    10071
11     7885
12     9055
Name: Penjualan, dtype: int32
```

### Visualisasi Data Temporal
Visualisasi tren penjualan harian
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 5))
monthly_sales.plot(kind='bar', color='orange')
plt.title('Total Penjualan Bulanan')
plt.xlabel('Bulan')
plt.ylabel('Total Penjualan')
plt.xticks(range(12), ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun', 'Jul', 'Agu', 'Sep', 'Okt', 'Nov', 'Des'], rotation=45)
plt.savefig(‘19_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20019/19_01.png" width=”500”>

Visualisasi tren penjualan bulanan
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 6))
plt.plot(df['Tanggal'], df['Penjualan'], label='Penjualan Harian', color='blue')
plt.title('Tren Penjualan Harian')
plt.xlabel('Tanggal')
plt.ylabel('Penjualan')
plt.legend()
plt.grid()
plt.savefig(‘19_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20019/19_02.png" width=”500”>

### Analisis Rolling Window
Terapkan fungsi rolling untuk menghitung rata-rata bergerak atau pola musiman.
```python
df['Rolling 7 Hari'] = df['Penjualan'].rolling(window=7).mean()

plt.figure(figsize=(12, 6))
plt.plot(df['Tanggal'], df['Penjualan'], label='Penjualan Harian', color='blue', alpha=0.5)
plt.plot(df['Tanggal'], df['Rolling 7 Hari'], label='Rata-Rata 7 Hari', color='red')
plt.title('Tren Penjualan Harian dengan Rata-Rata Bergerak')
plt.xlabel('Tanggal')
plt.ylabel('Penjualan')
plt.legend()
plt.grid()
plt.savefig(‘19_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20019/19_03.png" width=”500”>

### Kesimpulan 
1. Data temporal dapat dianalisis untuk memahami tren, pola musiman, dan fluktuasi.
2. Dengan Pandas, kita dapat memanipulasi kolom waktu, mengagregasi data, dan menghitung rata-rata bergerak untuk analisis lebih mendalam.
3. Visualisasi tren waktu membantu mengidentifikasi pola yang relevan.
