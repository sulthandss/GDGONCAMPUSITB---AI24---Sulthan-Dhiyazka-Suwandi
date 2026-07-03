# 📚 Sumber Belajar & Referensi - Week 1: Exploratory Data Analysis (EDA)

Halaman ini berisi daftar referensi dan sumber belajar yang relevan dan digunakan selama pengerjaan tugas **Week 1: Exploratory Data Analysis (EDA) dengan dataset Spotify Songs**. Sumber belajar dibagi menjadi beberapa kategori untuk memudahkan navigasi.

---

## 🎵 1. Dataset & Pemahaman Konsep Fitur Audio Spotify

*   **TidyTuesday Spotify Songs Dataset**:
    *   [TidyTuesday GitHub Repository (2020-01-21)](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-01-21/readme.md) — Halaman resmi repositori data, berisi kamus data (*data dictionary*) lengkap yang menjelaskan setiap kolom dan unit pengukurannya.
*   **Spotify Developer Documentation**:
    *   [Spotify Web API - Get Track's Audio Features](https://developer.spotify.com/documentation/web-api/reference/get-several-audio-features) — Penjelasan resmi dari Spotify mengenai cara kerja fitur-fitur seperti `danceability`, `energy`, `valence`, `loudness`, dan parameter audio lainnya.

---

## 🐼 2. Data Manipulation & EDA dengan Pandas

*   **Dokumentasi Resmi Pandas**:
    *   [Pandas API Reference](https://pandas.pydata.org/docs/reference/index.html) — Referensi utama untuk fungsi-fungsi Pandas.
    *   [Pandas GroupBy: Split-Apply-Combine](https://pandas.pydata.org/docs/user_guide/groupby.html) — Panduan mendalam tentang cara melakukan operasi agregasi data berkelompok (`groupby()`).
    *   [Handling Missing Data in Pandas](https://pandas.pydata.org/docs/user_guide/missing_data.html) — Dokumentasi pembersihan data kosong menggunakan `.isnull()`, `.isna()`, dan `.dropna()`.
*   **Tutorial & Panduan Praktis**:
    *   [Kaggle EDA Tutorial](https://www.kaggle.com/learn/data-visualization) — Kursus interaktif singkat untuk belajar visualisasi dan dasar-dasar EDA.
    *   [Pandas Cheat Sheet (Official)](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf) — Lembar contekan ringkas untuk sintaks-sintaks populer Pandas.

---

## 🧮 3. Operasi Vektor & Matematika dengan NumPy

*   **Dokumentasi Resmi NumPy**:
    *   [NumPy Quickstart Tutorial](https://numpy.org/doc/stable/user/quickstart.html) — Dasar-dasar pembuatan array dan operasi matematika dasar NumPy.
    *   [NumPy Broadcasting Guide](https://numpy.org/doc/stable/user/basics.broadcasting.html) — **Penting!** Panduan cara kerja operasi *broadcasting* (perluasan dimensi) yang digunakan untuk menghitung matriks jarak Euclidean antar-genre tanpa loop Python.
    *   [NumPy Mathematical Functions](https://numpy.org/doc/stable/reference/routines.math.html) — Dokumentasi operasi vektor seperti perkalian dot (`np.dot`), fungsi statistik (`np.nanpercentile`), matriks korelasi (`np.corrcoef`), dan aljabar linier norm (`np.linalg.norm`).

---

## 📐 4. Kemiripan (Similarity) & Jarak (Distance Metrics)

*   **Cosine Similarity**:
    *   [Cosine Similarity - Wikipedia](https://en.wikipedia.org/wiki/Cosine_similarity) — Penjelasan matematis tentang perbandingan sudut antara dua vektor berdimensi banyak.
    *   [Cosine Similarity in Machine Learning](https://towardsdatascience.com/cosine-similarity-how-does-it-measure-similarity-maths-behind-it-and-how-do-we-use-it-in-97a34195150) — Artikel praktis mengenai penerapan Cosine Similarity untuk sistem rekomendasi atau *user profiling*.
*   **Euclidean Distance**:
    *   [Euclidean Distance - Wikipedia](https://en.wikipedia.org/wiki/Euclidean_distance) — Dasar teori perhitungan jarak garis lurus antara dua titik dalam ruang Euclidean.

---

## 💻 5. Python Object-Oriented Programming (OOP) & Clean Code

*   **Python Type Hinting**:
    *   [Real Python - Python Type Checking](https://realpython.com/python-type-checking/) — Panduan lengkap penggunaan pengetikan statis (*type hints*) pada Python seperti pada class `SpotifyAnalyzer`.
*   **Google Python Style Guide**:
    *   [Google Style Docstrings](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings) — Contoh penulisan docstring standar industri (Google Style) dengan format Args, Returns, dan deskripsi kelas yang jelas.
