---
title: Fractional Knapsack Problem
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 2]
tags: [Kelompok 2, Algorithm, C++]
---

##  Knapsack Problem

adalah masalah optimasi klasik yang menantang kita untuk memilih sekumpulan barang agar total nilai yang dibawa menjadi maksimal, namun tidak melebihi kapasitas yang tersedia dalam sebuah "tas" atau knapsack.

Ada dua variasi utama dari masalah Knapsack:

- *0/1 Knapsack*: Di sini, setiap barang harus diambil secara seluruhnya atau tidak sama sekali. Tidak ada pilihan untuk mengambil sebagian. Masalah ini umumnya diselesaikan menggunakan pemrograman dinamis (dynamic programming).
- *Fractional Knapsack*: Dalam variasi ini, barang boleh diambil sebagian (misalnya, setengah dari sebuah apel). Ini adalah masalah yang bisa diselesaikan dengan algoritma greedy yang jauh lebih sederhana dan efisien.

### Memahami Fractional Knapsack

Fokus kita kali ini adalah *Fractional Knapsack*. Tujuan utamanya adalah memaksimalkan nilai total barang yang dapat kita masukkan ke dalam knapsack dengan kapasitas terbatas.

## Karakteristik Utama
- Pembagian Barang: Barang dapat dipotong atau diambil sebagian. Ini adalah perbedaan krusial yang membuat pendekatan greedy menjadi mungkin.
- Efisiensi: Kita tidak perlu menguji semua kemungkinan kombinasi seperti pada 0/1 Knapsack.
- Optimal dengan Greedy: Sifat masalah ini secara alami cocok untuk diselesaikan menggunakan algoritma greedy.

## Fitur Masalah
- Berat dan Nilai: Setiap barang memiliki dua atribut penting: berat (weight) dan nilai (value).
- Kapasitas Terbatas: Tas (knapsack) memiliki kapasitas maksimum yang tidak boleh dilampaui.
Fleksibilitas Fraksional: Kemampuan untuk mengambil barang sebagian adalah kunci.
- Greedy is Enough: Pendekatan greedy terbukti optimal karena pilihan lokal yang terbaik akan mengarah pada solusi global yang optimal.

### Strategi Penyelesaian: Algoritma Greedy

Untuk memecahkan *Fractional Knapsack Problem*, kita mengikuti strategi greedy yang lugas dan efektif.

## Langkah-langkah Penerapan
1. *Hitung Rasio Nilai per Berat*: Untuk setiap item, kita tentukan seberapa "berharga" per unit beratnya. Ini dihitung dengan rumus:
Rasio= Nilai / Berat
2. Urutkan Item: Setelah mendapatkan rasio untuk semua item, urutkan item tersebut dari yang memiliki rasio tertinggi hingga terendah. Ini memastikan kita selalu memilih item yang paling "menguntungkan" terlebih dahulu.
3. Ambil Item: Mulailah mengisi knapsack dengan mengambil sebanyak mungkin dari item yang memiliki rasio tertinggi. Terus lakukan ini sampai kapasitas knapsack terpenuhi atau item habis.
4. Ambil Sebagian (Jika Perlu): Jika setelah mengambil beberapa item secara penuh kapasitas knapsack belum penuh, dan item berikutnya terlalu berat untuk diambil seluruhnya, kita ambil sebagian dari item tersebut hingga knapsack terisi penuh.

### Analisis Kompleksitas
Efisiensi adalah salah satu kekuatan utama dari solusi greedy ini.

## Kompleksitas Waktu
1. Pengurutan Item: Langkah yang paling memakan waktu adalah pengurutan item berdasarkan rasio nilai/berat. Ini membutuhkan waktu O(nlogn), di mana n adalah jumlah item.
2. Pengisian Knapsack: Setelah diurutkan, proses pengisian knapsack hanya memerlukan satu lintasan melalui daftar item, sehingga kompleksitasnya adalah O(n).

*Total Kompleksitas Waktu*: Secara keseluruhan, algoritma Fractional Knapsack memiliki kompleksitas waktu O(n log n), menjadikannya sangat efisien bahkan untuk dataset yang besar.

### Aplikasi Fractional Knapsack di Dunia Nyata
Meskipun terlihat abstrak, Fractional Knapsack Problem memiliki banyak aplikasi praktis:

1. Penjadwalan Sumber Daya Terbatas: Memilih proyek atau tugas mana yang akan dikerjakan untuk memaksimalkan output dengan anggaran atau waktu yang terbatas.
2. Investasi Portofolio: Mengalokasikan dana ke berbagai aset investasi untuk memaksimalkan keuntungan berdasarkan rasio risiko/keuntungan.
3. Alokasi Bandwidth Jaringan: Menentukan bagaimana mendistribusikan bandwidth yang terbatas ke berbagai pengguna atau aplikasi untuk mengoptimalkan kinerja jaringan.
4. Optimasi Logistik: Memuat kargo ke dalam kendaraan pengangkut untuk memaksimalkan nilai barang yang dibawa, terutama ketika barang dapat dimuat dalam jumlah fraksional (misalnya, cairan atau bahan curah).

### Menggali Lebih Dalam: Algoritma Greedy

## Ciri Khas Algoritma Greedy
- Pilihan Optimal Lokal: Pada setiap langkah, algoritma greedy membuat pilihan yang tampak terbaik pada saat itu, tanpa mempertimbangkan konsekuensi di masa depan.
- Tanpa Melihat ke Depan: Keputusan dibuat berdasarkan informasi yang tersedia saat ini saja.
- Sederhana dan Cepat: Pendekatan ini seringkali lebih mudah diimplementasikan dan memiliki kompleksitas waktu yang lebih rendah dibandingkan metode lain seperti pemrograman dinamis.

## Kekuatan dan Kelemahan
- Kelebihan: Sangat efektif dan cepat untuk jenis masalah di mana pilihan optimal lokal secara otomatis mengarah pada solusi optimal global (seperti Fractional Knapsack).
- Kelemahan: Tidak selalu berhasil untuk semua jenis masalah optimasi. Contoh paling jelas adalah 0/1 Knapsack, di mana pendekatan greedy tidak akan memberikan solusi optimal karena sifat "tidak dapat dibagi"-nya barang.

### Kesimpulan
*Fractional Knapsack Problem* adalah variasi Knapsack Problem yang dapat diselesaikan secara sangat efisien dan optimal menggunakan algoritma greedy. Kunci efisiensi ini terletak pada kemampuan untuk mengambil barang secara parsial atau fraksional.

Untuk mendapatkan solusi optimal, kita cukup:
1. Menghitung rasio nilai per berat untuk setiap item.
2. Mengurutkan item berdasarkan rasio ini dari tertinggi ke terendah.
3. Mengisi tas dengan strategi greedy yang telah dijelaskan.

Algoritma greedy bekerja dengan sempurna untuk masalah ini karena sifatnya yang menjamin bahwa pilihan optimal lokal akan selalu menghasilkan solusi optimal global. Ini menjadikannya alat yang kuat dan praktis dalam berbagai skenario optimasi sumber daya.