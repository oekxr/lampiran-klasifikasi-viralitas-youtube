# Dataset Penelitian

## Berkas

`dataset_gabungan_final.csv`

Berkas ini merupakan data sumber sebelum pembersihan dan pembentukan label dalam notebook eksperimen.

| Kondisi | Video | Kanal |
|---|---:|---:|
| Data sumber | 38.963 | 219 |
| Data setelah pembersihan | 38.929 | 218 |

Sebanyak 34 video dikeluarkan pada pembersihan karena durasi bernilai nol. Sebanyak 32 video dengan penayangan nol termasuk dalam kelompok tersebut, sehingga jumlah pengecualian tidak dijumlahkan menjadi 66.

## Cakupan Data

- Sumber: YouTube Data API v3.
- Lingkup kanal: brainrot dan horor anak, termasuk gabungan keduanya.
- Periode publikasi: 1 Januari 2020 sampai 31 Desember 2025 UTC.
- Batas pengambilan: maksimal 300 ID video per kanal sebelum penyaringan periode.
- Statistik merupakan rekaman saat pengumpulan; periode publikasi bukan tanggal pengumpulan metadata.

## Kolom Dataset

| Kolom | Keterangan |
|---|---|
| video_id | Identitas video |
| title | Judul video |
| description | Deskripsi video |
| tags | Tag video; beberapa tag dipisahkan dengan karakter `\|` |
| published_at | Waktu publikasi video |
| duration_seconds | Durasi video dalam detik |
| view_count | Jumlah penayangan video |
| like_count | Jumlah suka |
| comment_count | Jumlah komentar |
| channel_id | Identitas kanal |
| channel_title | Nama kanal |
| channel_subscriber_count | Jumlah pelanggan kanal |
| channel_total_views | Jumlah penayangan kumulatif kanal |
| channel_video_count | Jumlah video kanal |

## Identitas Berkas

SHA-256 yang tercatat pada konfigurasi eksperimen:

```text
a8ce478d27b368fc67629e2552325aabbdf62f9187c003bde139de1030e193c2
```

Pada PowerShell, periksa berkas dengan:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath ".\data\dataset_gabungan_final.csv"
```

Bandingkan hasilnya dengan nilai di atas untuk memastikan dataset sama dengan yang digunakan dalam eksperimen.

## Penggunaan

Notebook melakukan pembersihan, pembentukan label, dan penyiapan fitur dari CSV ini.

Jangan mengganti CSV sumber dengan data yang telah dibersihkan tanpa menyesuaikan penjelasan dan prosedur eksperimen.

Penayangan, suka, dan komentar digunakan untuk membentuk label. Ketiganya, beserta turunannya dan identitas video/kanal, tidak menjadi masukan model.

Label dan distribusi kelas dapat berubah jika cakupan video atau waktu pengambilan metadata berubah.