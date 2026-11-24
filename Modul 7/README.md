# Modul 7: Integral Numerik (Aturan Trapesium Komposit)

Implementasi metode **Aturan Trapesium Komposit (*Composite Trapezoidal Rule*)** untuk menghitung hampiran nilai integral tentu:
$$I = \int_{0,2}^{2,6} e^{-x^2}\,dx$$
pada empat variasi jumlah subinterval $n \in \{6, 12, 18, 24\}$ dibandingkan terhadap nilai acuan $I \approx 0,688653$[cite: 10, 11].

---

## Gambaran & Ilustrasi Konsep

Fungsi kurva lonceng Gaussian $f(x) = e^{-x^2}$ tidak memiliki bentuk antiturunan elementer sederhana, sehingga luas daerah di bawah kurvanya dihitung dengan memotong-motong area menjadi beberapa bangun trapesium tegak[cite: 11].

```text
  f(x) = e^(-x²)
   ▲
   │  ●───●
   │  │   │\
   │  │   │ ●───●
   │  │   │ │   │\
   │  │   │ │   │ ●───●
   └──┴───┴─┴───┴─┴───┴──► x
     0.2         ...  2.6   (Semakin banyak partisi n, potongan makin rapat & akurat!)
```

* **Analogi Sederhana:** Bayangkan kamu ingin mengukur luas sebidang tanah yang salah satu sisinya melengkung seperti bukit[cite: 11]. Jika tanah itu hanya ditutup oleh 6 papan trapesium lebar ($n = 6$), masih ada celah kosong di bagian lengkungan atas. Namun, jika dipotong menjadi 24 bilah trapesium tipis ($n = 24$), atap papan akan mengikuti bentuk lengkungan bukit dengan sangat rapat sehingga luasnya hampir persis sama dengan luas aslinya[cite: 10, 11].

---

## Alur Kerja Kode

1. **Definisi Integran:** Mendefinisikan fungsi $f(x) = e^{-x^2}$ menggunakan `np.exp(-x**2)`[cite: 10].
2. **Partisi Selang (`trapesium`):**
   * Menghitung lebar setiap segmen `h = (b - a) / n`[cite: 10].
   * Membentuk array titik partisi seragam sebanyak `n + 1` titik menggunakan `np.linspace(a, b, n + 1)`[cite: 10].
3. **Rumus Trapesium Komposit:** Menghitung luas total dengan menjumlahkan ujung awal `y[0]`, dua kali seluruh titik tengah `2 * np.sum(y[1:-1])`, dan ujung akhir `y[-1]`, lalu dikalikan `h / 2`[cite: 10].
4. **Pengujian Multi-Partisi:** Menjalankan loop untuk `n = [6, 12, 18, 24]` dan menghitung galat absolut `abs(I_acuan - hasil)`[cite: 10].

---

## Perbandingan Hasil & Pengaruh Jumlah Partisi ($n$)

| Jumlah Partisi ($n$) | Lebar Langkah ($h$) | Nilai Integral Numerik | Nilai Acuan | Galat Absolut | Rasio Penurunan Galat |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **6** | `0.400000`[cite: 10] | `0.69378379`[cite: 10] | `0.688653`[cite: 10] | `0.00513079`[cite: 10] | Acuan awal |
| **12** | `0.200000`[cite: 10] | `0.68991899`[cite: 10] | `0.688653`[cite: 10] | `0.00126599`[cite: 10] | Turun **~4x lipat** dari $n=6$[cite: 10, 11] |
| **18** | `0.133333`[cite: 10] | `0.68921419`[cite: 10] | `0.688653`[cite: 10] | `0.00056119`[cite: 10] | Turun **~9x lipat** dari $n=6$[cite: 10, 11] |
| **24** | `0.100000`[cite: 10] | **`0.68896828`**[cite: 10] | `0.688653`[cite: 10] | **`0.00031528`**[cite: 10] | Turun **~16x lipat** dari $n=6$[cite: 10, 11] |

> **Catatan Akurasi:** Aturan Trapesium Komposit memiliki galat berorde $O(h^2)$ atau berbanding terbalik dengan $1/n^2$, sehingga setiap kali jumlah partisi $n$ digandakan menjadi dua kali lipat, nilai galatnya otomatis menyusut menjadi seperempatnya[cite: 11].

---

## Cara Menjalankan

* **File Notebook:** `Integral Turunan.ipynb` *(berisi kode Metode Integral Numerik)*[cite: 10, 12]
* **Library:** `numpy`[cite: 10]
* Jalankan sel kode di **Google Colab** atau **Jupyter Notebook** lokal.