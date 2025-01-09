# Challenge Day 8

## 📝 Topik
**Visualisasi Dasar dengan Matplotlib**

---

## 🎯 Learning Objectives
1. Memahami dasar-dasar penggunaan library Matplotlib untuk visualisasi data.
2. Membuat grafik sederhana seperti grafik garis, batang, dan histogram.
3. Meningkatkan kemampuan interpretasi data melalui visualisasi.
4. Memahami parameter utama yang digunakan untuk memperindah grafik.

---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Visualisasi data adalah langkah penting dalam analisis data untuk mengubah data mentah menjadi informasi yang lebih mudah dipahami. Library Matplotlib di Python memungkinkan kita membuat berbagai jenis grafik untuk membantu memahami pola, tren, atau distribusi data.

---
## 🚀 Langkah-Langkah

### Install Library Matplotlib
```bash
pip install matplotlib
```

### Import Library Matplotlib
```bash
import matplotlib.pyplot as plt
import numpy as np
```

###  Membuat Grafik Garis
Langkah-langkah:
Siapkan data untuk sumbu x dan y.
Gunakan plt.plot() untuk membuat grafik garis.
Tambahkan judul, label, dan legenda jika diperlukan.
```python
x = np.linspace(0, 10, 100) 
y = np.sin(x)

plt.figure(figsize=(8, 6))
plt.plot(x, y, label='Sine Wave', color='blue', linestyle='--', marker='o')
plt.title('Grafik Garis: Sine Wave')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.legend()
plt.grid(True)
plt.show()
```
Output:
```bash

```

### Membuat Grafik Batang
Langkah-langkah:
Siapkan data kategori (x) dan nilainya (y).
Gunakan plt.bar() untuk membuat grafik batang.
Gunakan warna atau pola berbeda untuk membedakan kategori.
```python
categories = ['A', 'B', 'C', 'D']
values = [10, 20, 15, 25]

plt.figure(figsize=(8, 6))
plt.bar(categories, values, color='orange', edgecolor='black')
plt.title('Grafik Batang: Penjualan Kategori')
plt.xlabel('Kategori')
plt.ylabel('Jumlah Penjualan')
plt.show()
```
Output:
```bash

```

### Membuat Histogram
Langkah-langkah:
Siapkan data numerik (misalnya, tinggi badan atau nilai).
Gunakan plt.hist() untuk membuat histogram.
Tentukan jumlah bins untuk membagi data menjadi interval.
```python
data = np.random.normal(loc=170, scale=10, size=100)  # 100 data tinggi badan dengan mean=170, std=10

plt.figure(figsize=(8, 6))
plt.hist(data, bins=10, color='green', edgecolor='black', alpha=0.7)
plt.title('Histogram: Distribusi Tinggi Badan')
plt.xlabel('Tinggi Badan (cm)')
plt.ylabel('Frekuensi')
plt.show()
```
Output:
```bash

```

### Menambahkan Elemen Estetika
*Warna:* Gunakan parameter ‘color’ untuk mengatur warna grafik.
*Marker:* Gunakan parameter ‘marker’ untuk menampilkan simbol pada data titik.
*Grid:* Gunakan ‘plt.grid(True)’ untuk menambahkan grid.
*Legenda:* Gunakan ‘plt.legend()’ untuk menambahkan keterangan pada grafik.
```python
x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y1, label='Sine Wave', color='blue', linestyle='--', marker='o')
plt.plot(x, y2, label='Cosine Wave', color='red', linestyle='-', marker='x')
plt.title('Grafik Garis: Sine & Cosine Waves')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.legend()
plt.grid(True)
plt.show()
```
Output:
```bash

```

### Interpretasi Data
Tambahkan anotasi jika ada poin penting dalam grafik
```python
plt.annotate('Puncak Sine', xy=(1.57, 1), xytext=(3, 1.5),
             arrowprops=dict(facecolor='black', arrowstyle='->'))
```
Output:
```bash

```
