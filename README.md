# 📊 Topic Modeling LDA — Program Makan Bergizi Gratis (MBG)

Proyek ini mengimplementasikan **Latent Dirichlet Allocation (LDA)** untuk menemukan topik-topik laten dari komentar publik terhadap program **Makan Bergizi Gratis (MBG)** di BBC News Indonesia. Pipeline mencakup preprocessing teks (normalisasi, tokenisasi, stopword removal), pemodelan topik, pelabelan, dan visualisasi hasil.

> **Dataset:** BBC News Indonesia — *"Setahun Program MBG - Siapa yang diuntungkan?"*  
> **Total Komentar:** 6.805 dokumen  
> **Topik Optimal:** 4 topik | **Coherence Score (C_v):** 0.5247

---

## 📁 Struktur Repository

```
MBG_LDA/
│
├── 1. Topic_Modelling_LDA_MBG Dengan data baru .ipynb   # Notebook utama (pipeline LDA)
├── backup_data_gabungan_concat.xlsx                      # Dataset komentar gabungan (raw)
├── normalization_dict_merged.csv                         # Kamus normalisasi (1.629 entri)
│
└── output/
    ├── data/
    │   ├── LDA_Topic_Labeling_MBG.ipynb                 # Notebook pelabelan topik
    │   ├── preprocessed_comments.csv                     # Teks hasil preprocessing
    │   ├── comments_with_topics.csv                      # Komentar + distribusi topik
    │   ├── comments_labeled_final.csv                    # Dataset final berlabel
    │   ├── fig1_distribusi_topik.png
    │   ├── fig2_distribusi_probabilitas.png
    │   ├── fig3_heatmap_sumber_topik.png
    │   ├── fig4_stacked_bar_sumber.png
    │   ├── fig5_tren_temporal.png
    │   ├── fig6_wordcloud_topik.png
    │   ├── fig7_panjang_komentar.png
    │   └── fig8_kepercayaan_penugasan.png
    │
    ├── models/
    │   ├── lda_model_final.model                         # Model LDA tersimpan (Gensim)
    │   ├── lda_model_final.model.expElogbeta.npy
    │   ├── lda_model_final.model.id2word
    │   ├── lda_model_final.model.state
    │   ├── corpus.pkl                                    # Corpus BoW tersimpan
    │   ├── dictionary.pkl                                # Dictionary Gensim
    │   ├── doc_topic_distribution.npy                   # Matriks distribusi topik
    │   └── topic_info.pkl                               # Metadata topik
    │
    ├── reports/
    │   └── topic_modelling_summary.txt                  # Laporan lengkap hasil modeling
    │
    └── visualizations/
        ├── 01_comment_statistics.png                    # Distribusi panjang komentar
        ├── 02_top_idf_features.png                      # Top 20 fitur berdasarkan IDF
        ├── 03_coherence_perplexity.png                  # Evaluasi model (coherence & perplexity)
        ├── 04_topics_words.png                          # Kata kunci utama per topik
        ├── 05_topic_distribution.png                    # Distribusi prevalensi topik
        ├── 06_wordclouds_topics.png                     # Word cloud tiap topik
        ├── 07_interactive_ldavis.html                   # Visualisasi interaktif (buka di browser)
        ├── 08_document_topic_heatmap.png                # Heatmap distribusi dokumen-topik
        └── 09_confidence_distribution.png               # Distribusi confidence score
```

---

## 🔍 Alur Pipeline

```
Raw Text  (backup_data_gabungan_concat.xlsx)
   ↓
Normalisasi  (normalization_dict_merged.csv — 1.629 entri)
   ↓
Tokenisasi & Stopword Removal
   ↓
TF-IDF Filtering  (max 5.000 fitur, n-gram 1–2)
   ↓
LDA Model  (Gensim LdaMulticore, 4 topik)     ← Notebook 1
   ↓
Evaluasi  (Coherence C_v: 0.5247 | Perplexity: -6.99)
   ↓
Pelabelan Topik per Dokumen                    ← Notebook 2
   ↓
Dataset Final  (comments_labeled_final.csv)
   ↓
Visualisasi & Analisis  (9 chart + 1 HTML interaktif)
```

---

## 🗂️ Hasil Topik

| Topik | Kata Kunci Utama | Jumlah Dokumen | Proporsi |
|---|---|---|---|
| Topik 1 | untung, rakyat, kerja, negara, anggaran | 1.458 | 21.4% |
| Topik 2 | program, gratis, Prabowo, presiden, gizi | 1.381 | 20.3% |
| Topik 3 | makan, anak, sekolah, gizi, racun | 2.387 | 35.1% |
| Topik 4 | program, sekolah, baik, korupsi, dana | 1.579 | 23.2% |

> **Rata-rata confidence score:** 0.78 | **Min:** 0.25 | **Max:** 0.997

---

## ⚙️ Konfigurasi Model

| Parameter | Nilai |
|---|---|
| Library | Gensim `LdaMulticore` |
| Jumlah Topik | 4 |
| Passes | 10 |
| Workers | 4 |
| N-gram | Unigram + Bigram (1,2) |
| Max TF-IDF Features | 5.000 |
| Min DF / Max DF | 2 / 80% |

---

## 🛠️ Teknologi yang Digunakan

| Library | Kegunaan |
|---|---|
| `gensim` | LDA modeling (`LdaMulticore`), TF-IDF, coherence score |
| `nltk` / `PySastrawi` | Tokenisasi & stemming Bahasa Indonesia |
| `pandas` / `numpy` | Manipulasi data & matriks |
| `pyLDAvis` | Visualisasi topik interaktif (HTML) |
| `matplotlib` / `seaborn` | Chart & heatmap |
| `wordcloud` | Word cloud per topik |

---

## 🚀 Cara Menjalankan

1. Clone repository ini:
   ```bash
   git clone https://github.com/Keiwaz/MBG_LDA.git
   cd MBG_LDA
   ```

2. Install dependensi:
   ```bash
   pip install gensim nltk PySastrawi pyLDAvis pandas openpyxl matplotlib seaborn wordcloud
   ```

3. Jalankan notebook secara berurutan:

   **Step 1 — Preprocessing & LDA Modeling:**
   ```bash
   jupyter notebook "1. Topic_Modelling_LDA_MBG Dengan data baru .ipynb"
   ```

   **Step 2 — Pelabelan Topik:**
   ```bash
   jupyter notebook "output/data/LDA_Topic_Labeling_MBG.ipynb"
   ```

4. Untuk visualisasi interaktif, buka langsung di browser:
   ```
   output/visualizations/07_interactive_ldavis.html
   ```

---

## 📄 Laporan

Ringkasan lengkap hasil pemodelan tersedia di:
```
output/reports/topic_modelling_summary.txt
```

---

## 👤 Author

**Kevin** — Mahasiswa S1 Manajemen, Universitas Terbuka  
🔗 [github.com/Keiwaz](https://github.com/Keiwaz)
