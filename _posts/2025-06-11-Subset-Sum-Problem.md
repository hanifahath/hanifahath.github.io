---
title: Subset Sum Problem (SSP)
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 5]
tags: [Kelompok 5]
---

## Definisi Masalah

*Subset Sum Problem* (SSP) adalah sebuah masalah klasik yang fundamental dalam ilmu komputer, termasuk dalam kategori masalah *NP-Complete*. Ini berarti, meskipun solusinya mudah diverifikasi, menemukan solusi yang efisien untuk semua kasus bisa sangat sulit.

**Tujuannya:** Diberikan sebuah *himpunan bilangan bulat* (misalnya, angka-angka dalam sebuah daftar) dan sebuah *nilai target*, kita diminta untuk menentukan apakah ada *subset* (bagian) dari himpunan bilangan tersebut yang jumlah elemen-elemennya persis sama dengan nilai target yang diberikan.

---

## Formulasi Formal

*Subset Sum Problem* pada dasarnya adalah masalah *keputusan* (*decision problem*). Artinya, jawabannya hanya "ya" atau "tidak". Kita hanya perlu mencari tahu apakah *mungkin* untuk memilih sejumlah angka dari sekumpulan bilangan bulat sehingga totalnya sama dengan target yang ditentukan.

---

## Variasi Masalah

*Subset Sum Problem* hadir dalam berbagai bentuk, masing-masing dengan nuansa dan tantangan tersendiri:

### Bounded Subset Sum Problem

Dalam variasi ini, setiap elemen dari himpunan hanya bisa digunakan *sekali* dalam subset.

* **Contoh:**
    * Himpunan = {3, 34, 4, 12, 5, 2}
    * Target = 9
    * **Subset yang valid:** {4, 5} karena 4 + 5 = 9. Ini adalah solusi "ya".

### Partition Problem

Ini adalah kasus khusus dari SSP di mana tujuannya adalah membagi himpunan bilangan menjadi *dua subset* yang memiliki total jumlah elemen yang sama. Ini setara dengan mencari subset yang jumlahnya setengah dari total jumlah semua elemen dalam himpunan.

* **Contoh:**
    * Himpunan = {1, 5, 11, 5}
    * Total semua elemen = 1 + 5 + 11 + 5 = 22.
    * Target untuk masing-masing subset adalah setengah dari total, yaitu 11.
    * **Subset yang valid:** Satu subset bisa {11}, dan subset lainnya {1, 5, 5}. Masing-masing berjumlah 11.

### Exact k Elements Subset Sum

Variasi ini mengharuskan subset yang ditemukan tidak hanya berjumlah sama dengan target, tetapi juga harus memiliki *jumlah elemen yang tepat* sebanyak *k*.

* **Contoh:**
    * Himpunan = {1, 2, 3, 4, 5}
    * Target = 9
    * $k$ (jumlah elemen) = 2
    * **Subset yang valid:** {4, 5} karena 4 + 5 = 9 dan memiliki tepat 2 elemen.

### Unbounded Subset Sum Problem

Berbeda dengan *Bounded SSP*, di sini setiap elemen dari himpunan *boleh digunakan berulang kali* dalam subset.

* **Contoh:**
    * Himpunan = {1, 3, 4}
    * Target = 6
    * **Beberapa solusi yang mungkin:**
        * 3 + 3 = 6
        * 1 + 1 + 1 + 3 = 6

### Multi-target Subset Sum Problem

Ini melibatkan pencarian subset yang memenuhi *lebih dari satu kriteria* secara bersamaan, misalnya, kombinasi yang memenuhi batasan harga *dan* berat.

* **Contoh:**
    * Barang A: harga = 40, berat = 1 kg
    * Barang B: harga = 60, berat = 1.5 kg
    * Barang C: harga = 30, berat = 0.5 kg
    * **Target:** total harga $\leq$ 100 *dan* total berat $\leq$ 2 kg
    * **Subset yang valid:** A + C (Total harga = 40 + 30 = 70; Total berat = 1 + 0.5 = 1.5 kg).

### Approximate Subset Sum

Ketika menemukan solusi *tepat* sangat sulit atau tidak diperlukan, variasi ini mencari subset yang jumlahnya *mendekati target* yang diberikan.

* **Contoh:**
    * Himpunan = {2, 5, 10, 14}
    * Target = 15
    * **Subset yang mendekati (atau tepat):** {5, 10} karena 5 + 10 = 15.

---

## Pendekatan Penyelesaian

Meskipun *Subset Sum Problem* adalah *NP-Complete*, ada beberapa pendekatan yang dapat digunakan untuk menyelesaikannya, dengan tingkat efisiensi yang bervariasi.

### Pendekatan Rekursif

Ini adalah cara paling intuitif untuk memikirkan masalah ini, meskipun kurang efisien untuk himpunan besar.

1.  **Untuk setiap elemen:** Pada setiap langkah, kita memiliki dua pilihan untuk elemen saat ini:
    * *Sertakan* elemen tersebut dalam subset yang sedang dibangun.
    * *Abaikan* elemen tersebut.
2.  **Basis Kasus:**
    * Jika *sum* (jumlah yang tersisa untuk dicari) sama dengan 0, itu berarti kita telah menemukan subset yang jumlahnya tepat target. Jadi, hasilnya *True*.
    * Jika kita telah memeriksa semua elemen dalam himpunan (jumlah elemen *n* menjadi 0) tetapi *sum* masih belum 0, itu berarti tidak ada subset yang ditemukan. Jadi, hasilnya *False*.
3.  **Kompleksitas:** Pendekatan rekursif murni memiliki kompleksitas waktu *O(2^n)*, karena pada dasarnya ia menjelajahi semua kemungkinan subset. Ini menjadi sangat lambat untuk nilai *n* yang besar.

---

## Pendekatan Pemrograman Dinamis (*Dynamic Programming*)

Untuk mengatasi keterbatasan efisiensi rekursif murni, kita beralih ke *pemrograman dinamis*, yang memanfaatkan *memoization* atau *tabulation* untuk menghindari perhitungan berulang.

### A. *Memoization* (Pendekatan *Top-Down DP*)

Metode ini menggunakan rekursi namun menyimpan hasil dari sub-masalah yang telah dipecahkan.

* Kita menggunakan sebuah tabel (*cache*) `dp[n][sum]` untuk menyimpan hasil dari pemanggilan fungsi `solve(index, current_sum)`.
* Jika hasil untuk kombinasi `(index, current_sum)` sudah ada di *cache*, kita langsung mengembalikannya, tanpa perlu menghitung ulang.
* **Kompleksitas Waktu:** *O(n x sum)*. Ini adalah peningkatan signifikan karena setiap `(index, sum)` dihitung paling banyak sekali.
* **Kompleksitas Ruang:** *O(n x sum)*, untuk tabel *memoization*.

### B. *Tabulation* (Pendekatan *Bottom-Up DP*)

Metode ini membangun solusi dari kasus dasar ke atas, mengisi tabel secara iteratif.

* Kita membuat tabel boolean `dp[n+1][sum+1]`, di mana `dp[i][j]` akan bernilai *True* jika subset dari *i* elemen pertama dapat menjumlahkan *j*.
* **Inisialisasi:**
    * `dp[i][0] = True` untuk semua *i* (kita selalu bisa mendapatkan jumlah 0 dengan mengambil subset kosong).
    * `dp[0][j] = False` untuk semua *j > 0* (kita tidak bisa mendapatkan jumlah positif dengan 0 elemen).
* **Iterasi:** Untuk setiap elemen `arr[i-1]` dan setiap jumlah `j` dari 1 hingga *sum*:
    * `dp[i][j]` akan *True* jika:
        * `dp[i-1][j]` adalah *True* (subset tanpa elemen `arr[i-1]` sudah bisa mencapai jumlah `j`), *ATAU*
        * Jika `j` lebih besar atau sama dengan `arr[i-1]` *dan* `dp[i-1][j - arr[i-1]]` adalah *True* (subset tanpa `arr[i-1]` bisa mencapai `j - arr[i-1]`, yang berarti kita bisa menambahkan `arr[i-1]` untuk mencapai `j`).
* **Kompleksitas Waktu:** *O(n x sum)*.
* **Kompleksitas Ruang:** *O(n x sum)*.

---

## Optimasi Ruang (*Space Optimization*)

Untuk kasus di mana hanya diperlukan untuk mengetahui apakah target dapat dicapai, dan tidak perlu merekonstruksi subsetnya, kita bisa mengoptimalkan penggunaan ruang dari *O(n x sum)* menjadi *O(sum)*.

* Kita hanya perlu menggunakan *dua array 1D*: `prev[]` (untuk menyimpan hasil dari baris sebelumnya) dan `curr[]` (untuk menghitung hasil baris saat ini).
* Rumusnya menjadi: `curr[j] = prev[j] OR prev[j - arr[i]]`.
* **Kompleksitas Waktu:** Tetap *O(n x sum)*.
* **Kompleksitas Ruang:** Berkurang drastis menjadi *O(sum)*.

---

## Contoh *Bottom-Up DP*

Mari kita lihat contoh sederhana dari pendekatan *Bottom-Up DP*:

* **Himpunan:** [1, 2, 3]
* **Target:** 3

Tabel `dp` akan terlihat seperti ini (dp[i][j] menunjukkan apakah subset dari i elemen pertama bisa berjumlah j):

| sum (j) | 0     | 1     | 2     | 3     |
| :------ | :---- | :---- | :---- | :---- |
| **{} (0)** | *True* | *False* | *False* | *False* |
| **{1} (1)** | *True* | *True* | *False* | *False* |
| **{1,2} (2)** | *True* | *True* | *True* | *True* |
| **{1,2,3} (3)** | *True* | *True* | *True* | *True* |

Dari tabel, kita bisa melihat `dp[3][3]` adalah *True*, yang benar karena subset {1, 2} berjumlah 3.

---

## Aplikasi di Dunia Nyata

*Subset Sum Problem* mungkin terdengar abstrak, tetapi memiliki berbagai aplikasi penting:

* **Kriptografi:** Merupakan dasar dari beberapa skema kriptografi berbasis ransel (*knapsack-based cryptography*), meskipun banyak yang telah terbukti tidak aman.
* **Alokasi Sumber Daya:** Membantu dalam memilih subset proyek, tugas, atau item yang paling sesuai dengan anggaran atau batasan sumber daya yang ketat.
* **Genetika & Bioinformatika:** Digunakan dalam analisis kombinasi gen atau fragmen DNA untuk mengidentifikasi pola atau karakteristik tertentu.
* **Keuangan & Investasi:** Menentukan kombinasi aset atau investasi yang paling optimal untuk mencapai target pengembalian atau risiko tertentu.
* **Perancangan Permainan & Teka-Teki:** Banyak teka-teki logika atau permainan yang melibatkan pencarian kombinasi skor atau item yang memenuhi kriteria tertentu.

---

## Kesimpulan

*Subset Sum Problem* adalah masalah penting yang termasuk dalam kategori *NP-Complete*, menawarkan tantangan dan wawasan berharga dalam komputasi.

Ia hadir dalam berbagai variasi menarik seperti:
* *Bounded* dan *Unbounded*
* *Exact k elements*
* *Partition*
* *Multi-target*
* *Approximate*

Meskipun pendekatan *rekursif* murni mungkin sederhana, ia tidak efisien untuk himpunan data yang besar. Solusi yang optimal dalam hal waktu dan ruang biasanya dicapai melalui *pemrograman dinamis* (baik *memoization* maupun *tabulation*), dengan kemungkinan *optimasi ruang* lebih lanjut. Keberagaman aplikasinya menunjukkan relevansi *Subset Sum Problem* di berbagai bidang nyata, dari keamanan siber hingga genetika dan perencanaan keuangan.