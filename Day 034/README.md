# Challenge Day 34

## 📝 Topik
**Evaluasi Model Klasifikasi**

Menganalisis performa model klasifikasi menggunakan metrik akurasi, precision, recall, dan F1-score.

---

## 🎯 Learning Objectives
1. Memahami pentingnya evaluasi model klasifikasi menggunakan berbagai metrik.
2. Menggunakan scikit-learn untuk menghitung akurasi, precision, recall, dan F1-score.
3. Menginterpretasikan hasil evaluasi untuk memahami kelebihan dan kekurangan model.
4. Menggunakan confusion matrix untuk analisis lebih lanjut.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Dalam machine learning, akurasi saja tidak cukup untuk mengevaluasi model klasifikasi, terutama jika data tidak seimbang. Oleh karena itu, kita perlu menggunakan metrik tambahan seperti precision, recall, dan F1-score.

#### Akurasi (Accuracy) 
**Seberapa sering model benar?**

Akurasi adalah persentase prediksi yang benar dibandingkan dengan total data.
Formula:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20034/Day_034_02.png" width=”500”>

- Cocok digunakan jika dataset seimbang (jumlah kelas hampir sama).
- Kurang baik jika dataset tidak seimbang (misalnya, jika ada 95% data kelas A dan 5% data kelas B, model bisa dapat 95% akurasi hanya dengan selalu memprediksi kelas A!).

#### Precision 
**Seberapa akurat model saat memprediksi kelas positif?**

Precision menunjukkan dari semua yang diprediksi sebagai kelas positif, berapa yang benar-benar positif.

Formula:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20034/Day_034_03.png" width=”500”>

- Penting jika false positive berbahaya (contoh: tes penyakit serius, lebih baik model hanya memprediksi positif jika yakin).
- Tidak terlalu peduli dengan false negative (melesetnya prediksi positif yang seharusnya benar).

#### Recall 
**Seberapa banyak kelas positif yang berhasil ditemukan model?**

Recall menunjukkan berapa banyak dari semua kasus positif yang berhasil dideteksi oleh model.
Formula:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20034/Day_034_04.png" width=”500”>

- Penting jika false negative berbahaya (contoh: mendeteksi kanker, lebih baik mendeteksi semua kasus meskipun ada false positive).
- Bisa tinggi tetapi mengorbankan precision (misalnya, jika model selalu memprediksi positif, recall 100% tetapi precision rendah).

#### F1-Score 
**Keseimbangan antara Precision dan Recall**

Karena precision dan recall sering bertolak belakang, kita bisa menggunakan F1-score, yang merupakan rata-rata harmonik precision dan recall.
Formula:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20034/Day_034_05.png" width="250">

- Cocok jika kita butuh keseimbangan antara precision dan recall.
- Baik digunakan jika dataset tidak seimbang.

---
## 🚀 Langkah-Langkah

### Import Library
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, confusion_matrix, classification_report
```

### Persipaan Dataset dan Model
```python
data = {
    "Feature 1": [2, 3, 10, 19, 25, 30, 45, 50, 60, 75],
    "Feature 2": [5, 7, 12, 22, 30, 35, 40, 55, 65, 80],
    "Label": [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]  # Label biner (0 dan 1)
}

df = pd.DataFrame(data)

X = df[["Feature 1", "Feature 2"]]
y = df["Label"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = DecisionTreeClassifier(criterion="gini", max_depth=3, random_state=42)
model.fit(X_train, y_train)
```
Output:
```bash
DecisionTreeClassifier(max_depth=3, random_state=42)
```

### Evaluasi Model dengan Metrik Klasifikasi
```python
y_pred = model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)

print(f"Akurasi: {accuracy:.2f}")
print(f"Precision: {precision:.2f}")
print(f"Recall: {recall:.2f}")
print(f"F1-Score: {f1:.2f}")

print("\nLaporan Klasifikasi:\n", classification_report(y_test, y_pred))

```
Output:
```bash
Akurasi: 1.00
Precision: 1.00
Recall: 1.00
F1-Score: 1.00

Laporan Klasifikasi:
               precision    recall  f1-score   support

           0       1.00      1.00      1.00         1
           1       1.00      1.00      1.00         1

    accuracy                           1.00         2
   macro avg       1.00      1.00      1.00         2
weighted avg       1.00      1.00      1.00         2
```

### Visualisasi Confusion Matrix
```python
cm = confusion_matrix(y_test, y_pred)

plt.figure(figsize=(5, 4))
sns.heatmap(cm, annot=True, fmt="d", cmap="Blues", xticklabels=["Class 0", "Class 1"], yticklabels=["Class 0", "Class 1"])
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix")
plt.savefig('Day_034_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20034/Day_034_01.png" width=”500”>


### Challenge
1. Coba dataset tidak seimbang

- Buat dataset dengan jumlah kelas yang tidak seimbang dan lihat bagaimana precision, recall, dan F1-score berubah.

2. Eksperimen dengan model lain

- Bandingkan Decision Tree dengan model lain seperti Logistic Regression atau Random Forest untuk melihat perbedaan performa.

### Kesimpulan 
- Evaluasi model tidak hanya melihat akurasi, tetapi juga precision, recall, dan F1-score untuk memahami kekuatan dan kelemahan model.
- Confusion matrix membantu menganalisis kesalahan klasifikasi, sehingga kita bisa melihat bagaimana model menangani data.
- Setiap metrik memiliki kegunaannya sendiri, tergantung pada masalah yang dihadapi. Precision lebih penting dalam kasus false positive yang mahal, sedangkan recall lebih penting jika false negative harus dikurangi.
