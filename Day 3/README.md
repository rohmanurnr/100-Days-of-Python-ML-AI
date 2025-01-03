# Challenge Day 3: Python Basics & Mini Project

## 📝 Deskripsi Hari Ke-3
Pada hari ketiga ini, kita fokus mempelajari **tipe data dasar** dalam Python dan cara menggunakannya dalam **program sederhana**. Selain itu, kita juga akan memahami logika seperti **loop** dan **percabangan** untuk membuat program interaktif.

---

## 🎯 Learning Objectives
1. Mengenal dan menggunakan tipe data Python: List, Tuple, dan Dictionary.
2. Mengimplementasikan loop (For, While) untuk iterasi data.
3. Membuat program sederhana menggunakan percabangan If-Else.
4. Menyelesaikan mini project interaktif berbasis Python.

---

## 🔧 Aktivitas dan Tantangan

### 1. Tipe Data Dasar
**List:** 
```python
buah = ["apel", "jeruk", "mangga"]
buah.append("pisang")
print(buah)
```

**Tuple:**
```python
hari = ("Senin", "Selasa", "Rabu")
print(f"Hari dalam seminggu: {hari}")
```

**Dictionary**
```Python
kontak = {"Nama": "Andi", "Nomor": "08123456789"}
kontak["Email"] = "andi@email.com"
print(f"Data kontak: {kontak}")
```

### 2. Loop dan Logika:
**For Loop dengan List**
```python
for item in buah:
    print(f"Buah: {item}")
```

**While Loop**
```python
angka = 5
while angka > 0:
    print(f"Countdown: {angka}")
    angka -= 1
```

**Percabangan**
```python
angka = int(input("Masukkan angka: "))
if angka % 2 == 0:
    print("Angka genap")
else:
    print("Angka ganjil")
```

### 3. Mini Project: Program Pemilihan Menu Sederhana
```python
menu = {"1": "Nasi Goreng", "2": "Mie Goreng", "3": "Soto Ayam"}

print("Menu:")
for key, value in menu.items():
    print(f"{key}. {value}")

pilihan = input("Pilih menu (1/2/3): ")
if pilihan in menu:
    print(f"Anda memilih: {menu[pilihan]}")
else:
    print("Pilihan tidak valid")
```

### Challenge Project: Membangun Program Interaktif
Buat program sederhana yang meminta pengguna memasukkan nama, umur, dan kota, lalu menampilkan kalimat sapaan yang disesuaikan.
Contoh output:
```bash
Halo, Andi!  
Kamu berumur 25 tahun dan tinggal di Jakarta.  
Selamat belajar Python di Sobat Berprostech!
```
---
## ❗ Catatan Penting
Tipe data seperti List, Tuple, dan Dictionary sangat penting dalam pengelolaan data.
Gunakan logika loop dan percabangan untuk membuat program yang lebih interaktif.
Jangan ragu untuk bereksperimen dengan variasi kode agar lebih memahami konsep.
