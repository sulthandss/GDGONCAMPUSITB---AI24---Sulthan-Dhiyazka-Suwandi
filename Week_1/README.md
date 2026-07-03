# 🎵 GDGOC ITB AI 2024 - Week 1: Exploratory Data Analysis (EDA) Spotify Dataset

Welcome to the **Week 1** repository of the Google Developer Groups On Campus (GDGOC) ITB - Artificial Intelligence program (Module 1). This folder contains the submission for Hands-On Module 1, focusing on Exploratory Data Analysis (EDA) of the Spotify Songs dataset.

The analysis and learning resources are documented in detail within:
📄 [**GDGOC_Week_1.pdf**](file:///c:/Users/Admin/Downloads/COMPFEST18_DSA_Solution_3_rapi-2/GDGONCAMPUSITB---AI24---Sulthan-Dhiyazka-Suwandi/Week%201/GDGOC_Week_1.pdf)  
📚 [**resources.md**](file:///c:/Users/Admin/Downloads/COMPFEST18_DSA_Solution_3_rapi-2/GDGONCAMPUSITB---AI24---Sulthan-Dhiyazka-Suwandi/Week%201/resources.md)

---

## 📊 Dataset Overview
- **Name**: Spotify Songs (TidyTuesday 2020-01-21)
- **Size**: 32,833 rows × 23 columns
- **Focus**: Analyzing audio features (danceability, energy, loudness, acousticness, valence, etc.) across 6 different playlist genres.

---

## 🚀 Ringkasan Tahapan Analisis (Stages)

### 📌 Stage 1: Setup & Inspeksi Awal
1. **Memuat Dataset**: Membaca dataset langsung dari URL mentah GitHub menggunakan `pandas`.
2. **Data Cleaning**: 
   - Mendeteksi dan menghapus baris dengan nilai kosong (*missing values*) pada kolom krusial seperti `track_name` dan `track_artist`.
   - Menganalisis data duplikat berdasarkan `track_id` (ditemukan 4.477 duplikasi).
   - **Justifikasi Strategi**: Menyiapkan dua versi data:
     - `df` (asli): untuk analisis berbasis genre (karena satu lagu bisa masuk ke beberapa genre playlist).
     - `df_unique`: hasil deduplikasi untuk analisis fitur audio per lagu guna menghindari bias statistik.
3. **Statistik Deskriptif**: Menghitung Mean, Median, Standar Deviasi, dan Interquartile Range (IQR) secara manual menggunakan NumPy (`np.nanpercentile`).

### 🎵 Stage 2: Analisis Genre & Popularitas
- **Distribusi Fitur per Genre**: Mengelompokkan data berdasarkan `playlist_genre` untuk melihat karakteristik audio tiap genre.
- **Variansi Popularitas**: Menemukan bahwa genre **R&B** memiliki variansi popularitas tertinggi ($\approx 670.53$), menandakan selera pasar yang sangat beragam, sementara **EDM** paling rendah/stabil ($\approx 536.12$).
- **Analisis Produktivitas Artis**: Meneliti korelasi antara produktivitas (jumlah lagu unik) dengan popularitas (misalnya, **Queen** paling produktif dengan 130 lagu, namun rata-rata popularitas tertinggi dipegang oleh **David Guetta** sebesar $\approx 49.37$).
- **Filter Multi-Kondisi**: Menyaring lagu dengan spesifikasi: popularitas $> 70$, *danceability* $> 0.7$, *energy* $> 0.6$, dan durasi $< 4$ menit. Genre **Latin** dan **Pop** menjadi yang paling dominan memenuhi kriteria ini.

### 🧮 Stage 3: Analisis NumPy (Vektorisasi)
- **Normalisasi Min-Max**: Melakukan penskalaan 9 fitur audio ke rentang $[0, 1]$ secara efisien dengan vektorisasi penuh (broadcasting) tanpa loop Python:
  ```python
  X_norm = (X - X.min(axis=0)) / (X.max(axis=0) - X.min(axis=0))
  ```
- **Korelasi Audio Fitur**:
  - Korelasi **Positif Terkuat**: `energy` & `loudness` ($+0.682$) — lagu yang keras cenderung memiliki energi tinggi.
  - Korelasi **Negatif Terkuat**: `energy` & `acousticness` ($-0.546$) — lagu akustik cenderung lebih tenang/kurang bertenaga.
- **Boolean Masking**: Menyaring lagu berenergi tinggi ($> \mu + \sigma$) dan membandingkan popularitasnya. Hasil menunjukkan lagu dengan energi sangat tinggi justru memiliki rata-rata popularitas lebih rendah ($\approx 34.04$) dibanding rata-rata keseluruhan ($\approx 39.34$).

### ✍️ Stage 4: Dokumentasi & Refleksi AI Tool
- Menerapkan format **Google-style docstrings** untuk pendokumentasian fungsi Python.
- Melakukan evaluasi kritis terhadap hasil rekomendasi docstring dari AI coding assistant untuk memastikan tipe data kembalian (`np.ndarray` vs `pd.DataFrame`) tertulis dengan tepat.

---

## 🌟 Fitur Tambahan (Bonus Modules)

### 👥 Bonus 1: Artist Audio Fingerprint & Cosine Similarity
Membuat representasi karakteristik audio unik seorang artis (*fingerprint*) dengan rata-rata 9 fitur audio yang telah dinormalisasi, lalu membandingkannya menggunakan rumus **Cosine Similarity** manual:
$$\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|}$$

```python
def cosine_similarity(A, B):
    return np.dot(A, B) / (np.linalg.norm(A) * np.linalg.norm(B))
```

*Contoh Kemiripan:*
- **Martin Garrix vs David Guetta**: $0.9849$ (Sangat mirip, sesama produser EDM)
- **David Guetta vs Queen**: $0.9803$ (Kemiripan tinggi karena seluruh fitur bernilai positif $[0,1]$)

### 🧬 Bonus 2: Genre Cluster Profile
Membangun profil rata-rata (centroid) untuk setiap genre, lalu menghitung matriks jarak Euclidean antar-genre menggunakan teknik broadcasting NumPy (tanpa loop):
```python
diff = centroids[:, None, :] - centroids[None, :, :]
dist = np.sqrt((diff ** 2).sum(axis=2))
```
- **Genre Paling Mirip**: Latin & Pop (jarak: $0.139$)
- **Genre Paling Berbeda**: EDM & R&B (jarak: $0.372$)
- Menyertakan fungsi `recommend_similar_genre` untuk merekomendasikan genre terdekat dari input user.

### 📦 Bonus 3: Reusable Analysis Class (`SpotifyAnalyzer`)
Mengintegrasikan seluruh pipeline analisis ke dalam kelas OOP yang dapat digunakan kembali (*reusable class*) lengkap dengan type-hints.

```python
class SpotifyAnalyzer:
    def __init__(self, url: str) -> None: ...
    def summarize_numeric(self) -> pd.DataFrame: ...
    def popularity_variance_by_genre(self) -> pd.Series: ...
    def top_artists(self, n: int = 10) -> pd.DataFrame: ...
    def correlation_pairs(self) -> dict: ...
    def high_energy_comparison(self) -> dict: ...
    def generate_report(self) -> dict: ...
```

Kelas ini memproduksi output laporan dalam format JSON yang merangkum metrik-metrik utama:
```json
{
  "dataset_shape": [32828, 23],
  "unique_tracks": 28352,
  "highest_variance_genre": "r&b",
  "most_productive_artist": "Queen",
  "most_popular_top_artist": "David Guetta",
  "correlation": {
    "most_positive": ["energy", "loudness", 0.682],
    "most_negative": ["energy", "acousticness", -0.546]
  },
  "energy_vs_popularity": {
    "n_high_energy": 4852,
    "mean_pop_high_energy": 34.04,
    "mean_pop_overall": 39.34
  }
}
```

---

## 💡 3 Key Business Insights
1. **Kuantitas Bukan Jaminan Kualitas**: Queen memproduksi lagu unik paling banyak, namun secara rata-rata popularitasnya kalah dari David Guetta yang lagunya lebih sedikit.
2. **Lagu Energik Bukan Resep Instan Hits**: Lagu dengan energi sangat tinggi rata-rata kurang populer dibanding lagu keseluruhan. Faktor lain seperti lirik, artis, dan promosi lebih menentukan kesuksesan.
3. **Tantangan Rekomendasi R&B**: Karena popularitas genre R&B memiliki variansi yang sangat tinggi (tidak seragam), platform *streaming* perlu menerapkan algoritma personalisasi yang lebih mendalam untuk pengguna dibanding genre EDM yang popularitasnya lebih homogen.
