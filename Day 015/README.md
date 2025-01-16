# Challenge Day 15

## 📝 Topik
**Korelasi Antar Fitur: Memahami korelasi antar fitur dalam dataset menggunakan heatmap**

---

## 🎯 Learning Objectives
1. Memahami konsep korelasi sebagai ukuran hubungan antara dua variabel.
2. Menggunakan metode statistik untuk menghitung korelasi antar fitur dalam dataset.
3. Membuat visualisasi heatmap korelasi menggunakan Seaborn untuk memahami hubungan antar fitur.
4. Menginterpretasikan heatmap untuk mengidentifikasi fitur yang saling berhubungan atau tidak terkait.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Korelasi adalah ukuran statistik yang menunjukkan sejauh mana dua variabel saling berhubungan. Nilai korelasi berkisar dari -1 hingga 1:

- +1: Hubungan positif sempurna (satu variabel naik, yang lain juga naik).
- 0: Tidak ada hubungan.
- -1: Hubungan negatif sempurna (satu variabel naik, yang lain turun).

Visualisasi korelasi menggunakan heatmap memudahkan kita untuk mengidentifikasi pola hubungan antara fitur dalam dataset. Hal ini sangat berguna untuk analisis data dan seleksi fitur sebelum membangun model prediktif.

---
## 🚀 Langkah-Langkah

### Persiapan Data
Gunakan dataset sederhana yang memiliki beberapa fitur numerik
```python
import pandas as pd
import numpy as np

np.random.seed(42)
data = {
    'Waktu Belajar (Jam)': np.random.randint(1, 10, 100),
    'Nilai': np.random.randint(50, 100, 100),
    'Kehadiran (%)': np.random.randint(75, 100, 100),
    'Latihan Soal (Jam)': np.random.randint(0, 5, 100)
}

df = pd.DataFrame(data)
print("Dataset:")
print(df.head())
```
Output:
```bash
Dataset:
   Waktu Belajar (Jam)   Nilai    Kehadiran (%)       Latihan Soal (Jam)
0          7               84           80                    2
1          4               86           98                    2
2          8               96           79                    4
3          5               63           94                    2
4          7               52           76                    2
```

### Hitung Korelasi
Gunakan fungsi `.corr()` dari Pandas untuk menghitung matriks korelasi antar fitur
```python
correlation_matrix = df.corr()
print("\nMatriks Korelasi:")
print(correlation_matrix)
```
Output:
```bash
Matriks Korelasi:
                          Waktu Belajar (Jam)               Nilai  
Waktu Belajar (Jam)             1.000000                 -0.009954      
Nilai                          -0.009954                  1.000000      
Kehadiran (%)                  -0.009696                 -0.137514         
Latihan Soal (Jam)             0.085673                  -0.090468        

                             Kehadiran (%)            Latihan Soal (Jam)  
Waktu Belajar (Jam)           -0.009696                    0.085673  
Nilai                         -0.137514                   -0.090468  
Kehadiran (%)                  1.000000                   -0.020836  
Latihan Soal (Jam)            -0.020836                    1.000000  
```

### Visualisasi Heatmap
Gunakan Seaborn untuk membuat heatmap dari matriks korelasi
```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt='.2f', linewidths=0.5)
plt.title('Heatmap Korelasi Antar Fitur', fontsize=14)
plt.savefig('15_01.png', format='png', dpi=300)
plt.show()
```
Output:
<img src="https://github.com/rohmanurnr/100-Days-of-Python-ML-AI/blob/main/Day%20015/15_01.png" width=”500”>


### Interpretasi Hasil
#### Analisis hubungan antar fitur berdasarkan warna dan nilai korelasi dalam heatmap:
1. Identifikasi pasangan fitur dengan korelasi tinggi (mendekati 1 atau -1).
2. Analisis fitur yang memiliki korelasi lemah (mendekati 0).
3. Pertimbangkan untuk memilih atau menghapus fitur tertentu berdasarkan hasil korelasi 

#### Hasil analisis:
- **Waktu belajar vs Nilai:** Korelasi sangat lemah (-0.009954), menunjukkan hampir tidak ada hubungan antara waktu belajar dan nilai.
- **Kehadiran vs Nilai:** Korelasi negatif lemah (-0.137514), artinya tingkat kehadiran sedikit mempengaruhi nilai, tetapi pengaruhnya sangat kecil.
- **Latihan Soal vs Waktu Belajar:** Korelasi lemah positif (0.085673), menunjukkan sedikit hubungan positif antara latihan soal dan waktu belajar.

Secara keseluruhan, tidak ada fitur dengan korelasi kuat, sehingga kemungkinan besar setiap fitur memberikan informasi unik tanpa redudansi.

#### Kesimpulan dan tindak lanjut:
1. Korelasi Lemah: Karena semua korelasi mendekati nol, fitur ini dapat digunakan secara independen dalam analisis atau modeling tanpa risiko multikolinearitas.
2. Tidak Ada Hubungan Jelas: Anda dapat mengeksplorasi lebih jauh menggunakan teknik analisis lain, seperti clustering atau PCA, untuk memahami struktur dataset lebih dalam.
