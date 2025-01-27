# Challenge Day 27

## 📝 Topik
**Analisis Hasil Clustering**

Menganalisis hasil clustering menggunakan visualisasi scatter plot untuk memahami pola yang terbentuk.

---

## 🎯 Learning Objectives
1. Memahami cara memvisualisasikan hasil clustering pada dataset.
2. Mengevaluasi hasil clustering berdasarkan distribusi data di scatter plot.
3. Mengidentifikasi pola dan anomali pada hasil clustering.
4. Menggunakan visualisasi untuk komunikasi dan interpretasi hasil.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Setelah mengelompokkan data menggunakan algoritma clustering (misalnya K-Means), langkah penting selanjutnya adalah menganalisis hasil clustering. Scatter plot adalah alat yang efektif untuk memvisualisasikan cluster, memahami pola distribusi, dan memvalidasi hasil algoritma. Dengan memvisualisasikan cluster bersama centroid, Anda dapat mengevaluasi apakah hasil clustering sudah sesuai dengan ekspektasi.

---
## 🚀 Langkah-Langkah

### Persiapan Dataset
Gunakan dataset sintetis yang telah dikelompokkan menggunakan K-Means
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
from sklearn.preprocessing import StandardScaler

X, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.2, random_state=42)

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

kmeans = KMeans(n_clusters=4, random_state=42)
kmeans.fit(X_scaled)
labels = kmeans.labels_
centroids = kmeans.cluster_centers_
```

### Visualisasi Scatter Plot
Buat scatter plot untuk memvisualisasikan cluster dan centroid.
```python
plt.figure(figsize=(8, 6))
for cluster in range(4):
    plt.scatter(X_scaled[labels == cluster, 0], X_scaled[labels == cluster, 1], label=f'Cluster {cluster + 1}')

plt.scatter(centroids[:, 0], centroids[:, 1], color='red', marker='X', s=200, label='Centroid')

plt.title("Visualisasi Hasil Clustering")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.legend()
plt.grid()
plt.savefig('27_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20027/27_01.png" width=”500”>

### Analisis Visualisasi
- Perhatikan jarak antar cluster: Apakah cluster terpisah dengan jelas?
- Periksa distribusi data dalam setiap cluster: Apakah terdapat tumpang tindih?
```python
plt.figure(figsize=(8, 6))
for cluster in range(4):
    plt.scatter(X_scaled[labels == cluster, 0], X_scaled[labels == cluster, 1], label=f'Cluster {cluster + 1}')
    centroid_x, centroid_y = centroids[cluster]
    plt.text(centroid_x, centroid_y, f'C{cluster + 1}', color='black', fontsize=12, ha='center', va='center')

plt.scatter(centroids[:, 0], centroids[:, 1], color='red', marker='X', s=200, label='Centroid')
plt.title("Hasil Clustering dengan Anotasi Centroid")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.legend()
plt.grid()
plt.savefig('27_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20027/27_02.png" width=”500”>

### Tugas Tambahan
1. **Eksperimen dengan Parameter:** Ubah jumlah cluster (𝑘) dan amati perubahan distribusi cluster pada plot.
2. **Dimensi Tambahan:** Jika dataset memiliki lebih dari dua fitur, gunakan visualisasi 3D atau PCA untuk mereduksi dimensi.
```python
from mpl_toolkits.mplot3d import Axes3D

X, _ = make_blobs(n_samples=300, centers=4, cluster_std=1.2, random_state=42, n_features=3)

X_scaled = scaler.fit_transform(X)
kmeans.fit(X_scaled)
labels = kmeans.labels_
centroids = kmeans.cluster_centers_

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')
for cluster in range(4):
    ax.scatter(X_scaled[labels == cluster, 0], X_scaled[labels == cluster, 1], X_scaled[labels == cluster, 2], label=f'Cluster {cluster + 1}')

ax.scatter(centroids[:, 0], centroids[:, 1], centroids[:, 2], color='red', marker='X', s=200, label='Centroid')
ax.set_title("Visualisasi Hasil Clustering (3D)")
ax.set_xlabel("Fitur 1")
ax.set_ylabel("Fitur 2")
ax.set_zlabel("Fitur 3")
plt.legend()
plt.savefig('27_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20027/27_03.png" width=”500”>


### Kesimpulan 
Scatter plot dapat mengevaluasi hasil clustering secara visual. Visualisasi ini membantu memahami distribusi cluster, keterpisahan antar cluster, dan relevansi hasil dengan konteks data.
