# Challenge Day 28

## 📝 Topik
**Pengenalan Data Dimensionality**

Pengenalan konsep dimensionalitas data, tantangan yang dihadapi dalam high-dimensional data, dan solusi awal untuk menangani masalah tersebut.

---

## 🎯 Learning Objectives
1. Memahami konsep high-dimensional data dan dampaknya terhadap analisis data.
2. Mengetahui tantangan seperti curse of dimensionality dalam pengolahan data berdimensi tinggi.
3. Mengenal teknik awal untuk menangani high-dimensional data, seperti reduksi dimensi.
4. Menggunakan Principal Component Analysis (PCA) untuk memvisualisasikan data berdimensi tinggi.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Data berdimensi tinggi mengandung banyak fitur, yang seringkali memperumit analisis karena tantangan seperti curse of dimensionality. Fenomena ini membuat data sulit untuk diproses karena semakin banyak dimensi, semakin sulit menemukan pola yang relevan. Selain itu, redundansi informasi dari fitur yang saling berkorelasi dapat menambah kompleksitas.
Solusi awal untuk menangani data berdimensi tinggi melibatkan reduksi dimensi, yang mengurangi jumlah fitur sambil mempertahankan informasi penting. Salah satu metode populer untuk ini adalah Principal Component Analysis (PCA).

---
## 🚀 Langkah-Langkah

### Memahami Tantangan Data Berdimensi Tinggi
#### Apa itu Curse of Dimensionality?
**Curse of Dimensionality** adalah istilah yang mengacu pada berbagai tantangan yang muncul saat bekerja dengan data berdimensi tinggi (data yang memiliki banyak fitur atau variabel). Ketika jumlah dimensi meningkat, data menjadi semakin sulit untuk dianalisis dan diproses secara efisien.

#### Mengapa Curse of Dimensionality Terjadi?
1. **Volume Data Bertambah Secara Eksponensial**
Dengan setiap tambahan dimensi, volume ruang data bertambah secara eksponensial. Ini berarti data menjadi semakin "sparse" atau tersebar, sehingga sulit untuk menemukan pola yang bermakna.

2. **Kesulitan dalam Mengukur Jarak**
Dalam dimensi tinggi, perbedaan jarak antar titik data menjadi kurang signifikan. Sebagai contoh, dalam data berdimensi tinggi, jarak antara dua titik cenderung hampir sama dengan jarak antara titik lain, membuat algoritma seperti k-nearest neighbors (KNN) kurang efektif.

3. **Overfitting dalam Machine Learning**
Model machine learning yang bekerja dengan banyak fitur sering kali menjadi terlalu kompleks, belajar dari noise daripada pola yang bermakna. Ini menyebabkan overfitting, di mana model tidak dapat bekerja dengan baik pada data baru.

#### Dampak Curse of Dimensionality pada Machine Learning
1. **Kinerja Model Menurun**
Dalam data berdimensi tinggi, algoritma seperti regresi, KNN, atau clustering sering gagal dalam menemukan pola yang relevan, mengakibatkan performa yang buruk.

2. **Kebutuhan Data yang Lebih Besar**
Untuk setiap dimensi tambahan, jumlah data yang dibutuhkan untuk menjaga densitas yang sama meningkat secara eksponensial. Tanpa data yang cukup, hasil analisis menjadi tidak representatif.

3. **Kesulitan dalam Visualisasi**
Dimensi tinggi sulit divisualisasikan, sehingga sulit untuk memahami pola secara intuitif.

#### Solusi untuk Curse of Dimensionality
1. **Reduksi Dimensi**
Teknik seperti Principal Component Analysis (PCA), t-SNE, atau UMAP digunakan untuk mengurangi jumlah dimensi sambil mempertahankan informasi penting.

2. **Feature Selection**
Pilih hanya fitur yang relevan berdasarkan analisis korelasi, pentingnya fitur (feature importance), atau algoritma seperti Lasso Regression.

3. **Feature Engineering**
Gabungkan atau transformasi fitur untuk menciptakan representasi yang lebih ringkas dan bermakna.

4. **Regularisasi**
Terapkan teknik regularisasi seperti L1 atau L2 untuk mengurangi dampak dimensi tinggi dalam algoritma machine learning.

### Persiapan Dataset
Gunakan dataset sintetis atau bawaan dari sklearn untuk mensimulasikan data berdimensi tinggi.
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_classification

X, y = make_classification(
    n_samples=500,
    n_features=20,  # 20 fitur
    n_informative=10,
    n_redundant=5,
    random_state=42)

print(f"Shape dataset: {X.shape}")
```
Output:
```bash
Shape dataset: (500, 20)
```

### Memahami Tantangan
Lakukan eksplorasi awal untuk melihat korelasi antar fitur.
```python
import seaborn as sns
import pandas as pd

df = pd.DataFrame(X, columns=[f"Feature_{i}" for i in range(1, 21)])

plt.figure(figsize=(12, 8))
sns.heatmap(df.corr(), annot=False, cmap="coolwarm")
plt.title("Korelasi Antar Fitur")
plt.savefig('28_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20028/28_01.png" width=”500”>

### Implementasi PCA
Lakukan reduksi dimensi menggunakan PCA dan visualisasikan dalam 2D.
```python
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

print(f"Explained variance ratio: {pca.explained_variance_ratio_}")

plt.figure(figsize=(10, 6))
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=y, cmap="viridis", edgecolor="k", s=50)
plt.title("Visualisasi Data Setelah PCA (2D)")
plt.xlabel("Komponen Utama 1")
plt.ylabel("Komponen Utama 2")
plt.colorbar(label="Kelas")
plt.savefig('28_02.png', format='png', dpi=300)
plt.show()
```
Output:
```bash
Explained variance ratio: [0.17013783 0.16259055]
```
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20028/28_02.png" width=”500”>

### Visualisasi 3D
```python
from mpl_toolkits.mplot3d import Axes3D

pca_3d = PCA(n_components=3)
X_pca_3d = pca_3d.fit_transform(X_scaled)

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')
scatter = ax.scatter(X_pca_3d[:, 0], X_pca_3d[:, 1], X_pca_3d[:, 2], c=y, cmap="viridis", edgecolor="k", s=50)
ax.set_title("Visualisasi Data Setelah PCA (3D)")
ax.set_xlabel("Komponen Utama 1")
ax.set_ylabel("Komponen Utama 2")
ax.set_zlabel("Komponen Utama 3")
plt.colorbar(scatter, label="Kelas")
plt.savefig('28_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20028/28_03.png" width=”500”>


### Kesimpulan 
Teknik PCA dapat menangani tantangan high-dimensional data, mengurangi kompleksitas analisis, dan tetap menjaga informasi penting.
