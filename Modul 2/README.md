# Modul 2: Penyelesaian SPL — Eliminasi Gauss & Dekomposisi LU

Implementasi dua metode langsung (*direct methods*) untuk menyelesaikan Sistem Persamaan Linear (SPL) $Ax = b$ berukuran $3 \times 3$:

$$A = \begin{bmatrix} 3.0 & 1.0 & -4.0 \\ -2.0 & 3.0 & 1.0 \\ 2.0 & 0.0 & 5.0 \end{bmatrix}, \quad b = \begin{bmatrix} 7.0 \\ -5.0 \\ 10.0 \end{bmatrix}$$

---

## Gambaran & Ilustrasi Konsep

Metode langsung bekerja seperti merapikan susunan balok angka yang rumit menjadi bentuk segitiga agar nilai variabel $x_1, x_2, x_3$ bisa dibongkar satu per satu dengan pasti.

```text
  Matriks Awal (Ab)         Eliminasi Maju (Segitiga Atas)      Substitusi Mundur
 ┌               ┐          ┌                     ┐
 │  3   1  -4 | 7 │          │  3    1     -4   | 7 │  ──► Hitung x1 (Terakhir)
 │ -2   3   1 |-5 │   ───►   │  0  3.67  -1.67 |-0.3│  ──► Hitung x2 (Kedua)
 │  2   0   5 |10 │          │  0    0    7.36 |5.27│  ──► Hitung x3 (Pertama!)
 └               ┘          └                     ┘
```

1. **Eliminasi Gauss**
   * **Analogi Sederhana:** Seperti menyusun anak tangga segitiga dari atas ke bawah. Baris pertama dipakai sebagai pijakan (*pivot*) untuk meng-nol-kan angka di bawahnya. Setelah terbentuk segitiga atas, kita tinggal menghitung nilai variabel mulai dari anak tangga paling bawah ($x_3$) naik ke atas hingga $x_1$.
2. **Dekomposisi LU**
   * **Analogi Sederhana:** Seperti memecah satu gembok matriks $A$ menjadi dua kunci terpisah: Matriks Segitiga Bawah ($L$) dan Matriks Segitiga Atas ($U$), sehingga $A = L \cdot U$. Kelebihannya, jika nilai target $b$ diganti berkali-kali, kita tidak perlu mengulang proses eliminasi matriks $A$ dari nol—cukup menyelesaikan $Ly = b$ lalu $Ux = y$.

---

## Alur Kerja Kode

1. **Eliminasi Gauss (`eliminasi_gauss`):**
   * Menggabungkan matriks $A$ dan vektor kolom $b$ menggunakan `np.hstack([A, b.reshape(-1, 1)])`.
   * Mengecek keamanan pembagi dengan `abs(pivot) < 1e-12` untuk mencegah *division by zero*.
   * Melakukan operasi baris elementer (*forward elimination*) dan menghitung solusi akhir dari bawah ke atas (*backward substitution*) memakai `np.dot`.
2. **Dekomposisi LU (`lu_decomposition`):**
   * Menginisialisasi diagonal utama matriks $L$ bernilai `1.0` (`L[i, i] = 1.0`).
   * Mengisi elemen matriks $U$ dan pengali matriks $L$ menggunakan skema Doolittle.
   * Menyelesaikan dua tahap substitusi: substitusi maju untuk mendapatkan vektor $y$, diikuti substitusi mundur untuk mendapatkan solusi $x$.

---

## Hasil Solusi Akhir

Kedua metode menghasilkan solusi eksak yang identik:

| Variabel | Nilai Desimal (4 Digit) | Bentuk Pecahan Eksak |
| :---: | :---: | :---: |
| **$x_1$** | `3.2099` | $260 / 81$ |
| **$x_2$** | `0.2346` | $19 / 81$ |
| **$x_3$** | `0.7160` | $58 / 81$ |

---

## Cara Menjalankan

* **File Notebook:** `Penyelesaian SPL dengan Metode Eliminasi Gauss dan Dekomposisi LU.ipynb`
* **Library:** `numpy`
* Jalankan sel program di **Google Colab** atau **Jupyter Notebook** lokal.