---
title: "DIJKSTRA'S ALGORITHM"
date: 2025-06-03
categories: [Desain dan Analisis Algoritma, Dijkstra's Algorithm]
tags: [dijkstra's algorithm]
---

## Pengantar

Selamat datang di repositori yang akan membahas secara mendalam tentang "Dijkstra's Algorithm". Algoritma ini adalah salah satu fondasi utama dalam teori graf dan optimasi, digunakan untuk menemukan jalur terpendek dalam berbagai aplikasi dunia nyata. Dalam materi ini, kita akan mempelajari definisi algoritma Dijkstra, cara kerjanya, contoh permasalahan, aplikasi praktis, serta kelebihan dan kekurangannya.

## 1. Apa itu Dijkstra's Algorithm ?

Dijkstra's Algorithm adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik dalam sebuah graf. Graf ini bisa berupa jaringan yang terdiri dari simpul (titik) dan sisi (hubungan antar titik) dengan bobot tertentu pada sisi-sisinya. Algoritma ini membantu kita menentukan jalur terpendek dari titik awal ke titik tujuan.

## 2. Cara Kerja Dijkstra's Algorithm

Algoritma Dijkstra bekerja dengan langkah-langkah sistematis :
1.  Buat tabel dan kolom sebagai tempat nilai atau jarak dari simpul, sedangkan baris sebagai posisi simpul.
2.  Pilih simpul awal dan simpul tujuan, dengan syarat simpul tersebut harus terhubung secara langsung.
3.  Hitung jarak beberapa simpul tujuan yang telah dipilih.
4.  Setelah semua simpul diuji, lalu pilih jarak yang terpendek.
5.  Simpul yang dipilih akan menjadi acuan untuk tahap selanjutnya, ulangi seperti sebelumnya sampai semua simpul telah diuji.

## 3. Contoh Permasalahan

Carilah nilai dan lintasan terpendek dari simpul A ke F pada graf berikut:

**Graf :**
A terhubung ke B (bobot 1), C (bobot 5)
B terhubung ke C (bobot 2), D (bobot 2), E (bobot 1)
C terhubung ke E (bobot 2)
D terhubung ke F (bobot 1)
E terhubung ke F (bobot 2)

**Solusi :**
Mari kita asumsikan simpul A adalah titik awal. Kita akan mencatat jarak terpendek yang ditemukan untuk setiap simpul.

| V (Simpul yang Diproses) | A | B | C | D | E | F |
| :----------------------- | :- | :- | :- | :- | :- | :- |
| A (Mulai dari A)         | 0 | 1 (AB) | 5 (AC) | $\infty$ | $\infty$ | $\infty$ |
| B (Pilih B)              | 0 | 1 (AB) | 3 (ABC) | 3 (ABD) | 2 (ABE) | $\infty$ |
| E (Pilih E)              | 0 | 1 (AB) | 3 (ABC) | 3 (ABD) | 2 (ABE) | 4 (ABEF) |
| C (Pilih C)              | 0 | 1 (AB) | 3 (ABC) | 3 (ABD) | 2 (ABE) | 4 (ABEF) |
| D (Pilih D)              | 0 | 1 (AB) | 3 (ABC) | 3 (ABD) | 2 (ABE) | 4 (ABEF) |

Setelah semua simpul diuji, lintasan terpendek dari A ke F adalah :
* **ABEF** (jalur A -> B -> E -> F): 1 + 1 + 2 = 4
* **ABDF** (jalur A -> B -> D -> F): 1 + 2 + 1 = 4

Lintasan Terpendek adalah **ABEF/ABDF** dengan total jarak = **4**.

## 4. Implementasi Kode

(Bagian ini tidak tersedia dalam PPT yang diberikan.)

## 5. Contoh Penggunaan Dijkstra's Algorithm

Dijkstra's Algorithm memiliki aplikasi luas di dunia nyata:
* **Navigasi Jalan :** Misalnya kita ingin mencari rute terpendek dari rumah ke sekolah. Dijkstra's Algorithm akan membantu kita menentukan jalan mana yang lebih pendek dengan mempertimbangkan semua jalan yang ada dan menghitung jarak yang terpendek dari rumah ke sekolah.
* **Pengiriman Barang :** Sebuah perusahaan ekspedisi ingin mengirim paket dari gudang ke beberapa pelanggan. Dijkstra's Algorithm akan membantu menentukan rute pengiriman yang paling efisien agar paket bisa sampai lebih cepat dan tidak boros bensin atau tenaga.

## 6. Kelebihan Dijkstra's Algorithm

* **Menjamin Jalur Terpendek :** Dijkstra selalu menemukan solusi yang optimal (jalur terpendek) dari titik asal ke semua titik lain, selama semua bobot *edge* (jarak/biaya) bernilai positif.
* **Efisien untuk Banyak Aplikasi :** Sangat cocok untuk graf yang padat dan sering digunakan dalam aplikasi nyata seperti GPS, *routing* jaringan, dan sistem navigasi.
* **Dapat Menyelesaikan Banyak Tujuan Sekaligus :** Sekali dijalankan dari satu titik, bisa memberikan informasi jarak terpendek ke semua titik lainnya dalam graf.

## 7. Kekurangan Dijkstra's Algorithm

* **Tidak Bekerja dengan Bobot Negatif :** Tidak bisa digunakan jika ada *edge* dengan bobot negatif.
* **Kurang Efisien untuk Graf Besar yang Jarang Terhubung :** Pada graf yang sangat besar dan *sparse* (jarang terhubung), Dijkstra bisa menjadi lambat jika tidak dioptimalkan dengan struktur data seperti *priority queue* (misalnya *heap*).
* **Perhitungan Bisa Terlalu Luas :** Jika kita hanya ingin jalur dari titik A ke titik B, Dijkstra tetap menghitung semua kemungkinan ke titik lain, yang kadang tidak efisien. Dalam kasus seperti ini, algoritma A\* (A Star) bisa lebih baik karena memperhitungkan arah tujuan.

## 8. Kesimpulan

Algoritma Dijkstra merupakan salah satu algoritma pencarian jalur terpendek yang paling efisien dan banyak digunakan dalam teori graf. Algoritma ini bekerja dengan cara mencari jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot non-negatif. Melalui pendekatan *greedy*, Dijkstra memastikan bahwa setiap langkahnya mendekatkan solusi menuju hasil optimal. Keunggulan utama algoritma ini terletak pada keakuratannya dan efisiensinya, terutama jika dikombinasikan dengan struktur data seperti *priority queue* atau *min-heap*. Dalam implementasi praktis, algoritma Dijkstra sangat berguna dalam berbagai bidang seperti jaringan komputer, sistem navigasi, dan pemodelan transportasi.

---

Thank You.