# Modul 3: Penyelesaian SPL — Metode Jacobi & Gauss-Seidel

Implementasi dua metode iteratif untuk mencari solusi Sistem Persamaan Linear $Ax = b$ berukuran $3 \times 3$ mulai dari tebakan awal $x^{(0)} = [0, 0, 0]$ dengan toleransi $10^{-6}$ dan batas $15$ iterasi:

$$A = \begin{bmatrix} 6.0 & -2.0 & 3.0 \\ -2.0 & -3.0 & 0.0 \\ 1.0 & 1.0 & -4.0 \end{bmatrix}, \quad b = \begin{bmatrix} 12.0 \\ 12.0 \\ 8.0 \end{bmatrix}$$

---

## Gambaran & Ilustrasi Konsep

Berbeda dengan Eliminasi Gauss yang mengubah bentuk matriks secara langsung, metode iteratif bekerja dengan cara **menebak lalu memperbaiki tebakan secara berulang** hingga angkanya berhenti berubah (konvergen).

```text
  METODE JACOBI (Serentak / Paralel)
  Tebakan Lama [x0, y0, z0] ──► Hitung semua (x1, y1, z1) bersamaan ──► Update serentak

  METODE GAUSS-SEIDEL (Estafet Langsung)
  x0 ──► Hitung x1 ──(langsung dipakai!)──► Hitung y1 ──(langsung dipakai!)──► Hitung z1
```

1. **Metode Jacobi**
   * **Analogi Sederhana:** Seperti kerja kelompok di mana semua anggota menghitung bagian masing-masing menggunakan catatan dari putaran sebelumnya. Hasil hitungan baru ditampung dulu di kertas terpisah (`x_baru`), lalu ditukar serentak setelah satu putaran penuh selesai.
2. **Metode Gauss-Seidel**
   * **Analogi Sederhana:** Seperti lari estafet tanpa menunggu. Begitu nilai $x$ terbaru ketemu di baris pertama, angka segar itu **langsung dipakai detik itu juga** untuk menghitung $y$ di baris kedua, dan keduanya langsung dipakai menghitung $z$. Karena selalu memakai informasi paling mutakhir, metode ini jauh lebih cepat mencapai konvergensi.

---

## Alur Kerja Kode

1. **Inisialisasi:** Menyiapkan vektor tebakan awal nol `x = np.zeros(n)` dan format tabel output.
2. **Perhitungan per Putaran:**
   * *Jacobi* menyisihkan elemen diagonal (`if j != i`) dan menyimpan hasil ke array baru `x_baru` sebelum menimpa `x`.
   * *Gauss-Seidel* menyalin `x_lama = x.copy()`, membagi penjumlahan menjadi `sumber_1` (variabel yang sudah diperbarui) dan `sumber_2` (variabel lama), lalu langsung memperbarui `x[i]`.
3. **Evaluasi Galat:** Mengukur pergeseran terbesar antar-iterasi menggunakan norma takhingga (`np.linalg.norm(..., ord=np.inf)`). Program berhenti saat `galat < 1e-6`.

---

## Perbandingan Kecepatan Konvergensi

| Metode | Jumlah Iterasi | Galat Akhir | Nilai $x$ | Nilai $y$ | Nilai $z$ | Status |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **Jacobi** | 15 (Batas Maks) | `0.001699` | `1.714766` | `-5.142044` | `-2.857354` | Belum mencapai toleransi $10^{-6}$ |
| **Gauss-Seidel** | **12 Iterasi** | **`0.000001`** | **`1.714286`** | **`-5.142857`** | **`-2.857143`** | **Konvergen lebih cepat** |

---

## Cara Menjalankan

* **File Notebook:** `Penyelesaian SPL dengan Metode Jacobi dan Gauss-Seidel.ipynb`
* **Library:** `numpy`
* Jalankan sel program di **Google Colab** atau **Jupyter Notebook** lokal.