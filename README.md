
# Sistem Rekomendasi Produk E-Commerce Berbasis Graf

**UTS Graf Sains Data**

## Identitas Mahasiswa

- **Nama:** Salwa Nadhifah Az Zahrah
- **NIM:** 23031554136
- **Program Studi:** Sains Data 2023
- **Mata Kuliah:** Graf Sains Data

---

## 1. Deskripsi Proyek

Proyek ini bertujuan membangun sistem rekomendasi produk e-commerce menggunakan metode *Item-Based KNN* berbasis graf. Sistem menghitung kemiripan antarproduk berdasarkan riwayat interaksi pengunjung untuk menghasilkan rekomendasi produk yang relevan.

**Metode dan teknologi yang digunakan:**
- **Neo4j:** Pengelolaan graf dan relasi antarentitas.
- **Vector Space Model (VSM):** Representasi interaksi pengunjung dan produk.
- **Cosine Similarity:** Pengukuran kemiripan antarproduk.
- **Item-Based KNN:** Pembentukan rekomendasi produk.
- **Hit@5 dan NDCG@5:** Evaluasi hasil rekomendasi.

## 2. Dataset

Dataset yang digunakan adalah [RetailRocket E-Commerce Dataset](https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset) dari Kaggle.

Dataset ini berisi interaksi pengunjung dengan produk e-commerce, seperti melihat produk, menambahkan produk ke keranjang, dan membeli produk.

### Pembagian Data

| Periode | Rentang Waktu | Fungsi |
|---|---|---|
| P1 | 20 Mei–19 Juni 2015 | Training |
| P2 | 15 Agustus–14 September 2015 | Testing |

### Jumlah Data

| Keterangan | Jumlah |
|---|---:|
| Data P1 | 633.522 |
| Data P2 | 561.408 |
| **Total setelah filter** | **1.194.930** |

### Bobot Interaksi

| Jenis Interaksi | Bobot |
|---|---:|
| `VIEWED` | 1 |
| `ADDED_TO_CART` | 2 |
| `BOUGHT` | 3 |

## 3. Eksplorasi Graf

### Komposisi Simpul

| Jenis Simpul | Jumlah |
|---|---:|
| Event | 5.512.202 |
| Item | 235.061 |
| Movie | 9.742 |
| Person | 4 |
| User | 610 |
| Visitor | 1.407.580 |

### Perbandingan Relasi

| Jenis Relasi | Sebelum | Sesudah |
|---|---:|---:|
| `VIEWED` | 2.673.973 | 2.673.973 |
| `ADDED_TO_CART` | 69.582 | 69.582 |
| `BOUGHT` | 22.546 | 22.546 |
| `RATED` | 100.836 | 100.836 |
| `KNOWS` | 3 | 3 |
| `SIMILAR_TO` | 0 | 86.275 |
| **Total** | **2.866.940** | **2.953.215** |

Setelah perhitungan kemiripan, terbentuk **86.275 relasi `SIMILAR_TO`**. Visualisasi graf menggunakan 40 simpul dan 362 relasi.

## 4. Vector Space Model (VSM)

VSM digunakan untuk merepresentasikan interaksi pengunjung terhadap produk dalam bentuk matriks.

| Karakteristik | VSM User | VSM Item |
|---|---:|---:|
| Dimensi matriks | 329.777 × 119.627 | 119.627 × 329.777 |
| Jumlah nilai nonzero | 492.096 | 492.096 |

VSM User merepresentasikan interaksi dari sisi pengunjung, sedangkan VSM Item merepresentasikan interaksi dari sisi produk. VSM Item digunakan untuk menghitung kemiripan antarproduk.

## 5. Hasil Kemiripan Antarproduk

Perhitungan *cosine similarity* menghasilkan:

- **Jumlah data similarity:** 86.275
- **Item yang memiliki tetangga:** 17.953
- **Item acuan:** `96680`
- **Visitor yang berinteraksi dengan item acuan:** 42

### Lima Item Paling Mirip

| Item Mirip | Similarity | Visitor Bersama |
|---:|---:|---:|
| 9199 | 0.207209 | 7 |
| 303517 | 0.115382 | 3 |
| 446524 | 0.111005 | 3 |
| 263258 | 0.106721 | 3 |
| 122467 | 0.098298 | 3 |

## 6. Hasil Rekomendasi

Sistem menggunakan metode *Item-Based KNN* untuk menghasilkan lima rekomendasi berdasarkan riwayat interaksi pengunjung. Tiga produk teratas dipilih sebagai kandidat iklan.

### Contoh Rekomendasi

**Visitor ID:** `127311`

| Peringkat | Item ID | Skor Rekomendasi |
|---:|---:|---:|
| 1 | 432861 | 0.358746 |
| 2 | 108936 | 0.268124 |
| 3 | 167653 | 0.122902 |
| 4 | 399748 | 0.089453 |
| 5 | 191807 | 0.073855 |

**Tiga kandidat iklan utama:** `432861`, `108936`, dan `167653`.

## 7. Evaluasi Sistem

Evaluasi dilakukan menggunakan data testing P2 dengan metrik Hit@5 dan NDCG@5.

### Hasil Evaluasi Keseluruhan

| Keterangan | Hasil |
|---|---:|
| Visitor pada P2 | 314.804 |
| Visitor yang terdapat pada P1 dan P2 | 6.678 |
| Visitor yang dapat dievaluasi | 2.707 |
| Rata-rata Hit@5 | 0.017 |
| Rata-rata NDCG@5 | 0.0072 |

### Evaluasi Visitor 127311

Pada pengujian ini, tidak ada item relevan yang masuk ke dalam lima rekomendasi yang dihasilkan.

| Metrik | Nilai |
|---|---:|
| Hit@5 | 0 |
| DCG@5 | 0.0000 |
| IDCG@5 | 2.1309 |
| NDCG@5 | 0.0000 |

## 8. Kesimpulan

Sistem rekomendasi berhasil dibangun menggunakan Neo4j, VSM, *cosine similarity*, dan *Item-Based KNN*. Perhitungan menghasilkan 86.275 relasi kemiripan antarproduk.

Evaluasi memperoleh rata-rata Hit@5 sebesar **0.017** dan NDCG@5 sebesar **0.0072**. Hasil ini menunjukkan bahwa sistem dapat menghasilkan rekomendasi, tetapi relevansi produk yang direkomendasikan masih perlu ditingkatkan.
