---
title: "SUBSET SUM PROBLEM"
date: 2025-05-20
categories: [Desain dan Analisis Algoritma, Subset Sum Problem]
tags: [subset sum problem]
---

## Pengantar

Selamat datang di repositori ini yang akan membahas secara mendalam tentang "Subset Sum Problem" (SSP). Ini adalah salah satu masalah klasik dan fundamental dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Kita akan menyelami definisi formal, berbagai variasi masalah, pendekatan solusi menggunakan rekursi dan *dynamic programming*, serta aplikasi nyata dalam berbagai bidang.

## 1. Konsep Dasar Subset Sum Problem

Subset Sum Problem adalah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target.

Sebagai contoh formal :
* **Input** : `arr = [1, 2, 3]`, `target_sum = 3`
* **Output** : `True`
* **Penjelasan** : Terdapat subset `{1, 2}` yang jumlahnya 3.

SSP termasuk dalam *decision problem*, yaitu jenis masalah yang hanya membutuhkan jawaban "ya" atau "tidak". Inti dari masalah ini adalah mencari apakah mungkin memilih sejumlah angka dari sekumpulan bilangan bulat sehingga totalnya pas sama dengan angka target. Dalam implementasinya di dunia nyata, Subset Sum Problem bisa ditemukan dalam bidang kriptografi, pengelolaan keuangan, perencanaan sumber daya, bahkan kecerdasan buatan.

## 2. Variasi Masalah Subset Sum Problem

Subset Sum Problem memiliki beberapa variasi penting:

### a. Bounded Subset Sum Problem
Setiap elemen dalam himpunan hanya dapat digunakan sekali untuk membentuk subset yang jumlahnya sama dengan target. Artinya, jika sebuah angka muncul sekali dalam himpunan, maka kita hanya bisa menggunakannya sekali saja dalam proses pencarian solusi.
* **Contoh Kasus** : `Set = {3, 34, 4, 12, 5, 2}`, `Target = 9`. Apakah mungkin? Ya. Subset `{4, 5}` menghasilkan total 9. Kita tidak boleh menggunakan 4 atau 5 lebih dari sekali. Ini cocok untuk kasus di mana barang atau sumber daya hanya tersedia satu unit.

### b. Partition Problem
Masalah membagi sebuah himpunan bilangan bulat menjadi dua subset yang memiliki jumlah total yang sama. Secara teknis, ini setara dengan mencari subset dengan jumlah sama dengan setengah dari total seluruh elemen himpunan.
* **Contoh Kasus** : `Set = {1, 5, 11, 5}`. `Total = 22` $\rightarrow$ `Target subset = 11`. Apakah mungkin? Ya. Kita bisa buat dua subset: `{11}` dan `{1, 5, 5}` $\rightarrow$ keduanya berjumlah 11. Masalah ini penting dalam manajemen sumber daya, seperti membagi beban *server*, tugas antar tim, atau membagi *file* secara seimbang.

### c. Exact k Elements Subset Sum
Mencari subset yang jumlahnya sama dengan target dan terdiri dari tepat *k* elemen. Variasi ini menambahkan batasan tambahan yaitu jumlah elemen dalam subset harus tepat sebanyak *k* elemen.
* **Contoh Kasus** : `Set = {1, 2, 3, 4, 5}`, `Target = 9`, `k = 2`. Apakah mungkin? Ya. Subset `{4, 5}` terdiri dari 2 elemen dan jumlahnya 9. Namun subset seperti `{2, 3, 4}` juga jumlahnya 9, tapi terdiri dari 3 elemen, tidak valid. Masalah ini cocok untuk memilih tim beranggotakan *k* orang dengan total nilai tertentu, atau memilih *k* item dengan total harga tepat.

### d. Unbounded Subset Sum Problem
Setiap elemen boleh digunakan berulang kali untuk mencapai target. Ini berarti jika kita memiliki angka 3 dalam himpunan, maka kita bisa memakainya dua, tiga, atau bahkan lebih kali selama tidak melebihi target.
* **Contoh Kasus** : `Set = {1, 3, 4}`, `Target = 6`. Apakah mungkin? Ya. Beberapa kemungkinan: `1+1+1+3=6`, `3+3=6`, `2x1+4=6`.

### e. Multi-target Subset Sum Problem
Mencari subset yang memenuhi lebih dari satu kriteria, misalnya jumlah total dan batas berat. Dalam variasi ini, masalah *subset sum* menjadi lebih kompleks karena tidak hanya melibatkan satu target jumlah, tetapi lebih dari satu kriteria atau batasan yang harus dipenuhi secara bersamaan.
* **Contoh Kasus** : Set barang :
    * Barang A: harga=40, berat=1 kg
    * Barang B: harga=60, berat=1.5 kg
    * Barang C: harga=30, berat=0.5 kg
    * Target: total harga $\le 100$ dan total berat $\le 2$ kg
    * Kombinasi Barang A+C $\rightarrow$ total harga 70, berat 1.5 kg $\rightarrow$ valid.
    * Tapi A+B $\rightarrow$ harga 100, berat 2.5 kg $\rightarrow$ tidak valid karena melebihi berat.
    * Masalah ini sering muncul dalam *e-commerce* (checkout produk dengan batas ongkir) atau logistik pengiriman.

### f. Approximate Subset Sum
Jika tidak ada subset yang jumlahnya tepat sama dengan target, maka dicari subset terbaik yang mendekati target, biasanya tidak boleh melebihi.
* **Contoh Kasus**: `Set = {2, 5, 10, 14}`, `Target = 15`. Apakah mungkin? Tidak ada subset yang tepat 15, tetapi `{5, 10} = 15` (tepat). Kalau target = 16, dan tidak ada kombinasi pas, kita bisa ambil `{14}` atau `{10, 5} = 15` $\rightarrow$ solusi terbaik.

## 3. Pendekatan Solusi untuk Subset Sum Problem

Ada beberapa pendekatan untuk menyelesaikan Subset Sum Problem :

### a. Pendekatan Rekursif (Recursive Approach)
Pendekatan ini secara eksplisit mengecek semua subset. Untuk setiap elemen dalam himpunan, ada dua pilihan: sertakan elemen tersebut dalam subset atau abaikan.
* **Basis kasus** :
    * Jika `sum == 0`, berarti subset ditemukan (True).
    * Jika `n == 0` dan `sum != 0`, berarti tidak ada elemen lagi untuk dicoba dan `sum` belum tercapai (False).
* **Kompleksitas** : $O(2^n)$. Pendekatan ini tidak efisien untuk array besar karena eksplorasi eksponensial.
* **Contoh Visualisasi (dengan `arr = {2, 3, 1, 1}`, `target = 4`):**
    * `SubsetSum(arr, 4, 4)` akan mencoba dua jalur: mengambil 4 atau tidak.
    * Jika mengambil 3: `SubsetSum(arr, 3, 4-3=1)`. Ini akan terus pecah hingga menemukan `{3, 1}` yang berjumlah 4.

### b. Dynamic Programming Approach

*Dynamic Programming* menawarkan solusi yang lebih efisien dengan menghindari perhitungan berulang untuk sub-masalah yang sama.

#### i. Memoization (Top-Down DP)
Ini adalah kombinasi rekursi dengan penyimpanan hasil submasalah.
* Gunakan struktur `dp[n][sum]` untuk menyimpan hasil yang sudah dihitung (cache).
* Mengurangi pemanggilan ulang fungsi yang sama.
* Efisien untuk input sedang, namun masih membutuhkan *stack* rekursi.
* **Kompleksitas Waktu**: $O(n \times sum)$
* **Kompleksitas Memori**: $O(n \times sum)$

#### ii. Tabulation (Bottom-Up DP)
Pendekatan ini bersifat iteratif dan mulai dari kasus paling kecil.
* Buat tabel `dp[n+1][sum+1]`.
* `dp[i][j]` akan bernilai `True` jika subset dari `arr[0...i-1]` bisa menghasilkan jumlah `j`.
* **Inisialisasi** :
    * `dp[i][0] = True` (karena subset kosong selalu bisa membentuk jumlah 0).
    * `dp[0][j] = False` (tidak bisa mendapatkan jumlah `j > 0` tanpa elemen apapun).
* **Iterasi solusi** dari bawah ke atas mengisi tabel.

* **Contoh Tabel DP untuk Subset Sum (`{1, 2, 3}`, `target = 3`):**
    Tabel DP berukuran (jumlah elemen + 1) x (target + 1).

| i\j | 0     | 1     | 2     | 3     |
| :-- | :---- | :---- | :---- | :---- |
| 0   | True  | False | False | False |
| 1   | True  | True  | False | False |
| 2   | True  | True  | True  | True  |
| 3   | True  | True  | True  | True  |

    * **i=0 (tanpa elemen)**: Hanya `dp[0][0]=True`, karena subset kosong bisa membentuk 0.
    * **i=1 (elemen: [1])**:
        * `dp[1][0]=True` (subset kosong)
        * `dp[1][1]=True` (pakai angka 1)
        * `dp[1][2]=False`, `dp[1][3]=False`
    * **i=2 (elemen: [1, 2])**:
        * Tambah angka 2 ke subset:
        * `dp[2][2]=True` karena 2 bisa dibentuk (hanya pakai 2)
        * `dp[2][3]=False` (belum bisa dapat 3)
    * **i=3 (elemen: [1, 2, 3])**:
        * Sekarang bisa membentuk 3:
        * `dp[3][3]=True` karena `1+2=3`

#### iii. Optimasi Ruang pada Subset Sum (Space Optimization)
Dalam pendekatan tabulasi, kita hanya membutuhkan baris sebelumnya (`i-1`) untuk menghitung baris saat ini. Karena itu, kita bisa menghemat ruang dari $O(n \times sum)$ menjadi $O(sum)$ dengan menggunakan dua array 1D: `prev` dan `curr`.
* `prev[j]`: apakah jumlah `j` bisa dicapai dengan elemen sebelumnya.
* `curr[j]`: status jumlah `j` saat mempertimbangkan elemen saat ini.
* **Aturan pengisian** :
    * Jika `j < arr[i]`: `curr[j] = prev[j]` (elemen saat ini terlalu besar, tidak bisa diambil)
    * Jika `j >= arr[i]`: `curr[j] = prev[j]` **atau** `prev[j - arr[i]]` (bisa tanpa elemen ini, atau dengan elemen ini)
* Setelah satu iterasi, salin `curr` ke `prev`.
* **Kompleksitas Waktu** : $O(n \times sum)$
* **Kompleksitas Ruang** : $O(sum)$
* Sangat berguna saat `sum` besar, karena jauh mengurangi penggunaan memori.

## 4. Implementasi Kode C++

Berikut adalah contoh implementasi rekursif untuk Subset Sum Problem:

```cpp
#include <iostream>
#include <vector>
#include <numeric> // Untuk std::accumulate (tidak ada di PPT, tapi berguna)

using namespace std;

// Fungsi untuk mencari subset yang jumlahnya sama dengan target
void cariSubset(int arr[], int n, int index, int target, vector<int>& subset) {
    // Basis kasus: Jika target sudah 0, subset ditemukan
    if (target == 0) {
        cout << "Subset ditemukan: ";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << endl;
        return;
    }

    // Basis kasus: Jika indeks sudah mencapai akhir array atau target < 0
    if (index == n || target < 0) {
        return;
    }

    // Opsi 1: Sertakan elemen arr[index] dalam subset
    subset.push_back(arr[index]);
    cariSubset(arr, n, index + 1, target - arr[index], subset);
    subset.pop_back(); // Backtrack: hapus elemen setelah rekursi selesai

    // Opsi 2: Abaikan elemen arr[index] dan lanjutkan ke elemen berikutnya
    cariSubset(arr, n, index + 1, target, subset);
}

int main() {
    int n, target;

    cout << "Masukkan jumlah elemen: ";
    cin >> n;

    int arr[100]; // Ukuran array maksimal 100
    cout << "Masukkan elemen: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Masukkan target: ";
    cin >> target;

    vector<int> subset; // Vector untuk menyimpan subset yang sedang dibangun
    cout << "Subset yang jumlahnya " << target << ":\n";
    cariSubset(arr, n, 0, target, subset);

    return 0;
}
```

Contoh implementasi untuk Unbounded Subset Sum (setiap elemen boleh diambil berkali-kali):

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Fungsi untuk mencari subset yang jumlahnya sama dengan target
// dengan elemen boleh diambil berkali-kali (Unbounded Subset Sum)
void cariUnboundedSubset(int arr[], int n, int index, int target, vector<int>& subset) {
    // Basis kasus: Jika target sudah 0, subset ditemukan
    if (target == 0) {
        cout << "Subset ditemukan: ";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << endl;
        return;
    }

    // Basis kasus: Jika indeks sudah mencapai akhir array atau target < 0
    if (index == n || target < 0) {
        return;
    }

    // Opsi 1: Ambil elemen arr[index] (boleh diambil berkali-kali, jadi index tetap)
    subset.push_back(arr[index]);
    cariUnboundedSubset(arr, n, index, target - arr[index], subset);
    subset.pop_back(); // Backtrack: hapus elemen setelah rekursi selesai

    // Opsi 2: Skip elemen ini, Lanjut ke elemen berikutnya
    cariUnboundedSubset(arr, n, index + 1, target, subset);
}

int main() {
    int n, target;

    cout << "Masukkan jumlah elemen: ";
    cin >> n;

    int arr[100]; // Ukuran array maksimal 100
    cout << "Masukkan elemen: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Masukkan target: ";
    cin >> target;

    vector<int> subset; // Vector untuk menyimpan subset yang sedang dibangun
    cout << "Subset (unbounded) yang jumlahnya " << target << ":\n";
    cariUnboundedSubset(arr, n, 0, target, subset);

    return 0;
}
```

## 5. Aplikasi Permasalahan Subset Sum di Dunia Nyata

Subset Sum Problem memiliki berbagai aplikasi praktis :
1.  **Kriptografi** : Digunakan dalam sistem kriptografi berbasis ransel, di mana kesulitan menyelesaikan Permasalahan Subset Sum menjadi dasar keamanan kunci publik.
2.  **Alokasi Sumber Daya** : Membantu memilih subset proyek atau item agar sesuai dengan anggaran atau target tertentu.
3.  **Genetika dan Bioinformatika** : Digunakan untuk menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
4.  **Keuangan dan Investasi** : Membantu menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
5.  **Perancangan Permainan dan Teka-Teki** : Muncul dalam permainan atau teka-teki yang melibatkan pencarian kombinasi angka sesuai skor target.

## 6. Kesimpulan

Subset Sum Problem (SSP) adalah masalah dalam ilmu komputer yang bertujuan untuk menentukan apakah terdapat subset dari sekumpulan bilangan bulat yang jumlahnya sama dengan nilai target tertentu. Masalah ini tergolong dalam kategori NP-Complete dan memiliki berbagai variasi, seperti *bounded, unbounded, exact k elements, partition, multi-target,* hingga *approximate subset sum*, yang masing-masing memiliki aplikasi dan batasan berbeda. Untuk menyelesaikan SSP, digunakan pendekatan rekursif yang sederhana namun kurang efisien, serta *dynamic programming* yang lebih optimal baik dari segi waktu maupun ruang. Subset Sum memiliki aplikasi nyata dalam bidang kriptografi, keuangan, pengelolaan sumber daya, hingga kecerdasan buatan, menjadikannya masalah penting yang tidak hanya teoritis, tetapi juga relevan dalam dunia praktis.

---

Thank You.