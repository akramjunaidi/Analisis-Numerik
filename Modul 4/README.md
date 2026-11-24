# Modul 4: Interpolasi Polinomial Lagrange

Implementasi metode **Interpolasi Polinomial Lagrange** pada studi kasus **Estimasi Throughput Jaringan** berdasarkan tingkat utilisasi *bandwidth*[cite: 2, 5].

---

## Gambaran & Ilustrasi Konsep

Interpolasi ibarat permainan menghubungkan titik-titik bintang dengan satu garis lengkung mulus[cite: 5]. Aturan utamanya: **kurva polinomial yang terbentuk wajib melewati setiap titik sampel yang diketahui secara presisi tanpa meleset sedikit pun**, sehingga kita bisa menebak nilai di celah yang kosong[cite: 5].

```text
  Throughput (Mbps)
   ▲
95 │                                        ● (80%, 95 Mbps)
87.22│                          ★ ◄── Estimasi saat Bandwidth 60%
80 │                    ● (50%, 80 Mbps)
   │               . '
45 │    ● (20%, 45 Mbps)
   └────┴───────────────┴───────┴───────────┴──► Utilisasi Bandwidth (%)
       20%             50%     60%         80%
```

* **Analogi Sederhana:** Misalkan kita baru mencatat kecepatan internet kantor saat beban jaringan berada di angka 20%, 50%, dan 80%[cite: 2, 5]. Tanpa harus melakukan pengukuran ulang secara langsung, Interpolasi Lagrange membangun jembatan kurva di antara ketiga titik tersebut untuk memperkirakan kecepatan jaringan tepat saat beban menyentuh 60%[cite: 2, 5].

---

## Alur Kerja Kode

1. **Input Data Sampel:** Menyimpan tiga pasangan titik pengamatan ke dalam array NumPy bertipe `float`:
   * `x = [20.0, 50.0, 80.0]` (Utilisasi *bandwidth* dalam %)[cite: 2]
   * `y = [45.0, 80.0, 95.0]` (*Throughput* dalam Mbps)[cite: 2]
2. **Pembentukan Polinomial:** Memanggil fungsi `lagrange(x, y)` dari `scipy.interpolate` untuk menyusun persamaan polinomial berderajat 2 secara otomatis[cite: 2].
3. **Evaluasi Titik Target:** Memasukkan nilai `x_target = 60` ke dalam fungsi `poly_lagrange(60)` untuk mendapatkan nilai prediksi `y_pred`[cite: 2].

---

## Hasil Estimasi Studi Kasus

| Parameter | Nilai |
| :--- | :--- |
| **Titik Sampel 1** | Utilisasi $20\%$ $\rightarrow$ $45,00\text{ Mbps}$[cite: 2, 5] |
| **Titik Sampel 2** | Utilisasi $50\%$ $\rightarrow$ $80,00\text{ Mbps}$[cite: 2, 5] |
| **Titik Sampel 3** | Utilisasi $80\%$ $\rightarrow$ $95,00\text{ Mbps}$[cite: 2, 5] |
| **Target Prediksi ($x$)** | Utilisasi **$60\%$**[cite: 2, 5] |
| **Hasil Estimasi ($y$)** | **`87.22 Mbps`**[cite: 2, 5] |

---

## Cara Menjalankan

* **File Notebook:** `Interpolasi.ipynb`[cite: 2]
* **Library:** `numpy`, `scipy`
* Jalankan sel kode di **Google Colab** atau **Jupyter Notebook** lokal.