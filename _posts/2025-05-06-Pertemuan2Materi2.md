---
title: "FRACTIONAL KNAPSACK"
date: 2025-05-06
categories: [Desain dan Analisis Algoritma, Fractional Knapsack]
tags: [fractional knapsack]
---

## Pengantar

Selamat datang di repositori yang membahas secara komprehensif tentang "Fractional Knapsack Problem". Ini adalah masalah optimasi klasik dalam ilmu komputer yang berfokus pada pemilihan item untuk memaksimalkan nilai total yang dapat dimasukkan ke dalam ransel dengan kapasitas terbatas, dengan keunikan bahwa item dapat diambil sebagian. Dalam pembahasan ini, kita akan menjelajahi definisi, karakteristik, strategi penyelesaian dengan algoritma *greedy*, aplikasi praktis, serta contoh kasus dan implementasi.

## 1. Apa itu Knapsack Problem ?

Knapsack Problem adalah masalah optimasi di mana kita harus memilih barang-barang dari sekumpulan item agar nilai totalnya maksimal tanpa melebihi kapasitas berat ransel yang tersedia. Ada dua variasi utama dari masalah ini: 0/1 Knapsack dan Fractional Knapsack.

* **0/1 Knapsack**: Pada variasi ini, kita hanya bisa memilih seluruh barang atau tidak sama sekali, sehingga barang tidak boleh dipotong-potong. Masalah ini lebih kompleks dan biasanya diselesaikan menggunakan metode pemrograman dinamis.
* **Fractional Knapsack**: Kita diperbolehkan mengambil sebagian dari barang tersebut, sehingga barang bisa dipotong sesuai kebutuhan agar mendapatkan nilai maksimal. Perbedaan ini membuat Fractional Knapsack dapat diselesaikan dengan algoritma *greedy* yang lebih sederhana dan efisien.

## 2. Definisi Fractional Knapsack

Fractional Knapsack adalah sebuah permasalahan optimisasi dalam bidang algoritma dan struktur data, di mana tujuannya adalah untuk memaksimalkan nilai total barang yang dimasukkan ke dalam sebuah *knapsack* (tas) dengan kapasitas tertentu, dengan kemungkinan mengambil sebagian (*fraksi*) dari barang.

## 3. Karakteristik Fractional Knapsack

Karakteristik utama dari Fractional Knapsack meliputi :
* Setiap barang memiliki berat (*weight*) dan nilai (*value*).
* Kapasitas tas adalah terbatas.
* Barang boleh dipotong atau diambil sebagian (misalnya 0.5 bagian dari barang A).
* Masalah ini dapat diselesaikan secara *greedy* karena tidak memerlukan pencarian kombinasi semua kemungkinan seperti pada 0/1 Knapsack.

## 4. Strategi Penyelesaian : Algoritma Greedy

Fractional Knapsack diselesaikan menggunakan pendekatan Greedy Algorithm:
1.  Hitung nilai per unit berat (*value per unit weight*) untuk setiap item: `value/weight`.
2.  Urutkan item berdasarkan nilai tersebut secara menurun.
3.  Ambil sebanyak mungkin dari item dengan rasio tertinggi, hingga tas penuh.
4.  Jika tidak bisa mengambil seluruh item karena kapasitas tersisa, ambil sebagian dari item terakhir.

## 5. Implementasi Aplikasi

Fractional Knapsack banyak diterapkan di berbagai bidang, antara lain:
* Penjadwalan
* Investasi dana ke beberapa proyek
* Pengalokasian *bandwidth* di jaringan
* Optimisasi logistik

## 6. Algoritma Greedy : Konsep Umum

Algoritma Greedy adalah sebuah pendekatan atau strategi dalam merancang algoritma yang membuat pilihan yang tampak terbaik pada saat itu (pilihan optimal lokal) dengan harapan bahwa pilihan tersebut akan mengarah pada solusi optimal global.

**Karakteristik Utama Algoritma Greedy :**
* **Pilihan Lokal**: Pada setiap langkah, algoritma memilih opsi yang paling menguntungkan atau "greedy" saat itu.
* **Sederhana dan Efisien** : Algoritma *greedy* seringkali sangat sederhana untuk diimplementasikan dan memiliki kompleksitas waktu yang rendah dibandingkan pendekatan lain seperti pemrograman dinamis.
* **Tidak Melihat ke Depan** : Keputusan dibuat berdasarkan informasi yang tersedia saat ini saja, tanpa mempertimbangkan sub-masalah yang akan muncul setelah keputusan tersebut dibuat.

Algoritma *greedy* sangat efektif dan sering digunakan untuk masalah-masalah tertentu di mana pilihan optimal lokal memang mengarah ke solusi optimal global. Namun, kelemahan utamanya adalah tidak selalu menghasilkan solusi optimal global untuk semua jenis masalah. Ada masalah di mana pilihan terbaik saat ini justru menghalangi tercapainya solusi terbaik secara keseluruhan.

## 7. Contoh Permasalahan dan Solusi

Mari kita lihat beberapa contoh permasalahan Fractional Knapsack:

### Contoh 1

**Item:**
| Item | Nilai (Value) | Berat (Weight) |
| :--- | :------------ | :------------- |
| A    | 50            | 10             |
| B    | 60            | 20             |
| C    | 140           | 40             |
| D    | 60            | 30             |

Kapasitas tas ($W$) = 50.

**Langkah Manual (Ringkasan) :**
1.  **Hitung rasio value/weight :**
    * A: 50/10 = 5.0
    * B: 60/20 = 3.0
    * C: 140/40 = 3.5
    * D: 60/30 = 2.0
2.  **Urutkan :** A (5.0), C (3.5), B (3.0), D (2.0)
3.  **Isi tas berdasarkan kapasitas :**
    * Ambil A (10kg, nilai 50) $\rightarrow$ sisa kapasitas 40kg
    * Ambil C (40kg, nilai 140) $\rightarrow$ sisa kapasitas 0kg
    * B dan D tidak diambil
4.  **Total nilai maksimum :** $50 + 140 = 190$

### Contoh 2

Pak Adi punya tas berkapasitas 50 kg. Di *basecamp* tersedia:

| Barang   | Berat (kg) | Nilai (pentingnya) |
| :------- | :--------- | :----------------- |
| Makanan  | 10         | 60                 |
| Selimut  | 20         | 100                |
| Kamera   | 30         | 120                |

**Solusi :**
1.  **Hitung value/weight :**
    * Makanan: $60/10 = 6$
    * Selimut: $100/20 = 5$
    * Kamera: $120/30 = 4$
2.  **Urutkan dan pilih :**
    * Ambil semua Makanan (10 kg) $\rightarrow$ Nilai = 60
    * Ambil semua Selimut (20 kg) $\rightarrow$ Nilai = 100
    * Sisa kapasitas = 20 kg. Ambil 2/3 Kamera (20 kg dari 30 kg) $\rightarrow$ Nilai = $120 \times 20/30 = 80$
3.  **Total nilai:** $60 + 100 + 80 = 240$

### Contoh 3

Bung bisa membawa 15 kg logam. Di tempat sampah ada:

| Logam     | Berat | Nilai jual |
| :-------- | :---- | :--------- |
| Tembaga   | 5     | 100        |
| Aluminium | 10    | 60         |
| Besi      | 20    | 80         |

**Solusi :**
1.  **Hitung value/weight :**
    * Tembaga: $100/5 = 20$
    * Aluminium: $60/10 = 6$
    * Besi: $80/20 = 4$
2.  **Urutan :** Tembaga $\rightarrow$ Aluminium $\rightarrow$ Besi
3.  **Pilih :**
    * Tembaga (5 kg) $\rightarrow$ Nilai = 100
    * Aluminium (10 kg) $\rightarrow$ Nilai = 60
    * Tas penuh (5 kg + 10 kg = 15 kg)
4.  **Total nilai :** $100 + 60 = 160$

### Contoh 4

Ali bisa membawa 30 kg barang. Barang prioritas:

| Barang     | Berat | Nilai Penting |
| :--------- | :---- | :------------ |
| Laptop     | 10    | 300           |
| Buku Paket | 20    | 200           |
| Baju       | 30    | 180           |

**Solusi :**
1.  **Hitung value/weight :**
    * Laptop: 300/10 = 30
    * Buku: 200/20 = 10
    * Baju: 180/30 = 6
2.  **Urutan :** Laptop $\rightarrow$ Buku $\rightarrow$ Baju
3.  **Pilih :**
    * Laptop (10 kg) $\rightarrow$ Nilai = 300
    * Buku (20 kg) $\rightarrow$ Nilai = 200
    * Tas penuh (10 kg + 20 kg = 30 kg)
4.  **Total nilai :** $300 + 200 = 500$

## 8. Implementasi Permasalahan 4 pada C++

Berikut adalah contoh implementasi C++ untuk menyelesaikan permasalahan Fractional Knapsack:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

using namespace std;

// Struktur untuk merepresentasikan setiap item
struct Item {
    string name;
    double weight;
    double value;

    // Fungsi untuk menghitung rasio value/weight
    double ratio() const {
        return value / weight;
    }
};

// Fungsi comparator untuk mengurutkan berdasarkan rasio terbesar
bool compare (Item a, Item b) {
    return a.ratio() > b.ratio(); // Urutan menurun berdasarkan rasio
}

int main() {
    double capacity = 30.0; // Kapasitas maksimal kurir

    // Daftar item yang tersedia
    vector<Item> items = {
        {"Laptop", 10, 300},    // Item Laptop
        {"Buku Paket", 20, 200},// Item Buku Paket
        {"Baju", 30, 180}       // Item Baju
    };

    // Urutkan item berdasarkan rasio value/weight tertinggi
    sort(items.begin(), items.end(), compare);

    double totalValue = 0.0; // Total nilai yang didapatkan
    double totalWeight = 0.0; // Total berat yang dibawa (opsional, untuk debugging)

    cout << "Barang yang dipilih:\n";

    // Iterasi melalui item yang sudah diurutkan
    for (const auto& item : items) {
        if (capacity == 0) break; // Jika kapasitas tas sudah penuh, berhenti

        if (item.weight <= capacity) {
            // Ambil seluruh barang jika beratnya kurang dari atau sama dengan kapasitas tersisa
            totalValue += item.value;
            capacity -= item.weight;
            totalWeight += item.weight; // Update total berat yang dibawa
            cout << "- " << item.name << " (berat: " << item.weight << "kg, nilai: " << item.value << ")\n";
        } else {
            // Ambil sebagian barang (fractional) jika beratnya melebihi kapasitas tersisa
            double fraction = capacity / item.weight;
            totalValue += item.value * fraction;
            totalWeight += capacity; // Ambil hanya sisa kapasitas
            cout << "- " << item.name << " (berat: " << capacity << "kg dari " << item.weight << "kg, nilai: " << item.value * fraction << ")\n";
            capacity = 0; // Kapasitas tas menjadi nol
        }
    }

    cout << "\nTotal nilai yang dibawa: " << totalValue << endl;
    // cout << "Total berat yang dibawa: " << totalWeight << endl; // Debugging
    return 0;
}
```

## 9. Kesimpulan

Fractional Knapsack adalah salah satu variasi dari Knapsack Problem yang dapat diselesaikan secara efisien menggunakan algoritma *greedy*. Dalam versi ini, barang boleh diambil sebagian (*fraksional*), berbeda dengan 0/1 Knapsack yang hanya membolehkan pengambilan penuh atau tidak sama sekali. Dengan menghitung rasio nilai terhadap berat (*value/weight*) untuk setiap barang, lalu mengambil barang dengan rasio tertinggi hingga kapasitas tas penuh, kita bisa mendapatkan solusi optimal secara cepat dan sederhana. Pendekatan *greedy* ini bekerja efektif karena pilihan optimal lokal (berdasarkan rasio) juga mengarah pada solusi optimal global dalam kasus Fractional Knapsack.

---

Thank You.