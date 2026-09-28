# Klasifikasi Tingkat Kemiskinan Kabupaten/Kota di Indonesia

Perbandingan algoritma machine learning untuk mengklasifikasikan kabupaten/kota di Indonesia
ke dalam kategori **Miskin** atau **Tidak Miskin**, sebagai upaya mendukung
**SDGs 1: Tanpa Kemiskinan**.

## Deskripsi

Proyek ini melatih dan membandingkan 6 algoritma klasifikasi:

- Decision Tree
- Random Forest
- Naive Bayes
- K-Nearest Neighbors (KNN)
- Support Vector Machine (SVM)
- Logistic Regression

Selain membandingkan akurasi, proyek ini juga memeriksa adanya **data leakage**: kolom
*Persentase Penduduk Miskin (P0)* diduga menjadi dasar pembentuk label, sehingga model
diuji ulang tanpa kolom tersebut agar hasilnya lebih jujur.

## Dataset

- **Nama:** Klasifikasi Tingkat Kemiskinan di Indonesia
- **Sumber:** Kaggle (dataset publik, bersumber dari data BPS)
- **Ukuran:** 514 baris (kabupaten/kota), 13 kolom
- **Label:** `Klasifikasi Kemiskinan` (0 = Tidak Miskin, 1 = Miskin)
- **Catatan:** kelas tidak seimbang (sekitar 88% Tidak Miskin, 12% Miskin), sehingga
  ditangani dengan SMOTE.
- **Format file:** pemisah kolom `;` dan desimal `,` (format Eropa).

Unduh file CSV dari Kaggle, lalu letakkan di folder yang sama dengan notebook dengan nama
`Klasifikasi_Tingkat_Kemiskinan_di_Indonesia.csv`.

## Alur Notebook

1. Import library
2. Memuat dan membersihkan data
3. Eksplorasi data (EDA)
4. Persiapan data: pisah fitur/label, SMOTE, split 80:20
5. Melatih dan membandingkan 6 algoritma
6. Memilih model terbaik, confusion matrix, feature importance
7. Pengecekan dan penanganan data leakage
8. Model final dan uji coba dengan input manual
9. Kesimpulan

## Hasil Ringkas

| Model | Akurasi (dengan P0) | Akurasi (tanpa P0) |
|---|---|---|
| Random Forest | 98,34% | **91,16%** |
| Decision Tree | 96,69% | 88,40% |
| Logistic Regression | 97,24% | 87,85% |
| KNN | 82,32% | 82,32% |
| SVM | 82,32% | 82,32% |
| Naive Bayes | 79,01% | 79,01% |

Akurasi turun cukup jauh setelah kolom P0 dibuang, yang menguatkan dugaan data leakage.
Model final yang dipakai adalah **Random Forest tanpa kolom P0** (akurasi 91,16%).

## Cara Menjalankan

```bash
git clone https://github.com/USERNAME/NAMA-REPO.git
cd NAMA-REPO

python -m venv venv
source venv/bin/activate

pip install -r requirements.txt
jupyter notebook kemiskinan.ipynb
```

Notebook juga bisa dibuka langsung di VS Code (ekstensi Jupyter) atau Google Colab.

## Struktur Repo

```
.
├── kemiskinan.ipynb
├── Klasifikasi_Tingkat_Kemiskinan_di_Indonesia.csv
├── requirements.txt
└── README.md
```

## Keterbatasan

- Data berada pada level kabupaten/kota, bukan rumah tangga, sehingga model memprediksi
  status wilayah, bukan status keluarga.
- Data tidak diperbarui secara berkala, jadi hasilnya untuk pembelajaran metode, bukan
  untuk keputusan kebijakan terkini.
- SMOTE dilakukan sebelum pembagian data latih/uji, sehingga data sintetis bisa muncul di
  kedua bagian dan akurasi bisa sedikit terlalu optimistis.

## Sumber Data

Badan Pusat Statistik (BPS) melalui dataset publik di Kaggle.
