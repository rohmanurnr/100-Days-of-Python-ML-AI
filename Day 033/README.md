# Challenge Day 33

## 📝 Topik
**Decision Tree Classifier (Praktik)**

Membangun model Decision Tree Classifier untuk menyelesaikan masalah klasifikasi sederhana.

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Decision Tree Classifier dan bagaimana algoritma ini bekerja dalam klasifikasi.
2. Menggunakan pustaka scikit-learn untuk membangun model Decision Tree Classifier.
3. Melatih dan mengevaluasi model klasifikasi menggunakan dataset sederhana.
4. Memvisualisasikan Decision Tree untuk memahami bagaimana model membuat keputusan.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Decision Tree adalah salah satu algoritma machine learning berbasis pohon keputusan yang digunakan untuk klasifikasi dan regresi. Algoritma ini bekerja dengan memecah data berdasarkan fitur tertentu hingga mencapai keputusan akhir.

---
## 🚀 Langkah-Langkah

### Import Library
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.metrics import accuracy_score, classification_report
```

### Persiapan Dataset
```python
data = {
    "Feature 1": [2, 3, 10, 19, 25, 30, 45, 50, 60, 75],
    "Feature 2": [5, 7, 12, 22, 30, 35, 40, 55, 65, 80],
    "Label": [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]  # Label biner (0 dan 1)
}

df = pd.DataFrame(data)
df.head()
```
Output:
```bash
Feature 1	Feature 2	Label
0	2	5	0
1	3	7	0
2	10	12	0
3	19	22	0
4	25	30	1
```

### Pisahkan Data menjadi Train dan Test Set
```python
X = df[["Feature 1", "Feature 2"]]
y = df["Label"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### Bangun Model Decision Tree Classifier
```python
model = DecisionTreeClassifier(criterion="gini", max_depth=3, random_state=42)

model.fit(X_train, y_train)
```
Output:
```bash
DecisionTreeClassifier(max_depth=3, random_state=42)
```

### Evaluasi Model
```python
y_pred = model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
print(f"Akurasi Model: {accuracy:.2f}")

print("Laporan Klasifikasi:\n", classification_report(y_test, y_pred))
```
Output:
```bash
Akurasi Model: 1.00
Laporan Klasifikasi:
               precision    recall  f1-score   support

           0       1.00      1.00      1.00         1
           1       1.00      1.00      1.00         1

    accuracy                           1.00         2
   macro avg       1.00      1.00      1.00         2
weighted avg       1.00      1.00      1.00         2
```

### Visualisasi Pohon Keputusan
```python
plt.figure(figsize=(10, 6))
plot_tree(model, feature_names=["Feature 1", "Feature 2"], class_names=["Class 0", "Class 1"], filled=True)
plt.savefig('Day_033_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20033/Day_033_01.png" width=”500”>

### Challenge
1. Ubah parameter Decision Tree

- Coba ubah parameter seperti `max_depth`, `criterion`, atau `min_samples_split` untuk melihat bagaimana model berubah.

2. Coba dengan dataset lain

- Gunakan dataset lain dari `sklearn.datasets` seperti `Iris` atau `Breast Cancer` untuk membangun model Decision Tree.

### Kesimpulan 
- Membangun Model: Kita membuat Decision Tree Classifier menggunakan scikit-learn untuk klasifikasi sederhana.
- Melatih & Mengevaluasi: Model dilatih dengan train-test split, lalu dievaluasi dengan akurasi dan classification report.
-  Visualisasi: Decision tree divisualisasikan untuk melihat bagaimana model mengambil keputusan berdasarkan fitur.
- Eksperimen: Model bisa ditingkatkan dengan mengubah parameter atau mencoba dataset lain.
