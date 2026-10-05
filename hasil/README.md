# Hasil Eksperimen

Folder ini menyimpan keluaran eksperimen penelitian dalam mode `full`.

## Daftar Berkas

| Berkas | Isi |
|---|---|
| configuration.json | Konfigurasi, versi pustaka, identitas dataset, dan rancangan eksperimen |
| run_summary.json | Ringkasan pelaksanaan dan model terpilih |
| split_summary.csv | Komposisi pembagian data |
| cv_summary.csv | Ringkasan keluaran validasi silang |
| model_decisions.json | Keputusan model, parameter terpilih, dan ambang keputusan |
| test_results.csv | Metrik pengujian model |
| baseline_results.csv | Hasil pembanding sederhana |
| cluster_bootstrap_ci.csv | Interval bootstrap kanal |
| paired_cluster_differences.csv | Selisih performa berpasangan antarprosedur |
| block_permutation_summary.csv | Kepentingan blok fitur berdasarkan pengacakan |

## Rancangan Pengujian

Enam skenario utama membandingkan XGBoost, Random Forest, dan Linear SVM tanpa resampling serta dengan SMOTENC.

Tiga skenario tambahan menggunakan ketiga algoritma tanpa statistik kanal dan tanpa resampling.

Pengujian menggunakan 7.639 video dari 44 kanal, termasuk 149 video viral.

## Penafsiran

- Model utama dipilih melalui AP validasi silang, bukan berdasarkan skor uji tertinggi.
- Ambang keputusan dipilih pada bagian data pemilihan ambang.
- Interval bootstrap menggambarkan variasi sampel kanal uji pada model tetap, tanpa pelatihan ulang.
- Interval selisih yang melintasi nol tidak membuktikan kesetaraan.
- Kepentingan blok fitur tidak menunjukkan hubungan sebab-akibat.
- Bagian uji pernah diamati pada eksperimen pendahuluan sehingga hasil merupakan evaluasi ulang.

## Kelengkapan

Arsip ringkas hasil penelitian memuat sepuluh berkas CSV/JSON di atas. Model tersimpan dan prediksi per video tidak terdapat dalam arsip tersebut.

Jika berkas tambahan disertakan, berkas harus berasal dari pelaksanaan eksperimen yang sama dan dicantumkan dalam dokumentasi ini.