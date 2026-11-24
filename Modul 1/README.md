# Modul 1: Pencarian Akar Persamaan Non-Linear

Implementasi tiga metode numerik untuk mencari titik akar $f(x) = 0$ pada fungsi non-linear:
$$f(x) = 2\sin(x) - e^{x/4} - 1$$
dengan rentang awal $[-5, -3]$, toleransi galat $10^{-6}$, dan batas maksimum $10$ iterasi.

---

## Gambaran & Ilustrasi Konsep

Mencari akar persamaan $f(x) = 0$ ibarat mencari titik di mana sebuah kurva memotong garis permukaan tanah (sumbu-$X$). Setiap metode punya strategi berbeda untuk menemukan titik potong tersebut:

```text
  f(x)
   ▲
   │  * (x0 = -5)
   │   \
───┼────\─────────●───────────► sumbu-X (Target: f(x) = 0 di x ≈ -3.901074)
   │     \       / \
   │      \_____/   * (x1 = -3)
```

1. **Metode Bisection (Bagi Dua)**
   * **Analogi Sederhana:** Seperti bermain tebak angka *"lebih besar atau lebih kecil"* dengan cara selalu membelah area pencarian tepat di tengah-tengah. Langkahnya sangat aman dan pasti mendekati target, tetapi butuh banyak putaran karena ukurannya hanya mengecil setengah di setiap langkah.
2. **Metode Newton-Raphson**
   * **Analogi Sederhana:** Seperti meluncur mengikuti kemiringan garis singgung kurva langsung menuju permukaan sumbu-$X$. Karena dibantu "kompas" berupa turunan pertama $f'(x) = 2\cos(x) - \frac{1}{4}e^{x/4}$, metode ini melesat sangat cepat menuju akar, meski wajib menghitung rumus turunan secara manual terlebih dahulu.
3. **Metode Secant**
   * **Analogi Sederhana:** Jalan tengah bagi yang tidak ingin repot mencari rumus turunan $f'(x)$. Metode ini menarik garis lurus dari dua titik tebakan terakhir untuk memperkirakan posisi akar berikutnya. Kecepatannya berada tepat di antara Bisection dan Newton-Raphson.

---

## Alur Kerja Kode

1. **Inisialisasi Fungsi:** Mendefinisikan fungsi target `f(x)` beserta turunan analitiknya `df(x)` (khusus Newton-Raphson).
2. **Validasi Awal:**
   * *Bisection* mengecek syarat pengurungan akar `f(a) * f(b) < 0`.
   * *Newton-Raphson* dan *Secant* mengecek agar penyebut (`dfx` atau `fx1 - fx0`) tidak bernilai nol.
3. **Iterasi Hampiran:** Memperbarui titik tebakan `c`, `x_baru`, atau `x2` di setiap putaran sambil menghitung selisih galat (`error`).
4. **Kriteria Berhenti:** Loop berhenti otomatis jika nilai galat sudah lebih kecil dari toleransi (`1e-6`) atau saat mencapai batas `max_iter = 10`.

---

## Perbandingan Hasil Eksekusi

| Metode | Syarat Input Awal | Iterasi Konvergen | Akar Hampiran ($x$) | Status pada `max_iter = 10` |
| :--- | :--- | :---: | :---: | :--- |
| **Bisection** | Interval $[-5, -3]$ | $> 10$ iterasi | `-3.900391` | Belum mencapai toleransi ($f(c) = -0.001056$) |
| **Newton-Raphson** | Titik tengah $x_0 = -4.0$ & $f'(x)$ | **Iterasi ke-4** | **`-3.901074`** | **Konvergen tercepat** (`error = 0.000000`) |
| **Secant** | Dua titik $x_0 = -5, x_1 = -3$ | **Iterasi ke-7** | **`-3.901074`** | **Konvergen** tanpa perlu turunan (`error = 0.000002`) |

---

## Cara Menjalankan

* **File Notebook:** `Bisection, Newton Raphson, dan Secant.ipynb`
* **Library:** Modul bawaan Python (`math`)
* Jalankan seluruh sel secara berurutan di **Google Colab** atau **Jupyter Notebook**.