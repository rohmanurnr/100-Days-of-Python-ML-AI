# Challenge Day 14

## 📝 Topik
**Pengenalan Exploratory Data Analysis (EDA): Identifikasi Pola dalam Data dengan Visualisasi Sederhana**

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Exploratory Data Analysis (EDA) dan tujuannya dalam analisis data.
2. Menggunakan statistik deskriptif untuk memahami distribusi data.
3. Membuat visualisasi sederhana seperti histogram, scatter plot, dan box plot untuk mengidentifikasi pola dalam data.
4. Menginterpretasikan visualisasi untuk menggali wawasan tentang distribusi, hubungan, dan outlier dalam data.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Exploratory Data Analysis (EDA) adalah langkah penting dalam proses analisis data. EDA membantu memahami karakteristik data, mendeteksi pola atau anomali, dan menghasilkan hipotesis awal untuk analisis lebih lanjut.
Beberapa langkah utama dalam EDA meliputi:

- Statistik Deskriptif: Menghitung mean, median, dan standar deviasi.
- Visualisasi Data: Menggunakan grafik untuk mempelajari distribusi dan hubungan antar variabel.

Visualisasi sederhana seperti histogram, scatter plot, dan box plot sangat efektif untuk mendapatkan wawasan awal dari dataset.

---
## 🚀 Langkah-Langkah

### Persiapan Data
Gunakan dataset sederhana, seperti data nilai siswa, penjualan produk, atau suhu harian.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

data = {
    'Nama': ['Ayu', 'Budi', 'Citra', 'Dedi', 'Eka', 'Fani', 'Gilang', 'Hana', 'Indah', 'Joko'],
    'Nilai': [78, 85, 62, 90, 88, 95, 81, 79, 85, 77],
    'Waktu Belajar': [2, 4, 1, 5, 4, 6, 3, 2, 4, 2]  # Jam belajar per minggu
}
df = pd.DataFrame(data)
print("Dataset:\n", df)
```
Output:
```bash
Dataset:
      Nama  Nilai  Waktu Belajar
0     Ayu     78              2
1    Budi     85              4
2   Citra     62              1
3    Dedi     90              5
4     Eka     88              4
5    Fani     95              6
6  Gilang     81              3
7    Hana     79              2
8   Indah     85              4
9    Joko     77              2
```

### Statistik Deskriptif
Hitung statistik dasar seperti mean, median, dan standar deviasi.
```python
mean = df['Nilai'].mean()
median = df['Nilai'].median()
std_dev = df['Nilai'].std()

print(f"\nMean: {mean}")
print(f"Median: {median}")
print(f"Standar Deviasi: {std_dev}")
```
Output:
```bash
Mean: 82.0
Median: 83.0
Standar Deviasi: 9.055385138137417
```

### Visualisasi Distribusi dengan Histogram
Gunakan histogram untuk melihat distribusi data.
```python
plt.figure(figsize=(8, 5))
plt.hist(df['Nilai'], bins=5, color='skyblue', edgecolor='black')
plt.title('Distribusi Nilai Siswa', fontsize=14)
plt.xlabel('Nilai', fontsize=12)
plt.ylabel('Frekuensi', fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.savefig('hist_eda.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/hist_eda.png" width=”500”>

### Hubungan Antar Variabel dengan Scatter Plot
Buat scatter plot untuk mengeksplorasi hubungan antar variabel.
```python
plt.figure(figsize=(8, 5))
sns.scatterplot(x='Waktu Belajar', y='Nilai', data=df, color='blue', s=100)
plt.title('Hubungan Waktu Belajar dan Nilai', fontsize=14)
plt.xlabel('Waktu Belajar (Jam/Minggu)', fontsize=12)
plt.ylabel('Nilai', fontsize=12)
plt.grid(True, linestyle='--', alpha=0.7)
plt.savefig('sct_eda.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/sct_eda.png" width=”500”>

### Deteksi Outlier dengan Box Plot
Gunakan box plot untuk mendeteksi outlier dalam data.
```python
plt.figure(figsize=(8, 5))
sns.boxplot(x='Nilai', data=df, color='orange')
plt.title('Deteksi Outlier pada Nilai Siswa', fontsize=14)
plt.xlabel('Nilai', fontsize=12)
plt.savefig('bxp_eda.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/bxp_eda.png" width=”500”>

## Challenge
Identifikasi distribusi nilai siswa menggunakan histogram. Apakah data simetris atau miring ke kanan/kiri?
Analisis hubungan antara waktu belajar dan nilai dari scatter plot. Adakah korelasi yang jelas?
Periksa apakah terdapat outlier dalam data nilai menggunakan box plot.

### Identifikasi Distribusi Nilai Siswa menggunakan Histogram
```python
# Histogram distribusi nilai siswa
plt.figure(figsize=(8, 5))
plt.hist(df['Nilai'], bins=5, color='skyblue', edgecolor='black')
plt.title('Distribusi Nilai Siswa', fontsize=14)
plt.xlabel('Nilai', fontsize=12)
plt.ylabel('Frekuensi', fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.savefig('challenge1_eda.png', format='png', dpi=300)
plt.show()

# Identifikasi simetri distribusi
skewness = df['Nilai'].skew()
if skewness > 0:
    print(f"Distribusi miring ke kanan (positif), skewness: {skewness:.2f}")
elif skewness < 0:
    print(f"Distribusi miring ke kiri (negatif), skewness: {skewness:.2f}")
else:
    print("Distribusi simetris.")
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/'challenge1_eda.png" width=”500”>
```bash
Distribusi miring ke kiri (negatif), skewness: -0.98
```

### Analisis Hubungan antara Waktu Belajar dan Nilai (Scatter Plot)
```python
# Scatter plot antara waktu belajar dan nilai
plt.figure(figsize=(8, 5))
sns.scatterplot(x='Waktu Belajar', y='Nilai', data=df, color='blue', s=100)
plt.title('Hubungan Waktu Belajar dan Nilai', fontsize=14)
plt.xlabel('Waktu Belajar (Jam/Minggu)', fontsize=12)
plt.ylabel('Nilai', fontsize=12)
plt.grid(True, linestyle='--', alpha=0.7)
plt.savefig('challenge2_eda.png', format='png', dpi=300)
plt.show()

# Hitung korelasi antara Waktu Belajar dan Nilai
correlation = df['Waktu Belajar'].corr(df['Nilai'])
print(f"Korelasi antara waktu belajar dan nilai: {correlation:.2f}")
if correlation > 0:
    print("Hubungan positif: Waktu belajar meningkat, nilai cenderung meningkat.")
elif correlation < 0:
    print("Hubungan negatif: Waktu belajar meningkat, nilai cenderung menurun.")
else:
    print("Tidak ada hubungan antara waktu belajar dan nilai.")
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/'challenge2_eda.png" width=”500”>
```bash
Korelasi antara waktu belajar dan nilai: 0.93
Hubungan positif: Waktu belajar meningkat, nilai cenderung meningkat.
```

### Periksa Outlier dengan Box Plot
```python
# Box plot nilai siswa
plt.figure(figsize=(8, 5))
sns.boxplot(x='Nilai', data=df, color='orange')
plt.title('Deteksi Outlier pada Nilai Siswa', fontsize=14)
plt.xlabel('Nilai', fontsize=12)
plt.savefig('challenge3_eda.png', format='png', dpi=300)
plt.show()

# Deteksi outlier menggunakan IQR
Q1 = df['Nilai'].quantile(0.25)
Q3 = df['Nilai'].quantile(0.75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df['Nilai'] < lower_bound) | (df['Nilai'] > upper_bound)]
if not outliers.empty:
    print(f"Terdapat {len(outliers)} outlier:\n{outliers}")
else:
    print("Tidak terdapat outlier dalam data nilai.")
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20014/'challenge3_eda.png" width=”500”>
```bash
Terdapat 1 outlier:
    Nama  Nilai  Waktu Belajar
2  Citra     62              1
```

