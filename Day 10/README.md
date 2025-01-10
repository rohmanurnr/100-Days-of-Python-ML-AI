# Challenge Day 10

## 📝 Topik
**Statistik Dasar: Mean, Median, dan Mode**

---

## 🎯 Learning Objectives
1. Memahami konsep dasar mean, median, dan mode dalam statistik.
2. Menghitung statistik deskriptif menggunakan dataset sederhana.
3. Menggunakan Pandas atau Python untuk menghitung mean, median, dan mode secara efisien.
4. Menginterpretasikan hasil statistik deskriptif untuk memahami distribusi data.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Statistik deskriptif adalah langkah awal dalam analisis data untuk merangkum dan mendeskripsikan data secara ringkas.
- **Mean (Rata-rata):** Nilai rata-rata dari semua data.
- **Median:** Nilai tengah dari data setelah diurutkan.
- **Mode:** Nilai yang paling sering muncul dalam data.

Statistik ini memberikan wawasan dasar mengenai distribusi data, yang berguna untuk analisis lebih lanjut. Dengan Python dan Pandas, kita dapat menghitung ketiga nilai ini dengan mudah, bahkan untuk dataset besar.

---
## 🚀 Langkah-Langkah

### Persiapan Data
```python
import pandas as pd

data = {
    'Nama': ['Ayu', 'Budi', 'Citra', 'Dedi', 'Eka', 'Fani', 'Gilang', 'Hadi', 'Indah', 'Joko'],
    'Nilai': [78, 85, 62, 74, 88, 90, 67, 72, 85, 81]
}
df = pd.DataFrame(data)
print("Dataset:\n", df)
```
Output:
```bash
Dataset:
      Nama  Nilai
0     Ayu     78
1    Budi     85
2   Citra     62
3    Dedi     74
4     Eka     88
5    Fani     90
6  Gilang     67
7    Hadi     72
8   Indah     85
9    Joko     81
```

### Menghitung Mean (Rata-rata)
```python
mean_value = df['Nilai'].mean()
print("\nMean (Rata-rata):", mean_value)
```
Output:
```bash
Mean (Rata-rata): 78.2
```

### Menghitung Median (Nilai Tengah)
```python
median_value = df['Nilai'].median()
print("Median (Nilai Tengah):", median_value)
```
Output:
```bash
Median (Nilai Tengah): 79.5
```

### Menghitung Mode (Nilai yang Paling Sering Muncul)
```python
mode_value = df['Nilai'].mode()[0]
print("Mode (Nilai yang Paling Sering Muncul):", mode_value)
```
Output:
```bash
Mode (Nilai yang Paling Sering Muncul): 85
```

### Interpretasi Data
Analisis hasil untuk memahami pola data.
```python
print("\nInterpretasi:")
if mean_value > median_value:
    print("Distribusi data miring ke kanan (Positively Skewed).")
elif mean_value < median_value:
    print("Distribusi data miring ke kiri (Negatively Skewed).")
else:
    print("Distribusi data simetris.")
```
Output:
```bash
Interpretasi:
Distribusi data miring ke kiri (Negatively Skewed).
```
