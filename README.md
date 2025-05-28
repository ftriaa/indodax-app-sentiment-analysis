# 📱 Analisis Sentimen Ulasan Aplikasi Indodax di Google Play

Proyek ini menganalisis sentimen pengguna aplikasi **Indodax** di Google Play Store. Tujuannya untuk mengetahui persepsi publik terhadap aplikasi dan mengembangkan model klasifikasi otomatis terhadap ulasan.

## 🔍 Ringkasan Proyek

- **Sumber data**: Ulasan dari Google Play Store (via `google-play-scraper`)
- **Jumlah data**: 39.625 ulasan
- **Fitur utama**: 
  - `content` (teks ulasan)  
  - `score` (rating bintang 1–5)  
  - `at` (tanggal ulasan)

## 🎯 Tujuan Proyek

- Mengkategorikan sentimen menjadi **positif**, **netral**, dan **negatif**
- Melatih beberapa model untuk memprediksi sentimen berdasarkan teks

## ⚙️ Alur Analisis

1. **Scraping Data**
   Mengambil data ulasan dari Play Store dengan `google-play-scraper`

2. ### 🧹 Praproses Data  
   - Lowercasing  
   - Pembersihan simbol, angka, emoji  
   - Konversi emoji ke kata (kamus emoji)  
   - Normalisasi kata tidak baku (kamus slang)  
   - Tokenisasi dan stopword removal (`Sastrawi`)

3. ### 🏷️ Labeling Sentimen  
   Berdasarkan `score`:
   - Skor ≥ 4 → **Positif**
   - Skor = 3 → **Netral**
   - Skor ≤ 2 → **Negatif**

4. ### 🔠 Ekstraksi Fitur  
   - **TF-IDF** untuk Random Forest, SVM, dan MLP  
   - **Bag of Words** untuk Simple RNN

5. ### 🤖 Modeling  
   - Random Forest (60/40 split)  
   - SVM (70/30 split)  
   - MLP (65/35 split)  
   - Simple RNN (70/30 split)

6. ### 📊 Evaluasi  
   - Metrik: akurasi dan confusion matrix  
   - Visualisasi dan perbandingan performa model

## 🧪 Hasil Evaluasi

| Model               | Akurasi Test |
|--------------------|--------------|
| **SVM + TF-IDF**    | **91.76%**   |
| Simple RNN + BoW   | 91.42%       |
| MLP + TF-IDF       | 89.10%       |
| RF + TF-IDF        | 84.39%       |

✅ Model terbaik: **SVM + TF-IDF**

## 📈 Insight Ulasan

- **Positif**: ulasan mencakup kata seperti *terpercaya*, *cepat*, *bagus*, *mantap*, *mudah*
- **Negatif**: ulasan mengandung *error*, *lemot*, *gagal login*, *scam*, *susah dibuka*
- **Netral**: berupa *pertanyaan pengguna*, *saran*, atau *ulasan tidak jelas*

## 🧰 Tools & Library

| Kategori | Tools |
|----------|-------|
| Scraping | `google-play-scraper` |
| NLP & Analisis | `pandas`, `nltk`, `Sastrawi`, `numpy` |
| Modeling | `scikit-learn`, `tensorflow`, `keras` |
| Visualisasi | `matplotlib`, `seaborn`, `wordcloud` |
