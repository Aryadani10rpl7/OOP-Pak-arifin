# LATIHAN 1 — Membuat Class Hero

## Jawaban Tugas Analisis 1

Jika nilai `hero1.hp` diubah menjadi `500`, maka atribut HP pada object `hero1` akan berubah dari 100 menjadi 500. Saat dilakukan `print(hero1.hp)`, output yang muncul adalah `500`.

Hal ini terjadi karena atribut object dapat diubah langsung setelah object dibuat.

---

# LATIHAN 2 — Interaksi Antar Object

## Jawaban Tugas Analisis 2

Parameter `lawan` menerima object utuh agar method dapat mengakses atribut dan method milik object tersebut, seperti `lawan.name` dan `lawan.diserang()`.

Jika hanya menggunakan string nama, program tidak dapat mengurangi HP lawan atau menjalankan method lain karena string tidak memiliki atribut dan method seperti object Hero.

---

# LATIHAN 3 — Inheritance (Pewarisan)

## Jawaban Tugas Analisis 3

### 1. Error yang Muncul

Jika `super().__init__(name, hp, attack_power)` dihapus, maka akan muncul error:

```python
AttributeError: 'Mage' object has no attribute 'name'
```

### 2. Penyebab Error

Hal ini terjadi karena atribut `name`, `hp`, dan `attack_power` sebenarnya dibuat di constructor class `Hero`. Ketika `super()` dihapus, constructor parent tidak dijalankan sehingga atribut tersebut tidak pernah dibuat.

### 3. Fungsi super()

`super()` digunakan untuk memanggil constructor atau method milik parent class agar child class dapat mewarisi atribut dan perilaku dari parent class.

Tanpa `super()`, child class tidak mendapatkan data dan fitur dari parent.

---

# LATIHAN 4 — Encapsulation

## Jawaban Tugas Analisis 4

### 1. Percobaan Hacking

Nilai HP tetap muncul walaupun atribut bersifat private.

Hal ini karena Python menggunakan konsep Name Mangling, yaitu nama atribut diubah menjadi `_NamaClass__namaAtribut`.

Walaupun masih bisa diakses, cara tersebut tidak disarankan karena melanggar prinsip Encapsulation dan standar pemrograman yang baik.

### 2. Pentingnya Setter

Jika validasi dihapus lalu menjalankan:

```python
hero1.set_hp(-100)
```

maka HP hero menjadi negatif.

Setter sangat penting untuk menjaga integritas data agar data tetap valid dan tidak rusak.

---

# LATIHAN 5 — Abstraction & Interface

## Jawaban Tugas Analisis 5

### 1. Melanggar Kontrak

Jika method `serang()` dihapus dari class Hero, maka muncul error:

```python
TypeError: Can't instantiate abstract class Hero with abstract method serang
```

Artinya class Hero belum memenuhi kontrak yang diwajibkan oleh abstract class GameUnit.

### 2. Mengapa Abstract Class Tidak Bisa Dibuat Objek?

Class `GameUnit` hanya digunakan sebagai blueprint atau kerangka dasar.

Tujuannya agar semua class turunannya memiliki method yang sama sehingga program lebih terstruktur dan konsisten.

---

# LATIHAN 6 — Polymorphism

## Jawaban Tugas Analisis 6

### 1. Keuntungan Polymorphism

Program tetap berjalan lancar walaupun ditambahkan class baru `Healer` tanpa mengubah kode looping.

Keuntungan polymorphism adalah program menjadi fleksibel dan mudah dikembangkan.

### 2. Konsistensi Nama Method

Jika method `serang()` pada Archer diubah menjadi `tembak_panah()`, maka saat looping program akan error karena method `serang()` tidak ditemukan.

Dalam polymorphism, nama method harus sama agar semua object dapat dipanggil dengan perintah yang sama.

---

# KESIMPULAN

Pada modul ini dipelajari konsep dasar Object Oriented Programming (OOP) di Python, yaitu:

1. Class dan Object
2. Inheritance
3. Encapsulation
4. Polymorphism
5. Abstraction
6. Interface

Dengan OOP, program menjadi lebih terstruktur, aman, fleksibel, dan mudah dikembangkan.

---
# SELESAI
