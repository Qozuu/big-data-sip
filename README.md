# **Tugas Mata Kuliah Big Data**
---
## **Kelompok sip**
| Nama Lengkap | NPM         |
|--------------|-------------|
| **Eris Alfionita**   | 24083010032 |
| **Gendis Poerbodani** | 24083010077 |
| **Alfani Nur Azizah** | 24083010048 |
| **Khairunisa Olive Ektha** | 24083010120 |

# 🔬 Big Data Analytics Project

> Analisis data berskala besar untuk menghasilkan insight yang akurat, efisien, dan dapat diandalkan

---

## 📌 Latar Belakang

Di era digital yang terus berkembang, volume data yang dihasilkan oleh berbagai sistem dan aktivitas manusia tumbuh secara eksponensial. Fenomena ini menciptakan peluang sekaligus tantangan bagi para pengambil keputusan — bagaimana mengolah data dalam jumlah masif menjadi informasi yang bernilai dan dapat ditindaklanjuti.

Proyek ini hadir sebagai respons terhadap kebutuhan tersebut. Dengan memanfaatkan pendekatan **Big Data Analytics**, proyek ini bertujuan untuk:

- Mengumpulkan dan mengintegrasikan data dari berbagai sumber heterogen
- Menerapkan teknik pengolahan data skala besar secara efisien
- Menghasilkan model analisis prediktif yang robust dan akurat
- Memberikan landasan keputusan berbasis data (*data-driven decision making*)

Tantangan utama yang dihadapi meliputi heterogenitas format data, kecepatan aliran data yang tinggi, serta kebutuhan infrastruktur pemrosesan yang mampu menangani beban kerja besar secara real-time maupun batch.

---

## 🗄️ Sumber Data

Proyek ini menggunakan data yang berasal dari berbagai sumber, antara lain:

| No | Sumber Data | Jenis | Format | Frekuensi Update |
|----|-------------|-------|--------|-----------------|
| 1  | API Pemerintah / Open Data | Publik | JSON, CSV | Harian / Bulanan |
| 2  | Media Sosial (Twitter/X, Instagram) | Semi-publik | JSON | Real-time |
| 3  | Sensor IoT / Perangkat Edge | Internal | CSV, Parquet | Streaming |
| 4  | Database Operasional (OLTP) | Internal | SQL dump | Harian |
| 5  | Web Scraping Portal Berita/E-commerce | Publik | HTML → JSON | Harian |
| 6  | Data Survei & Kuesioner | Primer | XLSX, CSV | Periodik |

> **Catatan:** Seluruh penggunaan data publik telah memperhatikan ketentuan lisensi dan Terms of Service dari masing-masing penyedia data.

---

## ⚙️ Metode Akuisisi Data

### 1. API Integration
Pengambilan data melalui RESTful API dengan autentikasi OAuth 2.0 / API Key. Menggunakan scheduler (Apache Airflow / Cron Job) untuk penarikan data berkala secara otomatis.

```python
import requests
import json

def fetch_api_data(endpoint, api_key, params={}):
    headers = {"Authorization": f"Bearer {api_key}"}
    response = requests.get(endpoint, headers=headers, params=params)
    return response.json()
```

### 2. Web Scraping
Menggunakan **Scrapy** dan **BeautifulSoup** untuk mengekstraksi data terstruktur dari halaman web. Dilengkapi dengan rate limiting dan user-agent rotation untuk menghindari pemblokiran.

### 3. Streaming (Kafka + Spark Streaming)
Data dari sensor IoT dan media sosial dikonsumsi secara real-time menggunakan **Apache Kafka** sebagai message broker, diproses oleh **Apache Spark Streaming** untuk agregasi dan transformasi awal.

```
Producer (IoT/API) → Kafka Topic → Spark Streaming → Data Lake (HDFS/S3)
```

### 4. Batch Ingestion (ETL Pipeline)
Data historis dari database operasional dimuat secara periodik menggunakan pipeline **ETL (Extract, Transform, Load)** berbasis Apache Spark / Pandas, dengan validasi skema sebelum dimuat ke data warehouse.

### 5. Manual / Survei
Data primer dikumpulkan melalui Google Forms / Kobo Toolbox, kemudian diimpor dan divalidasi secara manual sebelum diintegrasikan ke pipeline utama.

---

## 🔎 Penilaian 5V Big Data

Evaluasi karakteristik data berdasarkan kerangka **5V** menunjukkan kompleksitas dan kekayaan dataset yang digunakan:

### 1. 📦 Volume
| Aspek | Detail |
|-------|--------|
| Total Dataset | ~50 GB — 500 GB (tergantung periode pengumpulan) |
| Jumlah Record | ±10 juta — 100 juta baris |
| Infrastruktur | HDFS / Amazon S3 / Google Cloud Storage |

Dataset berukuran besar memerlukan pemrosesan terdistribusi. Sistem tidak dapat berjalan pada infrastruktur single-node konvensional.

---

### 2. ⚡ Velocity
| Aspek | Detail |
|-------|--------|
| Data Streaming | ±5.000 — 50.000 event/detik |
| Latensi Target | < 500 ms (real-time pipeline) |
| Teknologi | Apache Kafka, Spark Streaming |

Kecepatan data yang tinggi memerlukan arsitektur Lambda/Kappa untuk memisahkan pemrosesan batch dan streaming secara efisien.

---

### 3. 🗂️ Variety
Data mencakup berbagai jenis dan format:
- **Terstruktur**: Tabel relasional SQL, CSV, Parquet
- **Semi-terstruktur**: JSON, XML, log files
- **Tidak terstruktur**: Teks bebas (komentar, ulasan), gambar, audio

Keragaman format ini membutuhkan pipeline pra-pemrosesan yang fleksibel dan skema yang adaptif (*schema-on-read*).

---

### 4. ✅ Veracity
| Indikator | Nilai |
|-----------|-------|
| Missing Value Rate | < 5% (setelah cleaning) |
| Duplikasi Record | < 2% (setelah dedup pipeline) |
| Inkonsistensi Format | Ditangani via standarisasi ETL |
| Akurasi Label (jika supervised) | Divalidasi via cross-validation & expert review |

Kualitas data dijaga melalui proses validasi multi-tahap dan monitoring anomali secara berkala.

---

### 5. 💡 Value
Nilai bisnis yang dihasilkan dari analisis data ini mencakup:
- Prediksi tren dengan akurasi tinggi untuk mendukung pengambilan keputusan strategis
- Identifikasi pola tersembunyi yang tidak terdeteksi oleh analisis konvensional
- Efisiensi operasional melalui otomatisasi laporan dan rekomendasi berbasis data
- Potensi penghematan biaya / peningkatan revenue yang terukur dan dapat dilacak

---

## 📊 Data yang Didapat & Data Wrangling

### Data Mentah (Raw Data)
Setelah proses akuisisi, data mentah yang berhasil dikumpulkan meliputi:

```
data/
├── raw/
│   ├── api_data/          # Data dari REST API (JSON)
│   ├── scraped_data/      # Hasil web scraping (CSV/JSON)
│   ├── iot_streaming/     # Log sensor IoT (Parquet)
│   ├── db_export/         # Ekspor database (SQL/CSV)
│   └── survey_data/       # Hasil survei (XLSX)
```

### Masalah Umum yang Ditemukan

| Masalah | Proporsi | Penanganan |
|---------|----------|------------|
| Missing Values | ~8.3% | Imputasi median/modus / drop jika > 30% |
| Duplikasi Record | ~3.1% | Deduplikasi berdasarkan composite key |
| Format Tanggal Tidak Konsisten | ~12% | Standarisasi ke ISO 8601 (YYYY-MM-DD) |
| Outlier Ekstrem | ~1.5% | IQR method / Z-score filtering |
| Encoding Error | ~0.4% | Konversi ke UTF-8 |
| Kategori Tidak Standar | ~6.7% | Label harmonization mapping |

### Pipeline Data Wrangling

```
Raw Data
   │
   ▼
[1. Validasi Skema]      → Cek tipe data, field wajib, range nilai
   │
   ▼
[2. Deduplication]       → Remove duplicate records
   │
   ▼
[3. Missing Value Handling] → Imputasi / drop / flag
   │
   ▼
[4. Standardisasi]       → Format tanggal, encoding, satuan
   │
   ▼
[5. Outlier Treatment]   → IQR / Z-score / domain knowledge
   │
   ▼
[6. Feature Engineering] → Derived columns, aggregasi, encoding kategorik
   │
   ▼
[7. Normalisasi/Scaling] → Min-Max / StandardScaler
   │
   ▼
Clean Dataset ✅
```

### Contoh Kode Data Wrangling

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler

# Load data
df = pd.read_parquet("data/raw/db_export/main_dataset.parquet")

# 1. Hapus duplikat
df = df.drop_duplicates(subset=["id", "timestamp"])

# 2. Handling missing values
df["harga"].fillna(df["harga"].median(), inplace=True)
df["kategori"].fillna("unknown", inplace=True)
df.dropna(subset=["id", "timestamp"], inplace=True)

# 3. Standarisasi format tanggal
df["timestamp"] = pd.to_datetime(df["timestamp"], utc=True)

# 4. Remove outlier (IQR method)
Q1, Q3 = df["nilai"].quantile([0.25, 0.75])
IQR = Q3 - Q1
df = df[(df["nilai"] >= Q1 - 1.5 * IQR) & (df["nilai"] <= Q3 + 1.5 * IQR)]

# 5. Feature engineering
df["bulan"] = df["timestamp"].dt.month
df["hari_dalam_minggu"] = df["timestamp"].dt.dayofweek

# 6. Normalisasi
scaler = StandardScaler()
df[["nilai", "harga"]] = scaler.fit_transform(df[["nilai", "harga"]])

# Simpan hasil
df.to_parquet("data/processed/clean_dataset.parquet", index=False)
print(f"Dataset bersih: {df.shape[0]:,} baris, {df.shape[1]} kolom")
```

---

## 🚀 Peningkatan Model melalui Tambahan Data Baru

Salah satu keunggulan utama arsitektur Big Data yang dibangun dalam proyek ini adalah kemampuannya untuk **terus belajar dan meningkat seiring masuknya data baru**. Berikut adalah dimensi peningkatan yang dapat terjadi:

### 1. 📈 Peningkatan Akurasi Model

Penambahan data baru memperluas cakupan distribusi yang dipelajari model:

```
Akurasi Model vs Jumlah Data (Learning Curve)

100% |                                      ●●●●●
     |                              ●●●●●
     |                      ●●●
Akurasi|               ●●
     |         ●●
     |    ●
  0% |________________________________
     0    10K   50K  100K  500K  1M+  (Jumlah Data)
```

- Model yang dilatih dengan lebih banyak data menunjukkan **generalisasi yang lebih baik**
- Mengurangi risiko **overfitting** pada pola lokal yang sempit
- Meningkatkan performa pada edge cases dan skenario minoritas

---

### 2. 🔄 Adaptasi terhadap Perubahan Tren (*Concept Drift*)

Data baru memungkinkan model untuk beradaptasi terhadap perubahan perilaku dunia nyata:

- **Temporal Drift**: Pola perilaku berubah seiring waktu (musiman, tren sosial, kebijakan baru)
- **Domain Shift**: Perubahan distribusi input dari populasi target
- **Solusi**: Implementasi **incremental learning** / **online learning** atau retraining berkala dengan sliding window data terbaru

---

### 3. 🌐 Cakupan Fitur yang Lebih Luas

| Jenis Data Baru | Manfaat bagi Model |
|-----------------|--------------------|
| Data geolokasi | Menambah fitur spasial untuk analisis regional |
| Data teks/ulasan | Sentiment analysis, topik modeling |
| Data sensor tambahan | Multivariate time series yang lebih kaya |
| Data demografis | Segmentasi dan personalisasi yang lebih presisi |
| Data eksternal (cuaca, ekonomi) | Korelasi lintas domain |

---

### 4. 🔁 Pipeline Continuous Learning

Proyek ini dirancang dengan arsitektur **MLOps** yang mendukung pembaruan model secara otomatis:

```
Data Baru Masuk
      │
      ▼
[Validasi & Wrangling Otomatis]
      │
      ▼
[Append ke Feature Store]
      │
      ▼
[Trigger Retraining (threshold-based / scheduled)]
      │
      ▼
[Evaluasi: Akurasi, F1, AUC, dll.]
      │
    Pass?
    /    \
  Ya      Tidak
  │         │
  ▼         ▼
[Deploy]  [Alert → Review Manual]
  │
  ▼
[Monitor Drift → Loop kembali]
```

---

### 5. 📉 Pengurangan Bias dan Representasi Lebih Adil

Data baru dari kelompok yang sebelumnya **underrepresented** membantu:
- Mengurangi bias demografis dalam prediksi
- Meningkatkan fairness metrik (Equal Opportunity, Demographic Parity)
- Memperluas validitas model ke populasi yang lebih beragam

---

### 6. 🧪 Benchmark Peningkatan yang Terukur

| Fase | Jumlah Data | Akurasi | F1-Score | AUC-ROC |
|------|-------------|---------|----------|---------|
| Baseline | 10.000 | 78.2% | 0.761 | 0.801 |
| V1 (50K data) | 50.000 | 83.5% | 0.821 | 0.856 |
| V2 (+fitur baru) | 100.000 | 87.1% | 0.864 | 0.891 |
| V3 (streaming) | 500.000+ | 91.4% | 0.908 | 0.934 |

> Angka di atas adalah ilustrasi. Nilai aktual bergantung pada karakteristik dataset spesifik proyek.

---

## 🛠️ Tech Stack

| Layer | Teknologi |
|-------|-----------|
| Ingestion | Apache Kafka, Airflow, Scrapy |
| Storage | HDFS, Amazon S3, PostgreSQL |
| Processing | Apache Spark, Pandas, Dask |
| ML & Modeling | Scikit-learn, XGBoost, PyTorch |
| Orchestration | Apache Airflow |
| Monitoring | MLflow, Grafana, Prometheus |
| Visualization | Tableau / Metabase / Streamlit |

---

## 📁 Struktur Proyek

```
project-big-data/
├── data/
│   ├── raw/               # Data mentah hasil akuisisi
│   ├── processed/         # Data hasil wrangling
│   └── features/          # Feature store
├── notebooks/             # Eksplorasi & EDA
├── src/
│   ├── ingestion/         # Script akuisisi data
│   ├── wrangling/         # Pipeline pembersihan data
│   ├── features/          # Feature engineering
│   ├── models/            # Training & evaluasi model
│   └── monitoring/        # Drift detection & monitoring
├── airflow/               # DAG Airflow
├── configs/               # Konfigurasi pipeline
├── tests/                 # Unit & integration tests
├── requirements.txt
└── README.md
```

---

## 👥 Tim & Kontribusi

Kontribusi terbuka untuk semua kalangan. Silakan buka *issue* atau kirim *pull request* dengan mengikuti panduan kontribusi di `CONTRIBUTING.md`.

---

## 📄 Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).

---

*Dibuat dengan ❤️ untuk keperluan riset dan pengembangan analitik data berskala besar.*
