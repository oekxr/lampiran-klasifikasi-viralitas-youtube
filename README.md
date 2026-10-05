# Klasifikasi Viralitas Video YouTube

Repositori ini berisi kode, dataset, dan hasil eksperimen skripsi:

**KLASIFIKASI VIRALITAS VIDEO YOUTUBE PADA GENRE BRAINROT DAN HOROR ANAK BERBASIS ATRIBUT METADATA MENGGUNAKAN ALGORITMA XGBOOST, RANDOM FOREST, DAN SUPPORT VECTOR MACHINE**

## Identitas

- Nama: Wisnu Nugroho
- NIM: 22.11.4942
- Program Studi: Informatika
- Fakultas: Ilmu Komputer
- Universitas: Universitas AMIKOM Yogyakarta
- Dosen Pembimbing: Anggit Dwi Hartanto, M.Kom.

## Ringkasan Penelitian

Penelitian ini membandingkan XGBoost, Random Forest, dan Support Vector Machine linear untuk mengklasifikasikan viralitas relatif video YouTube berdasarkan metadata.

Brainrot dan horor anak merupakan lingkup konten kanal penelitian, bukan dua kelas prediksi. Target klasifikasi terdiri atas kelas viral dan tidak viral.

Data sumber berisi 38.963 video dari 219 kanal. Setelah pembersihan, data analisis terdiri atas 38.929 video dari 218 kanal, termasuk 712 video viral.

Penelitian bersifat retrospektif berdasarkan metadata saat pengumpulan, sehingga hasilnya tidak menunjukkan kemampuan memprediksi viralitas sejak video diunggah.

## Struktur Repositori

```text
klasifikasi-viralitas-youtube/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── README.md
│   ├── 01_pengumpulan_data.ipynb
│   └── 02_eksperimen_penelitian.ipynb
├── data/
│   ├── README.md
│   └── dataset_gabungan_final.csv
├── hasil/
│   ├── README.md
│   └── berkas hasil eksperimen CSV dan JSON
└── gambar/
    ├── README.md
    └── gambar alur dan hasil penelitian
```

## Dataset

Metadata dikumpulkan melalui YouTube Data API v3. Periode publikasi video adalah 1 Januari 2020 sampai 31 Desember 2025 UTC.

Pengumpulan menggunakan 38 kanal acuan dan 194 kanal tambahan. Dari 232 kanal yang diproses, 13 kanal tidak menghasilkan rekaman tersimpan, sehingga dataset sumber memuat 219 kanal.

Pengambilan dibatasi maksimal 300 ID video per kanal sebelum penyaringan periode. Kanal diperiksa berdasarkan kesesuaian judul, thumbnail, dan isi video dengan lingkup penelitian. Tidak dilakukan seleksi manual berdasarkan popularitas.

Dataset tersedia pada:

`data/dataset_gabungan_final.csv`

Keterangan kolom dan identitas dataset terdapat pada `data/README.md`.

## Metode Eksperimen

1. Memeriksa dan membersihkan metadata.
2. Membentuk label viralitas berdasarkan dua ukuran:
   - logaritma jumlah penayangan;
   - logaritma jumlah suka ditambah komentar.
3. Menghitung z-score kedua ukuran pada setiap kanal. Video diberi label viral jika kedua skor lebih besar dari 2,0.
4. Menyiapkan 12 fitur metadata.
5. Memisahkan data berdasarkan kanal:
   - fit: 19.573 video dari 111 kanal;
   - kalibrasi: 4.968 video dari 28 kanal;
   - pemilihan ambang: 6.749 video dari 35 kanal;
   - uji: 7.639 video dari 44 kanal.
6. Membandingkan tiga algoritma tanpa resampling dan dengan SMOTENC.
7. Menjalankan tiga skenario tambahan tanpa statistik kanal.
8. Memilih model berdasarkan rata-rata Average Precision pada validasi silang bagian fit.
9. Melakukan kalibrasi probabilitas dan pemilihan ambang keputusan menggunakan bagian data terpisah.
10. Mengevaluasi hasil, ketidakpastian melalui bootstrap kanal, dan kepentingan blok fitur.

Penayangan, suka, komentar, skor pembentuk label, serta identitas video dan kanal tidak digunakan sebagai fitur model.

## Cara Menjalankan

Notebook dikembangkan untuk Google Colaboratory. VS Code dapat digunakan untuk mengelola berkas dan melakukan commit.

1. Buka `notebooks/02_eksperimen_penelitian.ipynb` di Google Colaboratory.
2. Siapkan dataset CSV di Google Drive atau lingkungan eksekusi.
3. Sesuaikan `DATA_PATH` dengan lokasi dataset dan `OUTPUT_ROOT` dengan folder keluaran.
4. Gunakan `RUN_MODE='full'` untuk menjalankan eksperimen penelitian.
5. Jalankan sel secara berurutan. Jika instalasi meminta restart sesi, lakukan sebelum melanjutkan sel impor.
6. Periksa hasil pada folder keluaran.

Mode `smoke` hanya digunakan untuk pemeriksaan fungsi. Hasilnya tidak digunakan sebagai hasil skripsi.

Dependensi dapat dipasang melalui:

```python
%pip install -r requirements.txt
```

Perintah tersebut dijalankan dari lokasi tempat `requirements.txt` tersedia. Notebook juga memiliki sel instalasi pustaka utama.

Notebook pengumpulan membutuhkan YouTube Data API key milik pengguna. Key tidak boleh disertakan dalam repositori; gunakan Colab Secrets bernama `YOUTUBE_API_KEY`.

Mengumpulkan metadata kembali dapat menghasilkan nilai yang berbeda. Untuk memeriksa hasil skripsi, gunakan dataset yang sama dengan eksperimen penelitian.

## Ringkasan Hasil

Random Forest tanpa resampling terpilih berdasarkan rata-rata AP validasi silang sebesar 0,047754.

Pada data uji, model tersebut menghasilkan:

| Metrik | Nilai |
|---|---:|
| Average Precision | 0,028487 |
| Presisi | 0,025331 |
| Recall | 0,295302 |
| F1-score | 0,046660 |

XGBoost tanpa resampling memperoleh AP uji tertinggi secara deskriptif, yaitu 0,030412. Linear SVM tanpa resampling memperoleh F1-score uji tertinggi secara deskriptif, yaitu 0,048117.

SMOTENC belum menunjukkan peningkatan yang konsisten. Kepentingan fitur menunjukkan penggunaan informasi oleh model, bukan hubungan sebab-akibat terhadap viralitas.

Hasil lengkap tersedia pada folder `hasil/`.

## Batasan

- Data berasal dari kanal yang dipilih secara purposif dan tidak mewakili seluruh YouTube.
- Pemeriksaan genre dilakukan pada tingkat kanal; penelitian tidak memverifikasi usia penonton.
- Label viralitas relatif terhadap sampel video setiap kanal.
- Metadata merupakan rekaman saat pengumpulan, bukan riwayat perkembangan performa.
- Bagian uji pernah diamati pada eksperimen pendahuluan sehingga hasil merupakan evaluasi ulang.
- Pengujian berpasangan tidak mencakup seluruh pasangan antaralgoritma.
- Kemampuan klasifikasi pada kanal uji masih terbatas.