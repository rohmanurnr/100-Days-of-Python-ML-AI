#Manipulasi Data dengan Pandas

## Learning Objectives:
1. Menggunakan fungsi Pandas untuk mengurutkan data berdasarkan kolom tertentu.
2. Memfilter data sesuai kriteria yang diberikan.
3. Menggabungkan beberapa DataFrame menggunakan operasi seperti join, concat, atau merge.

---

## Aktivitas/Tantangan:
### Deskripsi Manipulasi Data
Manipulasi data adalah proses mengolah data mentah menjadi informasi yang lebih terstruktur dan relevan. Dalam analisis data, manipulasi data memungkinkan kita untuk menyusun, memfilter, dan menggabungkan data sesuai kebutuhan. Dengan pustaka **Pandas**, proses ini menjadi sangat efisien dan mudah dilakukan.

Beberapa jenis manipulasi data yang sering digunakan:
1. **Sorting**: Mengurutkan data berdasarkan satu atau lebih kolom, baik secara ascending (naik) maupun descending (turun).
2. **Filtering**: Menyaring data berdasarkan kondisi tertentu untuk menampilkan subset data yang relevan.
3. **Merging and Joining**: Menggabungkan dua atau lebih DataFrame untuk menciptakan dataset yang lebih kaya informasi.

---

### Sorting Data
```python
import pandas as pd

data = {
    'Nama': ['Ayu', 'Budi', 'Citra'],
    'Umur': [20, 21, 22],
    'Kota': ['Jakarta', 'Bandung', 'Jogja']
}
df = pd.DataFrame(data)
df
```
Output:
```bash
Nama	Umur	Kota
0	Ayu	20	Jakarta
1	Budi	21	Bandung
2	Citra	22	Jogja
```

```python
sorted_df = df.sort_values(by='Umur')
print(sorted_df)
```
Output:
```bash
   Nama  Umur     Kota
0    Ayu    20  Jakarta
1   Budi    21  Bandung
2  Citra    22    Jogja
```

```python
sorted_df_desc = df.sort_values(by='Nama', ascending=False)
print(sorted_df_desc)
```
Output:
```bash
    Nama  Umur     Kota
2  Citra    22    Jogja
1   Budi    21  Bandung
0    Ayu    20  Jakarta
```

### Filtering Data
```python
filtered_df = df[df['Umur'] > 20]
print(filtered_df)
```
Output:
```bash
    Nama  Umur     Kota
1   Budi    21  Bandung
2  Citra    22    Jogja
```

```python
filtered_city = df[df['Kota'] == 'Jakarta']
print(filtered_city)
```
Output:
```bash
  Nama  Umur     Kota
0  Ayu    20  Jakarta
```

 ### Merging DataFrames
```python
data2 = {
    'Nama': ['Ayu', 'Budi'],
    'Hobi': ['Membaca', 'Olahraga']
}
df2 = pd.DataFrame(data2)
df2
```
Output:
```bash
   Nama        Hobi
0   Ayu     Membaca
1  Budi   Olahraga
```

```python
merged_df = pd.merge(df, df2, on='Nama')
print(merged_df)
```
Output:
```bash
   Nama  Umur     Kota        Hobi
0   Ayu    20  Jakarta     Membaca
1  Budi    21  Bandung   Olahraga
```

```python
concat_df = pdf.concat([df, df2], axis=0, ignore_index=True)
print(concat_df)
```
Output:
```bash
    Nama  Umur     Kota        Hobi
0    Ayu  20.0  Jakarta         NaN
1   Budi  21.0  Bandung         NaN
2  Citra  22.0    Jogja         NaN
3    Ayu   NaN      NaN     Membaca
4   Budi   NaN      NaN   Olahraga
```

---
### Challenge
1. Buat DataFrame dari data favoritmu (misalnya film, makanan, buku) dan urutkan berdasarkan salah satu kolom.
   ```python
   data_film = {
     'Judul': ['Inception', 'Interstellar', 'The Dark Knight', 'Parasite', 'Coco'],
     'Rating': [8.8, 8.6, 9.0, 8.6, 8.4],
     'Genre': ['Sci-Fi', 'Sci-Fi', 'Action', 'Thriller', 'Animation']
   }
   df_film = pd.DataFrame(data_film)
   print("DataFrame Film:")
   print(df_film)
   ```
   Output:
   ```bash
                Judul  Rating       Genre
   0      Inception     8.8      Sci-Fi
   1   Interstellar     8.6      Sci-Fi
   2  The Dark Knight     9.0      Action
   3        Parasite     8.6    Thriller
   4            Coco     8.4   Animation
   ```
   
   ```python
   df_sorted = df_film.sort_values(by='Rating', ascending=False)
   print("\nDataFrame yang Diurutkan Berdasarkan Rating:")
   print(df_sorted)
   ```
   Output:
   ```bash
                Judul  Rating       Genre
   2  The Dark Knight     9.0      Action
   0      Inception     8.8      Sci-Fi
   1   Interstellar     8.6      Sci-Fi
   3        Parasite     8.6    Thriller
   4            Coco     8.4   Animation
   ```
3. Pilih subset data berdasarkan kriteria tertentu (contoh: rating di atas 8).
   ```python
   df_filtered = df_film[df_film['Rating'] > 8.5]
   print("\nSubset DataFrame dengan Rating > 8.5:")
   print(df_filtered)
   ```
   Output:
   ```bash
                Judul  Rating       Genre
   0      Inception     8.8      Sci-Fi
   1   Interstellar     8.6      Sci-Fi
   2  The Dark Knight     9.0      Action
   3        Parasite     8.6    Thriller
   ```

3. Gabungkan dua DataFrame berdasarkan kolom kunci tertentu (contoh: Nama, Kategori).
   ```python
   data_tambahan = {
       'Judul': ['Inception', 'Interstellar', 'Coco', 'The Lion King'],
       'Tahun': [2010, 2014, 2017, 1994],
       'Sutradara': ['Christopher Nolan', 'Christopher Nolan', 'Lee Unkrich', 'Roger Allers']
   }
   df_tambahan = pd.DataFrame(data_tambahan)
   print("\nDataFrame Tambahan:")
   print(df_tambahan)
   ```
   Output:
   ```bash
              Judul  Tahun         Sutradara
   0      Inception   2010  Christopher Nolan
   1   Interstellar   2014  Christopher Nolan
   2            Coco   2017       Lee Unkrich
   3  The Lion King   1994       Roger Allers
   ```

   ```python
   df_merged = pd.merge(df_film, df_tambahan, on='Judul', how='inner')
   print("\nDataFrame Hasil Penggabungan (Merge):")
   print(df_merged)
   ```
   Output:
   ```bash
                Judul  Rating       Genre  Tahun         Sutradara
   0      Inception     8.8      Sci-Fi   2010  Christopher Nolan
   1   Interstellar     8.6      Sci-Fi   2014  Christopher Nolan
   2            Coco     8.4   Animation   2017       Lee Unkrich
   ```
