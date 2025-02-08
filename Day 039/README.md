# Challenge Day 39

## 📝 Topik
**Support Vector Machine (SVM) (Praktik)**

Implementasi SVM untuk Klasifikasi Dataset Sederhana

---

## 🎯 Learning Objectives
1. Menerapkan Support Vector Machine (SVM) untuk klasifikasi dataset.
2. Memahami cara menggunakan kernel linear, polynomial, dan RBF dalam SVM.
3. Menggunakan train-test split untuk evaluasi model.
4. Mengukur performa model menggunakan akurasi, confusion matrix, dan classification report.
5. Memvisualisasikan hasil klasifikasi dengan decision boundary.

---

## 🏆 Aktivitas/Tantangan

### Agenda
- Melatih model SVM dengan dataset sederhana.
- Menguji berbagai jenis kernel (linear, polynomial, dan RBF).
- Mengevaluasi performa model menggunakan metrik evaluasi.
- Visualisasi decision boundary untuk memahami bagaimana SVM memisahkan data.

---
## 🚀 Langkah-Langkah

### Import Library dan Persiapan Dataset
Kita akan menggunakan dataset `make_classification()` dari `sklearn.datasets`.
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

X, y = make_classification(n_samples=200, n_features=2, n_informative=2, n_redundant=0, n_repeated=0, n_classes=2, n_clusters_per_class=1, random_state=42)

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm', edgecolors='k')
plt.xlabel("Fitur 1")
plt.ylabel("Fitur 2")
plt.title("Dataset untuk Klasifikasi SVM")
plt.savefig('Day_039_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20039/Day_039_01.png" width=”500”>

### Melatih Model SVM dengan Kernel Linear
Melatih SVM dengan kernel linear dan mengevaluasi akurasinya
```python
svm_linear = SVC(kernel='linear')

svm_linear.fit(X_train, y_train)

y_pred_linear = svm_linear.predict(X_test)

print("Akurasi Model SVM (Linear):", accuracy_score(y_test, y_pred_linear))
print("\nClassification Report:\n", classification_report(y_test, y_pred_linear))
```
Output:
```bash

Akurasi Model SVM (Linear): 0.85

Classification Report:
               precision    recall  f1-score   support

           0       0.95      0.78      0.86        23
           1       0.76      0.94      0.84        17

    accuracy                           0.85        40
   macro avg       0.85      0.86      0.85        40
weighted avg       0.87      0.85      0.85        40
```

### Melatih Model SVM dengan Kernel RBF
Mencoba kernel RBF, yang lebih fleksibel untuk data non-linear
```python
svm_rbf = SVC(kernel='rbf')

svm_rbf.fit(X_train, y_train)

y_pred_rbf = svm_rbf.predict(X_test)

print("Akurasi Model SVM (RBF):", accuracy_score(y_test, y_pred_rbf))
print("\nClassification Report:\n", classification_report(y_test, y_pred_rbf))
```
Output:
```bash

Akurasi Model SVM (RBF): 0.875

Classification Report:
               precision    recall  f1-score   support

           0       0.95      0.83      0.88        23
           1       0.80      0.94      0.86        17

    accuracy                           0.88        40
   macro avg       0.88      0.88      0.87        40
weighted avg       0.89      0.88      0.88        40
```

### Membandingkan Kernel Linear vs RBF dengan Visualisasi Decision Boundary
Melihat bagaimana SVM dengan kernel linear dan RBF membagi data
```python
pip install mlxtend

from mlxtend.plotting import plot_decision_regions

plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plot_decision_regions(X, y, clf=svm_linear, legend=2)
plt.title("Decision Boundary - Kernel Linear")

plt.subplot(1, 2, 2)
plot_decision_regions(X, y, clf=svm_rbf, legend=2)
plt.title("Decision Boundary - Kernel RBF")
plt.savefig('Day_039_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20039/Day_039_02.png" width=”500”>

### Evaluasi Model dengan Confusion Matrix
Melihat confusion matrix untuk model dengan kernel linear dan RBF
```python
import seaborn as sns

plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
sns.heatmap(confusion_matrix(y_test, y_pred_linear), annot=True, fmt="d", cmap="Blues")
plt.title("Confusion Matrix - Kernel Linear")

plt.subplot(1, 2, 2)
sns.heatmap(confusion_matrix(y_test, y_pred_rbf), annot=True, fmt="d", cmap="Oranges")
plt.title("Confusion Matrix - Kernel RBF")
plt.savefig('Day_039_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20039/Day_039_03.png" width=”500”>

### Challenge

- Coba gunakan SVM dengan kernel polynomial dan sigmoid dan bandingkan hasilnya.
- Coba ubah parameter C dan gamma pada SVM RBF dan lihat bagaimana hasilnya berubah.
- Gunakan dataset lain, seperti Iris Dataset atau Breast Cancer Dataset, dan latih model SVM di sana.

### Kesimpulan 
- SVM dengan kernel linear cocok untuk data yang dapat dipisahkan dengan garis lurus.
- SVM dengan kernel RBF lebih fleksibel dan dapat menangani data yang tidak bisa dipisahkan secara linear.
- Decision boundary dari SVM menunjukkan bagaimana model membagi data menjadi dua kelas.
- Confusion matrix membantu dalam mengevaluasi kesalahan prediksi model.
