---
title: Kahn's Algorithm:Topological Sorting pada Graf Berarah
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 9]
tags: [Kelompok 9]
---

## Apa Itu Kahn's Algorithm?

**Kahn's Algorithm** adalah sebuah metode yang digunakan untuk melakukan *topological sort* pada *graf berarah tanpa siklus* (*Directed Acyclic Graph* atau DAG). Diperkenalkan oleh Arthur B. Kahn pada tahun 1962, algoritma ini bertujuan untuk menyusun simpul-simpul (node) dalam graf menjadi urutan yang *logis*.

Secara fundamental, jika ada *edge* (arah) dari simpul U ke simpul V (U $\rightarrow$ V), maka dalam urutan topologis, simpul U *harus* muncul sebelum simpul V. Ini mencerminkan hubungan ketergantungan: V tidak dapat dikerjakan sebelum U selesai.

---

## Kegunaan Kahn's Algorithm

Kahn's Algorithm sangat vital dan digunakan dalam berbagai bidang penting, terutama di mana urutan tugas atau ketergantungan sangat krusial:

1.  **Penjadwalan Tugas (*Task Scheduling*):** Menentukan urutan optimal untuk menyelesaikan serangkaian tugas yang memiliki prasyarat.
2.  **Kompilasi Kode Program (*Compiler*):** Mengatur urutan kompilasi file-file sumber atau modul yang saling bergantung.
3.  **Sistem *Build* Otomatis (*Build Systems*):** Seperti Make atau Gradle, untuk menentukan urutan pembangunan komponen-komponen proyek.
4.  **Manajemen Dependensi Antar Modul:** Dalam pengembangan perangkat lunak, untuk menentukan urutan instalasi atau *loading* modul yang saling bergantung.

---

## Konsep Utama dalam Kahn's Algorithm

Memahami Kahn's Algorithm memerlukan pemahaman beberapa konsep dasar graf:

### 1. DAG (*Directed Acyclic Graph*)

Ini adalah jenis graf di mana semua *edge* memiliki arah (dari satu simpul ke simpul lain), dan yang terpenting, *tidak ada siklus* (*cycle*). Artinya, Anda tidak bisa memulai dari satu simpul dan kembali ke simpul itu lagi dengan mengikuti arah *edge*.
* *Contoh:* Struktur organisasi (atasan-bawahan), alur kerja proyek (tugas prasyarat).

### 2. *Acyclic* (Tanpa Siklus)

Kata kunci yang sangat penting. Sebuah graf dikatakan *acyclic* jika tidak ada *jalur melingkar*.
* *Peringatan:* Jika sebuah graf mengandung siklus, *tidak mungkin* untuk melakukan *topological sort*. Algoritma Kahn's akan dapat mendeteksi keberadaan siklus ini.

### 3. *In-Degree*

*In-degree* dari sebuah simpul adalah *jumlah *edge* yang *masuk* ke simpul tersebut*.
* Simpul dengan *in-degree* sama dengan 0 adalah simpul yang *tidak memiliki prasyarat*. Ini berarti simpul-simpul ini bisa diproses *lebih dulu* karena tidak bergantung pada simpul lain. Mereka adalah titik awal potensial dalam urutan topologis.

### 4. *Topological Sort*

*Topological sort* adalah sebuah *urutan linier* dari simpul-simpul dalam DAG sedemikian rupa sehingga untuk setiap *edge* U $\rightarrow$ V, U selalu muncul sebelum V dalam urutan.

### Ciri-ciri *Topological Sort*:

* Hanya bisa diterapkan pada *DAG*.
* Mungkin ada *banyak urutan* topologis yang sah untuk satu DAG. Misalnya, jika A tidak bergantung pada B dan B tidak bergantung pada A, maka A bisa datang sebelum B, atau B bisa datang sebelum A.
* Kompleksitas waktu algoritma Kahn's untuk *topological sort* adalah *O(V + E)*, di mana *V* adalah jumlah simpul (vertex) dan *E* adalah jumlah *edge*. Ini sangat efisien.

---

## Langkah-Langkah Kahn's Algorithm

Algoritma Kahn's bekerja secara iteratif, memanfaatkan konsep *in-degree*:

1.  **Hitung *In-Degree* Setiap Simpul:** Untuk setiap simpul dalam graf, tentukan berapa banyak *edge* yang masuk ke simpul tersebut.
2.  **Inisialisasi *Queue*:** Masukkan *semua simpul* yang memiliki *in-degree* sama dengan 0 ke dalam sebuah *queue* (antrian). Simpul-simpul ini adalah kandidat awal untuk urutan topologis.
3.  **Proses Antrian:** Selama *queue tidak kosong*, ulangi langkah-langkah berikut:
    * **Ambil Simpul:** Keluarkan satu simpul dari bagian depan *queue*.
    * **Tambahkan ke Hasil:** Tambahkan simpul ini ke daftar hasil *topological sort*.
    * **Perbarui Tetangga:** Untuk *setiap tetangga* (`V`) dari simpul yang baru saja diambil (`U`):
        * *Kurangi in-degree* dari `V` sebanyak satu (karena `U` sekarang sudah diproses, ketergantungan `V` pada `U` telah terpenuhi).
        * Jika *in-degree* dari `V` menjadi 0 setelah pengurangan, berarti `V` sekarang tidak memiliki prasyarat yang belum terpenuhi. Maka, masukkan `V` ke dalam *queue*.
4.  **Verifikasi Hasil:** Setelah *queue* kosong dan semua simpul telah diproses:
    * Jika jumlah simpul dalam daftar hasil *topological sort* sama dengan total jumlah simpul dalam graf, berarti graf tersebut valid (DAG) dan urutan topologis telah ditemukan.
    * Jika tidak (yaitu, ada beberapa simpul yang tidak pernah masuk ke *queue*), itu berarti graf tersebut *mengandung siklus* dan *topological sort* tidak mungkin dilakukan.

---

## Contoh Soal

Mari kita terapkan Kahn's Algorithm pada sebuah graf sederhana.

**Graf:**
```
1 → 2
2 → 3
1 → 4
2 → 4
```

### Hitung *In-Degree*:

| Node | *In-degree* |
| :--- | :---------- |
| 1    | 0           |
| 2    | 1           |
| 3    | 1           |
| 4    | 2           |

### Inisialisasi *Queue* Awal: `[1]`

### Proses Iteratif:

1.  **Ambil `1`:**
    * Tambahkan `1` ke hasil: `[1]`
    * Tetangga `1` adalah `2` dan `4`.
    * *In-degree* `2` berkurang jadi `0` $\rightarrow$ masukkan `2` ke *queue*.
    * *In-degree* `4` berkurang jadi `1`.
    * *Queue*: `[2]`

2.  **Ambil `2`:**
    * Tambahkan `2` ke hasil: `[1, 2]`
    * Tetangga `2` adalah `3` dan `4`.
    * *In-degree* `3` berkurang jadi `0` $\rightarrow$ masukkan `3` ke *queue*.
    * *In-degree* `4` berkurang jadi `0` $\rightarrow$ masukkan `4` ke *queue*.
    * *Queue*: `[3, 4]`

3.  **Ambil `3`:**
    * Tambahkan `3` ke hasil: `[1, 2, 3]`
    * `3` tidak punya tetangga.
    * *Queue*: `[4]`

4.  **Ambil `4`:**
    * Tambahkan `4` ke hasil: `[1, 2, 3, 4]`
    * `4` tidak punya tetangga.
    * *Queue*: `[]` (Kosong)

### Hasil Akhir:

* Urutan topologis yang ditemukan adalah **`[1, 2, 3, 4]`**.

---

## Simulasi Kahn's Algorithm

Secara sederhana, Kahn's Algorithm dapat divisualisasikan sebagai berikut:

1.  Kita mulai dari simpul-simpul yang *tidak bergantung* pada simpul lain (yaitu, *in-degree* = 0). Ini adalah "tugas" yang bisa langsung dimulai.
2.  Setelah sebuah "tugas" selesai diproses, kita memberi tahu semua "tugas" lain yang bergantung padanya bahwa salah satu prasyarat mereka telah terpenuhi. Ini diwakili dengan mengurangi *in-degree* dari tetangga.
3.  Ketika *in-degree* sebuah "tugas" menjadi 0, itu berarti semua prasyaratnya sudah selesai, dan "tugas" itu kini *bebas untuk diproses*.
4.  Jika pada akhirnya ada simpul yang *in-degree*-nya tidak pernah mencapai 0, itu menandakan adanya siklus. Ini seperti sekelompok tugas yang saling bergantung satu sama lain secara melingkar, sehingga tidak ada yang bisa dimulai.

---

## Kesimpulan

**Kahn's Algorithm** adalah metode yang *efisien* dan *elegan* untuk menyusun urutan tugas atau elemen berdasarkan ketergantungan logis dalam sebuah *Directed Acyclic Graph (DAG)*.

* Algoritma ini diterapkan secara luas di banyak *sistem teknologi modern* untuk *penjadwalan*, *kompilasi*, dan *manajemen dependensi*.
* Salah satu keunggulan pentingnya adalah kemampuannya untuk secara otomatis *mendeteksi keberadaan siklus* dalam graf.
* Dengan kompleksitas waktu *O(V + E)*, Kahn's Algorithm sangat efisien untuk memproses graf besar.
* Penting untuk diingat bahwa *Kahn's Algorithm tidak bisa digunakan untuk graf yang mengandung siklus*, karena topological sort memang tidak mungkin dilakukan pada graf tersebut.