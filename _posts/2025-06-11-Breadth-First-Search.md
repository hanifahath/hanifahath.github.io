---
title: Breadth-First Search (BFS)
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 7]
tags: [Kelompok 7]
---

## Deskripsi

**Breadth-First Search (BFS)** adalah sebuah algoritma fundamental untuk menelusuri atau mencari di dalam *graf* atau *pohon* secara *berlapis* (*level-order*). Prinsip inti dari BFS adalah menjelajahi semua simpul yang *paling dekat* dengan simpul awal terlebih dahulu, sebelum berpindah untuk menjelajahi simpul-simpul yang jaraknya *lebih jauh*.

*Ilustrasinya* sederhana: bayangkan Anda sedang mencari ruang kelas tertentu di sebuah gedung bertingkat. Anda akan memeriksa seluruh ruangan di lantai 1, lalu beralih ke seluruh ruangan di lantai 2, kemudian lantai 3, dan seterusnya. Anda tidak akan langsung naik ke lantai 5 sebelum semua ruangan di lantai di bawahnya diperiksa.

Algoritma ini memiliki banyak *aplikasi umum*, termasuk:
* Pencarian rute tercepat dalam berbagai jenis permainan.
* Penelusuran dan analisis jaringan sosial.
* Navigasi dan perencanaan rute pada peta digital.

---

## Konsep Dasar

BFS mengandalkan struktur data tertentu dan mengikuti pola traversal yang spesifik.

* **Struktur Data:** BFS secara esensial menggunakan *antrian* (*queue*) sebagai struktur data utamanya. Antrian bekerja dengan prinsip *FIFO* (*First-In-First-Out*), artinya elemen pertama yang masuk akan menjadi yang pertama keluar.
* **Traversal:** Algoritma ini melakukan *traversal level-order*, yang berarti ia akan menjelajahi semua simpul pada satu tingkat (level) sebelum pindah ke simpul-simpul pada tingkat berikutnya.
* **Proses:** Eksplorasi dimulai dari simpul awal, kemudian meluas ke semua tetangga langsungnya, lalu tetangga dari tetangga tersebut, dan seterusnya, menyebar seperti gelombang air.

---

## Langkah-langkah Algoritma BFS

Proses kerja BFS dapat dipecah menjadi serangkaian langkah yang jelas:

1.  **Tentukan Simpul Awal:** Pilih satu simpul sebagai titik keberangkatan untuk penelusuran.
2.  **Inisialisasi Antrian:** Masukkan simpul awal ini ke dalam *antrian* (queue).
3.  **Proses Antrian:** Selama *antrian tidak kosong*, ulangi langkah-langkah berikut:
    a.  **Ambil Simpul:** Keluarkan simpul dari bagian depan *antrian*. Simpul ini adalah simpul yang sedang kita proses.
    b.  **Tandai "Visited":** Tandai simpul yang baru saja diambil sebagai *sudah dikunjungi* (*visited*) untuk mencegah penelusuran ulang dan siklus tak terbatas.
    c.  **Cek Tujuan:** Jika simpul yang sedang diproses adalah *simpul tujuan* (*goal node*) yang kita cari, maka algoritma selesai dan jalur telah ditemukan (atau keberadaan tujuan dikonfirmasi).
    d.  **Tambahkan Tetangga:** Jika simpul bukan tujuan, kunjungi *semua tetangga* langsungnya yang *belum dikunjungi*. Untuk setiap tetangga yang belum dikunjungi ini, masukkan ke dalam *antrian*.
4.  **Ulangi:** Lanjutkan langkah 3 hingga simpul tujuan ditemukan atau *antrian kosong* (yang berarti semua simpul yang dapat dijangkau dari simpul awal telah dieksplorasi).

---

## Contoh Simulasi BFS

Mari kita lihat bagaimana BFS bekerja pada sebuah graf sederhana.

**Graf:**
```
S
| \
A   B
|   | \
C   D   E
|   |   |
F   G   H
```
Anggap S adalah simpul awal.

**Status Antrian (*Queue*) Selama Proses:**

* **[S]** (Awal)
* **[A, B]** (S diambil, tetangga A, B ditambahkan)
* **[B, C, D]** (A diambil, tetangga C, D ditambahkan)
* **[C, D, E]** (B diambil, tetangga E ditambahkan)
* **[D, E, F]** (C diambil, tetangga F ditambahkan)
* **[E, F, G]** (D diambil, tetangga G ditambahkan)
* **[F, G, H]** (E diambil, tetangga H ditambahkan)
* ...dan seterusnya hingga antrian kosong atau tujuan ditemukan.

**Urutan Simpul yang Dikunjungi (*Visited Order*):**

*S* $\rightarrow$ *A* $\rightarrow$ *B* $\rightarrow$ *C* $\rightarrow$ *D* $\rightarrow$ *E* $\rightarrow$ *F* $\rightarrow$ *H* $\rightarrow$ *G* (urutan ini bisa sedikit bervariasi tergantung pada bagaimana tetangga ditambahkan, tetapi lapisan akan tetap sama).

---

## Contoh Kode BFS (Pseudocode)

Berikut adalah *pseudocode* umum yang menggambarkan implementasi BFS.

```pseudocode
void BFS(Graph g, Node start) {
    Queue<Node> queue; // Gunakan antrian untuk menyimpan node yang akan dikunjungi
    Set<Node> visited; // Gunakan set untuk melacak node yang sudah dikunjungi

    // Inisialisasi: masukkan simpul awal ke antrian dan tandai sudah dikunjungi
    queue.enqueue(start);
    visited.add(start);

    // Lanjutkan selama antrian tidak kosong
    while (!queue.isEmpty()) {
        Node current = queue.dequeue(); // Ambil simpul dari depan antrian
        process(current); // Lakukan sesuatu dengan simpul saat ini (misal: cetak)

        // Jelajahi semua tetangga dari simpul saat ini
        for (Node neighbor : g.neighbors(current)) {
            // Jika tetangga belum dikunjungi
            if (!visited.contains(neighbor)) {
                queue.enqueue(neighbor); // Tambahkan tetangga ke antrian
                visited.add(neighbor);   // Tandai tetangga sebagai sudah dikunjungi
            }
        }
    }
}
```

---

## Aplikasi Nyata BFS

BFS bukan hanya konsep teoretis; ia memiliki beragam aplikasi praktis di dunia nyata.

### 1. BFS dalam Labirin / Game

* BFS ideal untuk mencari *jalan terpendek* dari satu titik ke titik lain dalam labirin atau grid permainan *tak berbobot*.
* **Contoh:** Karakter *Pac-Man* sering menggunakan varian BFS untuk menghitung rute terpendek menuju pelet atau menghindari hantu.

### 2. BFS di Media Sosial

* Algoritma ini sangat cocok untuk menemukan teman atau koneksi dalam "jarak" tertentu (misalnya, teman dari teman, teman dari teman dari teman).
* **Contoh:** Fitur "Orang yang mungkin Anda kenal" di *Facebook* atau *LinkedIn* sering memanfaatkan prinsip BFS untuk menemukan koneksi potensial.

### 3. BFS di Jaringan Komputer

* Dapat digunakan untuk *memetakan perangkat* dalam sebuah jaringan, mengidentifikasi semua perangkat yang terhubung dan hubungan di antaranya.
* **Ilustrasi:** Dari sebuah *switch* (level 1), BFS dapat menemukan semua PC atau server yang terhubung langsung (level 2), lalu perangkat yang terhubung ke PC/server tersebut (level 3), dan seterusnya.

### 4. BFS dalam Transportasi dan Navigasi

* BFS efektif untuk menemukan *rute terpendek* dalam peta yang *tidak memiliki bobot* (misalnya, setiap persimpangan atau ruas jalan memiliki "biaya" yang sama).
* **Contoh:** Layanan seperti *Google Maps*, *Grab*, atau *Gojek* dapat menggunakan BFS (atau variannya) untuk menghitung jalur dengan jumlah persimpangan atau "langkah" paling sedikit.

---

## Kelebihan dan Kekurangan

Meskipun kuat, BFS juga memiliki batasan.

### ✅ Kelebihan

1.  **Menjamin Solusi Optimal:** Untuk *graf tak berbobot*, BFS dijamin akan menemukan *jalur terpendek* dari simpul awal ke simpul tujuan. Ini adalah keunggulan besar.
2.  **Sederhana dan Mudah Diimplementasikan:** Konsepnya mudah dipahami dan diwujudkan dalam kode.

### ❌ Kekurangan

1.  **Memori dan Waktu Besar:** Untuk graf yang sangat besar dan padat, BFS dapat memerlukan *memori* yang signifikan untuk menyimpan *antrian* simpul yang belum dieksplorasi. Selain itu, waktu yang dibutuhkan bisa menjadi besar karena ia harus menjelajahi semua simpul pada setiap level.
2.  **Tidak Efisien untuk Graf Berbobot:** Jika setiap "ruas" atau "tepi" dalam graf memiliki biaya atau bobot berbeda (misalnya, waktu perjalanan), BFS tidak akan selalu menemukan jalur terpendek dalam arti "biaya terendah". Untuk kasus ini, algoritma lain seperti *Dijkstra's Algorithm* lebih cocok.

---

## Kesimpulan

**Breadth-First Search (BFS)** adalah algoritma penelusuran graf atau pohon yang fundamental, bekerja berdasarkan prinsip *level-order traversal*. Dengan memanfaatkan struktur data *antrian*, BFS secara sistematis menjelajahi simpul yang paling dekat terlebih dahulu sebelum memperluas pencariannya.

Kekuatan utama BFS terletak pada kemampuannya untuk menemukan *jalur terpendek* dalam graf *tak berbobot*. Karena keandalannya ini, BFS banyak digunakan dalam berbagai aplikasi dunia nyata, mulai dari *pengembangan game* dan *navigasi peta* hingga *analisis media sosial* dan *manajemen jaringan komputer*.

Apakah Anda tertarik untuk membandingkan BFS dengan algoritma penelusuran graf lainnya, seperti Depth-First Search (DFS)?