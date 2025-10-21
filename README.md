# Project-A-Kelompok-3-PBA-GASAL-2025-2026
# 🧠 Analisis Sentimen Berita Online Mengenai Aplikasi MitraDarat Menggunakan TF-IDF dan Support Vector Machine

## 📋 Deskripsi Proyek
Repositori ini berisi proyek *Natural Language Processing (NLP)* untuk menganalisis sentimen berita daring yang membahas **aplikasi MitraDarat**, sebuah platform digital layanan transportasi darat dari Kementerian Perhubungan Republik Indonesia.  
Penelitian ini bertujuan untuk mengetahui persepsi publik terhadap MitraDarat melalui pemberitaan online dengan pendekatan **TF-IDF** sebagai *feature extraction* dan **Support Vector Machine (SVM)** sebagai algoritma klasifikasi.

---

### 🧰 Built With
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-85C1E9?style=for-the-badge)
![Sastrawi](https://img.shields.io/badge/Sastrawi-00897B?style=for-the-badge)
![spaCy](https://img.shields.io/badge/spaCy-09A3D5?style=for-the-badge&logo=spacy&logoColor=white)
![Stanza](https://img.shields.io/badge/Stanza-0C4B33?style=for-the-badge)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-5A9BD4?style=for-the-badge)
![WordCloud](https://img.shields.io/badge/WordCloud-FFB300?style=for-the-badge)
![TextBlob](https://img.shields.io/badge/TextBlob-4CAF50?style=for-the-badge)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 🧩 Struktur File
├── PBA_MitraDarat.ipynb
├── news_mitradarat_scraped.csv
├── news_mitradarat_preprocessed.csv
├── news_mitradarat_preprocessed2.csv
├── README.md

---

## ⚙️ Tahapan Penelitian
### 1️⃣ Data Acquisition  
- Data diperoleh melalui **web scraping** menggunakan *Python*, pustaka **Requests** dan **BeautifulSoup**, dari berbagai portal berita nasional melalui RSS Feed Google News.  
- Kriteria pencarian: artikel yang mengandung kata kunci “MitraDarat” dalam periode **Januari 2023 – Oktober 2025**.  
- Data disimpan dalam format `.csv` dengan kolom:
  | No | Field Name | Deskripsi |
  |----|-------------|-----------|
  | 1 | `title` | Judul artikel berita |
  | 2 | `publication_date` | Tanggal publikasi |
  | 3 | `content_raw` | Isi teks artikel |
  | 4 | `source` | Sumber media |
  | 5 | `url` | Tautan berita asli |

---

### 2️⃣ Data Preprocessing  
- Semua teks dibersihkan menggunakan tahapan:
  - *Case Folding*  
  - *Tokenization* (NLTK)  
  - *Stopword Removal* (bahasa Indonesia + Inggris)  
  - *Stemming* menggunakan pustaka **Sastrawi**  
- Hasil bersih disimpan di kolom `content_clean` dengan total **174 artikel**.  

---

### 3️⃣ Feature Extraction (TF-IDF)
- Representasi teks dilakukan menggunakan **TfidfVectorizer** dari *scikit-learn*.
- Parameter: `max_features=1000`, `ngram_range=(1,1)` (unigram).
- Kata dengan bobot TF-IDF tertinggi di seluruh korpus:
mudik, gratis, daftar, kemenhub, bus, aplikasi, program, darat, motor

- Dataset yang tidak memiliki bobot fitur (kosong) dieliminasi otomatis.

---

### 4️⃣ Analisis Tambahan
#### 🔹 Distribusi Waktu Publikasi
- Artikel terbanyak diterbitkan pada **Kuartal I (Januari–Maret 2025)**.  
- Dominasi ini selaras dengan periode pembukaan dan pendaftaran program *Mudik Gratis*.  

#### 🔹 POS Tagging (Stanza)
- Dominasi kategori:
NOUN 12092
PROPN 11700
VERB 4855
→ Menunjukkan teks berita bersifat informatif dan deskriptif.  

#### 🔹 Named Entity Recognition (spaCy)
- Label entitas paling sering:
PER 3657
LOC 1830
MISC 1283
ORG 668
- Entitas populer: *Mitra Darat*, *Kemenhub*, *Jakarta*, *Wonogiri*, *Yogyakarta*.

---

### 5️⃣ Sentiment Analysis
#### 🔹 Label Awal (TextBlob)
- Analisis awal dilakukan dengan **TextBlob** untuk menghasilkan skor polaritas (*polarity*):  
- `> 0` → *positive*  
- `< 0` → *negative*  
- `= 0` → *neutral*  

#### 🔹 Model Klasifikasi (SVM)
- Algoritma: `LinearSVC` dari *scikit-learn*  
- Split data: 80% training, 20% testing  
- **Akurasi Model:** `84.6%`  

| Label | Precision | Recall | F1-score |
|--------|------------|--------|-----------|
| Negative | 1.00 | 0.57 | 0.73 |
| Neutral  | 0.81 | 1.00 | 0.89 |
| Positive | 1.00 | 0.50 | 0.67 |

- **Akurasi per kelas:**  
- Positive → 50%  
- Neutral → 100%  
- Negative → 60%

#### 🔹 Visualisasi Sentimen
- *WordCloud* menunjukkan perbedaan konteks yang jelas:
| Sentimen | Kata Dominan | Makna |
|-----------|---------------|--------|
| **Positif** | gratis, program, layanan, mudik, aplikasi | Fokus pada manfaat & inovasi |
| **Negatif** | gugur, wajib, surat, arus, posko | Fokus pada kendala administratif |

---

## 🧠 Hasil dan Temuan
- Sebagian besar berita bersifat **netral hingga positif**, dengan fokus pada keberhasilan program *Mudik Gratis*.  
- Persepsi negatif lebih banyak disebabkan oleh **hambatan administratif** seperti dokumen dan kuota peserta.  
- Model **TF-IDF + SVM** berhasil memberikan gambaran objektif mengenai persepsi media terhadap aplikasi MitraDarat.  

---

## 📦 Requirements
Pastikan dependensi berikut telah terinstal:
```bash
pip install pandas numpy scikit-learn nltk Sastrawi seaborn matplotlib wordcloud spacy stanza textblob
python -m spacy download xx_ent_wiki_sm
```

## 🚀 Cara Menjalankan
1. Jalankan notebook PBA_MitraDarat.ipynb di Google Colab atau VSCode (Jupyter).
2. Pastikan file news_mitradarat_scraped.csv berada di direktori yang sama.
3. Notebook akan otomatis menghasilkan: File hasil preprocessing, Visualisasi POS, NER, WordCloud, dan distribusi waktu, Evaluasi model SVM.

## 👥 Anggota Kelompok
5026221093 - MUHAMMAD VIGGO FUDAIL
5026221163 - MOHAMMAD GERESIDI RACHMADI
5026221165 - SATRIA JATI KUSUMA
