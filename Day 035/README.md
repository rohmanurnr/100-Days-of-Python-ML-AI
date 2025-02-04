# Challenge Day 35

## 📝 Topik
**Random Forest & Ensemble Learning**

Algoritma Random Forest merupakan salah satu model machine learning berbasis ensemble learning, yang menggabungkan banyak decision tree untuk meningkatkan akurasi dan mengurangi overfitting.

---

## 🎯 Learning Objectives
1. Memahami konsep Ensemble Learning dan bagaimana meningkatkan performa model dengan teknik ini.
2. Menjelaskan prinsip dasar Random Forest, kelebihannya dibanding Decision Tree, dan bagaimana cara kerjanya.
3. Mempelajari hyperparameter penting dalam Random Forest.
4. Mengimplementasikan Random Forest Classifier menggunakan `scikit-learn`.
5. Mengevaluasi model dengan akurasi, confusion matrix, dan feature importance.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Random Forest adalah algoritma supervised learning yang digunakan untuk klasifikasi maupun regresi. Ini bekerja dengan membangun banyak decision tree dari subset data yang berbeda dan kemudian menggabungkan hasilnya melalui voting (untuk klasifikasi) atau rata-rata (untuk regresi).

Keunggulan utama dari Random Forest:

- Mengurangi overfitting dibanding Decision Tree.
- Lebih stabil terhadap data baru.
- Dapat menangani data dengan fitur yang banyak.
- Memberikan ranking fitur (Feature Importance) untuk interpretasi model.

---
## 🚀 Langkah-Langkah

### Import Library
```python
import numpy as np  
import pandas as pd  
import matplotlib.pyplot as plt  
import seaborn as sns  

from sklearn.model_selection import train_test_split  
from sklearn.ensemble import RandomForestClassifier  
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report  

from sklearn.tree import plot_tree  
```

### Persiapan dan Eksplorasi Dataset
```python
from sklearn.datasets import load_iris  

iris = load_iris()  
df = pd.DataFrame(iris.data, columns=iris.feature_names)  
df['target'] = iris.target  

df.head()
```
Output:
```bash
	sepal length (cm)	sepal width (cm)	petal length (cm)	petal width (cm)	target
0	5.1	3.5	1.4	0.2	0
1	4.9	3.0	1.4	0.2	0
2	4.7	3.2	1.3	0.2	0
3	4.6	3.1	1.5	0.2	0
4	5.0	3.6	1.4	0.2	0
```

### Split Data untuk Training dan Testing
```python
X = df.drop(columns=['target'])  
y = df['target']  

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)  
```

### Membangun Model Random Forest
```python
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)  

rf_model.fit(X_train, y_train)  
```
Output:
```bash
RandomForestClassifier(random_state=42)
```

### Evaluasi Model
```python
y_pred = rf_model.predict(X_test)  

accuracy = accuracy_score(y_test, y_pred)  
print(f"Akurasi Model: {accuracy:.2f}")  

cm = confusion_matrix(y_test, y_pred)  
sns.heatmap(cm, annot=True, cmap="Blues", fmt='d')  
plt.xlabel("Prediksi")  
plt.ylabel("Aktual")  
plt.title("Confusion Matrix")  
plt.savefig('Day_035_01.png', format='png', dpi=300)
plt.show()
```
Output:
```bash
Akurasi Model: 1.00
```
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20035/Day_035_01.png" width=”500”>

### Interpretasi Model - Feature Importance
```python
feature_importances = rf_model.feature_importances_  

feature_df = pd.DataFrame({"Fitur": X.columns, "Importance": feature_importances})  
feature_df = feature_df.sort_values(by="Importance", ascending=False)  

plt.figure(figsize=(8,5))  
sns.barplot(x="Importance", y="Fitur", data=feature_df, palette="viridis")  
plt.title("Feature Importance dari Random Forest")  
plt.savefig('Day_035_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20035/Day_035_02.png" width=”500”>

### Visualisasi Salah Satu Pohon dalam Random Forest
```python
plt.figure(figsize=(20,10))  
plot_tree(rf_model.estimators_[0], feature_names=X.columns, class_names=iris.target_names, filled=True)  
plt.savefig('Day_035_03.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20035/Day_035_03.png" width=”500”>

### Challenge
1. Ubah jumlah `n_estimators` dan lihat bagaimana itu mempengaruhi akurasi model.
2. Gunakan dataset lain (contoh: Titanic, Wine Dataset) untuk mengimplementasikan Random Forest.
3. Bandingkan hasilnya dengan Decision Tree – apakah Random Forest memiliki akurasi lebih baik?

### Kesimpulan 
1. Random Forest adalah algoritma berbasis ensemble learning yang menggabungkan banyak decision tree untuk meningkatkan akurasi dan mengurangi overfitting.
2. Dibandingkan dengan Decision Tree, Random Forest lebih stabil terhadap perubahan data dan memiliki generalizability lebih baik.
3. Hyperparameter penting dalam Random Forest termasuk n_estimators (jumlah pohon), max_depth (kedalaman maksimum), dan max_features (jumlah fitur yang dipilih di setiap split).
4. Random Forest juga memberikan informasi mengenai Feature Importance, membantu dalam feature selection untuk model yang lebih efisien.
5. Evaluasi model dilakukan dengan metrik seperti akurasi, confusion matrix, dan classification report, yang menunjukkan seberapa baik model dalam melakukan prediksi.
6. Semakin banyak pohon dalam Random Forest, semakin stabil modelnya, tetapi juga membutuhkan lebih banyak komputasi.
7. Random Forest bisa digunakan untuk klasifikasi dan regresi, menjadikannya salah satu algoritma yang serbaguna dalam machine learning.
