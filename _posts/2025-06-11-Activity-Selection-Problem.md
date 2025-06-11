---
title: "Greedy Algorithm: Activity Selection Problem"
date: 2025-06-11 00:00:00 +0800
categories: [Kelompok 1]
tags: [Kelompok 1, algorithm, C++]
---

---
## Memaksimalkan Jadwal: Memahami *Activity Selection Problem*

*Activity Selection Problem* adalah sebuah tantangan optimasi yang umum dalam ilmu komputer. Bayangkan Anda memiliki daftar kegiatan, masing-masing dengan **waktu mulai** dan **waktu selesai** yang telah ditentukan. Tujuan utamanya adalah memilih sebanyak mungkin kegiatan yang bisa dilakukan *tanpa ada yang tumpang tindih*. Dua kegiatan dianggap *kompatibel* jika satu kegiatan selesai sebelum kegiatan lainnya dimulai.

---
## Strategi *Greedy* untuk Seleksi Aktivitas

Masalah ini paling sering dipecahkan dengan **algoritma *greedy***. Ide dasarnya sangat intuitif: di setiap langkah, kita memilih aktivitas yang *paling cepat selesai*. Mengapa? Karena dengan menyelesaikan sebuah aktivitas lebih awal, kita menyisakan waktu semaksimal mungkin untuk kegiatan-kegiatan selanjutnya. Ini adalah kunci untuk menemukan solusi *optimal*.

### Cara Kerja Algoritma

Algoritma ini mengikuti langkah-langkah sederhana:

1.  **Urutkan** semua aktivitas berdasarkan waktu selesainya, dari yang paling awal hingga paling akhir.
2.  **Pilih aktivitas pertama**, yaitu aktivitas dengan waktu selesai paling awal. Ini akan menjadi aktivitas pertama dalam daftar hasil kita.
3.  **Telusuri sisa aktivitas** satu per satu. Untuk setiap aktivitas yang dipertimbangkan, kita akan memilihnya jika waktu mulainya sama atau lebih lambat dari waktu selesai aktivitas terakhir yang sudah kita pilih. Jika cocok, tambahkan aktivitas ini ke daftar hasil dan perbarui aktivitas terakhir yang dipilih.

### Pseudocode

```pseudocode
ACTIVITY-SELECTOR(s, f, n)
    A = {a1}                 // Pilih aktivitas pertama (yang selesai paling awal)
    j = 1
    for i = 2 to n
        if s[i] >= f[j]      // Cek apakah tidak ada tumpang tindih
            A = A ∪ {ai}     // Jika tidak tumpang tindih, tambahkan ke hasil
            j = i            // Update aktivitas terakhir yang dipilih
    return A
```

---
## Efisiensi dan Sumber Daya

Algoritma *greedy* ini cukup efisien dalam hal kompleksitas waktu dan ruang.

### Kompleksitas Waktu

1.  Langkah pengurutan aktivitas mendominasi waktu eksekusi, membutuhkan **$O(n \log n)$**.
2.  Langkah pemilihan aktivitas setelah pengurutan hanya membutuhkan **$O(n)$** karena kita hanya melakukan satu lintasan.
3.  Secara keseluruhan, kompleksitas waktu adalah **$O(n \log n)$**, yang sangat efisien untuk *dataset* besar.

### Kompleksitas Ruang

1.  Algoritma ini membutuhkan **$O(n)$** ruang untuk menyimpan daftar aktivitas.
2.  Selain itu, tidak ada kebutuhan signifikan untuk ruang tambahan, menjadikannya cukup *hemat memori*.

---
## Kekuatan dan Keterbatasan

Seperti algoritma lainnya, pendekatan *greedy* untuk *Activity Selection Problem* memiliki kelebihan dan kekurangan.

### Keunggulan

* **Sederhana dan Mudah Diimplementasikan**, bahkan oleh mereka yang baru belajar algoritma.
* **Efisiensi Tinggi**, terutama untuk kumpulan data yang besar.
* Menghasilkan *solusi optimal* untuk masalah seleksi aktivitas dasar tanpa batasan yang rumit.

### Batasan

* Memerlukan proses *pengurutan awal*, yang menjadi penyumbang utama kompleksitas waktu.
* Tidak selalu cocok untuk masalah yang memiliki *banyak batasan tambahan*, seperti prioritas aktivitas, lokasi geografis, atau pertimbangan biaya. Untuk skenario yang lebih kompleks, mungkin diperlukan pendekatan yang berbeda.

---
## Aplikasi di Dunia Nyata

Fleksibilitas *Activity Selection Problem* membuatnya relevan di berbagai bidang:

* **Penjadwalan & Pengaturan Fasilitas**: Ideal untuk mengatur jadwal ruang kelas, sesi rapat, penggunaan laboratorium, atau lapangan olahraga agar kapasitasnya maksimal.
* **Sistem Operasi**: Menerapkan prinsip ini dalam menjadwalkan proses CPU atau mengalokasikan memori untuk berbagai tugas.
* **Logistik**: Mengoptimalkan jadwal pengiriman barang atau merencanakan rute kendaraan agar efisien.
* **Telekomunikasi**: Membantu dalam alokasi *bandwidth* atau penjadwalan transmisi data untuk memastikan penggunaan sumber daya yang optimal.

---
## Kesimpulan

Singkatnya, *Activity Selection Problem* secara efektif diselesaikan menggunakan pendekatan *greedy* dengan mengurutkan aktivitas berdasarkan waktu selesai. Pendekatan ini menjamin *solusi optimal* dalam kompleksitas waktu **$O(n \log n)$**. Meskipun sangat cocok untuk berbagai tugas penjadwalan, masalah yang lebih kompleks dengan berbagai batasan mungkin memerlukan teknik yang lebih canggih, seperti pemrograman dinamis atau metaheuristik.