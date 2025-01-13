# Challenge Day 11

## 📝 Topik
**Statistik Lanjutan: Variance dan Standar Deviasi**

---

## 🎯 Learning Objectives
1. Memahami konsep dasar varians (variance) dan standar deviasi (standard deviation) dalam statistik.
2. Mengetahui bagaimana menghitung varians dan standar deviasi menggunakan Python dan Pandas.
3. Mampu menginterpretasikan varians dan standar deviasi untuk memahami tingkat penyebaran data.
4. Menggunakan visualisasi sederhana untuk mendukung pemahaman distribusi data.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Varians dan standar deviasi adalah metrik yang digunakan untuk mengukur penyebaran data dalam statistik.
- **Variance (Varians):** Mengukur seberapa jauh data tersebar dari nilai rata-rata. Nilai varians yang tinggi menunjukkan data yang lebih tersebar.
- **Standard Deviation (Standar Deviasi):** Akar kuadrat dari varians, memberikan ukuran penyebaran dalam satuan yang sama dengan data.

Pengukuran ini membantu kita memahami seberapa "konsisten" data dan apakah terdapat anomali atau outlier yang signifikan.

---
## Persiapan Data
Buat dataset sederhana untuk digunakan dalam perhitungan.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = {
    'Nama': ['Ayu', 'Budi', 'Citra', 'Dedi', 'Eka', 'Fani', 'Gilang', 'Hadi', 'Indah', 'Joko'],
    'Nilai': [78, 85, 62, 74, 88, 90, 67, 72, 85, 81]
}
df = pd.DataFrame(data)
print("Dataset:\n", df)
```
Output:
```bash
Dataset:
      Nama  Nilai
0     Ayu     78
1    Budi     85
2   Citra     62
3    Dedi     74
4     Eka     88
5    Fani     90
6  Gilang     67
7    Hadi     72
8   Indah     85
9    Joko     81
```

## Menghitung Variance
Gunakan Pandas untuk menghitung varians data.
```python
variance = df['Nilai'].var()
print("\nVariance (Varians):", variance)
```
Output:
```bash
Variance (Varians): 86.62222222222223
```

## Menghitung Standard Deviation
Gunakan Pandas untuk menghitung standar deviasi data.
```python
std_dev = df['Nilai'].std()
print("Standard Deviation (Standar Deviasi):", std_dev)
```
Output:
```bash
Standard Deviation (Standar Deviasi): 9.307106006822004
```

## Visualisasi Penyebaran Data
Gunakan grafik seperti histogram untuk memvisualisasikan distribusi data.
```python
plt.hist(df['Nilai'], bins=5, color='skyblue', edgecolor='black')
plt.title('Distribusi Nilai Siswa')
plt.xlabel('Nilai')
plt.ylabel('Frekuensi')
plt.axvline(df['Nilai'].mean(), color='red', linestyle='dashed', linewidth=1, label='Mean')
plt.axvline(df['Nilai'].mean() + std_dev, color='green', linestyle='dotted', linewidth=1, label='+1 SD')
plt.axvline(df['Nilai'].mean() - std_dev, color='green', linestyle='dotted', linewidth=1, label='-1 SD')
plt.legend()
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20011/vis_var_std.png" width=”500”>

## Interpretasi
Analisis hasil untuk memahami tingkat variasi dalam dataset.
```python
print("\nInterpretasi:")
if variance < 100:
    print("Data memiliki tingkat penyebaran yang rendah.")
elif variance > 500:
    print("Data memiliki tingkat penyebaran yang sangat tinggi.")
else:
    print("Data memiliki tingkat penyebaran sedang.")
```
Output:
```bash
Interpretasi:
Data memiliki tingkat penyebaran yang rendah.
```
