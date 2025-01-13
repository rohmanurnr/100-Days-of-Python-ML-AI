# Challenge Day 13

## 📝 Topik
**Pembersihan Data Lanjutan: Menangani Outlier Menggunakan Metode IQR**

---

## 🎯 Learning Objectives
1. Memahami konsep outlier dan pengaruhnya terhadap analisis data.
2. Mengenal metode Interquartile Range (IQR) untuk mendeteksi dan menangani outlier.
3. Menggunakan Pandas dan NumPy untuk menghitung IQR dan membersihkan data dari outlier.
4. Memvalidasi hasil pembersihan data untuk memastikan tidak ada outlier yang tersisa.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Outlier adalah data yang memiliki nilai jauh di luar rentang data lainnya. Outlier dapat memengaruhi analisis statistik seperti mean, regresi, dan model prediksi.
Metode Interquartile Range (IQR) adalah cara yang efektif untuk mendeteksi dan menangani outlier. 

### Rumus IQR
IQR=Q3−Q1

Dimana:
Q1: Kuartil pertama (25%)
Q3: Kuartil ketiga (75%)
Data dianggap outlier jika berada di bawah (Q1 − 1.5 × IQR) atau di atas (Q3 + 1.5 × IQR).

---

### Persiapan Dataset
Buat dataset sederhana yang mengandung outlier.
```python
import pandas as pd
import numpy as np

data = {
    'Nama': ['Ayu', 'Budi', 'Citra', 'Dedi', 'Eka', 'Fani', 'Gilang', 'Hana', 'Indah', 'Joko'],
    'Nilai': [78, 85, 62, 90, 88, 300, 81, 79, 85, 77]  
}
df = pd.DataFrame(data)
print("Dataset Asli:\n", df)
```
Output:
```bash
Dataset Asli:
      Nama  Nilai
0     Ayu     78
1    Budi     85
2   Citra     62
3    Dedi     90
4     Eka     88
5    Fani    300
6  Gilang     81
7    Hana     79
8   Indah     85
9    Joko     77
```

### Identifikasi Outlier
Hitung IQR dan tentukan batas bawah serta atas.
```python
Q1 = df['Nilai'].quantile(0.25)
Q3 = df['Nilai'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

print("\nBatas Bawah:", lower_bound)
print("Batas Atas:", upper_bound)
```
Output:
```bash
Batas Bawah: 64.75
Batas Atas: 100.75
```
Menandai outlier
```python
df['Outlier'] = (df['Nilai'] < lower_bound) | (df['Nilai'] > upper_bound)
print("\nDataset dengan Penanda Outlier:\n", df)
```
Output:
```bash
Dataset dengan Penanda Outlier:
      Nama  Nilai  Outlier
0     Ayu     78    False
1    Budi     85    False
2   Citra     62     True
3    Dedi     90    False
4     Eka     88    False
5    Fani    300     True
6  Gilang     81    False
7    Hana     79    False
8   Indah     85    False
9    Joko     77    False
```

### Hapus Outlier
Bersihkan data dengan menghapus nilai yang berada di luar batas.
```python
df_cleaned = df[~df['Outlier']].drop(columns='Outlier')
print("\nDataset Setelah Menghapus Outlier:\n", df_cleaned)
```
Output:
```bash
Dataset Setelah Menghapus Outlier:
      Nama  Nilai
0     Ayu     78
1    Budi     85
3    Dedi     90
4     Eka     88
6  Gilang     81
7    Hana     79
8   Indah     85
9    Joko     77
```

### Validasi Data
Periksa kembali dataset untuk memastikan tidak ada outlier yang tersisa.
```python
new_Q1 = df_cleaned['Nilai'].quantile(0.25)
new_Q3 = df_cleaned['Nilai'].quantile(0.75)
new_IQR = new_Q3 - new_Q1

new_lower_bound = new_Q1 - 1.5 * new_IQR
new_upper_bound = new_Q3 + 1.5 * new_IQR

print("\nValidasi Batas Baru:")
print("Batas Bawah:", new_lower_bound)
print("Batas Atas:", new_upper_bound)
```
Output:
```bash
Validasi Batas Baru:
Batas Bawah: 68.25
Batas Atas: 96.25
```
Periksa apakah ada outlier yang tersisa
```python
outlier_remaining = df_cleaned[(df_cleaned['Nilai'] < new_lower_bound) | (df_cleaned['Nilai'] > new_upper_bound)]
print("\nOutlier yang Tersisa (Jika Ada):\n", outlier_remaining)
```
Output:
```bash
Outlier yang Tersisa (Jika Ada):
 Empty DataFrame
Columns: [Nama, Nilai]
Index: []
```
