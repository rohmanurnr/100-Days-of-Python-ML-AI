# Challenge Day 26

## 📝 Topik
**Implementasi K-Means Clustering**

Mengimplementasikan algoritma K-Means clustering untuk mengelompokkan data dengan langkah-langkah praktis.

---

## 🎯 Learning Objectives
1. Memahami cara kerja algoritma K-Means melalui implementasi
2. Mengelompokkan dataset menjadi beberapa cluster berdasarkan kesamaan fitur
3. Mengevaluasi hasil clustering dengan visualisasi dan analisis
4. Menggunakan parameter dan atribut model K-Means untuk memahami performa

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
K-Means adalah algoritma clustering yang mempartisi data ke dalam k cluster berdasarkan kedekatan jarak ke centroid. Implementasi K-Means memungkinkan kita untuk mengelompokkan data berdasarkan pola yang tersembunyi.

Bagaimana K-Means berkerja?

1. Pilih jumlah cluster (k)
2. Inisialisasi centroid secara acak
3. Iterasi hingga konvergensi:
- Tetapkan setiap data ke cluster terdekat
- Hitung ulang centroid berdasarkan anggota ke centroid


---
## 🚀 Langkah-Langkah

### Eksplorasi Dataset
Gunakan dataset nyata atau sintetis dengan lebih dari dua fitur.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
from sklearn.preprocessing import StandardScaler

X, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.2, random_state=42)

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

plt.figure(figsize=(8, 6))
plt.scatter(X_scaled[:, 0], X_scaled[:, 1], color='gray', alpha=0.7)
plt.title("Dataset Awal (Distandarisasi)")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.savefig('26_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20026/26_01.png" width=”500”>

### Implementasi K-Means
- Pilih jumlah cluster (𝑘) yang sesuai.
- Kelompokkan data menggunakan algoritma K-Means.
```python
kmeans = KMeans(n_clusters=4, random_state=42)
kmeans.fit(X_scaled)

labels = kmeans.labels_
centroids = kmeans.cluster_centers_
```

### Visualisasi Hasil Clustering
- Gunakan scatter plot untuk menampilkan hasil clustering pada dataset dua dimensi.
- Tampilkan centroid untuk setiap cluster.
```python
plt.figure(figsize=(8, 6))
for cluster in range(4):
    plt.scatter(X_scaled[labels == cluster, 0], X_scaled[labels == cluster, 1], label=f'Cluster {cluster + 1}')

plt.scatter(centroids[:, 0], centroids[:, 1], color='red', marker='X', s=200, label='Centroid')

plt.title("Hasil Clustering dengan K-Means")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.legend()
plt.grid()
plt.savefig('26_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20026/26_02.png" width=”500”>

### Analisis Performa
Gunakan atribut seperti inertia atau nilai SSE untuk mengevaluasi hasil clustering.
```python
print(f"Inertia (SSE): {kmeans.inertia_}")
print(f"Jumlah Iterasi: {kmeans.n_iter_}")
```
Output:
```bash
Inertia (SSE): 24.56291318544907
Jumlah Iterasi: 2
```

## Tugas Tambahan
1. Eksperimen dengan 𝑘
Ubah jumlah cluster (𝑘) dan amati perbedaan hasil.
2. Evaluasi Inertia
Catat nilai inertia untuk beberapa nilai 𝑘. Buat elbow plot untuk memilih 
𝑘 terbaik
```python
inertia = []
k_values = range(1, 10)

for k in k_values:
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(X_scaled)
    inertia.append(kmeans.inertia_)

plt.figure(figsize=(8, 6))
plt.plot(k_values, inertia, marker='o')
plt.title("Elbow Plot untuk Menentukan k")
plt.xlabel("Jumlah Cluster (k)")
plt.ylabel("Inertia (SSE)")
plt.grid()
plt.savefig('26_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20026/26_03.png" width=”500”>


### Kesimpulan 
Implementasi K-Means berhasil mengelompokkan data menjadi beberapa cluster. Performa model dievaluasi menggunakan inertia dan visualisasi.
