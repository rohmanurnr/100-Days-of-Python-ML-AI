# 100 Days Challenge - Hari ke-2: Menguasai Dasar Python

## 📚 Deskripsi Hari Ke-2
Pada hari kedua, kita mempelajari dasar-dasar penggunaan Python melalui Jupyter Notebook. Fokus pembelajaran mencakup cara menulis, menjalankan, dan menyimpan script Python, serta memahami konsep penting seperti variabel, tipe data, operasi dasar, dan logika pemrograman.

---

## 🎯 Learning Objectives
1. Mengenal dasar-dasar penggunaan Python di Jupyter Notebook.
2. Memahami bagaimana menulis, menjalankan, dan menyimpan script Python.
3. Memahami fungsi dasar Python seperti variabel, tipe data, dan operasi.

---

## 🏆 Aktivitas dan Tantangan

### 1. Mengenal Jupyter Notebook
- Buka Jupyter Notebook melalui Anaconda Navigator atau terminal.
- Pelajari fungsi utama Jupyter Notebook:
  - Menambah cell
  - Menjalankan cell
  - Menyimpan notebook
- Buat file baru dengan nama **Day_2_Challenge.ipynb**.

### 2. Belajar Variabel, Tipe Data, dan Operasi Dasar
#### Deklarasi Variabel:
```python
nama = "Sobat Berprostech"
usia = 20
```
#### Operasi Matematika Sederhana:
```python
hasil = 5 + 3
print(hasil)
```
#### Pangkat:
```python
hasil_pangkat = 3**2
print(f"Hasil pangkat: {hasil_pangkat}")
```
#### Modulus:
```python
hasil_modulus = 10 % 3
print(f"Hasil modulus: {hasil_modulus}")
```
#### Pembagian Bulat:
```python
hasil_bagi_bulat = 15 // 4
print(f"Hasil pembagian bulat: {hasil_bagi_bulat}")
```

### 3. Menggunakan Input Pengguna
```python
nama = input("Masukkan nama Anda: ")
usia = int(input("Masukkan usia Anda: "))
print(f"Hi {nama}, Anda berusia {usia} tahun.")
```

### 4. Percabangan (if-else)
Contoh 1:
```python
if usia >= 18:
    print("Anda sudah cukup dewasa")
else:
    print("Anda masih di bawah umur.")
```

Contoh 2:
```python
nilai = int(input("Masukkan nilai ujian Anda: "))
if nilai >= 90:
    print("Grade: A")
elif nilai >= 75:
    print("Grade: B")
elif nilai >= 60:
    print("Grade: C")
else:
    print("Grade: D")
```

### 5. Mini Project: Kalkulator Sederhana
```python
print("Kalkulator Sederhana")
angka1 = float(input("Masukkan angka pertama: "))
angka2 = float(input("Masukkan angka kedua: "))
operasi = input("Masukkan operasi (+, -, *, /): ")

if operasi == "+":
    print(f"Hasil: {angka1 + angka2}")
elif operasi == "-":
    print(f"Hasil: {angka1 - angka2}")
elif operasi == "*":
    print(f"Hasil: {angka1 * angka2}")
elif operasi == "/":
    if angka2 != 0:
        print(f"Hasil: {angka1 / angka2}")
    else:
        print("Tidak bisa membagi dengan nol")
else:
    print("Operasi tidak valid")
```

### 6. Format String & F-String
```python
nama = "Sobat Berprostech"
usia = 25
print("Halo, nama saya {} dan usia saya {} tahun.".format(nama, usia))
print(f"Halo, nama saya {nama} dan usia saya {usia} tahun.")
```

### 7. Menghitung Luas Bangun Datar
Luas Lingkaran:
```python
jari_jari = float(input("Masukkan jari-jari lingkaran: "))
luas = 3.14 * jari_jari**2
print(f"Luas lingkaran: {luas}")
```

Luas Segitiga:
```python
alas = float(input("Masukkan panjang alas: "))
tinggi = float(input("Masukkan tinggi segitiga: "))
luas = 0.5 * alas * tinggi
print(f"Luas segitiga: {luas}")
```

### 8. Latihan Logika: Tebak Angka
```python
import random

angka_rahasia = random.randint(1, 10)
tebakan = int(input("Tebak angka antara 1-10: "))

if tebakan == angka_rahasia:
    print("Tebakan Anda benar!")
else:
    print(f"Salah! Angka yang benar adalah {angka_rahasia}.")
```

### 9. Konversi Satuan
Konversi Suhu:
```python
celsius = float(input("Masukkan suhu dalam Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"Suhu dalam Fahrenheit: {fahrenheit}")
```

## ✍️ Catatan Penting
- Semua script disimpan dalam file Day_2_Challenge.ipynb.
- Jangan ragu untuk bereksperimen dengan fungsi Python lainnya.
- Share hasil tantangan di media sosial dengan tagar #SobatBerprostech!
