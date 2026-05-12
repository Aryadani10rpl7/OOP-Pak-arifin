# LATIHAN 1 — Membuat Class Hero

## Koding Google Colab

```python
# LATIHAN 1

class Hero:
    # Constructor
    def __init__(self, name, hp, attack_power):
        self.name = name
        self.hp = hp
        self.attack_power = attack_power

    # Method menampilkan info hero
    def info(self):
        print(f"Hero: {self.name} | HP: {self.hp} | Power: {self.attack_power}")


# Main Program
hero1 = Hero("Layla", 100, 15)
hero2 = Hero("Zilong", 120, 20)

hero1.info()
hero2.info()

# Analisis perubahan HP
hero1.hp = 500
print("HP terbaru hero1:", hero1.hp)
```

## Jawaban Tugas Analisis 1

Jika nilai `hero1.hp` diubah menjadi `500`, maka atribut HP pada object `hero1` akan berubah dari 100 menjadi 500. Saat dilakukan `print(hero1.hp)`, output yang muncul adalah `500`.

Hal ini terjadi karena atribut object dapat diubah langsung setelah object dibuat.

---

# LATIHAN 2 — Interaksi Antar Object

## Koding Google Colab

```python
# LATIHAN 2

class Hero:
    def __init__(self, name, hp, attack_power):
        self.name = name
        self.hp = hp
        self.attack_power = attack_power

    def info(self):
        print(f"Hero: {self.name} | HP: {self.hp} | Power: {self.attack_power}")

    # Method menyerang
    def serang(self, lawan):
        print(f"{self.name} menyerang {lawan.name}!")
        lawan.diserang(self.attack_power)

    # Method menerima damage
    def diserang(self, damage):
        self.hp -= damage
        print(f"{self.name} terkena damage {damage}. Sisa HP: {self.hp}")


# Main Program
hero1 = Hero("Layla", 100, 15)
hero2 = Hero("Zilong", 120, 20)

print("\n--- Pertarungan Dimulai ---")
hero1.serang(hero2)
hero2.serang(hero1)
```

## Jawaban Tugas Analisis 2

Parameter `lawan` menerima object utuh agar method dapat mengakses atribut dan method milik object tersebut, seperti `lawan.name` dan `lawan.diserang()`.

Jika hanya menggunakan string nama, program tidak dapat mengurangi HP lawan atau menjalankan method lain karena string tidak memiliki atribut dan method seperti object Hero.

---

# LATIHAN 3 — Inheritance (Pewarisan)

## Koding Google Colab

```python
# LATIHAN 3

class Hero:
    def __init__(self, name, hp, attack_power):
        self.name = name
        self.hp = hp
        self.attack_power = attack_power

    def info(self):
        print(f"Hero: {self.name} | HP: {self.hp} | Power: {self.attack_power}")

    def serang(self, lawan):
        print(f"{self.name} menyerang {lawan.name}!")
        lawan.diserang(self.attack_power)

    def diserang(self, damage):
        self.hp -= damage
        print(f"{self.name} terkena damage {damage}. Sisa HP: {self.hp}")


# Child Class
class Mage(Hero):
    def __init__(self, name, hp, attack_power, mana):
        super().__init__(name, hp, attack_power)
        self.mana = mana

    def info(self):
        print(f"{self.name} [Mage] | HP: {self.hp} | Mana: {self.mana}")

    def skill_fireball(self, lawan):
        if self.mana >= 20:
            print(f"{self.name} menggunakan Fireball ke {lawan.name}!")
            self.mana -= 20
            lawan.diserang(self.attack_power * 2)
        else:
            print(f"{self.name} gagal skill! Mana tidak cukup.")


# Main Program
print("\n--- Update Class Hero ---")

eudora = Mage("Eudora", 80, 30, 100)
balmond = Hero("Balmond", 200, 10)

eudora.info()
eudora.serang(balmond)
eudora.skill_fireball(balmond)
```

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

## Koding Google Colab

```python
# LATIHAN 4

class Hero:
    def __init__(self, nama, hp_awal):
        self.nama = nama
        self.__hp = hp_awal

    # Getter
    def get_hp(self):
        return self.__hp

    # Setter
    def set_hp(self, nilai_baru):
        if nilai_baru < 0:
            self.__hp = 0
        elif nilai_baru > 1000:
            print("Cheat terdeteksi! HP dimaksimalkan ke 1000 saja.")
            self.__hp = 1000
        else:
            self.__hp = nilai_baru

    def diserang(self, damage):
        sisa_hp = self.get_hp() - damage
        self.set_hp(sisa_hp)
        print(f"{self.nama} terkena damage {damage}. Sisa HP: {self.get_hp()}")


# Uji Coba
hero1 = Hero("Layla", 100)

hero1.set_hp(-50)
print(hero1.get_hp())

# Percobaan akses paksa
print(f"Mencoba akses paksa: {hero1._Hero__hp}")
```

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

## Koding Google Colab

```python
# LATIHAN 5

from abc import ABC, abstractmethod

# Abstract Class / Interface
class GameUnit(ABC):

    @abstractmethod
    def serang(self, target):
        pass

    @abstractmethod
    def info(self):
        pass


# Class Hero
class Hero(GameUnit):
    def __init__(self, nama):
        self.nama = nama

    def serang(self, target):
        print(f"Hero {self.nama} menebas {target}!")

    def info(self):
        print(f"Saya adalah Hero: {self.nama}")


# Class Monster
class Monster(GameUnit):
    def __init__(self, jenis):
        self.jenis = jenis

    def serang(self, target):
        print(f"Monster {self.jenis} menggigit {target}!")

    def info(self):
        print(f"Saya adalah Monster: {self.jenis}")


# Main Program
h = Hero("Alucard")
m = Monster("Serigala")

h.info()
m.info()
```

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

## Koding Google Colab

```python
# LATIHAN 6

class Hero:
    def __init__(self, nama):
        self.nama = nama

    def serang(self):
        print("Hero menyerang dengan tangan kosong.")


# Child Class 1
class Mage(Hero):
    def serang(self):
        print(f"{self.nama} (Mage) menembakkan Bola Api! Boom!")


# Child Class 2
class Archer(Hero):
    def serang(self):
        print(f"{self.nama} (Archer) memanah dari jauh! Jleb!")


# Child Class 3
class Fighter(Hero):
    def serang(self):
        print(f"{self.nama} (Fighter) memukul dengan pedang! Slash!")


# Child Class Tambahan
class Healer(Hero):
    def serang(self):
        print(f"{self.nama} tidak menyerang, tapi menyembuhkan teman!")


# Polymorphism
pasukan = [
    Mage("Eudora"),
    Archer("Miya"),
    Fighter("Zilong"),
    Mage("Gord"),
    Healer("Rafaela")
]

print("--- PERANG DIMULAI ---")

for pahlawan in pasukan:
    pahlawan.serang()
```

## Jawaban Tugas Analisis 6

### 1. Keuntungan Polymorphism

Program tetap berjalan lancar walaupun ditambahkan class baru `Healer` tanpa mengubah kode looping.

Keuntungan polymorphism adalah program menjadi fleksibel dan mudah dikembangkan.

### 2. Konsistensi Nama Method

Jika method `serang()` pada Archer diubah menjadi `tembak_panah()`, maka saat looping program akan error karena method `serang()` tidak ditemukan.

Dalam polymorphism, nama method harus sama agar semua object dapat dipanggil dengan perintah yang sama.

---

# TUGAS PROYEK INTEGRASI — TECHMASTER

## Koding Lengkap Google Colab

```python
# PROJECT OOP TECHMASTER

from abc import ABC, abstractmethod


# ABSTRACT CLASS
class BarangElektronik(ABC):

    def __init__(self, nama, harga_dasar):
        self.nama = nama
        self.__stok = 0
        self.__harga_dasar = harga_dasar

    # Getter stok
    def get_stok(self):
        return self.__stok

    # Getter harga
    def get_harga_dasar(self):
        return self.__harga_dasar

    # Method tambah stok
    def tambah_stok(self, jumlah):
        if jumlah < 0:
            print(f"Gagal update stok {self.nama}! Stok tidak boleh negatif ({jumlah}).")
        else:
            self.__stok += jumlah
            print(f"Berhasil menambahkan stok {self.nama}: {jumlah} unit.")

    @abstractmethod
    def tampilkan_detail(self):
        pass

    @abstractmethod
    def hitung_harga_total(self, jumlah):
        pass


# CLASS LAPTOP
class Laptop(BarangElektronik):

    def __init__(self, nama, harga_dasar, processor):
        super().__init__(nama, harga_dasar)
        self.processor = processor

    def tampilkan_detail(self):
        print(f"[LAPTOP] {self.nama} | Proc: {self.processor}")
        print(f"Harga Dasar: Rp {self.get_harga_dasar():,}")

    def hitung_harga_total(self, jumlah):
        pajak = self.get_harga_dasar() * 0.10
        subtotal = (self.get_harga_dasar() + pajak) * jumlah

        print(f"Pajak (10%): Rp {int(pajak):,}")
        print(f"Beli: {jumlah} unit | Subtotal: Rp {int(subtotal):,}")

        return subtotal


# CLASS SMARTPHONE
class Smartphone(BarangElektronik):

    def __init__(self, nama, harga_dasar, kamera):
        super().__init__(nama, harga_dasar)
        self.kamera = kamera

    def tampilkan_detail(self):
        print(f"[SMARTPHONE] {self.nama} | Cam: {self.kamera}")
        print(f"Harga Dasar: Rp {self.get_harga_dasar():,}")

    def hitung_harga_total(self, jumlah):
        pajak = self.get_harga_dasar() * 0.05
        subtotal = (self.get_harga_dasar() + pajak) * jumlah

        print(f"Pajak (5%): Rp {int(pajak):,}")
        print(f"Beli: {jumlah} unit | Subtotal: Rp {int(subtotal):,}")

        return subtotal


# FUNGSI POLYMORPHISM
# daftar_barang = list tuple (barang, jumlah)
def proses_transaksi(daftar_barang):
    total = 0

    print("\n--- STRUK TRANSAKSI ---")

    nomor = 1

    for barang, jumlah in daftar_barang:
        print(f"{nomor}.", end=" ")
        barang.tampilkan_detail()

        subtotal = barang.hitung_harga_total(jumlah)
        total += subtotal

        print("-" * 40)
        nomor += 1

    print(f"TOTAL TAGIHAN: Rp {int(total):,}")


# MAIN PROGRAM
print("--- SETUP DATA ---")

laptop1 = Laptop("ROG Zephyrus", 20000000, "Ryzen 9")
smartphone1 = Smartphone("iPhone 13", 15000000, "12MP")

# Tambah stok
laptop1.tambah_stok(10)
smartphone1.tambah_stok(-5)
smartphone1.tambah_stok(20)


# Keranjang belanja
keranjang = [
    (laptop1, 2),
    (smartphone1, 1)
]

# Proses transaksi
proses_transaksi(keranjang)
```

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
