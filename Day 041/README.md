# Challenge Day 41

## 📝 Topik
**Logistic Regression**

Implementasi Logistic Regression untuk Klasifikasi Biner

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Logistic Regression dan bagaimana ia digunakan untuk klasifikasi.
2. Menjelaskan bagaimana fungsi sigmoid bekerja untuk mengubah output menjadi probabilitas.
3. Mengimplementasikan Logistic Regression menggunakan Scikit-Learn.
4. Mengevaluasi model menggunakan akurasi, confusion matrix, dan classification report.
5. Memvisualisasikan decision boundary untuk memahami bagaimana Logistic Regression bekerja.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Logistic Regression adalah algoritma klasifikasi yang digunakan untuk memprediksi label biner (0 atau 1) berdasarkan sekumpulan fitur.

**Konsep utama dalam Logistic Regression**:

- **Fungsi Sigmoid**: Mengubah hasil prediksi menjadi nilai probabilitas antara 0 dan 1.
- **Decision Boundary**: Garis pemisah yang menentukan apakah suatu titik diklasifikasikan sebagai 0 atau 1.
- **Cost Function (Log Loss)**: Digunakan untuk mengukur seberapa baik model membuat prediksi probabilitas.

**Rumus Fungsi Sigmoid**:
di mana z = wX + b, dengan:
- w sebagai bobot fitur
- X sebagai fitur input
- b sebagai bias


---
## 🚀 Langkah-Langkah

### Import Library dan Persiapan Dataset
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

X, y = make_classification(n_samples=200, n_features=2, n_informative=2, n_redundant=0, n_repeated=0, n_classes=2, n_clusters_per_class=1, random_state=42)

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm', edgecolors='k')
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.title("Dataset untuk Klasifikasi Logistic Regression")
plt.savefig('Day_041_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20041/Day_041_01.png" width=”500”>

### Melatih Model Logistic Regression
```python
log_reg = LogisticRegression()

log_reg.fit(X_train, y_train)

y_pred = log_reg.predict(X_test)

print("Akurasi Model Logistic Regression:", accuracy_score(y_test, y_pred))
print("\nClassification Report:\n", classification_report(y_test, y_pred))
```
Output:
```bash
Akurasi Model Logistic Regression: 0.875

Classification Report:
               precision    recall  f1-score   support

           0       1.00      0.78      0.88        23
           1       0.77      1.00      0.87        17

    accuracy                           0.88        40
   macro avg       0.89      0.89      0.87        40
weighted avg       0.90      0.88      0.88        40
```

### Visualisasi Fungsi Sigmoid
Fungsi sigmoid adalah dasar dari Logistic Regression
```python
def sigmoid(z):
    return 1 / (1 + np.exp(-z))

z_values = np.linspace(-10, 10, 100)
sigmoid_values = sigmoid(z_values)

plt.plot(z_values, sigmoid_values, color='b')
plt.axvline(0, linestyle="--", color="gray")
plt.axhline(0.5, linestyle="--", color="gray")
plt.xlabel("z (wX + b)")
plt.ylabel("Sigmoid Output")
plt.title("Fungsi Sigmoid dalam Logistic Regression")
plt.savefig('Day_041_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20041/Day_041_02.png" width=”500”>

### Visualisasi Decision Boundary Logistic Regression
Logistic Regression membagi data dengan decision boundary
```python
from mlxtend.plotting import plot_decision_regions

plt.figure(figsize=(6, 4))
plot_decision_regions(X, y, clf=log_reg, legend=2)
plt.title("Decision Boundary - Logistic Regression")
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.savefig('Day_041_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20041/Day_041_03.png" width=”500”>

### Evaluasi Model dengan Confusion Matrix
```python
plt.figure(figsize=(6, 4))
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, fmt="d", cmap="Blues")
plt.xlabel("Prediksi")
plt.ylabel("Aktual")
plt.title("Confusion Matrix - Logistic Regression")
plt.savefig('Day_041_04.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20041/Day_041_04.png" width=”500”>

### Challenge
- Coba gunakan dataset nyata seperti Iris Dataset atau Titanic Dataset.
- Coba ubah regularisasi model dengan penalty='l1' atau penalty='l2'.
- Bandingkan Logistic Regression dengan KNN atau SVM dalam klasifikasi dataset yang sama.

### Kesimpulan 
- Logistic Regression adalah algoritma klasifikasi biner yang menggunakan fungsi sigmoid.
- Fungsi sigmoid mengubah output menjadi probabilitas antara 0 dan 1.
- Decision boundary menentukan pemisahan antara dua kelas dalam Logistic Regression.
- Model dievaluasi dengan akurasi, classification report, dan confusion matrix.
- Logistic Regression cocok untuk dataset sederhana dengan hubungan linear antar fitur.
