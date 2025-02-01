# Challenge Day 31

## 📝 Topik
**Pengenalan Supervised Learning**

Pelajari perbedaan regresi dan klasifikasi dengan contoh kasus untuk memahami bagaimana model memprediksi nilai kontinu dan kategori.

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Supervised Learning.
2. Mengerti perbedaan antara Regresi (prediksi nilai kontinu) dan Klasifikasi (prediksi kategori).
3. Memahami cara kerja algoritma regresi dan klasifikasi dengan contoh data nyata.
4. Mencoba implementasi dasar regresi menggunakan Linear Regression dan klasifikasi menggunakan Logistic Regression.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Supervised Learning adalah jenis algoritma Machine Learning yang melibatkan data yang sudah dilabeli untuk melatih model. Dua jenis utama dalam supervised learning adalah Regresi dan Klasifikasi:

- **Regresi** digunakan untuk memprediksi nilai kontinu, misalnya memprediksi harga rumah berdasarkan luas tanah.
- **Klasifikasi** digunakan untuk memprediksi kategori atau kelas, misalnya memprediksi apakah seseorang akan lulus ujian berdasarkan jumlah jam belajar.

---
## 🚀 Langkah-Langkah

### Persiapan Lingkungan
Pastikan kamu sudah menginstal Scikit-learn
```bash
pip install scikit-learn
```
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression, LogisticRegression
from sklearn.metrics import mean_squared_error, accuracy_score
```

### Regresi: Memprediksi Harga Rumah Berdasarkan Luas Tanah
#### Persiapan data & pembagian dataset menjadi training dan testing
```python
X = np.array([30, 50, 70, 90, 110, 130, 150]).reshape(-1, 1)  
y = np.array([300, 500, 700, 900, 1100, 1300, 1500])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42) 
```

#### Membuat model regresi linear & prediksi harga rumah
```python
model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

#### Evaluasi model
```python
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
```
Output:
```bash
Mean Squared Error: 2.1002632740604218e-26
```

#### Visualisasi hasil
```python
plt.scatter(X, y, color="blue", label="Data Asli")
plt.plot(X, model.predict(X), color="red", linestyle="--", label="Prediksi")
plt.xlabel("Luas Rumah (m2)")
plt.ylabel("Harga Rumah (juta)")
plt.legend()
plt.savefig('Day_031_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20031/Day_031_01.png" width=”500”>


### Klasifikasi: Prediksi Kelulusan Berdasarkan Jam Belajar
#### Persiapan data & pembagian dataset menjadi training dan testing
```python
X = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]).reshape(-1, 1)  
y = np.array([0, 0, 0, 0, 1, 1, 1, 1, 1, 1])  

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

#### Membuat model klasifikasi & prediksi kelulusan
```python
clf = LogisticRegression()
clf.fit(X_train, y_train)

y_pred = clf.predict(X_test)
```

#### Evaluasi model
```python
accuracy = accuracy_score(y_test, y_pred)
print(f"Akurasi Model: {accuracy * 100:.2f}%")
```
Output:
```bash
Akurasi Model: 100.00%
```

#### Visualisasi hasil
```python
plt.scatter(X, y, color="green", label="Data Asli")
plt.scatter(X_test, y_pred, color="red", marker="x", label="Prediksi Model")
plt.xlabel("Jam Belajar")
plt.ylabel("Status Kelulusan (0=Tidak Lulus, 1=Lulus)")
plt.legend()
plt.savefig('Day_031_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20031/Day_031_02.png" width=”500”>


### Kesimpulan 
1. **Regresi** digunakan untuk memprediksi **nilai kontinu** (seperti harga atau suhu).
2. **Klasifikasi** digunakan untuk memprediksi **kategori atau kelas** (seperti lulus atau tidak lulus).
3. **Evaluasi model** sangat penting untuk mengetahui kualitas prediksi. Untuk regresi, kita menggunakan **Mean Squared Error (MSE)**, sementara untuk klasifikasi, kita menggunakan **Akurasi**.
4. **Scikit-learn** menyediakan berbagai model yang dapat diterapkan dengan mudah untuk tugas-tugas **regresi** dan **klasifikasi**.
