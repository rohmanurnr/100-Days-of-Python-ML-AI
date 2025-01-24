  # Challenge Day 24

## 📝 Topik
**Visualisasi Hasil Model**

Membuat visualisasi untuk membandingkan prediksi model dengan data asli menggunakan scatter plot.

---

## 🎯 Learning Objectives
1. Memahami pentingnya visualisasi dalam mengevaluasi model regresi.
2. Membuat scatter plot untuk membandingkan prediksi dengan nilai asli.
3. Menginterpretasikan pola dari visualisasi untuk menilai kinerja model.
4. Menggunakan visualisasi untuk mengidentifikasi area di mana model dapat diperbaiki.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Visualisasi hasil model adalah langkah penting dalam memahami kinerja model. Scatter plot digunakan untuk membandingkan nilai prediksi model dengan nilai asli (ground truth). Pola ideal menunjukkan data menyebar di sekitar garis diagonal (y = x), yang menunjukkan prediksi mendekati nilai asli.

Mengapa ini penting?

- Scatter plot memudahkan identifikasi bias atau kesalahan sistematik.
- Memahami penyebaran data membantu mengevaluasi akurasi model secara visual.

---
## 🚀 Langkah-Langkah

### Persiapan Dataset dan Model
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
import matplotlib.pyplot as plt

data = {
    "Waktu Belajar (Jam)": [1, 2, 3, 4, 5, 6, 7, 8],
    "Nilai": [50, 55, 60, 65, 70, 75, 80, 85]
}
df = pd.DataFrame(data)

X = df[["Waktu Belajar (Jam)"]]
y = df["Nilai"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

### Scatter Plot: Prediksi vs Nilai Asli
```python
plt.figure(figsize=(8, 6))
plt.scatter(y_test, y_pred, color='blue', label='Prediksi vs Nilai Asli')
plt.plot([min(y_test), max(y_test)], [min(y_test), max(y_test)], color='red', linestyle='--', label='Garis Referensi (y=x)')

plt.title("Visualisasi Hasil Model: Prediksi vs Nilai Asli")
plt.xlabel("Nilai Asli")
plt.ylabel("Nilai Prediksi")
plt.legend()
plt.grid()
plt.savefig('24_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20024/24_01.png" width=”500”>

### Analisis Visualisasi
- **Garis Referensi (y = x):** Prediksi ideal ada di garis ini.
- **Pola Penyebaran:** Jika data tersebar jauh dari garis, model mungkin memiliki bias atau kesalahan yang perlu diperbaiki.

### Kesimpulan 
1. Scatter plot membantu Anda mengevaluasi kinerja model secara visual.
2. Pola penyebaran data memberikan wawasan tentang area di mana model bekerja dengan baik atau perlu diperbaiki.
3. Langkah berikutnya adalah meningkatkan model jika visualisasi menunjukkan ketidaksesuaian yang signifikan.
