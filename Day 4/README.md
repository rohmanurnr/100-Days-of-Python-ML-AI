# Pengenalan NumPy

## Learning Objectives:
- Memahami konsep dasar array NumPy dan cara penggunaannya.
- Mengenal keunggulan array NumPy dibandingkan dengan list Python.
- Menggunakan operasi dasar pada array NumPy.
- Melakukan manipulasi bentuk array.
- Menggunakan fungsi statistik dasar.
- Menerapkan teknik slicing dan indexing.

## Aktivitas/Tantangan:

### Array
Sebelum mempelajari lebih lanjut tentang NumPy, penting untuk memahami apa itu array. Array adalah struktur data yang digunakan untuk menyimpan sekumpulan nilai dalam urutan tertentu dan terorganisir. Nilai-nilai dalam array dapat diakses menggunakan indeks, dan biasanya semua elemen dalam array memiliki tipe data yang sama.

### Deskripsi NumPy
NumPy (Numerical Python) adalah pustaka Python yang digunakan untuk komputasi numerik, dan salah satu fitur utamanya adalah NumPy array. Struktur data ini mirip dengan list Python, tetapi dengan banyak keunggulan.

NumPy Array dirancang untuk:
- Menyimpan elemen-elemen dengan tipe data yang sama, seperti angka, dan mendukung array multidimensi.
- Melakukan operasi matematis langsung pada seluruh array tanpa perlu menulis loop manual, sehingga operasi ini lebih efisien dan cepat dibandingkan dengan list biasa di Python.

### Keunggulan NumPy
1. **Kecepatan:**
   NumPy jauh lebih cepat dibandingkan dengan list Python untuk operasi matematis karena array Numpy dikelola secara internal dalam format yang lebih efisien.
   
2. **Memory-Efficient:**
   NumPy menggunakan lebih sedikit memori untuk menyimpan data karena array NumPy menyimpan data dalam format yang lebih padat dibandingkan dengan list Python.
   
3. **Fungsi-fungsi canggih:**
   NumPy menyediakan fungsi matematis, statistik, aljabar linier, dan fungsi lainnya yang sangat berguna dalam analisis data.

### Instalasi NumPy
Kamu perlu menginstal library NumPy melalui terminal atau command prompt dengan perintah:

```bash
pip install numpy
```

### Membuat Array NumPy
Membuat Array Numpy
```python
import numpy as np

#Membuat array 1D
array_1d = np.array([1, 2, 3, 4, 5])
print(array_1d)

#Membuat array 2D
array_2d = np.array([[1, 2, 3], [4, 5, 6]])
print(array_2d)
```

Output:
```bash
[1 2 3 4 5]
[[1 2 3]
 [4 5 6]]
```

### Operasi Matematika pada Array Numpy
```python
import numpy as np
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

#Penjumlahan array
print(a + b)

#Perkalian array
print(a * b)

#Operasi skalar
print(a * 2)
```

Output:
```bash
[5 7 9]
[4 10 18]
[2 4 6]
```

### Fungsi Statistik di NumPy
```python
import numpy as np
data = np.array([10, 20, 30, 40, 50])

mean = np.mean(data)
median = np.median(data)
std_dev = np.std(data)

print(f“Mean: {mean}, Median: {median}, Standard Deviation: {std_dev}”)
```

Output:
```bash
Mean: 30.0, Median: 30.0, Standard Deviation: 14.142135623730951
```

### Manipulasi Bentuk Array
```python
import numpy as np
array = np.array([1, 2, 3, 4, 5, 6])
print(array)

#Mengubah bentuk array menjadi 2D
reshaped_array = array.reshape(2, 3)
print(reshaped_array)
```

Output:
```bash
[1 2 3 4 5 6]
[[1 2 3]
 [4 5 6]]
```

### Slicing dan Indexing
```python
import numpy as np

array = np.array([10, 20, 30, 40, 50])

#Mengakses elemen dengan indeks
print(array[2])

#Slicing array
print(array[1:4])
```

Output:
```bash
30
[20 30 40]
```
