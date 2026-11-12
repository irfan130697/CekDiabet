# CekGula: Prediksi Diabetes

Aplikasi web sederhana untuk memperkirakan risiko diabetes dari lima data kesehatan. Proyek ini adalah bagian deploy dari notebook **Prediksi Diabetes 2026** yang memakai dataset Pima Indians Diabetes.

Seluruh aplikasi berjalan di browser (satu file `index.html`), tanpa server dan tanpa instalasi.

## Fitur

- Form input lima fitur: Kehamilan, Glukosa, Ketebalan Kulit, IMT, dan Usia
- Pengukur peluang diabetes dalam persen dengan status "Terindikasi" atau "Tidak terindikasi"
- Rincian kontribusi tiap faktor terhadap hasil
- Validasi isian, tampilan responsif untuk HP, dan mode terang atau gelap
- Antarmuka berbahasa Indonesia

## Struktur Repositori

```
.
├── index.html   # seluruh aplikasi (HTML, CSS, JavaScript)
└── README.md
```

## Cara Menjalankan

**Lokal:** unduh repositori, lalu buka `index.html` di browser.

**GitHub Pages:**

1. Buat repositori baru di GitHub, lalu unggah `index.html` dan `README.md`.
2. Buka **Settings → Pages**.
3. Pada **Source**, pilih **Deploy from a branch**, lalu pilih branch `main` dan folder `/ (root)`.
4. Simpan. Setelah beberapa menit, situs aktif di `https://<username>.github.io/<nama-repositori>/`.

## Tentang Model

Notebook asli melatih model **K-Nearest Neighbors** dengan fitur hasil seleksi: `Kehamilan`, `Glukosa`, `KetebalanKulit`, `IMT`, dan `Usia`. Kolom `TekananDarah`, `Insulin`, dan `FungsiSilsilahDiabetes` dibuang pada tahap seleksi fitur.

Halaman ini **tidak memuat file model `.pkl`** karena berjalan sepenuhnya di sisi klien. Perhitungannya memakai pendekatan regresi logistik dengan bobot perkiraan dari pola dataset yang sama:

```
logit = -9.0 + 0.13·Kehamilan + 0.037·Glukosa + 0.003·KetebalanKulit + 0.085·IMT + 0.012·Usia
peluang = 1 / (1 + e^(-logit))
```

Status "Terindikasi" ditampilkan jika peluang mencapai 50% atau lebih. Hasilnya cocok untuk demonstrasi dan tidak identik dengan keluaran model KNN.

### Memakai model KNN asli

Untuk hasil yang sama dengan notebook, sajikan model lewat backend, misalnya Gradio, Hugging Face Spaces, atau Flask. Pastikan transformasi `QuantileTransformer` yang dipakai saat pelatihan ikut disimpan dan diterapkan lagi pada data baru sebelum prediksi. Selain itu, latih transformer hanya pada fitur (tanpa kolom `Outcome`) dan setelah data dipisah menjadi train dan test, agar tidak terjadi kebocoran data.

## Dataset

[Pima Indians Diabetes Database](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database): 768 baris dan 9 kolom, berisi data pasien perempuan berusia minimal 21 tahun.

## Penafian

Aplikasi ini dibuat untuk pembelajaran dan **bukan alat diagnosis medis**. Konsultasikan hasil pemeriksaan kadar gula darah dengan dokter atau laboratorium.

## Teknologi

HTML, CSS, dan JavaScript murni. Font dari Google Fonts (Bricolage Grotesque dan Public Sans), dengan font sistem sebagai cadangan.

## Lisensi

Tambahkan lisensi pilihan Anda (misalnya MIT) pada file `LICENSE`.
