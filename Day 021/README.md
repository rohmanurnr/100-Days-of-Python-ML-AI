# Challenge Day 21

## 📝 Topik
**Linear Regression (Teori)**
Mempelajari teori dasar regresi linear, bagaimana cara kerjanya, dan aplikasinya dalam prediksi berbasis data.

---

## 🎯 Learning Objectives
1. Memahami konsep regresi linear dan persamaan garis regresi `y=mx+c`.
2. Menjelaskan bagaimana regresi linear digunakan untuk memprediksi nilai kontinu berdasarkan fitur.
3. Memahami metode Ordinary Least Squares (OLS) untuk mencari garis regresi terbaik.
4. Menerapkan regresi linear sederhana menggunakan Python.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Regresi linear adalah salah satu algoritma machine learning paling dasar yang digunakan untuk prediksi nilai kontinu.
Pada regresi linear:

- **Supervised Learning:** Model dilatih menggunakan data berlabel `(𝑋 dan 𝑦)`.
- **Tujuan:** Menemukan hubungan linear antara fitur (independen) dan target (dependen).
- **Metode:** Ordinary Least Squares (OLS) digunakan untuk meminimalkan error antara prediksi dan data sebenarnya.

---
## 🚀 Langkah-Langkah

### Memahami Teori Regresi Linear
Persamaan garis: `𝑦 =𝑚𝑥 + 𝑐`, di mana:
- `m`: kemiringan garis
- `c`: intercept

Metode OLS: Meminimumkan sum of squared errors 
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20021/21_01.png" width=”300”>

### Implementasi Regresi Linear Sederhana
Gunakan Python untuk membangun model regresi linear menggunakan dataset sederhana (contoh: data prediksi nilai berdasarkan waktu belajar).
```python
import pandas as pd
import numpy as np

data = {
    "Waktu Belajar (Jam)": [1, 2, 3, 4, 5],
    "Nilai": [50, 55, 65, 70, 75]
}
df = pd.DataFrame(data)
print("Dataset:\n", df)
```
Output:
```bash
Dataset:
    Waktu Belajar (Jam)  Nilai
0                    1     50
1                    2     55
2                    3     65
3                    4     70
4                    5     75
```

### Visualisasi Data
Scatter plot untuk melihat hubungan antara variabel
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
plt.scatter(df["Waktu Belajar (Jam)"], df["Nilai"], color='blue', label='Data')
plt.title("Hubungan Waktu Belajar dan Nilai")
plt.xlabel("Waktu Belajar (Jam)")
plt.ylabel("Nilai")
plt.legend()
plt.grid()
plt.savefig(‘21_02.png’, format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20021/21_02.png" width=”500”>

### Regresi Linear dengan Python
Membuat model regresi linear
```python
from sklearn.linear_model import LinearRegression

X = df[["Waktu Belajar (Jam)"]]
y = df["Nilai"]

model = LinearRegression()
model.fit(X, y)

print("Koefisien (m):", model.coef_[0])
print("Intercept (c):", model.intercept_)

y_pred = model.predict(X)

df["Prediksi"] = y_pred
print("\nData dengan Prediksi:\n", df)
```
Output:
```bash
Koefisien (m): 6.500000000000001
Intercept (c): 43.5

Data dengan Prediksi:
    Waktu Belajar (Jam)  Nilai  Prediksi
0                    1     50      50.0
1                    2     55      56.5
2                    3     65      63.0
3                    4     70      69.5
4                    5     75      76.0
```

### Visualisasi Garis Regresi
```python
plt.figure(figsize=(8, 6))
plt.scatter(df["Waktu Belajar (Jam)"], df["Nilai"], color='blue', label='Data Asli')
plt.plot(df["Waktu Belajar (Jam)"], df["Prediksi"], color='red', label='Garis Regresi')
plt.title("Garis Regresi Linear")
plt.xlabel("Waktu Belajar (Jam)")
plt.ylabel("Nilai")
plt.legend()
plt.grid()
plt.savefig(‘21_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20021/21_03.png" width=”500”>


### Evaluasi Model
Mean Squared Error
```python
from sklearn.metrics import mean_squared_error

mse = mean_squared_error(y, y_pred)
print("Mean Squared Error (MSE):", mse)
```
Output:
```bash
Mean Squared Error (MSE): 1.5
```

### Kesimpulan 
1. **Persamaan Regresi Linear:** Dapat digunakan untuk memodelkan hubungan linear sederhana antara dua variabel.
2. **OLS:** Teknik untuk meminimalkan error prediksi.
3. **Implementasi Sederhana:** Python menyediakan alat seperti `LinearRegression` untuk membangun model dengan mudah.
