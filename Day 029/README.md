# Challenge Day 29

## 📝 Topik
**Principal Component Analysis (PCA)**

Mengenal dan mengimplementasikan Principal Component Analysis (PCA) untuk reduksi dimensi data dan visualisasi hasilnya.

---

## 🎯 Learning Objectives
1. Memahami konsep PCA sebagai metode reduksi dimensi dalam machine learning.
2. Mengetahui bagaimana PCA bekerja dalam mengubah data berdimensi tinggi menjadi representasi yang lebih sederhana.
3. Menggunakan PCA untuk mengekstrak fitur utama dari dataset.
4. Memvisualisasikan hasil reduksi dimensi dalam bentuk 2D dan 3D.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Dalam machine learning, kita sering menghadapi dataset dengan banyak fitur atau dimensi. Namun, semakin banyak dimensi, semakin sulit untuk menganalisis dan menemukan pola dalam data (curse of dimensionality).

Principal Component Analysis (PCA) adalah teknik yang digunakan untuk mengurangi dimensi tanpa kehilangan terlalu banyak informasi penting. PCA bekerja dengan mengubah dataset asli menjadi komponen utama yang merepresentasikan variasi terbesar dalam data.

---
## 🚀 Langkah-Langkah

### Membaca dan Memahami Teori PCA
#### Apa itu PCA?
Principal Component Analysis (PCA) adalah teknik reduksi dimensi yang digunakan dalam pembelajaran mesin dan analisis data. PCA bekerja dengan mengubah kumpulan variabel yang mungkin berkorelasi menjadi kumpulan variabel baru yang tidak berkorelasi, yang disebut principal components (komponen utama).

#### Bagaimana PCA Mengubah Data?
1. **Menstandarisasi Data** → PCA pertama-tama mengubah data ke dalam skala yang sama agar setiap variabel memiliki kontribusi yang seimbang.
2. **Membangun Matriks Kovarians** → PCA menghitung hubungan antar fitur dalam dataset.
3. **Menghitung Eigenvalues dan Eigenvectors** → Digunakan untuk menentukan arah dan besaran variasi data.
4. **Memilih Komponen Utama** → Komponen utama dengan varians terbesar dipilih sebagai representasi data yang lebih ringkas.
5. **Transformasi Data** → Data asli diproyeksikan ke ruang dengan dimensi yang lebih kecil berdasarkan komponen utama yang dipilih.

#### Apa Manfaat Menggunakan PCA?
- **Mengurangi Dimensi Data** → Mengurangi jumlah variabel tanpa banyak kehilangan informasi penting.
- **Meningkatkan Efisiensi Komputasi** → Model pembelajaran mesin dapat berjalan lebih cepat dengan lebih sedikit fitur.
- **Mengurangi Overfitting** → Menghilangkan fitur yang kurang informatif atau redundan.
- **Membantu dalam Visualisasi Data** → Data berdimensi tinggi dapat divisualisasikan dalam 2D atau 3D menggunakan PCA.

### Import Library dan Dataset
Gunakan dataset wine dari sklearn yang memiliki banyak fitur.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import load_wine

data = load_wine()
X = data.data  
y = data.target  

df = pd.DataFrame(X, columns=data.feature_names)
df["target"] = y

df.head()
```
Output:
```bash
	alcohol	malic_acid	ash	alcalinity_of_ash	magnesium	total_phenols	flavanoids	nonflavanoid_phenols	proanthocyanins	color_intensity	hue	od280/od315_of_diluted_wines	proline	target
0	14.23			1.71	2.43			15.6		127.0		2.80		3.06			0.28		2.29		5.64	1.04				3.92	1065.0	0
1	13.20			1.78	2.14			11.2		100.0		2.65		2.76			0.26		1.28		4.38	1.05			3.40	1050.0	0
2	13.16			2.36	2.67			18.6		101.0		2.80		3.24			0.30		2.81		5.68	1.03			3.17	1185.0	0
3	14.37			1.95	2.50			16.8		113.0		3.85		3.49			0.24		2.18		7.80	0.86			3.45	1480.0	0
4	13.24			2.59	2.87			21.0		118.0		2.80		2.69			0.39		1.82		4.32	1.04			2.93	735.0	0
```

### Eksplorasi Data
Cek jumlah fitur dalam dataset & cek korelasi antar fitur dengan heatmap
```python
print(f"Jumlah fitur dalam dataset: {X.shape[1]}")

plt.figure(figsize=(12, 8))
sns.heatmap(df.iloc[:, :-1].corr(), cmap="coolwarm", annot=False)
plt.title("Korelasi Antar Fitur dalam Dataset Wine")
plt.savefig('29_01.png', format='png', dpi=300)
plt.show()
```
Output:
Jumlah fitur dalam dataset: 13
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20029/29_01.png" width=”500”>

### Normalisasi Data
PCA bekerja lebih baik jika data distanardisasi terlebih dahulu.
```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

### Implementasi PCA untuk 2 Dimensi
Lakukan reduksi ke 2 komponen utama & visualisasi hasil PCA dalam scatter plot 2D.
```python
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

print(f"Variansi yang dijelaskan oleh 2 komponen utama: {pca.explained_variance_ratio_}")

plt.figure(figsize=(10, 6))
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=y, cmap="viridis", edgecolor="k", s=50)
plt.xlabel("Komponen Utama 1")
plt.ylabel("Komponen Utama 2")
plt.title("Visualisasi PCA - Reduksi Dimensi ke 2D")
plt.colorbar(label="Kelas")
plt.savefig('29_02.png', format='png', dpi=300)
plt.show()
```
Output:
Variansi yang dijelaskan oleh 2 komponen utama: [0.36198848 0.1920749 ]
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20029/29_02.png" width=”500”>

### Implementasi PCA untuk 3 Dimensi
Lakukan reduksi ke 3 komponen utama & Visualisasi dalam scatter plot 3D.
```python
pca_3d = PCA(n_components=3)
X_pca_3d = pca_3d.fit_transform(X_scaled)

print(f"Variansi yang dijelaskan oleh 3 komponen utama: {pca_3d.explained_variance_ratio_}")

from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection="3d")
scatter = ax.scatter(X_pca_3d[:, 0], X_pca_3d[:, 1], X_pca_3d[:, 2], c=y, cmap="viridis", edgecolor="k", s=50)

ax.set_xlabel("Komponen Utama 1")
ax.set_ylabel("Komponen Utama 2")
ax.set_zlabel("Komponen Utama 3")
ax.set_title("Visualisasi PCA - Reduksi Dimensi ke 3D")

plt.colorbar(scatter, label="Kelas")
plt.savefig('29_03.png', format='png', dpi=300)
plt.show()
```
Output:
Variansi yang dijelaskan oleh 3 komponen utama: [0.36198848 0.1920749  0.11123631]
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20029/29_03.png" width=”500”>

### Analisis Variansi yang Dijelaskan oleh PCA
Cek berapa banyak informasi yang dipertahankan oleh setiap komponen utama.
```python
plt.figure(figsize=(8, 5))
plt.plot(range(1, X.shape[1] + 1), np.cumsum(PCA().fit(X_scaled).explained_variance_ratio_), marker="o", linestyle="--")
plt.xlabel("Jumlah Komponen Utama")
plt.ylabel("Cumulative Explained Variance")
plt.title("Analisis Variansi oleh PCA")
plt.savefig('29_04.png', format='png', dpi=300)
plt.show()
```
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20029/29_04.png" width=”500”>

### Challenges
1. **Uji PCA dengan Dataset Lain**
Gunakan dataset lain seperti `breast_cancer` atau `digits` dari `sklearn`.
2. **Coba Model Machine Learning Sebelum dan Sesudah PCA**
Bandingkan akurasi model dengan data asli vs setelah reduksi PCA.

### Kesimpulan 
**PCA** dapat membantu dalam reduksi dimensi dataset dengan tetap mempertahankan informasi yang penting.

- PCA mengubah data berdimensi tinggi menjadi beberapa komponen utama.
- Hasil PCA bisa divisualisasikan dalam bentuk 2D atau 3D.
- PCA dapat menyederhanakan analisis data tanpa kehilangan terlalu banyak informasi.
