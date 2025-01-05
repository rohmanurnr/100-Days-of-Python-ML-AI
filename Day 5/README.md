# Day 5: Pengenalan Pandas

## Topik
Pengenalan Pandas

## Learning Objectives
1. Memahami konsep dasar DataFrame dan Series di Pandas.
2. Mengenal fungsi-fungsi dasar untuk membaca, menampilkan, dan mengeksplorasi data.
3. Mempelajari operasi dasar pada DataFrame, seperti memilih kolom, menyaring data, dan menganalisis statistik.
4. Memfilter data berdasarkan kondisi tertentu.

---

## Aktivitas/Tantangan

### Pengenalan Pandas
Pandas adalah pustaka Python yang dirancang khusus untuk manipulasi data, analisis data, dan eksplorasi data secara efisien. Nama ‘Pandas’ berasal dari kata “Panel Data”, yang sering digunakan dalam analisis data ekonomi dan statistika.

### Struktur Data Utama di Pandas:
1. **Series**: Struktur data satu dimensi (seperti daftar atau array) yang memiliki indeks unik untuk setiap elemen.
2. **DataFrame**: Struktur data dua dimensi (mirip dengan tabel Excel) yang memiliki baris dan kolom.

### Fungsi Utama Pandas
Pandas dirancang untuk membantu pekerjaan dengan data berbentuk tabel atau data terstruktur. Berikut beberapa fungsi utamanya:
- Membaca dan menulis data: Mendukung berbagai format data seperti CSV, Excel, JSON, SQL, dan banyak lagi.
- Eksplorasi data: Mudah melihat struktur, dimensi, atau nilai-nilai ringkasan dari data.
- Manipulasi data: Menambah, menghapus, atau mengubah kolom/bagian data, mengurutkan atau menyaring data berdasarkan kriteria tertentu.
- Statistik dan agregasi: Menghitung rata-rata, median, atau jumlah total.
- Transformasi data: Mengubah bentuk data (pivot, reshape, atau merge), mengatasi nilai yang hilang (missing values).

### Instal Pandas
Gunakan perintah berikut jika Pandas belum terinstal:
```bash
pip install pandas
```

### Membuat DataFrame
Cobalah membuat DataFrame sederhana di Python:
```python
import pandas as pd

# Membuat DataFrame
data = {
    'Nama': ['Ayu', 'Budi', 'Citra'],
    'Umur': [21, 22, 20],
    'Kota': ['Jakarta', 'Surabaya', 'Bandung']
}

df = pd.DataFrame(data)
print(df)
```
**Output:**
```bash
    Nama  Umur      Kota
0    Ayu    21   Jakarta
1   Budi    22  Surabaya
2  Citra    20   Bandung
```

### Eksplorasi Data
Gunakan fungsi berikut untuk mengenal struktur data:
```python
#Melihat 5 baris pertama
print(df.head())
```
Output:
```bash
   Nama  Umur      Kota
0    Ayu    21   Jakarta
1   Budi    22  Surabaya
2  Citra    20   Bandung
```

```python
#Informasi umum data
print(df.info())
```
Output:
```bash
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3 entries, 0 to 2
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype 
---  ------  --------------  ----- 
 0   Nama    3 non-null      object
 1   Umur    3 non-null      int64 
 2   Kota    3 non-null      object
dtypes: int64(1), object(2)
memory usage: 200.0+ bytes
None
```
```python
#Statistik deskriptif
print(df.describe())
```
Output:
```bash
      Umur
count   3.0
mean   21.0
std     1.0
min    20.0
25%    20.5
50%    21.0
75%    21.5
max    22.0
```

### Manipulasi Data
Akses kolom atau baris tertentu dan filter data berdasarkan kondisi:
```python
# Akses kolom 'Nama'
print(df['Nama'])

# Filter: Data dengan umur > 20
filtered = df[df['Umur'] > 20]
print(filtered)
```
Output:
```bash
0      Ayu
1     Budi
2    Citra
Name: Nama, dtype: object
    Nama  Umur      Kota
0    Ayu    21   Jakarta
1   Budi    22  Surabaya
```

## Challenge:
1. Buat DataFrame sederhana yang memuat data favoritmu (contoh: daftar buku, film, atau makanan).
2. Gunakan fungsi Pandas untuk:
   - Melihat data menggunakan `.head()` dan `.info()`.
   - Menampilkan statistik deskriptif dengan `.describe()`.
   - Melakukan filter data berdasarkan satu kondisi, lalu tampilkan hasilnya.

Code:
```python
import pandas as pd

# DataFrame sederhana
data = {
    'Judul': ['The Alchemist', 'Inception', 'Nasi Goreng', 'The Dark Knight', 'Sushi'],
    'Kategori': ['Buku', 'Film', 'Makanan', 'Film', 'Makanan'],
    'Rating': [9.0, 8.8, 9.5, 9.1, 8.6]
}

df = pd.DataFrame(data)

# Menampilkan data 5 baris pertama
print(df.head())

# Menampilkan informasi struktur data
print(df.info())

# Menampilkan statistik deskriptif
print(df.describe())

# Filter data berdasarkan kondisi rating > 9.0
filtered_df = df[df['Rating'] > 9.0]
print(filtered_df)
```

**Output:**
```bash
Judul              Kategori    Rating
0     The Alchemist       Buku      9.0
1          Inception      Film      8.8
2       Nasi Goreng    Makanan      9.5
3   The Dark Knight      Film      9.1
4              Sushi    Makanan     8.6

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 3 columns):
 #   Column    Non-Null Count  Dtype  
---  ------    --------------  -----  
 0   Judul     5 non-null      object 
 1   Kategori  5 non-null      object 
 2   Rating    5 non-null      float64
dtypes: float64(1), object(2)
memory usage: 248.0+ bytes
None

       Rating
count  5.000000
mean   9.000000
std    0.339116
min    8.600000
25%    8.800000
50%    9.000000
75%    9.100000
max    9.500000

           Judul  Kategori  Rating
2     Nasi Goreng  Makanan     9.5
3  The Dark Knight     Film     9.1
```

---

Selamat belajar Pandas dan eksplorasi data!
