# Challenge Day 9

## 📝 Topik
**Visualisasi Lanjutan dengan Seaborn**

---

## 🎯 Learning Objectives
1. Memahami dasar-dasar penggunaan library `Seaborn` untuk visualisasi data.
2. Membuat visualisasi `heatmap` untuk merepresentasikan korelasi antar data.
3. Membuat `pairplot` untuk melihat hubungan antar variabel dalam dataset.
4. Menggunakan parameter tambahan untuk memperindah visualisasi dengan Seaborn.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Seaborn adalah library Python yang dirancang untuk mempermudah visualisasi data statistik. Dibangun di atas Matplotlib, Seaborn menyediakan antarmuka tingkat tinggi untuk membuat grafik yang menarik secara visual. Dalam analisis data, heatmap dan pairplot adalah alat penting untuk memahami hubungan antar variabel dalam dataset.
- **Heatmap** digunakan untuk memvisualisasikan data matriks, seperti matriks korelasi.
- **Pairplot** adalah alat yang sangat baik untuk mengeksplorasi hubungan antar variabel numerik dalam dataset.
Dengan Seaborn, visualisasi data menjadi lebih intuitif dan estetis, membantu interpretasi data secara efektif.

---
## 🚀 Langkah-Langkah

### Install Library Matplotlib
```bash
pip install seaborn matplotlib pandas
```

### Import Library Matplotlib
```bash
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
```

### Unggah Dataset Iris
```python
df = sns.load_dataset("iris")
df
```
Output:
```bash 
   sepal.length  sepal.width  petal.length  petal.width variety
0           5.1          3.5           1.4          0.2  Setosa
1           4.9          3.0           1.4          0.2  Setosa
2           4.7          3.2           1.3          0.2  Setosa
3           4.6          3.1           1.5          0.2  Setosa
4           5.0          3.6           1.4          0.2  Setosa
```

### 1. Membuat heatmap untuk melihat korelasi antar data
`df.corr()` menghitung korelasi antar kolom dalam dataset.
`sns.heatmap()` digunakan untuk memvisualisasikan korelasi tersebut dalam bentuk heatmap, dengan parameter tambahan seperti `annot=True` untuk menampilkan nilai korelasi, `cmap` untuk memilih skema warna, dan `fmt=".2f"` untuk format angka dengan dua tempat desimal.

#### Menghitung korelasi antar kolom dalam dataset 
```python
correlation_matrix = df.corr()
```
#### Visualisasi heatmap 
```python
plt.figure(figsize=(8, 6)) 
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm", fmt=".2f", linewidths=0.5)
plt.title("Heatmap Korelasi Antar Data") 
plt.show()
```
Output:
<img src=”x” width=”500”>

### 2. Membuat pairplot untuk melihat hubungan antar variabel
`sns.pairplot()` membuat plot pairwise untuk semua variabel numerik dalam dataset.
Parameter `hue="species"` digunakan untuk memberi warna berdasarkan kolom `species`, dan `palette="Set1"` memilih palet warna.
`markers` digunakan untuk mengubah bentuk titik pada plot, dan `plot_kws={'alpha': 0.7}` untuk menambahkan transparansi pada plot.
```python
sns.pairplot(df, hue="species", palette="Set1") 
plt.title("Pairplot Hubungan Antar Variabel")
plt.show()
```
Output:
<img src=”x” width=”500”>

### 3. Menambahkan parameter untuk memperindah visualisasi
Kedua visualisasi berikut menggunakan berbagai parameter tambahan seperti `figsize`, `markers`, `cmap`, dan `linewidths` untuk memperindah tampilan.
#### Pairplot dengan lebih banyak pengaturan estetika
```python
sns.pairplot(df, hue="species", palette="Set2", markers=["o", "s", "D"], plot_kws={'alpha': 0.7})
plt.suptitle("Pairplot yang Ditingkatkan", y=1.02)
plt.show()
```
Output:
<img src=”x” width=”500”>

#### Heatmap dengan gaya lebih estetis
```python
plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap="YlGnBu", fmt=".2f", linewidths=0.8, cbar_kws={"shrink": 0.8})
plt.title("Heatmap Estetis Korelasi Antar Data")
plt.show()
```
Output:
<img src=”x” width=”500”>
