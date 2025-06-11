---
title: Dijkstra's Algorithm:Menemukan Jalur Terpendek dalam Graf
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 10]
tags: [Kelompok 10]
---

## Pengertian Dijkstra's Algorithm

**Dijkstra's Algorithm** adalah sebuah algoritma penemuan jalur terpendek yang sangat terkenal, dikembangkan oleh ilmuwan komputer asal Belanda, Edsger Dijkstra, dan pertama kali dipublikasikan pada tahun 1959.

Algoritma ini dirancang khusus untuk menemukan *jalur terpendek* dari satu *simpul awal* (sumber) ke *semua simpul lainnya* dalam sebuah graf. Penting untuk dicatat bahwa algoritma ini bekerja dengan efisien pada *graf berarah* (*directed graph*) atau *graf tak berarah* (*undirected graph*) dengan kondisi semua *bobot sisi* (atau *edge weight*) harus bernilai *positif atau nol* ($\ge 0$).

Dijkstra's Algorithm termasuk dalam kategori *Algoritma Greedy* (*Greedy Algorithm*). Ini berarti, di setiap langkahnya, algoritma selalu memilih solusi yang tampak *terbaik secara lokal* dengan harapan bahwa serangkaian pilihan lokal terbaik ini akan menghasilkan *solusi global yang optimal*.

---

## Tujuan Dijkstra's Algorithm

Tujuan utama dari Dijkstra's Algorithm adalah untuk secara sistematis menentukan *jalur terpendek* (dengan total bobot paling kecil) dari sebuah simpul awal yang telah ditentukan ke setiap simpul lain yang dapat dijangkau dalam graf berbobot positif.

Sebagai contoh konkret, algoritma ini sangat fundamental dalam kasus-kasus seperti:
* Menentukan *rute tercepat* di jalan raya.
* Menemukan *jalur termurah* dalam jaringan pengiriman.
* Mengidentifikasi *jalur paling efisien* dalam sistem transportasi publik, semuanya dari titik A ke titik B.

---

## Kegunaan Dijkstra's Algorithm dalam Kehidupan Nyata

Dijkstra's Algorithm memiliki aplikasi yang luas dan vital di berbagai sektor teknologi dan kehidupan sehari-hari, seringkali tanpa kita sadari.

1.  **Navigasi & Pemetaan Digital:** Ini adalah salah satu aplikasi paling jelas. Algoritma ini digunakan secara intensif oleh aplikasi seperti *Google Maps*, *Waze*, dan perangkat *GPS* untuk mencari rute tercepat atau terpendek antar lokasi, dengan mempertimbangkan faktor-faktor seperti jarak, waktu tempuh, atau bahkan kepadatan lalu lintas.
2.  **Jaringan Komputer & Telekomunikasi:** Dalam infrastruktur jaringan, Dijkstra's Algorithm digunakan dalam protokol *routing* seperti *OSPF* (*Open Shortest Path First*) untuk menentukan jalur transmisi data yang paling efisien antara server, router, dan perangkat lainnya. Ini memastikan data sampai tujuan dengan cepat dan minim *latency*.
3.  **Pengembangan Game (*Game Development*):** Dalam permainan video, algoritma ini membantu karakter non-pemain (*Non-Player Character* - NPC) atau *game AI* dalam memilih rute terbaik untuk bergerak menuju target, menghindari rintangan, atau menemukan jalan keluar dari labirin secara logis dan cepat.
4.  **Logistik & Transportasi:** Perusahaan logistik dan transportasi mengandalkan algoritma ini untuk merancang rute distribusi barang yang paling hemat waktu dan biaya, mengoptimalkan jadwal pengiriman, dan mengurangi konsumsi bahan bakar.
5.  **Kecerdasan Buatan (AI):** Selain dalam navigasi robot untuk perencanaan rute dan navigasi cerdas, prinsip Dijkstra juga dapat ditemukan dalam sistem rekomendasi, di mana ia membantu menemukan "jalur" atau hubungan terpendek antara preferensi pengguna.

---

## Cara Kerja Dijkstra's Algorithm

Dijkstra's Algorithm bekerja secara iteratif, membangun jalur terpendek selangkah demi selangkah.

### Langkah-langkah Kerja Algoritma:

1.  **Inisialisasi:**
    * *Pilih simpul awal* (sumber). Beri simpul ini nilai jarak 0. Ini adalah titik awal perhitungan kita.
    * Berikan *nilai awal tak terhingga* ($\infty$) kepada semua simpul lain. Ini merepresentasikan bahwa jarak ke simpul-simpul tersebut masih belum diketahui.
    * Buat sebuah set (atau *priority queue*) untuk menyimpan simpul-simpul yang belum diproses.

2.  **Periksa Semua Tetangga Simpul Aktif:**
    * Dari simpul yang sedang aktif (yang memiliki jarak terkecil dan belum selesai diproses), kunjungi *semua tetangga* langsungnya.
    * Untuk setiap tetangga, *hitung total jarak* dari simpul awal ke simpul tetangga tersebut melalui simpul aktif saat ini (jarak simpul awal ke simpul aktif + bobot sisi dari simpul aktif ke tetangga).

3.  **Perbarui Jarak Minimum:**
    * Jika jalur baru yang dihitung lebih pendek dari jarak minimum yang sudah tercatat untuk simpul tetangga tersebut, maka *perbarui nilai jarak* simpul tetangga dengan nilai yang lebih pendek ini.

4.  **Tandai Simpul sebagai "Terkunci":**
    * Setelah semua tetangga dari simpul aktif saat ini diperbarui (atau tidak ada lagi yang bisa diperbarui), *tandai simpul aktif tersebut sebagai "terkunci"* (atau 'visited'). Ini berarti jarak terpendek dari simpul awal ke simpul ini sudah final dan tidak akan diubah lagi. Simpul ini tidak akan diperiksa kembali.

5.  **Ulangi Proses:**
    * Pindah ke simpul berikutnya yang *belum terkunci* dan memiliki *jarak terkecil* dari simpul awal.
    * Ulangi langkah 2 sampai 4 sampai *semua simpul selesai diproses* (terkunci) atau *simpul tujuan telah tercapai dan terkunci*.

---

## 5 Langkah Menggunakan Metode Tabel

Untuk mempermudah perhitungan manual dan visualisasi Dijkstra's Algorithm, kita bisa menggunakan pendekatan tabel.

### Langkah-langkah dengan Tabel:

1.  **Buat Tabel:** Buat sebuah tabel di mana barisnya merepresentasikan setiap simpul dalam graf, dan kolomnya berisi informasi seperti jarak saat ini dari simpul awal, serta simpul sebelumnya dalam jalur.
2.  **Pilih Simpul Awal dan Tujuan:** Tentukan simpul sumber dan simpul tujuan yang ingin Anda cari jalurnya. Pastikan ada jalur yang memungkinkan di antara keduanya.
3.  **Hitung Jarak Awal:** Dari simpul awal, hitung jarak langsung ke setiap simpul tetangganya. Perbarui nilai jarak di tabel jika jarak ini lebih pendek dari $\infty$.
4.  **Pilih Jarak Terpendek & Tetapkan Pusat:** Dari semua simpul yang belum 'terkunci', pilih simpul dengan jarak minimum yang belum final. Tetapkan simpul ini sebagai 'pusat' perhitungan untuk iterasi berikutnya dan 'kunci' simpul ini.
5.  **Ulangi:** Terus ulangi langkah 3 dan 4 sampai semua simpul telah mendapat jarak minimum yang final dari simpul awal (atau sampai simpul tujuan telah 'terkunci').

---

## Kesimpulan

**Dijkstra's Algorithm** adalah salah satu algoritma paling *penting* dan *kuat* dalam ilmu komputer, khususnya dalam bidang teori graf untuk menemukan jalur terpendek dalam graf berbobot positif.

Mengikuti prinsip *Greedy*, algoritma ini:
* Membangun solusi secara *langkah demi langkah* menuju hasil yang *optimal*.
* Terbukti sangat *efisien* dan digunakan secara luas dalam berbagai sektor teknologi dan aspek kehidupan nyata kita, dari navigasi sehari-hari hingga infrastruktur jaringan yang kompleks.
* **Menjamin** untuk menemukan jalur yang paling *singkat* dan *logis* antara dua titik dalam kondisi bobot sisi positif.

Tanpa Dijkstra, mungkin kita masih nyasar di jalan atau data kita akan mengitari dunia dengan jalur yang tidak efisien!