# Challenge Day 22

## 📝 Topik
**Linear Regression (Praktik)**

Membangun model regresi linear untuk memprediksi data sederhana menggunakan Python, dan mengevaluasi kinerjanya.

---

## 🎯 Learning Objectives
1. Menggunakan Python untuk membangun model regresi linear.
2. Melatih model pada dataset sederhana.
3. Mengevaluasi kinerja model menggunakan metrik seperti Mean Squared Error (MSE) dan `R^2 - score`
4. Memvisualisasikan hubungan data asli, prediksi, dan garis regresi.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Setelah mempelajari teori regresi linear, kini saatnya mengimplementasikan model ini pada dataset sederhana.
Regresi linear adalah model yang sangat efektif untuk hubungan linear antara variabel. Anda akan:

- Melatih model menggunakan dataset.
- Menganalisis hasil prediksi.
- Mengevaluasi kinerjanya untuk memahami seberapa baik model bekerja.

---
## 🚀 Langkah-Langkah

### Persiapan Dataset
Gunakan dataset sederhana yang berisi informasi waktu belajar (jam) dan nilai ujian.
```python
import pandas as pd
import numpy as np

data = {
    "Waktu Belajar (Jam)": [1, 2, 3, 4, 5, 6, 7, 8],
    "Nilai": [50, 55, 60, 65, 70, 75, 80, 85]
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
2                    3     60
3                    4     65
4                    5     70
5                    6     75
6                    7     80
7                    8     85
```

### Membagi Dataset
Bagi dataset menjadi training dan testing set  (80% train, 20% test) untuk melatih dan menguji model.
```python
from sklearn.model_selection import train_test_split

X = df[["Waktu Belajar (Jam)"]]
y = df["Nilai"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print("Training Data:\n", X_train)
print("Testing Data:\n", X_test)
```
Output:
```bash
Training Data:
    Waktu Belajar (Jam)
0                    1
7                    8
2                    3
4                    5
3                    4
6                    7
Testing Data:
    Waktu Belajar (Jam)
1                    2
5                    6
```

### Melatih Model
Bangun model regresi linear menggunakan library `scikit-learn`.
```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)

print("Koefisien (m):", model.coef_[0])
print("Intercept (c):", model.intercept_)
```
Output:
```bash
Koefisien (m): 4.999999999999999
Intercept (c): 45.0
```

### Prediksi dan Evaluasi Kinerja
Gunakan metrik MSE dan R^2-score untuk mengevaluasi kinerja model.
```python
from sklearn.metrics import mean_squared_error, r2_score

y_pred = model.predict(X_test)

mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print("Mean Squared Error (MSE):", mse)
print("R-squared (R^2):", r2)
```
Output:
```bash
Mean Squared Error (MSE): 0.0
R-squared (R^2): 1.0
```

### Visualisasi
Visualisasi data asli dan garis regresi
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
plt.scatter(X, y, color='blue', label='Data Asli')  # Data asli
plt.plot(X, model.predict(X), color='red', label='Garis Regresi')  # Garis regresi
plt.title("Linear Regression: Waktu Belajar vs Nilai")
plt.xlabel("Waktu Belajar (Jam)")
plt.ylabel("Nilai")
plt.legend()
plt.grid()
plt.savefig(‘22_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20022/22_01.png" width=”500”>

### Kesimpulan 
1. **Model Training:** Anda berhasil melatih model regresi linear menggunakan dataset sederhana.
2. **Evaluasi Kinerja:** Metrik seperti MSE dan R^2-score memberikan informasi seberapa baik model memprediksi data.
3. **Visualisasi:** Garis regresi menunjukkan hubungan linear antara waktu belajar dan nilai.
