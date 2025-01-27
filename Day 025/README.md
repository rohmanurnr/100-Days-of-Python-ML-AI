# Challenge Day 25

## 📝 Topik
**Pengenalan Clustering**

Memahami konsep clustering dan penerapannya pada data untuk menemukan kelompok-kelompok yang tersembunyi.

---

## 🎯 Learning Objectives
1. Memahami apa itu clustering dan bagaimana clustering berbeda dari supervised learning
2. Mempelajari konsep dasar algoritma clustering seperti K-Means
3. Menerapkan clustering pada dataset sederhana untuk menemukan pola-pola tersembunyi
4. Menginterpretasikan hasil clustering secara visual

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Clustering adalah teknik dalam machine learning yang digunakan untuk mengelompokkan data ke dalam grup berdasarkan kesamaan. Clustering termasuk dalam kategori unsupervised learning karena tidak memerlukan label pada data.

Mengapa Clustering Penting?

- Membantu memahami struktur data
- Berguna dalam eksplorasi data sebelum analisis lebih lanjut
- Digunakan dalam berbagai aplikasi seperti segmentasi pelanggan, analisis citra, dan pengelompokkan dokumen.

---
## 🚀 Langkah-Langkah

### Pahami Konsep K-Means Clustering & Persiapan Data
K-Means mengelompokkan data berdasarkan jarak ke pusat cluster (centroid)
Parameter utama: jumlah cluster (k)
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs

X, _ = make_blobs(n_samples=200, centers=3, cluster_std=1.0, random_state=42)

plt.figure(figsize=(8, 6))
plt.scatter(X[:, 0], X[:, 1], color='gray', alpha=0.7)
plt.title("Dataset Awal")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.savefig('25_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20025/25_01.png" width=”500”>

### Terapkan K-Means pada Dataset Sederhana
```python
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(X)

labels = kmeans.labels_
centroids = kmeans.cluster_centers_
```
Output:

### Visualisasi Hasil Clustering
Tampilkan data dalam scatter plot dengan warna berbeda untuk setiap cluster
```python
plt.figure(figsize=(8, 6))
for cluster in range(3):
    plt.scatter(X[labels == cluster, 0], X[labels == cluster, 1], label=f'Cluster {cluster + 1}')

plt.scatter(centroids[:, 0], centroids[:, 1], color='red', marker='X', s=200, label='Centroid')

plt.title("Hasil Clustering dengan K-Means")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.legend()
plt.grid()
plt.savefig('25_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20025/25_02.png" width=”500”>


### Analisis dan Diskusi
1. **Cluster yang terbentuk:** Apakah data dalam setiap cluster terlihat terpisah dengan baik?
2. **Centroid:** Apakah posisi centroid mencerminkan pust dari setiap cluster?
3. **Jumlah Cluster (k):** Bagaimana jika k diubah menjadi nilai lain?

### Kesimpulan 
- Clustering adalah teknik yang berguna untuk menemukan pola tersembunyi dalam data
- Algoritma K-Means memisahkan data berdasarkan kedekatan ke centroid
- Visualisasi membantu memahami hasil clustering secara intuitif
