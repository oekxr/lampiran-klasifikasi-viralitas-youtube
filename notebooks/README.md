# Notebook Penelitian

| Berkas | Fungsi |
|---|---|
| `01_pengumpulan_data.ipynb` | Pencarian kanal dan pengumpulan metadata melalui YouTube Data API v3 |
| `02_eksperimen_penelitian.ipynb` | Pembersihan, pembentukan label dan fitur, pelatihan, serta evaluasi model |

## Notebook Pengumpulan

Notebook pengumpulan dijalankan melalui Google Colaboratory dan membutuhkan YouTube Data API key.

Simpan key dalam Colab Secrets dengan nama `YOUTUBE_API_KEY`. Pembacaan key dapat dilakukan dengan:

```python
from google.colab import userdata

API_KEY = userdata.get("YOUTUBE_API_KEY")
```

Sesuaikan nama variabel dengan program. Jangan menuliskan nilai key dalam kode atau keluaran notebook yang diunggah.

Pengumpulan ulang tidak diperlukan untuk membaca hasil penelitian yang tersedia dan dapat menghasilkan metadata berbeda dari dataset penelitian.

## Notebook Eksperimen

1. Buka notebook di Google Colaboratory.
2. Jalankan sel instalasi pada sesi baru.
3. Sesuaikan `DATA_PATH` dan `OUTPUT_ROOT`.
4. Pastikan `RUN_MODE='full'`.
5. Jalankan sel secara berurutan.

Bagian fit digunakan untuk pelatihan dan pencarian hiperparameter. Data kalibrasi, pemilihan ambang, serta uji memiliki fungsi terpisah dan mempertahankan distribusi kelas asli.

Mode `smoke` hanya memeriksa fungsi program; hasilnya bukan hasil penelitian.

## Lingkungan

Pustaka utama mengikuti versi pada `../requirements.txt` dan konfigurasi eksperimen. Notebook awal menargetkan Python 3.11–3.12; keberhasilan pada lingkungan lain perlu diperiksa saat dijalankan.

Perubahan nama berkas notebook tidak mengubah metode penelitian. Namun, lokasi dataset dan keluaran perlu disesuaikan dengan lingkungan pengguna.

Notebook yang dirujuk naskah harus berasal dari pelaksanaan yang menghasilkan berkas pada folder `../hasil/`.