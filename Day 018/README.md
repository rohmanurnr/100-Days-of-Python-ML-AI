# Challenge Day 18

## 📝 Topik
**Pengenalan Data Imbalance**

Memahami konsep data imbalance dalam dataset klasifikasi dan merancang solusi, seperti oversampling, untuk mengatasi masalah tersebut.

---

## 🎯 Learning Objectives
1. Memahami apa itu data imbalance dan dampaknya pada model pembelajaran mesin.
2. Mengidentifikasi apakah dataset mengalami data imbalance.
3. Menggunakan teknik statistik untuk menganalisis distribusi kelas dalam dataset.
4. Menerapkan teknik oversampling, seperti SMOTE (Synthetic Minority Oversampling Technique), untuk mengatasi data imbalance.
5. Menginterpretasikan hasil distribusi kelas setelah dilakukan oversampling.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Data imbalance terjadi ketika distribusi kelas dalam dataset tidak seimbang, dengan salah satu kelas memiliki jumlah data yang jauh lebih banyak daripada kelas lainnya. Misalnya, dalam sebuah dataset fraud detection, hanya 1% data yang berlabel fraud, sedangkan 99% lainnya adalah non-fraud.

Ketidakseimbangan ini dapat menyebabkan model prediktif memberikan kinerja buruk pada kelas minoritas karena terfokus pada kelas mayoritas. Untuk mengatasinya, salah satu solusi adalah oversampling, di mana jumlah data pada kelas minoritas diperbanyak agar distribusinya lebih seimbang.

---
## 🚀 Langkah-Langkah

### Persiapan Data
Buat dataset dummy dengan distribusi kelas tidak seimbang.
```python
import pandas as pd
import numpy as np

np.random.seed(42)
data = {
    'Fitur 1': np.random.normal(0, 1, 100),
    'Fitur 2': np.random.normal(1, 1, 100),
    'Kelas': [0] * 90 + [1] * 10 
}

df = pd.DataFrame(data)
print("Dataset Asli:")
print(df['Kelas'].value_counts())
```
Output:
```bash
Dataset Asli:
Kelas
0    90
1    10
Name: count, dtype: int64
```

### Analisis Data Imbalance
Visualisasikan distribusi kelas menggunakan bar plot.
```python
import matplotlib.pyplot as plt

df['Kelas'].value_counts().plot(kind='bar', color=['blue', 'orange'])
plt.title('Distribusi Kelas')
plt.xlabel('Kelas')
plt.ylabel('Jumlah Data')
plt.savefig(‘18_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20018/18_01.png" width=”500”>

### Oversampling dengan SMOTE
Gunakan pustaka `imblearn` untuk melakukan oversampling.
```python
from imblearn.over_sampling import SMOTE
from sklearn.model_selection import train_test_split

X = df[['Fitur 1', 'Fitur 2']]
y = df['Kelas']

smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X, y)

df_resampled = pd.DataFrame(X_resampled, columns=['Fitur 1', 'Fitur 2'])
df_resampled['Kelas'] = y_resampled

print("\nDataset Setelah Oversampling:")
print(df_resampled['Kelas'].value_counts())
```
Output:
```bash
Dataset Setelah Oversampling:
Kelas
0    90
1    90
Name: count, dtype: int64
```

### Validasi Hasil
Visualisasikan distribusi kelas setelah oversampling.
```python
df_resampled['Kelas'].value_counts().plot(kind='bar', color=['blue', 'orange'])
plt.title('Distribusi Kelas Setelah Oversampling')
plt.xlabel('Kelas')
plt.ylabel('Jumlah Data')
plt.savefig(18_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20018/18_02.png" width=”500”>

### Kesimpulan 
1. Data imbalance dapat mengakibatkan bias model terhadap kelas mayoritas.
2. SMOTE adalah salah satu teknik oversampling yang efektif untuk memperbaiki distribusi kelas.
3. Dataset yang telah dioversampling memungkinkan model pembelajaran mesin untuk mempelajari pola pada kelas minoritas dengan lebih baik.
