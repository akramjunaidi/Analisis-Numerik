# Modul 6: Turunan Numerik (Metode Selisih Hingga)

Implementasi pendekatan **Selisih Hingga (*Finite Difference*)** untuk menghitung turunan pertama fungsi:
$$f(x) = 2x \cos(2x)$$
pada titik $x = 2,0$ dengan ukuran langkah $h = 0,1$, serta membandingkan tingkat akurasinya terhadap solusi analitik $f'(2,0) = 4,747133$[cite: 6, 7].

---

## Gambaran & Ilustrasi Konsep

Turunan pertama adalah kemiringan garis singgung tepat di titik tempat kita berpijak ($x = 2,0$)[cite: 7]. Karena komputer menghitung berdasarkan titik-titik diskrit berjarak $h$, ada tiga cara mengintip kemiringan tersebut:

```text
  Beda Mundur          Titik Pijak          Beda Maju
  (x - h = 1.9)        (x = 2.0)            (x + h = 2.1)
       ●◄────── h ──────►●◄────── h ──────►●
       │                 │                 │
       └─ Beda Mundur ───┘                 │
                         └─ Beda Maju ─────┘
       └────────── Beda Tengah (2h) ───────┘  ◄── Paling seimbang & akurat!
```

* **Analogi Sederhana:** Bayangkan kamu berdiri di tengah jalan menanjak ($x = 2,0$) dan ingin mengukur seberapa curam tanjakan tepat di bawah kakimu:
  * **Selisih Maju:** Kamu hanya melirik satu langkah ke depan ($x + h$)[cite: 7].
  * **Selisih Mundur:** Kamu hanya menengok satu langkah ke belakang ($x - h$)[cite: 7].
  * **Selisih Tengah:** Kamu melihat satu langkah ke belakang **dan** satu langkah ke depan secara seimbang[cite: 7]. Karena kesalahan dari sisi depan dan belakang saling meniadakan, kemiringan di titik pijakmu terukur jauh lebih akurat[cite: 7]!

---

## Alur Kerja Kode

1. **Definisi Fungsi & Parameter:** Mendefinisikan $f(x) = 2x \cos(2x)$ dengan `math.cos`, titik `x = 2.0`, langkah `h = 0.1`, dan nilai eksak `x_analitik = 4.747133`[cite: 6].
2. **Perhitungan Tiga Pendekatan:**
   * **Selisih Maju:** `(f(x + h) - f(x)) / h`[cite: 6]
   * **Selisih Mundur:** `(f(x) - f(x - h)) / h`[cite: 6]
   * **Selisih Tengah:** `(f(x + h) - f(x - h)) / (2 * h)`[cite: 6]
3. **Evaluasi Galat Absolut:** Menghitung selisih mutlak `abs(x_analitik - hasil)` untuk masing-masing metode[cite: 6].

---

## Perbandingan Hasil & Tingkat Akurasi

| Metode Pendekatan | Orde Galat | Hasil Numerik | Nilai Analitik | Galat Absolut |
| :--- | :---: | :---: | :---: | :---: |
| **Selisih Maju (*Forward*)** | $O(h)$ | `5.554790`[cite: 6] | `4.747133`[cite: 6] | `0.807657`[cite: 6] |
| **Selisih Mundur (*Backward*)** | $O(h)$ | `3.911028`[cite: 6] | `4.747133`[cite: 6] | `0.836105`[cite: 6] |
| **Selisih Tengah (*Central*)** | **$O(h^2)$** | **`4.732909`**[cite: 6] | `4.747133`[cite: 6] | **`0.014224`**[cite: 6] |

> **Catatan Akurasi:** Selisih Tengah jauh lebih presisi (galat hanya `0.014224`) dibandingkan Selisih Maju dan Mundur karena memiliki akurasi orde kedua $O(h^2)$[cite: 6, 7].

---

## Cara Menjalankan

* **File Notebook:** `Turunan Integral.ipynb` *(berisi kode Metode Turunan Numerik)*[cite: 6, 12]
* **Library:** Modul bawaan Python (`math`)[cite: 6]
* Jalankan sel kode di **Google Colab** atau **Jupyter Notebook** lokal.