# Modul 5: Aproksimasi Kuadrat Terkecil (Least Squares)

Implementasi metode **Regresi Linear Kuadrat Terkecil (*Least Squares*)** pada studi kasus **Hubungan Ukuran File Model AI (IndoBERT) terhadap Tingkat Akurasi Validasi**[cite: 3, 4].

---

## Gambaran & Ilustrasi Konsep

Berbeda dengan interpolasi yang memaksa garis kurva berbelok-belok menyentuh semua titik, metode aproksimasi sadar bahwa data eksperimen dunia nyata sering mengandung variasi acak (*noise*)[cite: 4].

```text
  Akurasi (%)
   ▲
92 │                                  ● (40 MB, 92%)
88 │                        ● ── / ── (30 MB, 88%)
86.75│                   ★ ◄── Prediksi saat 25 MB (y = 0.33x + 78.50)
85 │              ● ── / ── (20 MB, 85%)
82 │    ● ────── / ──────── (10 MB, 82%)
   └────┴─────────┴────┴────┴─────────┴──► Ukuran File Model (MB)
       10        20   25   30        40
```

* **Analogi Sederhana:** Bayangkan kamu menaruh penggaris lurus di tengah-tengah sebaran titik data di atas kertas, lalu menggeser kemiringannya sampai jarak selisih total antara garis penggaris dengan seluruh titik menjadi sekecil mungkin[cite: 4]. Garis lurus itulah model *best-fit* $y = ax + b$ yang menangkap tren utama data[cite: 3, 4].

---

## Alur Kerja Kode

1. **Input Data Eksperimen:** Menyimpan 4 hasil pengujian ukuran model (`x` dalam MB) dan akurasi validasi (`y` dalam %) menggunakan array `numpy`[cite: 3, 4].
2. **Pencocokan Garis (*Curve Fitting*):** Menggunakan fungsi `np.polyfit(x, y, 1)` untuk mencari koefisien polinomial derajat 1 (garis lurus), menghasilkan kemiringan `a` dan titik potong `b`[cite: 3, 4].
3. **Prediksi Kompresi Model:** Menghitung estimasi akurasi saat model dikompresi menjadi `x_target = 25.0` MB dengan rumus linear `y_pred = a * x_target + b`[cite: 3, 4].

---

## Hasil Aproksimasi Studi Kasus

| Komponen | Hasil Komputasi |
| :--- | :--- |
| **Data Ukuran File ($x$)** | `[10.0, 20.0, 30.0, 40.0]` MB[cite: 3] |
| **Data Akurasi Aktual ($y$)** | `[82.0, 85.0, 88.0, 92.0]` %[cite: 3] |
| **Persamaan Garis Best-Fit** | **`y = 0.33x + 78.50`**[cite: 3] |
| **Target Kompresi ($x$)** | `25.0 MB`[cite: 3] |
| **Estimasi Akurasi ($y$)** | **`86.75 %`**[cite: 3] |

---

## Cara Menjalankan

* **File Notebook:** `Aproksimasi.ipynb`[cite: 3]
* **Library:** `numpy`
* Jalankan sel kode di **Google Colab** atau **Jupyter Notebook** lokal.