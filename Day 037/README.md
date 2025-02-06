# Challenge Day 37

## 📝 Topik
**Hyperparameter Tuning**

Optimasi Model dengan Grid Search untuk Hyperparameter Tuning

---

## 🎯 Learning Objectives
1. Memahami pentingnya hyperparameter tuning dalam meningkatkan performa model machine learning.
2. Menjelaskan perbedaan antara hyperparameter dan parameter model.
3. Mempelajari cara menggunakan Grid Search untuk mencari kombinasi hyperparameter terbaik.
4. Menerapkan GridSearchCV pada Random Forest Classifier untuk meningkatkan akurasi model.
5. Membandingkan kinerja model sebelum dan sesudah tuning.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Hyperparameter adalah nilai yang **tidak dipelajari langsung oleh model** tetapi **ditentukan sebelum training** untuk mengontrol proses pembelajaran. Contoh hyperparameter pada Random Forest adalah:

- `n_estimators`: Jumlah pohon dalam hutan
- `max_depth`: Kedalaman maksimum pohon
- `min_samples_split`: Jumlah minimum sampel untuk membagi node
- `min_samples_leaf`: Jumlah minimum sampel di setiap leaf

**Mengapa perlu tuning hyperparameter?**
Pemilihan hyperparameter yang tepat dapat meningkatkan akurasi dan generalisasi model, sehingga model bekerja lebih baik pada data baru.

---
## 🚀 Langkah-Langkah

### Import Library dan Persiapan Dataset
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split, GridSearchCV
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
- Isi missing values pada kolom 'age' dengan median
- Hapus kolom yang tidak relevan
- Ubah data kategorikal menjadi numerik
- Pilih fitur dan target
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

### Training Model Random Forest Classifier (Baseline Model)
Sebelum melakukan hyperparameter tuning, kita akan melatih model dengan default parameters dan melihat performanya.
```python
rf_baseline = RandomForestClassifier(random_state=42)

rf_baseline.fit(X_train, y_train)

y_pred_baseline = rf_baseline.predict(X_test)

accuracy_baseline = accuracy_score(y_test, y_pred_baseline)
print(f"Akurasi Model Default: {accuracy_baseline:.2f}")
```
Output:
```bash
Akurasi Model Default: 0.80
```

### Hyperparameter Tuning dengan Grid Search
Grid Search akan mencari kombinasi terbaik dari beberapa nilai hyperparameter yang kita tentukan.
```python
param_grid = {
    'n_estimators': [50, 100, 150],  # Jumlah pohon
    'max_depth': [10, 20, None],     # Kedalaman pohon
    'min_samples_split': [2, 5, 10], # Minimum sampel untuk split
    'min_samples_leaf': [1, 2, 4]    # Minimum sampel di leaf node
}

rf_model = RandomForestClassifier(random_state=42)

grid_search = GridSearchCV(rf_model, param_grid, cv=5, scoring='accuracy', n_jobs=-1, verbose=1)

grid_search.fit(X_train, y_train)

print("Hyperparameter Terbaik:", grid_search.best_params_)
```
Output:
```bash
Fitting 5 folds for each of 81 candidates, totalling 405 fits
```

### Evaluasi Model dengan Hyperparameter Optimal
Setelah mendapatkan kombinasi hyperparameter terbaik, kita akan melatih ulang model dan mengevaluasi performanya.
```python
best_rf = grid_search.best_estimator_

y_pred_best = best_rf.predict(X_test)

accuracy_best = accuracy_score(y_test, y_pred_best)
print(f"Akurasi Model Setelah Tuning: {accuracy_best:.2f}")

print("\nClassification Report Setelah Tuning:")
print(classification_report(y_test, y_pred_best))

plt.figure(figsize=(5, 4))
sns.heatmap(confusion_matrix(y_test, y_pred_best), annot=True, cmap="Blues", fmt="d", xticklabels=["Tidak Selamat", "Selamat"], yticklabels=["Tidak Selamat", "Selamat"])
plt.xlabel("Prediksi")
plt.ylabel("Aktual")
plt.title("Confusion Matrix Setelah Tuning")
plt.savefig('Day_037_01.png', format='png', dpi=300)
plt.show()
```
Output:
```bash
Akurasi Model Setelah Tuning: 0.80

Classification Report Setelah Tuning:
              	precision    	recall  	f1-score	support

                 0    	0.80      	0.90 	0.84       	105
                 1    	0.82      	0.68   	0.74        	74

      accuracy  				0.80       	179
    macro avg 	0.81      	0.79  	0.79       	179
weighted avg 	0.81      	0.80   	0.80       	179
```
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20037/Day_037_01.png" width=”500”>

### Challenge
- Coba gunakan RandomizedSearchCV untuk mempercepat tuning hyperparameter.
- Bandingkan performa Random Forest dengan model lain seperti Logistic Regression atau SVM setelah tuning.

### Kesimpulan 
- Hyperparameter tuning sangat penting untuk meningkatkan performa model.
- Grid Search membantu menemukan kombinasi hyperparameter terbaik secara otomatis.
- Model yang sudah dioptimalkan menghasilkan akurasi lebih tinggi dibanding model default.
- Evaluasi model setelah tuning menunjukkan peningkatan akurasi dan klasifikasi yang lebih baik.
- Proses tuning memerlukan waktu lebih lama, tetapi hasilnya lebih optimal untuk prediksi.
