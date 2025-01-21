# Challenge Day 17

## 📝 Topik
**Encoding Data Kategori**
Mengonversi data kategori menjadi bentuk numerik dengan teknik one-hot encoding.

---

## 🎯 Learning Objectives
1. Memahami pentingnya mengubah data kategori menjadi angka dalam proses analisis data dan pembelajaran mesin.
2. Mengenal metode encoding, terutama one-hot encoding, dan kapan menggunakannya.
3. Menggunakan Pandas untuk melakukan one-hot encoding pada data kategori.
4. Memahami cara menyimpan data yang telah di-encode untuk digunakan dalam analisis lebih lanjut atau pembuatan model.


---

## 🏆 Aktivitas/Tantangan

### Deskripsi
Data kategori adalah data yang merepresentasikan nilai dalam bentuk kategori, seperti "merah", "kuning", "biru" atau "rendah", "sedang", "tinggi". Karena sebagian besar algoritma pembelajaran mesin bekerja dengan data numerik, kita perlu mengonversi data kategori menjadi angka. Salah satu metode populer adalah one-hot encoding, di mana setiap kategori diubah menjadi kolom biner (0 atau 1).

Misalnya:

Kolom Warna dengan nilai ["Merah", "Hijau", "Biru"] akan diubah menjadi:

Merah | Hijau | Biru
  1   |   0   |  0
  0   |   1   |  0
  0   |   0   |  1


---
## 🚀 Langkah-Langkah

### Persiapan Data
Buat dataset sederhana dengan kolom kategori.
```python
import pandas as pd

data = {
    'Nama': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Warna Favorit': ['Merah', 'Hijau', 'Biru', 'Merah', 'Hijau'],
    'Tingkat Pendidikan': ['SMA', 'D3', 'S1', 'SMA', 'S1']
}

df = pd.DataFrame(data)
print("Dataset Asli:")
print(df)
```
Output:
```bash

Dataset Asli:
      Nama Warna Favorit Tingkat Pendidikan
0    Alice         Merah                SMA
1      Bob         Hijau                 D3
2  Charlie          Biru                 S1
3    David         Merah                SMA
4      Eve         Hijau                 S1
```

### One-Hot Encoding
Gunakan fungsi Pandas `get_dummies()` untuk mengonversi kolom kategori menjadi bentuk numerik.
```python
df_encoded = pd.get_dummies(df, columns=['Warna Favorit', 'Tingkat Pendidikan'], prefix=['Warna', 'Pendidikan'])

print("\nDataset Setelah One-Hot Encoding:")
print(df_encoded)
```
Output:
```bash
Nama     Warna_Merah     Warna_Hijau     Warna_Biru
Alice        1                0              0
Bob          0                1              0
Charlie      0                0              1
David        1                0              0 
Eve          0                1              0

Pendidikan_SMA     Pendidikan_D3     Pendidikan_S1
      1                  0                 0
      0                  1                 0
      0                  0                 1
      1                  0                 0 
      0                  0                 1
```

### Simpan Data
Ekspor data yang telah di-encode untuk digunakan dalam analisis lebih lanjut.
```python
df_encoded.to_csv("dataset_encoded.csv", index=False)
```

### Analisis Hasil
1. Perhatikan bagaimana kategori diubah menjadi kolom biner.
2. Pastikan tidak ada kehilangan informasi dari data kategori asli.

### Kesimpulan 
1. One-hot encoding adalah teknik penting untuk mengonversi data kategori menjadi angka tanpa mengubah makna data.
2. Teknik ini cocok untuk data dengan kategori nominal (tanpa urutan).
3. Dataset hasil encoding siap digunakan untuk analisis atau model pembelajaran mesin.
