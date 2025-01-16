# Challenge Day 16

## 📝 Topik
**Transformasi Data: Normalisasi dan Standardisasi**

---

## 🎯 Learning Objectives
1. Memahami konsep transformasi data untuk analisis dan machine learning.
2. Memahami perbedaan antara normalisasi dan standardisasi.
3. Melakukan normalisasi dan standardisasi pada dataset menggunakan library Python seperti `scikit-learn` dan `pandas`.
4. Memahami kapan harus menggunakan normalisasi atau standardisasi dalam konteks analisis data dan modeling.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Transformasi data adalah proses penting untuk mengubah data mentah menjadi format yang lebih sesuai untuk analisis atau modeling.

1. :**Normalisasi:** Mengubah data menjadi rentang [0, 1], sering digunakan untuk algoritma yang sensitif terhadap skala, seperti k-Nearest Neighbors atau Neural Networks.
Formula:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20016/formula_normalisasi.png" width=”200”>

2. :**Standardisasi::** Mengubah data menjadi distribusi dengan rata-rata 0 dan standar deviasi 1. Ini penting untuk algoritma yang mengandalkan distribusi normal, seperti Support Vector Machine atau PCA.
Formula:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20016/formula_standarisasi.png" width=”200”>

Transformasi membantu mempercepat proses konvergensi dalam model machine learning dan meningkatkan interpretasi data.

---
## 🚀 Langkah-Langkah

### Persiapan Data
Gunakan dataset numerik sederhana
```python
import pandas as pd
import numpy as np

np.random.seed(42)
data = {
    'Waktu Belajar (Jam)': np.random.randint(1, 10, 10),
    'Nilai': np.random.randint(50, 100, 10),
    'Kehadiran (%)': np.random.randint(75, 100, 10)
}

df = pd.DataFrame(data)
print("Dataset Asli:")
print(df)
```
Output:
```bash
Dataset Asli:
   Waktu Belajar (Jam)        Nilai                  Kehadiran (%)
0                    7                     89                             95
1                    4                     73                             75
2                    8                     52                             86
3                    5                     71                             96
4                    7                     51                             86
5                    3                     73                             99
6                    7                     93                             91
7                    8                     79                             84
8                    5                     87                             90
9                    4                     51                             89
```

### Normalisasi Data
Gunakan Min-Max Scaler dari scikit-learn
```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
normalized_data = scaler.fit_transform(df)
normalized_df = pd.DataFrame(normalized_data, columns=df.columns)

print("\nDataset Setelah Normalisasi:")
print(normalized_df)
```
Output:
```bash
Dataset Setelah Normalisasi:
   Waktu Belajar (Jam)            Nilai                 Kehadiran (%)
0                  0.8                 0.904762                      0.833333
1                  0.2                 0.523810                      0.000000
2                  1.0                 0.023810                      0.458333
3                  0.4                 0.476190                      0.875000
4                  0.8                 0.000000                      0.458333
5                  0.0                 0.523810                      1.000000
6                  0.8                 1.000000                      0.666667
7                  1.0                 0.666667                      0.375000
8                  0.4                 0.857143                      0.625000
9                  0.2                 0.000000                      0.583333
```

### Standardisasi Data
Gunakan Standard Scaler dari scikit-learn
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

standardized_data = scaler.fit_transform(df)
standardized_df = pd.DataFrame(standardized_data, columns=df.columns)

print("\nDataset Setelah Standardisasi:")
print(standardized_df)
```
Output:
```bash
Dataset Setelah Standardisasi:
   Waktu Belajar (Jam)              Nilai            Kehadiran (%)
0             0.697486            1.130271                 0.900895
1            -1.046229            0.072708                -2.152985
2             1.278724           -1.315345                -0.473351
3            -0.464991           -0.059488                 1.053589
4             0.697486           -1.381443                -0.473351
5            -1.627467            0.072708                 1.511671
6             0.697486            1.394662                 0.290119
7             1.278724            0.469294                -0.778739
8            -0.464991            0.998076                 0.137425
9            -1.046229           -1.381443                -0.015269
```

### Visualisasi Data
Visualisasi data asli
```python
import matplotlib.pyplot as plt
plt.figure(figsize=(12, 6))
df.hist(bins=10, figsize=(12, 4), color='blue', alpha=0.7)
plt.suptitle('Distribusi Data Asli', fontsize=14)
plt.savefig('16_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20016/16_01.png" width=”500”>

Visualisasi data setelah normalisasi
```python
import matplotlib.pyplot as plt
normalized_df.hist(bins=10, figsize=(12, 4), color='green', alpha=0.7)
plt.suptitle('Distribusi Data Setelah Normalisasi', fontsize=14)
plt.savefig('16_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20016/16_02.png" width=”500”>

Visualisasi data setelah standardisasi
```python
import matplotlib.pyplot as plt
standardized_df.hist(bins=10, figsize=(12, 4), color='orange', alpha=0.7)
plt.suptitle('Distribusi Data Setelah Standardisasi', fontsize=14)
plt.savefig('16_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20016/16_03.png" width=”500”>

### Analisis Hasil
Bandingkan distribusi data sebelum dan sesudah transformasi
1. Normalisasi: Semua nilai berada dalam rentang [0, 1]
2. Standardisasi: Data memiliki rata-rata 0 dan standar deviasi 1

### Kesimpulan 
1. Normalisasi memberikan nilai dalam rentang [0, 1], menjaga proporsi data awal.
2. Standardisasi membuat data terpusat pada rata-rata 0, dengan distribusi standar deviasi 1.
3. Pilihan metode bergantung pada algoritma yang digunakan:
- Gunakan normalisasi untuk algoritma berbasis jarak.
- Gunakan standardisasi untuk algoritma yang memerlukan data terdistribusi normal.
