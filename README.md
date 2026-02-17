# Koreksi Bias Data CHIRPS: Metode Algoritma Genetika (Genetic Algorithm)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Research-orange)

## Deskripsi Proyek

Repositori ini memuat implementasi kode Python untuk melakukan **koreksi bias non-linear** pada data estimasi curah hujan satelit **CHIRPS v3.0**. Metode yang digunakan adalah pendekatan *Power Law* yang parameternya dioptimasi secara otomatis menggunakan **Algoritma Genetika (Genetic Algorithm/GA)**.

Metode ini dirancang untuk menangani hubungan non-linear antara data satelit dan data observasi yang sering kali tidak dapat ditangkap dengan baik oleh metode regresi linear biasa.

## Metodologi

Bias pada data satelit dimodelkan menggunakan persamaan pangkat (*Power Law Equation*):

$$P_{corr} = a \times P_{sat}^b$$

Dimana:
- $P_{corr}$: Curah hujan terkoreksi.
- $P_{sat}$: Data mentah CHIRPS.
- $a$: Parameter Skala (*Scale Factor*).
- $b$: Parameter Bentuk (*Shape Factor*).

Nilai optimal untuk $a$ dan $b$ dicari menggunakan **Algoritma Genetika** melalui pustaka `pygad`. Algoritma ini melakukan simulasi evolusi (seleksi, crossover, mutasi) untuk meminimalkan nilai *Root Mean Square Error* (RMSE) antara data satelit dan stasiun kalibrasi.

## Prasyarat Instalasi

Script ini dikembangkan untuk lingkungan **Google Colab**. Berikut adalah dependensi pustaka yang digunakan:

### Daftar Pustaka
* **Optimasi AI:** `pygad` (Genetic Algorithm Engine)
* **Geospasial:** `rasterio`, `geopandas`, `shapely`, `folium`
* **Analisis Data:** `pandas`, `numpy`, `scikit-learn`, `scipy`
* **Visualisasi:** `matplotlib`, `seaborn`
* **Utilitas:** `tqdm`

### Instalasi
```bash
pip install rasterio geopandas shapely matplotlib scikit-learn pandas numpy seaborn tqdm folium pygad

```

## Struktur Direktori Data

Script ini membutuhkan struktur direktori data sebagai berikut di Google Drive:

```text
/Direktori_Project/
├── CHIRPS v3/                  # File raster .tif (input)
│   └── bias_corrected_ga/      # (Output) Hasil koreksi
├── Batas Adm Jambi/            # Shapefile batas wilayah
├── Data Stasiun BWS/           # File .csv data curah hujan observasi
└── script_ga.ipynb             # Script utama

```

## Cara Penggunaan

1. **Persiapan Data**: Siapkan data raster CHIRPS, Shapefile batas wilayah, dan data stasiun (Time Series CSV).
2. **Konfigurasi**: Sesuaikan path `BASE_DIR` dan parameter GA (jumlah generasi, populasi) jika diperlukan.
3. **Jalankan Script**:
* Script akan melakukan training GA untuk menemukan nilai  dan  terbaik.
* Menampilkan grafik konvergensi (Fitness vs Generation).
* Menerapkan rumus  ke seluruh data raster.


4. **Validasi**: Hasil validasi statistik (NSE, R, RSR) akan disimpan otomatis.

## Contoh Hasil Optimasi

Algoritma Genetika mampu menemukan parameter yang unik untuk karakteristik wilayah studi.

**Contoh Hasil Parameter:**

* **Scale (a):** 1.1542
* **Shape (b):** 0.9821
* **Persamaan:** 

**Performa Statistik:**

| Stasiun Validasi | NSE (Raw) | NSE (Corrected) | RSR (Raw) | RSR (Corrected) |
| --- | --- | --- | --- | --- |
| **Muara Tembesi** | -0.45 | **0.68** | 1.20 | **0.55** |
| **Rantau Pandan** | 0.12 | **0.62** | 0.93 | **0.61** |

## Penulis

**Jariyan Arifudin** Mahasiswa Geografi Lingkungan

Universitas Gadjah Mada (UGM)

## Lisensi & Sitasi

Kode ini didistribusikan di bawah **MIT License**.
Jika Anda menggunakan metode ini untuk penelitian, silakan sitasi repositori ini:

> Arifudin, J. (2026). *Koreksi Bias Data CHIRPS: Metode Algoritma Genetika (Genetic Algorithm)*. GitHub Repository.
