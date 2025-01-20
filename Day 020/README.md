# Challenge Day 20

## 📝 Topik
**Pengenalan Machine Learning**
Mempelajari konsep dasar machine learning, termasuk perbedaan antara supervised dan unsupervised learning.

---

## 🎯 Learning Objectives
1. Memahami konsep dasar machine learning dan bagaimana ia digunakan untuk membuat prediksi dan keputusan berbasis data.
2. Menjelaskan perbedaan antara supervised dan unsupervised learning.
3. Mengenal algoritma umum untuk supervised learning (contoh: regresi, klasifikasi) dan unsupervised learning (contoh: clustering, reduksi dimensi).
4. Menerapkan contoh sederhana algoritma supervised dan unsupervised menggunakan dataset yang tersedia.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Machine learning (ML) adalah cabang kecerdasan buatan yang memungkinkan komputer belajar dari data tanpa harus diprogram secara eksplisit.

- **Supervised Learning:** Model dilatih dengan data berlabel untuk memprediksi hasil (contoh: klasifikasi email sebagai spam atau tidak).
- **Unsupervised Learning:** Model menemukan pola dalam data tanpa label (contoh: mengelompokkan pelanggan berdasarkan kebiasaan belanja).


---
## 🚀 Langkah-Langkah

### Persiapan Dataset
Dataset Iris untuk supervised learning
```python
from sklearn.datasets import load_iris
import pandas as pd

iris = load_iris()
iris_data = pd.DataFrame(iris.data, columns=iris.feature_names)
iris_data['Target'] = iris.target

print("Dataset Iris:")
print(iris_data.head())
```
Output:
```bash
Dataset Iris:
   sepal length (cm)  sepal width (cm)  petal length (cm)  petal width (cm)  \
0                5.1               3.5                1.4               0.2   
1                4.9               3.0                1.4               0.2   
2                4.7               3.2                1.3               0.2   
3                4.6               3.1                1.5               0.2   
4                5.0               3.6                1.4               0.2   

   Target  
0       0  
1       0  
2       0  
3       0  
4       0 
```

### Persiapan Dataset
Data Dummy untuk unsupervised learning
```python
from sklearn.datasets import make_blobs
data, labels = make_blobs(n_samples=200, centers=3, random_state=42)
unsupervised_data = pd.DataFrame(data, columns=["Feature 1", "Feature 2"])

print("\nData Dummy untuk Clustering:")
print(unsupervised_data.head())
```
Output:
```bash
Data Dummy untuk Clustering:
   Feature 1  Feature 2
0   6.505653   2.447003
1  -5.128943   9.836189
2  -6.891874  -7.777364
3  -8.327712  -8.287573
4  -7.468992  -6.030507
```

### Supervised Learning: Klasifikasi Sederhana
Latih model klasifikasi sederhana menggunakan data Iris.
```python
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

X = iris_data[iris.feature_names]
y = iris_data['Target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

clf = DecisionTreeClassifier(random_state=42)
clf.fit(X_train, y_train)

y_pred = clf.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
print("\nAkurasi Model Klasifikasi Decision Tree:", accuracy)
```
Output:
```bash
Akurasi Model Klasifikasi Decision Tree: 1.0
```

### Unsupervised Learning: Clustering
Lakukan clustering menggunakan algoritma K-Means untuk mengelompokkan data berdasarkan pola.
```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

kmeans = KMeans(n_clusters=3, random_state=42)
clusters = kmeans.fit_predict(unsupervised_data)

unsupervised_data['Cluster'] = clusters

plt.figure(figsize=(8, 6))
for cluster in range(3):
    cluster_data = unsupervised_data[unsupervised_data['Cluster'] == cluster]
    plt.scatter(cluster_data['Feature 1'], cluster_data['Feature 2'], label=f'Cluster {cluster}')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], color='red', marker='X', label='Centroid')
plt.title('Hasil Clustering K-Means')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.legend()
plt.grid()
plt.savefig(20_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20020/20_01.png" width=”500”>

### Kesimpulan 
1. **Supervised Learning:** Cocok untuk masalah dengan data berlabel (misalnya klasifikasi atau prediksi nilai).
2. **Unsupervised Learning:** Cocok untuk eksplorasi data dan menemukan pola tersembunyi.
3. Penerapan yang tepat dari kedua pendekatan bergantung pada jenis data dan tujuan analisis.
