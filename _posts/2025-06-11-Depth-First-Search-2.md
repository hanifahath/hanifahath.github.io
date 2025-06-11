---
title: Depth First Search (DFS) - Part 2
date: 2025-06-10 00:00:00 +0800
last_modified_at: 2025-06-10 14:45:00 +0700
categories: [Kelompok 8]
tags: [Kelompok 8]
---

## Deskripsi Umum

Proyek ini menghadirkan implementasi algoritma **Depth First Search (DFS)**, sebuah teknik pencarian graf yang esensial. Tujuan utamanya adalah menjelajahi simpul-simpul dalam sebuah graf untuk menemukan simpul tertentu atau sekadar menelusuri seluruh strukturnya. DFS terbukti sangat *berguna* dalam beragam aplikasi, seperti pemecahan labirin (*maze*), deteksi siklus pada graf, penyelesaian *puzzle*, dan banyak lagi.

---

## Apa Itu DFS?

**Depth First Search (DFS)** adalah metode eksplorasi graf yang unik. Ia bekerja dengan menjelajahi satu cabang graf *sedalam mungkin* hingga mencapai ujungnya atau simpul yang tidak memiliki tetangga belum dikunjungi. Barulah setelah itu, algoritma akan kembali (*backtrack*) dan mulai menjelajahi cabang lain. Implementasi DFS dapat dilakukan secara *rekursif* atau menggunakan struktur data *stack*.

### Karakteristik Utama DFS:

1.  **Eksplorasi Mendalam:** DFS menelusuri graf secara *menyeluruh ke kedalaman* dari setiap cabang sebelum beralih ke cabang berikutnya.
2.  **Fleksibilitas Pencarian:** Algoritma ini dapat digunakan untuk *pencarian jalur* tertentu atau sekadar *menelusuri seluruh simpul* yang dapat dijangkau dalam graf.
3.  **Perbandingan dengan BFS:** DFS cenderung *kurang efisien* dibandingkan dengan *Breadth-First Search (BFS)* jika solusi yang dicari terletak dekat dengan simpul awal, karena DFS akan menjelajahi cabang jauh terlebih dahulu.

---

## Cara Kerja DFS

Algoritma DFS mengikuti serangkaian langkah logis untuk menjelajahi graf.

### Langkah-langkah Utama dalam Algoritma DFS:

1.  **Mulai dari Simpul Awal:** Tentukan simpul (node) dari mana penelusuran akan dimulai.
2.  **Tandai Sudah Dikunjungi:** Segera setelah mengunjungi sebuah simpul, tandai simpul tersebut sebagai *telah dikunjungi* untuk menghindari perulangan tak terbatas atau mengunjungi simpul yang sama berkali-kali.
3.  **Telusuri Tetangga:** Dari simpul saat ini, pilih salah satu *simpul tetangga yang belum dikunjungi*.
4.  **Lanjutkan Rekursif:** Panggil kembali fungsi DFS (atau dorong simpul ke *stack*) untuk simpul tetangga yang baru dipilih. Proses ini akan berlanjut secara mendalam.
5.  **Kembali (*Backtrack*):** Jika dari simpul saat ini tidak ada lagi simpul tetangga yang belum dikunjungi (atau semua jalur dari simpul tersebut telah dieksplorasi), algoritma akan *kembali* (*backtrack*) ke simpul sebelumnya dan menelusuri jalur lain yang belum dieksplorasi.

---

## Visualisasi

Untuk memahami DFS lebih baik, mari kita gunakan sebuah graf sederhana.

### Graf yang Digunakan dalam Studi Kasus:

```
    A
   / \
  B   C
 /     \
D       E
```

### Representasi Graf dalam Bentuk *Adjacency List*:

Graf ini dapat direpresentasikan dalam Python menggunakan kamus (*dictionary*), di mana setiap kunci adalah simpul dan nilainya adalah daftar simpul tetangga.

```python
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': []
}
```

---

## Implementasi dalam Python

Berikut adalah contoh kode Python yang mengimplementasikan algoritma DFS.

### Kode Program DFS:

```python
# Definisi graf menggunakan adjacency list
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': []
}

# Set untuk menyimpan simpul yang sudah dikunjungi
# Ini penting untuk mencegah loop tak terbatas pada graf dengan siklus
visited = set()

# Fungsi rekursif DFS
def dfs(visited, graph, node):
    # Jika simpul belum dikunjungi
    if node not in visited:
        print(node, end=" ") # Cetak simpul yang dikunjungi
        visited.add(node)    # Tandai simpul sebagai sudah dikunjungi
        
        # Iterasi melalui semua tetangga dari simpul saat ini
        for neighbour in graph[node]:
            # Panggil DFS secara rekursif untuk setiap tetangga
            dfs(visited, graph, neighbour)

# Menjalankan DFS dari simpul 'A' sebagai titik awal
print("Hasil Penelusuran DFS:")
dfs(visited, graph, 'A')
```

---

## Hasil dan Output

Ketika kode di atas dijalankan, inilah *output* yang akan dihasilkan:

```
Hasil Penelusuran DFS:
A B D C E
```

Output ini menunjukkan bagaimana simpul-simpul dikunjungi secara *mendalam* terlebih dahulu:
1.  Penelusuran dimulai dari **A**.
2.  Dari A, ia menjelajah ke **B**.
3.  Dari B, ia lanjut ke **D**.
4.  Karena D tidak memiliki tetangga lain yang belum dikunjungi, algoritma *kembali* (*backtrack*) ke B, lalu ke A.
5.  Dari A, ia kemudian melanjutkan ke cabang lain, yaitu **C**.
6.  Dan dari C, ia akhirnya mengunjungi **E**.

---

## Analisis dan Kesimpulan

DFS memiliki karakteristik yang membuatnya cocok untuk beberapa jenis masalah, namun kurang ideal untuk yang lain.

### Kelebihan:

1.  **Implementasi Sederhana:** Kode DFS, terutama versi rekursifnya, seringkali lebih ringkas dan mudah dipahami dibandingkan dengan BFS.
2.  **Menemukan Solusi Lebih Dalam dengan Cepat:** Jika solusi yang dicari berada jauh di dalam salah satu cabang graf, DFS cenderung menemukannya lebih cepat daripada BFS yang harus menjelajahi seluruh level.
3.  **Hemat Memori:** DFS umumnya *tidak membutuhkan banyak memori* dibandingkan dengan BFS, terutama untuk graf yang sangat lebar (banyak simpul di setiap level), karena DFS hanya perlu menyimpan jalur saat ini di *stack* rekursi, bukan semua simpul di level saat ini.

### Kekurangan:

1.  **Tidak Menjamin Jalur Terpendek:** DFS *tidak menjamin* akan menemukan jalur terpendek antara dua simpul, terutama pada graf tak berbobot. Untuk jalur terpendek, BFS adalah pilihan yang lebih baik.
2.  **Potensi *Loop*:** Jika graf mengandung *siklus* dan tidak ada pengecekan simpul yang telah dikunjungi, DFS bisa terjebak dalam *loop* tak terbatas.
3.  **Kurang Optimal untuk Graf Sangat Besar dan Kompleks:** Untuk graf yang sangat besar dan padat, atau ketika kedalaman bisa sangat ekstrem, DFS bisa menjadi lambat karena harus menjelajahi seluruh cabang.

---

## Kesimpulan

Algoritma **Depth First Search (DFS)** adalah pilihan yang *tepat* untuk penelusuran graf yang memerlukan eksplorasi *mendalam*. Karakteristiknya membuatnya sangat cocok untuk berbagai konteks, seperti pemrosesan graf, pencarian solusi dalam *puzzle*, dan khususnya *deteksi siklus*. Meskipun ia tidak selalu menemukan jalur terpendek dan perlu penanganan siklus, kesederhanaan dan efisiensi memorinya menjadikannya alat yang sangat berharga dalam kotak peralatan seorang programmer.

Apakah Anda ingin membahas perbedaan mendalam antara DFS dan BFS, atau melihat contoh aplikasi DFS lainnya?