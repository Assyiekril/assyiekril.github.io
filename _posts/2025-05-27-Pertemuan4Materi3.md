---
title: "DEPTH FIRST SEARCH"
date: 2025-05-27
categories: [Desain dan Analisis Algoritma, Depth First Search]
tags: [depth first search]
---

## Pengantar

Selamat datang di repositori yang akan membahas secara mendalam tentang "Depth-First Search" (DFS). Ini adalah salah satu algoritma pencarian atau penelusuran graf atau pohon yang fundamental dalam ilmu komputer, dikenal karena pendekatannya yang mendalam dalam menjelajahi simpul-simpul. Dalam materi ini, kita akan mempelajari definisi DFS, prinsip dasarnya, cara kerja melalui simulasi, contoh implementasi kode, serta kelebihan dan kekurangannya.

## 1. Apa itu Depth-First Search (DFS)?

Depth-First Search (DFS) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (*backtrack*) dan melanjutkan ke cabang berikutnya.

## 2. Prinsip Utama DFS

DFS menggunakan struktur data tumpukan (*stack*) yang mengikuti prinsip LIFO (*Last In, First Out*).

**Langkah-langkah Pencarian :**
1.  Masukkan simpul (node) akar ke dalam *stack*.
2.  Ambil node dari *stack* teratas, lalu cek apakah node tersebut merupakan solusi?
    * Jika node merupakan solusi, pencarian selesai dan hasil dikembalikan.
    * Jika node bukan solusi, masukkan seluruh node anak ke dalam *stack*.
3.  Jika *stack* kosong dan setiap node sudah dicek, pencarian berakhir.
4.  Jika *stack* tidak kosong, ulangi pencarian mulai langkah ke-2.

## 3. Contoh Kasus

Diberikan sebuah graf, jika penelusuran dilakukan menggunakan Depth-First Search (DFS) dari simpul awal 1, mari kita lihat beberapa kemungkinan urutan kunjungan simpul.

**Graf :**
(Graf visual dengan node 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 dan edge yang sesuai)
* 1 terhubung ke 2
* 2 terhubung ke 1, 4, 5
* 3 terhubung ke 5
* 4 terhubung ke 2, 7
* 5 terhubung ke 2, 3, 6
* 6 terhubung ke 5, 7, 8, 9
* 7 terhubung ke 4, 6
* 8 terhubung ke 6
* 9 terhubung ke 6, 10
* 10 terhubung ke 9

**Kemungkinan DFS (Urutan Eksplorasi Berbeda) dari simpul awal 1 :**

1.  1, 2, 4, 7, 6, 5, 3, 9, 10, 8 (Contoh urutan, bisa bervariasi tergantung prioritas tetangga)
2.  1, 2, 5, 6, 7, 4, 9, 10, 8, 3 (Contoh urutan, bisa bervariasi tergantung prioritas tetangga)
3.  1, 2, 5, 6, 9, 10, 7, 4, 8, 3 (Contoh urutan, bisa bervariasi tergantung prioritas tetangga)

**Contoh Kasus dengan Akhir 10 :**
Jika penelusuran dilakukan menggunakan DFS dari simpul awal 1, dengan tujuan akhir 10, salah satu kemungkinan urutan kunjungan simpul adalah:
1, 2, 4, 6, 9, 10 (Jika 10 adalah tujuan, pencarian berhenti di sini)

## 4. Kelebihan & Kekurangan DFS

### Kelebihan
* **Penggunaan Memori Lebih Efisien :** Dibandingkan BFS, DFS menggunakan memori yang lebih sedikit karena tidak perlu menyimpan semua simpul pada satu level dalam memori.
* **Mudah Diimplementasikan :** Algoritma ini relatif mudah diimplementasikan, baik secara rekursif maupun iteratif menggunakan *stack*.
* **Cocok untuk Menemukan Solusi Kedalaman Maksimal :** Ideal untuk masalah di mana solusi cenderung berada di kedalaman yang lebih jauh dari simpul awal.
* **Digunakan dalam Banyak Algoritma Penting :** Merupakan dasar untuk banyak algoritma graf lainnya, seperti mencari komponen terhubung, pengurutan topologi, dan mendeteksi siklus.

### Kekurangan
* **Tidak Menjamin Solusi Terbaik :** Jika ada banyak solusi, DFS mungkin menemukan solusi yang bukan jalur terpendek atau optimal jika graf tidak berbobot.
* **Bisa Masuk ke Infinite Loop (pada Graf Siklik) :** Jika tidak ada mekanisme untuk melacak simpul yang sudah dikunjungi, DFS bisa terjebak dalam siklus tak terbatas pada graf yang memiliki siklus.
* **Kurang Efisien di Graf Luas tapi Dangkal :** Pada graf yang sangat luas tetapi dangkal (banyak cabang di level awal), DFS mungkin membutuhkan waktu lebih lama untuk menemukan solusi dekat simpul awal.
* **Tidak Cocok untuk Semua Masalah :** Ada jenis masalah tertentu (misalnya, mencari jalur terpendek pada graf tak berbobot) di mana BFS lebih cocok.

## 5. Implementasi Kode C++

Berikut adalah contoh implementasi DFS dalam C++ :

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_map> // Biasanya digunakan untuk graf yang lebih fleksibel

// Fungsi DFS
void DFS(int start, std::vector<std::vector<int>>& graph, std::vector<bool>& visited) {
    std::stack<int> s; // Menggunakan stack untuk DFS
    s.push(start); // Masukkan node awal ke stack

    while (!s.empty()) {
        int node = s.top(); // Ambil node teratas dari stack
        s.pop(); // Hapus node dari stack

        // Jika node belum dikunjungi, kunjungi dan tandai
        if (!visited[node]) {
            std::cout << node << " "; // Cetak node yang dikunjungi
            visited[node] = true; // Tandai sebagai sudah dikunjungi
        }

        // Kunjungi tetangga node saat ini
        // Iterasi dari akhir ke awal untuk meniru perilaku rekursif DFS
        // agar node "paling kiri" (terkecil) diproses lebih dulu jika ada multiple paths
        for (int i = graph[node].size() - 1; i >= 0; --i) {
            int neighbor = graph[node][i];
            if (!visited[neighbor]) {
                s.push(neighbor); // Masukkan tetangga yang belum dikunjungi ke stack
            }
        }
    }
}

int main() {
    // Jumlah node dalam graf (misalnya 6 node, dari 0 sampai 5)
    int n = 6; 
    
    // Representasi graf menggunakan adjacency list
    // graph[i] akan berisi daftar node yang terhubung dengan node i
    std::vector<std::vector<int>> graph(n);

    // Menambahkan edge (sisi) ke graf
    // Contoh graf dari PPT, namun disesuaikan menjadi 0-indexed untuk array
    // (0 terhubung ke 1)
    graph[0].push_back(1);
    // (0 terhubung ke 2)
    graph[0].push_back(2);
    // (1 terhubung ke 0)
    graph[1].push_back(0);
    // (1 terhubung ke 3)
    graph[1].push_back(3);
    // (1 terhubung ke 4)
    graph[1].push_back(4);
    // (2 terhubung ke 0)
    graph[2].push_back(0);
    // (2 terhubung ke 5)
    graph[2].push_back(5);
    // (3 terhubung ke 1)
    graph[3].push_back(1);
    // (4 terhubung ke 1)
    graph[4].push_back(1);
    // (5 terhubung ke 2)
    graph[5].push_back(2);

    // Vektor untuk melacak node yang sudah dikunjungi (inisialisasi dengan false)
    std::vector<bool> visited(n, false);

    // Memulai DFS dari node 0 (seperti contoh 1 di slide, diasumsikan 1-indexed di slide berarti 0-indexed di kode)
    // Jika ingin mulai dari node 2 (seperti contoh di slide), panggil DFS(2, graph, visited);
    std::cout << "DFS traversal starting from node 0 (analogous to 1 in slides): ";
    DFS(0, graph, visited);
    std::cout << std::endl;

    // Reset visited for another traversal if needed
    std::fill(visited.begin(), visited.end(), false);
    std::cout << "DFS traversal starting from node 2: ";
    DFS(2, graph, visited);
    std::cout << std::endl;

    return 0;
}
```

**Catatan :** Dalam contoh kode C++ di atas, graf diasumsikan berbasis 0-indexed (node 0, 1, 2, ... N-1). Jika node di PPT adalah 1-indexed (node 1, 2, ... N), maka penyesuaian mungkin diperlukan pada pemanggilan `DFS` dan representasi graf.

## 6. Kesimpulan

Depth-First Search (DFS) merupakan algoritma penelusuran pada struktur data graf atau pohon yang menjelajahi simpul sedalam mungkin sebelum kembali (*backtracking*) dan melanjutkan ke simpul lainnya. Proses penelusuran ini dilakukan dengan menggunakan struktur data *stack* yang mengikuti prinsip LIFO (*Last In, First Out*). DFS dimulai dari simpul akar, kemudian terus menyusuri anak-anak simpul hingga mencapai simpul terdalam, sebelum kembali ke simpul sebelumnya untuk menjelajahi cabang lain yang belum dikunjungi. DFS cocok digunakan untuk pencarian solusi pada kedalaman maksimal dan dapat menghasilkan jalur penelusuran yang berbeda tergantung pada urutan pemrosesan simpul.

---

Thank You.