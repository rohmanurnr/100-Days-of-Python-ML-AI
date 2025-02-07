# Challenge Day 38

## 📝 Topik
**Support Vector Machine (SVM)**

Konsep Hyperplane, Margin, dan Kernel dalam Support Vector Machine (SVM)

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Support Vector Machine (SVM) sebagai algoritma klasifikasi.
2. Menjelaskan hyperplane sebagai garis pemisah dalam klasifikasi.
3. Memahami konsep margin dan peran support vectors dalam SVM.
4. Mengetahui bagaimana kernel trick digunakan untuk menangani data non-linear.
5. Memahami perbedaan antara SVM linear dan non-linear.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Support Vector Machine (SVM) adalah algoritma klasifikasi yang bekerja dengan mencari hyperplane terbaik untuk memisahkan kelas-kelas dalam data.
Konsep utama dalam SVM:

- Hyperplane → Garis atau bidang yang memisahkan kelas dalam ruang fitur.
- Margin → Jarak antara hyperplane dan titik data terdekat dari masing-masing kelas.
- Support Vectors → Titik data yang berada paling dekat dengan hyperplane dan menentukan posisi hyperplane.
- Kernel Trick → Teknik yang memungkinkan SVM bekerja dengan data yang tidak bisa dipisahkan secara linear.

SVM sangat populer dalam klasifikasi gambar, teks, dan bioinformatika karena kemampuannya dalam menangani data berdimensi tinggi dan memberikan margin maksimal untuk klasifikasi yang lebih baik.

---
## 🚀 Langkah-Langkah

### Konsep Hyperplane dan Margin dalam SVM
Pada SVM, hyperplane adalah garis yang membagi data ke dalam dua kelas.

- Jika data 2 dimensi, hyperplane berupa garis.
- Jika data 3 dimensi, hyperplane berupa bidang.
- Jika lebih dari 3 dimensi, hyperplane berada dalam dimensi yang lebih tinggi.

Persamaan hyperplane dalam 2D:

w1​x1 + w2x2 + b = 0

di mana:

𝑤1, 𝑤2 → bobot (weights)
𝑥1, 𝑥2 → fitur data
𝑏 → bias

SVM memilih hyperplane yang memiliki margin terbesar untuk memisahkan kelas.
Margin adalah jarak antara support vectors (titik data terdekat) dan hyperplane.

### Membuat Dataset untuk Klasifikasi dengan SVM
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_classification

X, y = make_classification(n_samples=100, n_features=2, n_informative=2, 
                           n_redundant=0, n_clusters_per_class=1, random_state=42)

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm', edgecolors='k')
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.title("Dataset untuk Klasifikasi SVM")
plt.savefig('Day_038_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20038/Day_038_01.png" width=”500”>

### Melatih Model SVM dengan Kernel Linear
```python
from sklearn.svm import SVC

svm_model = SVC(kernel='linear')

svm_model.fit(X, y)
```
Output:
```bash
SVC(kernel='linear')
```

### Menampilkan Hyperplane dan Margin
- Ambil bobot dan bias dari model SVM
- Buat garis hyperplane
- Plot dataset dan hyperplane
- Tambahkan support vectors ke plot

```python
w = svm_model.coef_[0]
b = svm_model.intercept_[0]

x_vals = np.linspace(min(X[:, 0]), max(X[:, 0]), 100)
y_vals = - (w[0] * x_vals + b) / w[1]

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm', edgecolors='k')
plt.plot(x_vals, y_vals, 'k--', label='Hyperplane')

plt.scatter(svm_model.support_vectors_[:, 0], svm_model.support_vectors_[:, 1], s=100, edgecolors='black', facecolors='none', label="Support Vectors")

plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.title("Hyperplane dan Support Vectors dalam SVM")
plt.legend()
plt.savefig('Day_038_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20038/Day_038_02.png" width=”500”>

### Memahami Peran Kernel dalam SVM
Beberapa dataset tidak bisa dipisahkan dengan hyperplane linear.
SVM menggunakan kernel trick untuk mengubah data ke dimensi yang lebih tinggi agar bisa dipisahkan dengan lebih baik.

- Linear Kernel → Cocok untuk data yang dapat dipisahkan dengan garis lurus.
- Polynomial Kernel → Memungkinkan pemisahan dengan kurva polinomial.
- RBF (Radial Basis Function) Kernel → Cocok untuk data kompleks yang tidak dapat dipisahkan secara linear.
- Sigmoid Kernel → Digunakan dalam model yang menyerupai jaringan saraf tiruan (ANN).

### Mencoba Kernel Linear vs RBF
Bandingkan bagaimana SVM dengan kernel linear dan kernel RBF menangani dataset berbentuk moons yang tidak dapat dipisahkan secara linear.

- Buat dataset berbentuk moon (non-linear)
- Latih model SVM dengan kernel linear
- Latih model SVM dengan kernel RBF
- Visualisasi hasil klasifikasi dengan linear dan RBF kernel
- Plot untuk kernel linear
- Plot untuk kernel RBF

```python
from sklearn.datasets import make_moons
import seaborn as sns

X_moon, y_moon = make_moons(n_samples=100, noise=0.2, random_state=42)

svm_linear = SVC(kernel='linear')
svm_linear.fit(X_moon, y_moon)

svm_rbf = SVC(kernel='rbf')
svm_rbf.fit(X_moon, y_moon)

fig, ax = plt.subplots(1, 2, figsize=(12, 5))

sns.scatterplot(x=X_moon[:, 0], y=X_moon[:, 1], hue=y_moon, edgecolor='k', palette='coolwarm', ax=ax[0])
ax[0].set_title("SVM dengan Kernel Linear")

sns.scatterplot(x=X_moon[:, 0], y=X_moon[:, 1], hue=y_moon, edgecolor='k', palette='coolwarm', ax=ax[1])
ax[1].set_title("SVM dengan Kernel RBF")
plt.savefig('Day_038_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20038/Day_038_03.png" width=”500”>

### Challenge
- Coba gunakan SVM dengan kernel polynomial dan bandingkan hasilnya.
- Cari contoh kasus di dunia nyata di mana SVM sering digunakan.
- Pelajari kelebihan dan kekurangan SVM dibanding algoritma lain seperti Random Forest atau Logistic Regression.

#### SVM dengan kernel polynomial
```python
from sklearn.datasets import make_moons
from sklearn.svm import SVC
import seaborn as sns
import matplotlib.pyplot as plt

X_moon, y_moon = make_moons(n_samples=100, noise=0.2, random_state=42)

svm_linear = SVC(kernel='linear')
svm_linear.fit(X_moon, y_moon)

svm_rbf = SVC(kernel='rbf')
svm_rbf.fit(X_moon, y_moon)

svm_poly = SVC(kernel='poly', degree=3)  # SVM dengan kernel polynomial derajat 3
svm_poly.fit(X_moon, y_moon)

fig, ax = plt.subplots(1, 3, figsize=(18, 5))

sns.scatterplot(x=X_moon[:, 0], y=X_moon[:, 1], hue=y_moon, edgecolor='k', palette='coolwarm', ax=ax[0])
ax[0].set_title("SVM dengan Kernel Linear")

sns.scatterplot(x=X_moon[:, 0], y=X_moon[:, 1], hue=y_moon, edgecolor='k', palette='coolwarm', ax=ax[1])
ax[1].set_title("SVM dengan Kernel RBF")

sns.scatterplot(x=X_moon[:, 0], y=X_moon[:, 1], hue=y_moon, edgecolor='k', palette='coolwarm', ax=ax[2])
ax[2].set_title("SVM dengan Kernel Polynomial (Degree=3)")

plt.savefig('Day_038_04.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20038/Day_038_04.png" width=”500”>

### Kesimpulan 
- SVM bekerja dengan mencari hyperplane terbaik untuk memisahkan kelas.
- Hyperplane dipilih berdasarkan margin terbesar dengan support vectors sebagai referensi.
- Kernel trick memungkinkan SVM menangani data yang tidak bisa dipisahkan secara linear.
- Linear SVM cocok untuk dataset sederhana, sedangkan non-linear SVM (dengan kernel RBF atau polynomial) lebih fleksibel untuk dataset kompleks.
- SVM sangat berguna untuk klasifikasi dengan dimensi fitur tinggi dan banyak digunakan dalam pengenalan pola, deteksi wajah, dan klasifikasi teks.
