# Challenge Day 12

## 📝 Topik
**Pengenalan Data Cleaning: Menangani Missing Values dan Data Duplikat**

---

## 🎯 Learning Objectives
1. Memahami pentingnya data cleaning dalam proses analisis data.
2. Mengenal metode menangani missing values, seperti penghapusan atau imputasi data.
3. Mengetahui cara mendeteksi dan menghapus data duplikat.
4. Menggunakan Pandas untuk membersihkan data secara efisien.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Data cleaning adalah langkah penting dalam analisis data. Data yang bersih dan berkualitas tinggi menghasilkan wawasan yang lebih akurat. 
Dua masalah umum dalam data adalah:
- **Missing Values:** Nilai yang hilang dapat memengaruhi analisis. Ini bisa ditangani dengan menghapus data atau menggantinya (imputasi).
- **Data Duplikat::** Data yang berulang dapat menyebabkan bias dalam analisis dan perlu dihapus.
Dengan Python dan Pandas, kita dapat dengan mudah mendeteksi, menangani, dan membersihkan masalah tersebut.

---
## 🚀 Langkah-Langkah

### Persiapan Dataset
Buat dataset sederhana dengan missing values dan data duplikat.
```python
import pandas as pd

data = {
    'Nama': ['Ayu', 'Budi', 'Citra', 'Dedi', 'Eka', 'Ayu', 'Fani', None, 'Indah', 'Joko'],
    'Nilai': [78, 85, 62, None, 88, 78, None, 90, 85, 81],
    'Kelas': ['A', 'B', 'A', 'B', 'A', 'A', None, 'B', 'B', 'A']
}
df = pd.DataFrame(data)
print("Dataset Asli:\n", df)
```
Output:
```bash
Dataset Asli:
     Nama  Nilai Kelas
0    Ayu   78.0     A
1   Budi   85.0     B
2  Citra   62.0     A
3   Dedi    NaN     B
4    Eka   88.0     A
5    Ayu   78.0     A
6   Fani    NaN  None
7   None   90.0     B
8  Indah   85.0     B
9   Joko   81.0     A
```

### Deteksi Missing Values
Identifikasi nilai yang hilang di dataset.
```python
print("\n=== Missing Values ===")
print(df.isnull().sum()) 
```
Output:
```bash
=== Missing Values ===
Nama     1
Nilai    2
Kelas    1
dtype: int64
```

### Menangani Missing Values
Tangani missing values dengan metode penghapusan.
```python
df_cleaned = df.dropna()
print("\nDataset setelah Menghapus Missing Values:\n", df_cleaned)
```
Output:
```bash
Dataset setelah Menghapus Missing Values:
     Nama  Nilai Kelas
0    Ayu   78.0     A
1   Budi   85.0     B
2  Citra   62.0     A
4    Eka   88.0     A
5    Ayu   78.0     A
8  Indah   85.0     B
9   Joko   81.0     A
```
Tangani missing values dengan metode imputasi.
```python
df['Nilai'] = df['Nilai'].fillna(df['Nilai'].mean())
df['Kelas'] = df['Kelas'].fillna('Tidak Ada')
print("\nDataset setelah Imputasi Missing Values:\n", df)
```
Output:
```bash
Dataset setelah Imputasi Missing Values:
     Nama   Nilai      Kelas
0    Ayu  78.000          A
1   Budi  85.000          B
2  Citra  62.000          A
3   Dedi  80.875          B
4    Eka  88.000          A
5    Ayu  78.000          A
6   Fani  80.875  Tidak Ada
7   None  90.000          B
8  Indah  85.000          B
9   Joko  81.000          A
```

### Deteksi Data Duplikat
Identifikasi baris yang duplikat.
```python
print("\n=== Data Duplikat ===")
print(df[df.duplicated()])
```
Output:
```bash
=== Data Duplikat ===
  Nama  Nilai Kelas
5  Ayu   78.0     A
```

### Menghapus Data Duplikat
Bersihkan data dari baris yang berulang.
```python
df = df.drop_duplicates()
print("\nDataset setelah Menghapus Duplikat:\n", df)
```
Output:
```bash
Dataset setelah Menghapus Duplikat:
     Nama   Nilai      Kelas
0    Ayu  78.000          A
1   Budi  85.000          B
2  Citra  62.000          A
3   Dedi  80.875          B
4    Eka  88.000          A
6   Fani  80.875  Tidak Ada
7   None  90.000          B
8  Indah  85.000          B
9   Joko  81.000          A
```

### Validasi Data
Pastikan data bersih setelah proses cleaning.
```python
print("\nValidasi Data:")
print("Jumlah missing values per kolom:\n", df.isnull().sum())
print("Jumlah baris duplikat:", df.duplicated().sum())
```
Output:
```bash
Validasi Data:
Jumlah missing values per kolom:
 Nama     1
Nilai    0
Kelas    0
dtype: int64
Jumlah baris duplikat: 0
```
