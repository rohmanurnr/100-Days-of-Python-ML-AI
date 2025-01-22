# Challenge Day 23

## 📝 Topik
**Evaluasi Model**

Mengukur performa model regresi menggunakan metrik evaluasi seperti Mean Squared Error (MSE), Root Mean Squared Error (RMSE), dan R^2-score.

---

## 🎯 Learning Objectives
1. Memahami pentingnya evaluasi model dalam regresi.
2. Menggunakan MSE, RMSE, dan R^2-score untuk mengevaluasi kinerja model.
3. Menganalisis hasil evaluasi untuk mengidentifikasi kelebihan dan kekurangan model.
4. Meningkatkan wawasan dalam interpretasi hasil evaluasi untuk perbaikan model.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Evaluasi model adalah langkah penting dalam machine learning untuk menentukan seberapa baik model memprediksi data baru. Dalam regresi, metrik seperti Mean Squared Error (MSE), Root Mean Squared Error (RMSE), dan R^2-score digunakan untuk menilai performa model.
Mengapa ini penting?

- **MSE** mengukur rata-rata kesalahan kuadrat antara prediksi dan data sebenarnya, memberikan penalti lebih besar pada kesalahan besar.
- **RMSE** memberikan skala kesalahan yang sama dengan data asli, memudahkan interpretasi.
- **R^2-score** mengukur seberapa baik model menjelaskan variabilitas data target.

—

## 🚀 Langkah-Langkah

### Persiapan Dataset
```python
import pandas as pd
from sklearn.model_selection import train_test_split

data = {
    "Waktu Belajar (Jam)": [1, 2, 3, 4, 5, 6, 7, 8],
    "Nilai": [50, 55, 60, 65, 70, 75, 80, 85]}
df = pd.DataFrame(data)

X = df[["Waktu Belajar (Jam)"]]
y = df["Nilai"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### Melatih Model Regresi
```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

### Evaluasi Model
- Hitung MSE, RMSE, dan R^2-score.
- Analisis hasil dan pahami apa yang dapat ditingkatkan.
```python
from sklearn.metrics import mean_squared_error, r2_score
import numpy as np

mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, y_pred)

print("Mean Squared Error (MSE):", mse)
print("Root Mean Squared Error (RMSE):", rmse)
print("R-squared (R^2):", r2)
```
Output:
```bash
Mean Squared Error (MSE): 0.0
Root Mean Squared Error (RMSE): 0.0
R-squared (R^2): 1.0
```

### Visualisasi Hasil
Visualisasi data asli dan prediksi
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
plt.scatter(X, y, color='blue', label='Data Asli')  
plt.plot(X, model.predict(X), color='red', label='Garis Regresi') 
plt.title("Evaluasi Model: Waktu Belajar vs Nilai")
plt.xlabel("Waktu Belajar (Jam)")
plt.ylabel("Nilai")
plt.legend()
plt.grid()
plt.savefig('23_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20023/23_01.png" width=”500”>

### Kesimpulan 
1. **MSE:** Menunjukkan rata-rata kesalahan kuadrat model. Nilai lebih kecil menunjukkan model lebih baik.
2. **RMSE:** Interpretasi lebih mudah karena memiliki satuan yang sama dengan data asli.
3. **R^2-score:** Semakin mendekati 1, semakin baik model menjelaskan variabilitas data.

Evaluasi ini membantu Anda memahami kekuatan dan kelemahan model regresi linear.
