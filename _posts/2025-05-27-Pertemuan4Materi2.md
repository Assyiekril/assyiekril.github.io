---
title: "BREADTH FIRST SEARCH"
date: 2025-05-27
categories: [Desain dan Analisis Algoritma, Breadth First Search]
tags: [breadth first search]
---

## Pengantar

Selamat datang di repositori yang akan membahas secara mendalam tentang "Breadth-First Search" (BFS). Ini adalah salah satu algoritma penelusuran graf atau pohon yang fundamental dalam ilmu komputer, dikenal karena pendekatannya yang sistematis dalam menjelajahi simpul-simpul. Dalam materi ini, kita akan mempelajari definisi BFS, konsep dasarnya, langkah-langkah algoritma, cara kerja melalui simulasi, contoh implementasi kode, aplikasi di dunia nyata, serta kelebihan dan kekurangannya.

## 1. Pengertian Breadth-First Search (BFS)

Breadth-First Search (BFS) adalah metode untuk menjelajahi graf atau pohon dengan menelusuri simpul-simpul berdasarkan jaraknya dari titik awal. Secara sederhana, BFS akan mengeksplorasi semua simpul yang paling dekat terlebih dahulu, baru kemudian beralih ke simpul yang lebih jauh. Jadi, pendekatannya menyebar ke seluruh arah secara merata dari pusat. Sebagai ilustrasi, bayangkan kita sedang mencari ruang kelas di sebuah gedung kampus berlantai 3. Kita pasti akan memeriksa seluruh ruangan dari lantai pertama sebelum lanjut ke lantai atas. Itulah cara kerja BFS: menjelajah secara mendatar.

BFS banyak digunakan dalam berbagai aplikasi, mulai dari pencarian rute tercepat dalam *game*, penelusuran jaringan sosial, hingga pencarian jalur optimal dalam sistem navigasi dan peta digital.

## 2. Konsep Dasar BFS

1.  BFS menggunakan struktur data *queue* (antrian) untuk menyimpan simpul-simpul yang akan dikunjungi.
2.  Dimulai dari simpul awal, BFS akan mengunjungi semua tetangga simpul tersebut pada level yang sama terlebih dahulu, kemudian berlanjut ke tetangga dari tetangga pada level berikutnya.
3.  Bersifat *level-order traversal* (penelusuran per lapisan).

## 3. Langkah-Langkah Algoritma Breadth-First Search

Berikut adalah langkah-langkah dalam algoritma BFS :
1.  Tentukan simpul awal (*start node*).
2.  Masukkan simpul awal ke dalam antrian (*queue*).
3.  Tandai simpul awal sebagai sudah dikunjungi.
4.  Selama antrian tidak kosong atau simpul aktif bukan merupakan tujuan, lakukan:
    * Ambil simpul dari depan antrian (*dequeue*).
    * Tandai bahwa simpul tersebut telah dikunjungi.
    * Cek apakah simpul tersebut merupakan solusi/tujuan. Jika ya, hentikan proses.
    * Untuk setiap tetangga dari simpul yang sedang aktif (jika ada):
        * Kunjungi semua tetangga yang belum dikunjungi.
        * Tandai tetangga tersebut sebagai dikunjungi.
        * Tambahkan tetangga tersebut ke dalam antrian (*enqueue*).
5.  Ulangi langkah 4 sampai simpul tujuan (*goal node*) ditemukan atau antrian sudah kosong (artinya tidak ada jalur ke tujuan).

## 4. Cara Kerja Breadth-First Search (Simulasi)

Mari kita simulasikan cara kerja BFS pada graf sederhana dengan simpul awal 'S' dan simpul tujuan 'G'.

**Graf :**
S terhubung ke A, B
A terhubung ke C, D
B terhubung ke E, F
C tidak terhubung ke mana-mana
D tidak terhubung ke mana-mana
E terhubung ke H
F terhubung ke G
G tidak terhubung ke mana-mana
H tidak terhubung ke mana-mana

| QUEUE        | VISITED      | SIMPUL AKTIF |
| :----------- | :----------- | :----------- |
| S            | S            | S            |
| A, B         | SA           | A            |
| B, C, D      | SAB          | B            |
| C, D, E, F   | SABC         | C            |
| D, E, F      | SABCD        | D            |
| E, F         | SABCDE       | E            |
| F, H, G      | SABCDEF      | F            |
| H, G         | SABCDEFH     | H            |
| G            | SABCDEFHG    | G            |

* **S (Start Node):**
    * `QUEUE : [S]`, `VISITED: [S]`
    * Ambil S. Kunjungi tetangga S: A, B.
    * `QUEUE : [A, B]`, `VISITED: [S, A, B]`
* **A:**
    * Ambil A. Kunjungi tetangga A: C, D.
    * `QUEUE : [B, C, D]`, `VISITED: [S, A, B, C, D]`
* **B:**
    * Ambil B. Kunjungi tetangga B: E, F.
    * `QUEUE : [C, D, E, F]`, `VISITED: [S, A, B, C, D, E, F]`
* **C:**
    * Ambil C. Tidak ada tetangga baru.
    * `QUEUE : [D, E, F]`, `VISITED: [S, A, B, C, D, E, F]`
* **D:**
    * Ambil D. Tidak ada tetangga baru.
    * `QUEUE : [E, F]`, `VISITED: [S, A, B, C, D, E, F]`
* **E:**
    * Ambil E. Kunjungi tetangga E: H.
    * `QUEUE : [F, H]`, `VISITED: [S, A, B, C, D, E, F, H]`
* **F:**
    * Ambil F. Kunjungi tetangga F: G.
    * `QUEUE : [H, G]`, `VISITED: [S, A, B, C, D, E, F, H, G]`
* **H:**
    * Ambil H. Tidak ada tetangga baru.
    * `QUEUE : [G]`, `VISITED: [S, A, B, C, D, E, F, H, G]`
* **G (Goal Node) :**
    * Ambil G. G adalah tujuan. Proses berhenti.

## 5. Contoh Kode (C++)

Berikut adalah contoh implementasi BFS dalam C++ untuk mencari jalur terpendek:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <algorithm> // Untuk std::reverse

using namespace std;

// Inisialisasi graf dengan adjacency list
unordered_map<char, vector<char>> graf;

// Menyimpan simpul yang sudah dikunjungi
unordered_map<char, bool> sudahDikunjungi;

// Menyimpan jalur: simpul sekarang -> simpul_sebelumnya (parent)
unordered_map<char, char> parent;

void bfs(char start, char goal) {
    queue<char> q;

    q.push(start);
    sudahDikunjungi[start] = true;
    parent[start] = '\0'; // Titik awal tidak punya parent (menggunakan null char)

    cout << "Proses BFS:\n";

    while (!q.empty()) {
        char sekarang = q.front();
        q.pop();

        cout << "Kunjungi node : " << sekarang << endl;

        // Jika goal ditemukan, langsung hentikan
        if (sekarang == goal) {
            cout << "Goal node '" << goal << "' ditemukan!\n";
            break;
        }

        // Jelajahi tetangga
        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }
    }

    // Cetak jalur terpendek dari goal ke start
    vector<char> jalur;
    char current = goal;
    bool pathExists = false;

    // Cek apakah goal benar-benar ditemukan
    if (sudahDikunjungi[goal]) {
        pathExists = true;
        while (current != '\0') { // Loop sampai kembali ke start node
            jalur.push_back(current);
            current = parent[current];
        }
        reverse(jalur.begin(), jalur.end()); // Balikkan jalur agar dari start ke goal
    }

    cout << "\n=== HASIL ===" << endl;
    cout << "Start Node: " << start << endl;
    cout << "Goal Node: " << goal << endl;

    if (pathExists) {
        cout << "Jalur Terpendek: ";
        for (int i = 0; i < jalur.size(); i++) {
            cout << jalur[i];
            if (i != jalur.size() - 1) cout << " -> ";
        }
        cout << endl;
    } else {
        cout << "Tidak ada jalur dari " << start << " ke " << goal << endl;
    }
}

int main() {
    // Definisi graf (sesuai simulasi di PPT)
    graf['S'] = {'A', 'B'};
    graf['A'] = {'C', 'D'};
    graf['B'] = {'E', 'F'};
    graf['C'] = {};
    graf['D'] = {};
    graf['E'] = {'H'};
    graf['F'] = {'G'};
    graf['G'] = {};
    graf['H'] = {};

    bfs('S', 'G');

    return 0;
}
```

## 6. Aplikasi Nyata BFS

BFS memiliki berbagai aplikasi praktis di dunia nyata:
1.  **BFS dalam Labirin :** Digunakan untuk mencari jalan terpendek dari titik awal ke tujuan. Contoh: *Game* Pac-Man menghitung rute terpendek untuk mengejar pemain. Cara kerja: Mengeksplorasi semua jalur level demi level (tetangga terdekat dulu) hingga menemukan *exit*.
2.  **BFS dalam Jaringan Komputer :** Memetakan semua perangkat (PC, *server*, *router*) dalam jaringan. Cara Kerja: Mulai dari *router* utama, telusuri perangkat yang terhubung per level. Level 1: *Switch* langsung terhubung ke *router*. Level 2: PC/*server* yang terhubung ke *switch* tersebut.
3.  **BFS di Media Sosial :** Platform seperti Facebook atau LinkedIn menggunakan BFS untuk menemukan teman atau koneksi dalam jarak tertentu (misal: "Orang yang mungkin Anda kenal"). Cara kerja: Menelusuri teman langsung (level 1), lalu temannya teman (level 2), dst.
4.  **BFS dalam Transportasi & Navigasi (Google Maps, Grab, Gojek) :** BFS digunakan untuk menemukan rute terpendek dari titik A ke B dengan asumsi semua *edge* memiliki bobot yang sama (misal: jumlah jalan, bukan jarak). Contoh: Mencari jalur dengan paling sedikit persimpangan.

## 7. Kelebihan dan Kekurangan BFS

### Kelebihan
* Menjamin ditemukannya solusi yang paling baik (*complete* dan *optimal*) untuk graf tidak berbobot, artinya selalu menemukan jalur terpendek jika ada.

### Kekurangan
* Membutuhkan memori dan waktu yang cukup banyak, terutama pada graf yang sangat besar dengan banyak simpul dan *edge*, karena BFS harus menyimpan semua simpul pada level saat ini di dalam *queue*.

## 8. Kesimpulan

1.  BFS adalah algoritma penelusuran graf atau pohon yang menjelajahi simpul secara berlapis, dimulai dari simpul awal.
2.  Menggunakan struktur data *queue* untuk memastikan semua simpul dengan jarak terdekat dijelajahi lebih dulu.
3.  BFS cocok untuk mencari jalur terpendek pada graf tak berbobot.
4.  Efektif digunakan dalam berbagai aplikasi seperti *game*, peta, dan pencarian data.

---

Thank You.