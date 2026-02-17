# Koreksi Bias Data CHIRPS Menggunakan Algoritma Genetika (Genetic Algorithm)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Research-orange)

## Deskripsi Proyek

Repositori ini memuat implementasi komputasi untuk koreksi bias pada data estimasi curah hujan satelit **CHIRPS (Climate Hazards Group InfraRed Precipitation with Station data) v3.0**. Penelitian ini bertujuan untuk meningkatkan akurasi data presipitasi satelit terhadap data observasi permukaan (stasiun penakar hujan) di wilayah Provinsi Jambi, Indonesia.

Metode yang digunakan adalah pendekatan koreksi non-linear (*Power Law*) yang parameternya dioptimasi menggunakan **Algoritma Genetika (Genetic Algorithm/GA)**. Pendekatan ini dipilih untuk meminimalkan *error* sistematik yang sering ditemukan pada data satelit akibat faktor topografi dan kondisi atmosfer lokal.

## Metodologi

Koreksi bias dilakukan dengan memodelkan hubungan antara curah hujan satelit ($P_{sat}$) dan curah hujan observasi ($P_{obs}$) menggunakan persamaan pangkat:

$$P_{corr} = a \times P_{sat}^b$$

Dimana:
- $P_{corr}$: Curah hujan terkoreksi.
- $P_{sat}$: Data mentah CHIRPS.
- $a$: Parameter skala (Scale factor).
- $b$: Parameter bentuk (Shape factor).

Kedua parameter ($a$ dan $b$) ditentukan melalui proses optimasi **Algoritma Genetika** dengan fungsi objektif (fitness function) meminimalkan *Root Mean Square Error (RMSE)* pada dataset pelatihan.

## Fitur Utama

Script ini mencakup seluruh alur kerja pemrosesan data, meliputi:
1.  **Pra-pemrosesan Data Spasial**: 
    - *Clipping* data raster global CHIRPS sesuai batas administrasi (Shapefile).
    - Ekstraksi nilai piksel (Point Sampling) pada koordinat stasiun hujan.
2.  **Optimasi Model (GA)**:
    - Pencarian parameter optimal menggunakan pustaka `pygad`.
    - Konfigurasi populasi, mutasi, dan crossover yang dapat disesuaikan.
3.  **Penerapan Koreksi**:
    - Aplikasi model pada data runtun waktu (time-series) raster 2009-2020.
    - Penyimpanan output dalam format GeoTIFF standar.
4.  **Validasi Statistik**:
    - Perhitungan performa model menggunakan metrik NSE (*Nash-Sutcliffe Efficiency*), Pearson Correlation ($r$), dan RSR.
    - Visualisasi perbandingan data sebelum dan sesudah koreksi.

## Struktur Direktori

Pastikan struktur folder data Anda di Google Drive/Local sesuai dengan konfigurasi berikut:

```text
├── data/
│   ├── CHIRPS v3/          # File .tif data mentah CHIRPS
│   ├── Batas Adm/          # Shapefile batas wilayah studi
│   └── Data Stasiun/       # File .csv data curah hujan observasi
├── output/
│   ├── bias_corrected_ga/  # (Auto-generated) Hasil raster terkoreksi
│   └── validation/         # (Auto-generated) Tabel & plot validasi
├── script.py               # Script utama
├── requirements.txt        # Daftar pustaka Python
└── README.md               # Dokumentasi proyek
