# Challenge Day 36

## 📝 Topik
**Random Forest Classifier**

Implementasi Random Forest pada Dataset Klasifikasi

---

## 🎯 Learning Objectives
1. Memahami cara menerapkan Random Forest Classifier pada dataset nyata.
2. Melakukan preprocessing data, termasuk menangani nilai yang hilang dan mengubah data kategori menjadi numerik.
3. Melatih Random Forest Classifier menggunakan scikit-learn.
4. Mengevaluasi performa model menggunakan akurasi, confusion matrix, dan classification report.
5. Mengeksplorasi feature importance untuk memahami faktor utama dalam prediksi.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Kita akan menggunakan dataset Titanic untuk membangun model Random Forest Classifier yang dapat memprediksi apakah seorang penumpang akan selamat atau tidak berdasarkan berbagai fitur seperti usia, jenis kelamin, dan kelas tiket.

Kita akan melakukan preprocessing, training model, evaluasi performa, dan analisis feature importance untuk memahami faktor yang paling berpengaruh dalam prediksi.

---
## 🚀 Langkah-Langkah

### Import Library dan Persiapan Dataset
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

df = sns.load_dataset("titanic")

df.head()
```
Output:
```bash
	survived	pclass	sex	age	sibsp	parch	fare	embarked	class	who	adult_male	deck	embark_town	alive	alone
0	0	3	male	22.0	1	0	7.2500	S	Third	man	True	NaN	Southampton	no	False
1	1	1	female	38.0	1	0	71.2833	C	First	woman	False	C	Cherbourg	yes	False
2	1	3	female	26.0	0	0	7.9250	S	Third	woman	False	NaN	Southampton	yes	True
3	1	1	female	35.0	1	0	53.1000	S	First	woman	False	C	Southampton	yes	False
4	0	3	male	35.0	0	0	8.0500	S	Third	man	True	NaN	Southampton	no	True
```

### Data Preprocessing
Kita perlu membersihkan dataset sebelum melatih model.

- Mengisi nilai yang hilang pada kolom age dengan median.
- Menghapus kolom yang tidak relevan.
- Mengubah data kategorikal menjadi numerik.
- Split dataset menjadi training (80%) dan testing (20%)

```python
df['age'].fillna(df['age'].median(), inplace=True)

df.drop(columns=['deck', 'embark_town'], inplace=True)

df['sex'] = df['sex'].map({'male': 0, 'female': 1})
df = pd.get_dummies(df, columns=['embarked'], drop_first=True)
df['class'] = df['class'].map({'First': 1, 'Second': 2, 'Third': 3})
df['who'] = df['who'].map({'man': 0, 'woman': 1, 'child': 2})
df['alive'] = df['alive'].map({'yes': 1, 'no': 0})

X = df[['pclass', 'sex', 'age', 'sibsp', 'parch', 'fare', 'embarked_Q', 'embarked_S']]
y = df['survived']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### Training Model Random Forest Classifier
Buat model Random Forest dengan 100 pohon
```python
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)

rf_model.fit(X_train, y_train)

y_pred = rf_model.predict(X_test)
```

### Evaluasi Model
Evaluasi model dengan akurasi, confusion matrix, dan classification report.
```python
accuracy = accuracy_score(y_test, y_pred)
print(f"Akurasi Model: {accuracy:.2f}")

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

plt.figure(figsize=(5, 4))
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, cmap="Blues", fmt="d", xticklabels=["Tidak Selamat", "Selamat"], yticklabels=["Tidak Selamat", "Selamat"])
plt.xlabel("Prediksi")
plt.ylabel("Aktual")
plt.title("Confusion Matrix")
plt.savefig('Day_036_01.png', format='png', dpi=300)
plt.show()
```
Output:
```bash
Akurasi Model: 0.80

Classification Report:
              precision    recall  f1-score   support

           0       0.82      0.84      0.83       105
           1       0.76      0.74      0.75        74

    accuracy                           0.80       179
   macro avg       0.79      0.79      0.79       179
weighted avg       0.80      0.80      0.80       179
```
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20036/Day_036_01.png" width=”500”>


### Analisis Feature Importance
Analisis fitur yang paling berpengaruh dalam prediksi
```python
feature_importances = pd.DataFrame({'Feature': X.columns, 'Importance': rf_model.feature_importances_})
feature_importances = feature_importances.sort_values(by='Importance', ascending=False)

plt.figure(figsize=(8, 5))
sns.barplot(x='Importance', y='Feature', data=feature_importances, palette='coolwarm')
plt.xlabel('Importance Score')
plt.ylabel('Feature')
plt.title('Feature Importance dalam Random Forest')
plt.savefig('Day_036_02.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20036/Day_036_02.png" width=”500”>

### Challenge
Coba tuning hyperparameter seperti n_estimators, max_depth, dan max_features untuk meningkatkan performa model!

### Kesimpulan 
- Random Forest Classifier dapat digunakan untuk klasifikasi dataset nyata, seperti Titanic.
- Preprocessing data sangat penting sebelum melatih model, termasuk menangani missing values dan encoding data kategorikal.
- Model dievaluasi menggunakan metrik akurasi, confusion matrix, dan classification report.
- Feature importance membantu kita memahami fitur yang paling berpengaruh dalam prediksi.
- Random Forest bekerja dengan membangun banyak pohon keputusan, yang membuat model lebih akurat dan tahan terhadap overfitting.
