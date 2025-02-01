# Challenge Day 32

## 📝 Topik
**Decision Tree Classifier (Teori)**

Pelajari konsep dasar Decision Tree, cara kerja splitting criteria seperti Gini dan Entropy, serta bagaimana algoritma ini digunakan dalam klasifikasi.

---

## 🎯 Learning Objectives
1. Memahami konsep dasar Decision Tree sebagai model klasifikasi.
2. Mempelajari bagaimana splitting criteria bekerja, seperti Gini Impurity dan Entropy.
3. Mengetahui bagaimana Decision Tree membangun pohon keputusan untuk mengklasifikasikan data.
4. Memahami cara Decision Tree mengoptimalkan pemisahan data untuk mencapai akurasi terbaik.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Decision Tree adalah algoritma Machine Learning yang digunakan untuk tugas klasifikasi dan regresi. Algoritma ini bekerja dengan cara membagi dataset menjadi cabang-cabang (nodes) berdasarkan fitur terbaik yang dapat memisahkan data. Setiap pembagian didasarkan pada kriteria pemisahan yang dikenal sebagai splitting criteria, yang paling umum adalah Gini Impurity dan Entropy.

- Gini Impurity digunakan untuk mengukur seberapa sering elemen yang dipilih secara acak dari dataset akan salah diklasifikasikan.
- Entropy adalah ukuran ketidakteraturan atau ketidakpastian dalam sistem, dan kita berusaha untuk mengurangi ketidakpastian ini melalui pembagian data.

Pohon keputusan dibuat dengan memilih fitur terbaik yang memisahkan data secara optimal berdasarkan kriteria ini. Model ini mudah dimengerti dan sangat kuat dalam berbagai jenis masalah klasifikasi.

#### Gini Impurity
**Gini Impurity** mengukur ketidakpastian dalam distribusi kelas suatu node. Nilai **Gini** yang lebih rendah menunjukkan node yang lebih "murni" (yaitu, sebagian besar data di dalam node memiliki kelas yang sama).

Rumus perhitungan Gini Impurity adalah:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20032/Day_032_02.png" width=”500”>

Dimana:
n adalah jumlah kelas dalam data (misalnya, 2 kelas untuk klasifikasi biner).
pi​ adalah proporsi dari kelas i dalam node Dataset.

**Contoh Perhitungan Gini Impurity:**
Misalkan kita memiliki dataset dengan dua kelas, **A** dan **B**. Dataset ini memiliki 10 elemen, 6 di antaranya adalah kelas **A** dan 4 adalah kelas **B**. Maka, perhitungan Gini Impurity untuk dataset ini adalah:
1. Hitung proporsi kelas A dan B:
- 𝑝A  = 6/10 = 0.6
- 𝑝𝐵 = 4/10 = 0.4
2. Hitung Gini Impurity:
Gini (D) = 1 - (0.6^2 + 0.4^2)
Gini (D) = 1 - (0.36 + 0.16) = 1 - 0.52 = 0.48
Jadi, **Gini Impurity** untuk dataset ini adalah **0.48**.

#### Entropy
Entropy mengukur tingkat ketidakpastian atau ketidakteraturan dalam distribusi kelas di dalam sebuah node. Nilai Entropy yang lebih rendah menunjukkan bahwa data di dalam node tersebut lebih teratur, yaitu lebih banyak data yang termasuk dalam satu kelas.

Rumus perhitungan Entropy adalah:

<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20032/Day_032_03.png" width=”500”>

Dimana:

- C adalah jumlah kelas.
- 𝑝𝑖 adalah proporsi dari kelas 𝑖 dalam dataset 

**Contoh Perhitungan Entropy:**
Misalkan kita memiliki dataset dengan dua kelas, **A** dan **B**, dan distribusinya adalah 6 elemen untuk kelas **A** dan 4 untuk kelas **B**.

1. Hitung proporsi kelas A dan B:
- 𝑝A  = 6/10 = 0.6
- 𝑝𝐵 = 4/10 = 0.4
2. Hitung Entropy:
Entropy(D) = -(0.6 log2 0.6 + 0.4 log2 0.4)

Hitung logaritmaL
log2 0.6 = -0.736
log2 0.4 = -1.322

Entropy(D) = -(0.6 x -0.736 + 0.4 x -1.322)
Entropy(D) = -(-0.4416 - 0.5288) = 0.9704

Jadi, **Entropy** untuk dataset ini adalah sekitar **0.97**.

---
## 🚀 Langkah-Langkah

### Persiapan Lingkungan
Pastikan kamu sudah menginstal Scikit-learn
```bash
pip install scikit-learn
```
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
```

### Persiapan Dataset
Kita akan memulai dengan menggunakan dataset Iris dari Scikit-learn, yang merupakan dataset klasik untuk klasifikasi bunga berdasarkan fitur panjang dan lebar kelopak dan daun.
```python
data = load_iris()
X = data.data  
y = data.target  

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

### Membuat model Decision Tree dengan kriteria Gini & Prediksi data uji
**criterion='gini'** menunjukkan bahwa kita menggunakan **Gini Impurity** sebagai kriteria pemisahan
```python
clf = DecisionTreeClassifier(criterion='gini', random_state=42)
clf.fit(X_train, y_train)

y_pred = clf.predict(X_test)
```

### Evaluasi model
```python
accuracy = accuracy_score(y_test, y_pred)
print(f"Akurasi Model Decision Tree (Gini): {accuracy * 100:.2f}%")
```
Output:
```bash
Akurasi Model Decision Tree (Gini): 100.00%
```

### Visualisasi Decision Tree
```python
from sklearn.tree import plot_tree

plt.figure(figsize=(12,8))
plot_tree(clf, filled=True, feature_names=data.feature_names, class_names=data.target_names, rounded=True, proportion=False, precision=2)
plt.title("Decision Tree - Gini Impurity")
plt.savefig('Day_032_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20032/Day_032_01.png" width=”500”>

### Membuat model Decision Tree dengan kriteria Entropy & Prediksi data uji
```python
clf_entropy = DecisionTreeClassifier(criterion='entropy', random_state=42)
clf_entropy.fit(X_train, y_train)

y_pred_entropy = clf_entropy.predict(X_test)
```

### Evaluasi model
```python
accuracy_entropy = accuracy_score(y_test, y_pred_entropy)
print(f"Akurasi Model Decision Tree (Entropy): {accuracy_entropy * 100:.2f}%")
```
Output:
```bash
Akurasi Model Decision Tree (Entropy): 97.78%
```

### Perbandingan Kinerja
Bandingkan akurasi antara Gini Impurity dan Entropy untuk melihat mana yang memberikan hasil terbaik.
```python
print(f"Akurasi dengan Gini: {accuracy * 100:.2f}%")
print(f"Akurasi dengan Entropy: {accuracy_entropy * 100:.2f}%")
```
Output:
```bash
Akurasi dengan Gini: 100.00%
Akurasi dengan Entropy: 97.78%
```

### Kesimpulan 
1. **Decision Tree** adalah algoritma yang sangat mudah dipahami, karena memberikan aturan keputusan yang jelas.
2. **Gini Impurity** dan **Entropy** digunakan untuk memilih fitur terbaik dalam setiap langkah pemisahan. Keduanya bertujuan untuk mengurangi ketidakpastian dan mencapai pemisahan yang terbaik.
3. **Gini Impurity** lebih cepat dihitung daripada **Entropy**, tetapi keduanya dapat memberikan hasil yang mirip dalam banyak kasus.
4. **Overfitting** adalah masalah yang umum terjadi dengan Decision Tree. Kamu bisa menggunakan teknik seperti **pruning** atau **penyempurnaan hyperparameter** untuk mengurangi overfitting.
