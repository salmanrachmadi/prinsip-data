# Analisis Perilaku Siswa untuk Prediksi Performa Ujian Menggunakan Machine Learning

Proyek *data science* untuk mata kuliah **Prinsip Sains Data** (S2 Informatika, Telkom University).
Menganalisis faktor perilaku belajar yang memengaruhi performa ujian siswa, membangun model
klasifikasi kelulusan, dan merumuskan rekomendasi intervensi berbasis perilaku — dengan
penekanan pada pemisahan prediktor yang **prediktif** dari yang **aksiionabel**.

| | |
|---|---|
| **Penulis** | Salman Rachmadi (203012420009) |
| **Pembimbing** | Dr. Warih Maharani |
| **Tahun Ajaran** | 2025/2026  |
| **Dataset** | Student Exam Performance (Kaggle) — 10.000 siswa, 23 fitur |

---

## Abstrak

Dua pertanyaan penelitian diuji: (1) faktor perilaku mana yang berkorelasi dengan performa
ujian, dan (2) seberapa efektif model klasifikasi memprediksi kelulusan. **Jam belajar**
berkorelasi positif (r = 0,58) dan **media sosial** negatif (r = −0,25) dengan skor ujian
— keduanya signifikan setelah koreksi *Benjamini-Hochberg*. Untuk klasifikasi, **Logistic
Regression sedikit namun signifikan mengungguli Random Forest** (akurasi 87,05% vs 86,05%;
*corrected resampled t-test* p = 0,040), menandakan hubungan fitur-target relatif linear.
Ablation menunjukkan `previous_gpa` menyumbang ~13% akurasi namun bersifat non-aksiionabel;
model berbasis perilaku saja tetap mencapai ~75% (jauh di atas baseline 51,4%). Kontribusi
utama bersifat **metodologis**: memisahkan prediktor *actionable* dari *non-actionable*.

---

## Dataset

- **Sumber:** Student Exam Performance Dataset (Kaggle, unggahan user "ssssws").
- **Skala:** 10.000 siswa, 23 kolom mentah.
- **Target:** `pass_fail` (biner, cutoff skor = 50). Seimbang: Pass 48,6% / Fail 51,4%.
- **Evolusi fitur:** 23 → 18 (drop 5 skor internal) → 35 (encoding + 5 fitur turunan) →
  **19 fitur modeling** (16 dikecualikan: 1 identifier + 6 kategorikal mentah + 4 target + 5 *one-hot* grade).
- ⚠️ **Caveat:** provenans dataset tidak terverifikasi (kemungkinan sintetis) — temuan
  dibingkai sebagai kontribusi **metodologis/demonstratif**, bukan klaim substantif tentang
  populasi siswa nyata.

---

## Pertanyaan & Hipotesis Penelitian

| RQ | Hipotesis | Hasil |
|----|-----------|-------|
| **RQ1** — Faktor perilaku apa yang berkorelasi dengan performa? | **H1:** jam belajar (+), media sosial (−) berkorelasi signifikan | ✅ **DITERIMA** |
| **RQ2** — Seberapa efektif klasifikasi; apakah RF > LR? | **H2:** Random Forest mengungguli Logistic Regression | ⚠️ **TIDAK DIDUKUNG** (LR justru signifikan lebih baik, p = 0,040) |

**KPI akurasi ≥ 80% tercapai** (LR 87,05%, RF 86,05%).

> Catatan ruang lingkup: notebook juga memuat analisis **clustering eksploratoris** 
> lingkup pada RQ1 dan RQ2.** Lihat `project/deliverables/final_report/`.

---

## Metodologi (Pipeline CRISP-DM)

Setiap tahap diimplementasikan sebagai notebook berurutan (`project/notebooks/`):

| # | Notebook | Tahap |
|---|----------|-------|
| 01 | `01_proposal_exploration.ipynb` | Eksplorasi awal untuk proposal |
| 02 | `02_data_cleaning.ipynb` | Validasi, IQR outlier (dipertahankan), drop skor internal (23 → 18) |
| 03 | `03_feature_engineering.ipynb` | Encoding kategorikal + 5 fitur perilaku turunan |
| 04 | `04_eda.ipynb` | EDA: univariate, bivariate (korelasi), deteksi outlier |
| 05 | `05_visualizations.ipynb` | Visualisasi publikasi (Gambar 01–11) |
| 06 | `06_statistical_tests.ipynb` | Pearson/t-test/ANOVA + effect size, 95% CI, koreksi BH-FDR |
| 07 | `07_predictive_modeling.ipynb` | LR vs RF, GridSearchCV, 5-fold CV, ablation, ROC-AUC |
| 08 | `08_clustering.ipynb` | K-Means eksploratoris (RQ3 — di luar lingkup laporan) |
| 09 | `09_recommendation.ipynb` | Rekomendasi intervensi berbasis aturan |
| 10 | `10_final_insights.ipynb` | Sintesis hasil akhir |

**Prinsip analitis:** pada N = 10.000, signifikansi statistik mudah dicapai, sehingga setiap
uji dilengkapi **effect size** (Cohen's d, η²), **95% CI**, dan koreksi *multiple-comparison*
(Benjamini-Hochberg). Perbandingan model memakai *corrected resampled t-test* (Nadeau-Bengio)
untuk menghormati overlap antar-fold CV.

---

## Hasil Utama

- **H1 DITERIMA** — `study_hours_per_day` r = 0,58 (r² = 33%), `social_media_hours` r = −0,25;
  bertahan signifikan setelah BH-FDR.
- **H2 TIDAK DIDUKUNG** — LR menang di seluruh metrik (acc, prec, rec, F1, CV, ROC-AUC);
  selisih CV 0,48% tetap signifikan (konsisten antar-fold). Hubungan fitur-target relatif
  **linear** → kompleksitas RF tak membantu. LR direkomendasikan (unggul + interpretable).
- **Feature importance** `previous_gpa` dominan (0,42) namun non-aksiionabel.
- **Ablation** tanpa GPA: akurasi turun ke ~75% (GPA ~13%), namun model perilaku-only tetap
  jauh di atas baseline majority 51,4%.
- **Demografi** (income, ortu, gender) tidak bermakna praktis (χ² NS, d ≈ 0).

---

## Struktur Proyek

```
project/
├── datasets/                      # data mentah & terproses + model_results.json
├── notebooks/                     # pipeline 01–10 (lihat tabel di atas)
├── scripts/                       # generator dokumen/slide
│   ├── md_to_docx.py              # konversi .md → .docx (dukung --template)
│   ├── build_final_presentation.py# pembangun presentation_id.pptx
│   ├── build_proposal_pptx.py
│   └── ... (skrip legacy)
├── deliverables/
│   ├── figures/                   # 20 visualisasi PNG
│   ├── proposal/                  # proposal .md/.docx/.pdf + slides
│   ├── progress_report_1/         # Progress Report 1
│   ├── progress_report_2/         # Progress Report 2
│   ├── final_report/              # laporan akhir .md (ID + EN); .docx regenerasi
│   ├── presentation/              # presentation_id.pptx + naskah narasi
│   └── template/                  # template laporan akhir (Week 15)
└── docs/                          # plans, notes, task
```


---

## Cara Reproduksi

### 1. Lingkungan
```bash
pip install pandas numpy scikit-learn scipy matplotlib seaborn jupyter python-docx python-pptx
```

### 2. Jalankan pipeline analisis
Buka & run `project/notebooks/` berurutan dari `02_data_cleaning.ipynb` sampai `10_final_insights.ipynb`
(dijalankan dari direktori `project/notebooks/` agar path relatif `../datasets/` benar).
Notebook membaca `student_exam_performance_dataset.csv` dan menghasilkan dataset turunan +
`model_results.json` (sumber kebenaran metrik model).

---

## Tech Stack

**Python** · pandas · numpy · scikit-learn (LR, RF, GridSearchCV, K-Means) · scipy (uji
statistik) · matplotlib · seaborn · Jupyter

---

## Keterbatasan

- **Provenans data tidak terverifikasi** (kemungkinan sintetis) → temuan tak dapat
  digeneralisasi tanpa validasi pada data nyata.
- **Cross-sectional** → korelasi ≠ kausalitas.
- **previous_gpa mendominasi** prediksi → kontribusi perilaku sulit diisolasi tanpa ablation.
- Model **belum layak deployment operasional**; jika dipakai sebagai *early-warning*, gunakan
  varian tanpa-GPA dan terapkan governance (akses terbatas, *human-in-the-loop*).

---

## Deliverables

- **Proposal** — `project/deliverables/proposal/`
- **Final Report**  `project/deliverables/final_report/work.docx`
- **Presentation** — `project/deliverables/presentation/presentation_id.pptx`
- **Figures** — `project/deliverables/figures/` (20 PNG)

---

*Salman Rachmadi — 203012420009 · Prinsip Sains Data 2025/2026 · Telkom University*
