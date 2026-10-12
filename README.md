# Prediksi Kebakaran Hutan dengan Machine Learning

Perbandingan algoritma **Random Forest** dan **Logistic Regression** untuk memprediksi apakah suatu hari
terjadi kebakaran hutan atau tidak, berdasarkan data cuaca dan indeks kekeringan.
Proyek ini mendukung **SDGs 15: Ekosistem Daratan**.

## Deskripsi

Masalah ini adalah klasifikasi dua kelas: **Kebakaran** atau **Tidak Kebakaran**.
Dua model dilatih dan dibandingkan dari akurasi pada data uji (20% data yang tidak dipakai saat pelatihan).
Model terbaik kemudian dipakai untuk menebak satu hari baru lewat input manual di notebook.

## Dataset

- **Nama:** The Extended Algerian Forest Fires Dataset
- **Sumber:** Faroudja Abid, IEEE Dataport / Mendeley Data (2026)
- **Ukuran:** 1215 hari pengamatan dari 10 lokasi di Aljazair (tahun 2012, 2017, dan 2021)
- **Label:** `Status` (633 hari Kebakaran, 582 hari Tidak Kebakaran, sudah seimbang)
- **File:** `The_extended_Algerian_forest_fires_dataset.xlsx`

### Fitur (10 kolom)

| Fitur | Arti |
| --- | --- |
| Suhu | Suhu udara siang hari (°C) |
| Kelembapan | Kelembapan relatif udara (%) |
| Angin | Kecepatan angin (km/jam) |
| Hujan | Curah hujan seharian (mm) |
| FFMC | Kekeringan daun dan ranting di permukaan tanah |
| DMC | Kekeringan tumpukan daun lapuk |
| DC | Kekeringan lapisan tanah yang dalam |
| ISI | Kecepatan api menyebar di awal |
| BUI | Jumlah bahan bakar yang tersedia untuk terbakar |
| FWI | Tingkat bahaya api secara keseluruhan |

## Alur Notebook

1. Masalah
2. Data
3. Persiapan data: rapikan nama kolom dan label, pisah fitur/label, bagi data 80:20, standarisasi untuk Logistic Regression
4. Melatih model Random Forest dan Logistic Regression
5. Evaluasi: akurasi, confusion matrix, fitur paling berpengaruh
6. Penerapan: prediksi hari baru dengan input manual
7. Pemantauan
8. Kesimpulan

## Cara Menjalankan

```
git clone https://github.com/JollKimochi/AI_PROJECT.git
cd AI_PROJECT

python -m venv venv
source venv/bin/activate

pip install -r requirements.txt
jupyter notebook Prediksi_Kebakaran_Hutan.ipynb
```

Pastikan file dataset `.xlsx` berada di folder yang sama dengan notebook.
Notebook juga bisa dibuka di VS Code (ekstensi Jupyter) atau Google Colab.

## Struktur Repo

```
.
├── Prediksi_Kebakaran_Hutan.ipynb
├── The_extended_Algerian_forest_fires_dataset.xlsx
├── requirements.txt
└── README.md
```

## Hasil

Dievaluasi pada data uji (243 hari, 20% dari data):

| Model | Akurasi | Recall Kebakaran | Precision Kebakaran |
| --- | --- | --- | --- |
| Random Forest | **88,89%** | 84% | 94% |
| Logistic Regression | 87,65% | 87% | 89% |

- Menebak "kebakaran" terus hanya benar 52,10%, jadi kedua model jauh lebih baik dari tebakan buta.
- Selisih akurasi kedua model kecil, sehingga performanya cukup mirip.
- **Random Forest** terpilih sebagai model terbaik karena akurasinya paling tinggi.
- Fitur paling berpengaruh pada Random Forest: **FFMC** (27,8%), **FWI** (25,7%), dan **ISI** (17,3%).

## Keterbatasan

- Enam indeks kekeringan (FFMC sampai FWI) dihitung dari data cuaca, sehingga informasinya sebagian tumpang tindih.
- Akurasi dihitung dari satu pembagian data uji (80:20), jadi bisa berubah jika pembagiannya berbeda.
- File data tidak menjelaskan bagaimana label kebakaran ditentukan.
- Data berasal dari Aljazair, bukan Indonesia, sehingga model perlu dilatih ulang jika dipakai di daerah lain.

## Anggota Kelompok 1

- [Zolahuddin Ahmad](https://github.com/JollKimochi)
- [Nadya Trialika](https://github.com/dyalikaaaa)
- [Ranti Kurniasih](https://github.com/RantiKurniasih)
