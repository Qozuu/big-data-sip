# **Tugas Mata Kuliah Big Data**
---
## **Kelompok sip**
| Nama Lengkap | NPM         |
|--------------|-------------|
| **Eris Alfionita**   | 24083010032 |
| **Gendis Poerbodani** | 24083010077 |
| **Alfani Nur Azizah** | 24083010048 |
| **Khairunisa Olive Ektha** | 24083010120 |

# 📱💻 Analisis Pasar Produk Teknologi di Tokopedia

> Scraping dan analisis data produk HP & Laptop (baru & bekas) dari Tokopedia  
> untuk mengidentifikasi Brand Dominance dan Anomali Harga di pasar e-commerce Indonesia

---

## 👥 Kelompok Sip

| Nama Lengkap | NPM | Bagian Scraping |
|---|---|---|
| **Eris Alfionita** | 24083010032 | HP (Eris) |
| **Gendis Poerbodani** | 24083010077 | Laptop (Gendis) |
| **Alfani Nur Azizah** | 24083010048 | HP (Alfani) |
| **Khairunisa Olive Ektha** | 24083010120 | Laptop (Olive) |

---

## 📌 Latar Belakang

Pasar produk teknologi — khususnya smartphone dan laptop — merupakan salah satu segmen paling dinamis di platform e-commerce Indonesia. Tokopedia sebagai salah satu marketplace terbesar di Indonesia menjadi tempat bertemunya penjual produk baru maupun bekas dari berbagai merek ternama seperti Samsung, Asus, Xiaomi, dan lainnya.

Fenomena yang menarik untuk dikaji antara lain:

- **Dominasi merek tertentu** dalam volume listing dan penjualan di kategori HP dan laptop
- **Anomali harga** — produk bekas yang dijual lebih mahal dari harga wajar, atau produk baru dengan harga jauh di bawah pasaran
- Perbedaan karakteristik pasar antara produk **baru** dan **bekas** (*second*)

Proyek ini hadir untuk menjawab pertanyaan-pertanyaan tersebut melalui pendekatan **Big Data**: mengumpulkan ribuan listing produk secara otomatis via scraping, membersihkan dan mengintegrasikan data, lalu menerapkan analisis berbasis data untuk menghasilkan insight yang valid dan terukur.

> **Catatan Perkembangan Proyek:**  
> Setelah berdiskusi dengan dosen pengampu (Pak Zulhaj Alian), sumber data dipindahkan dari OLX ke **Tokopedia** untuk memperkaya dimensi data (volume penjualan, rating, kategori). Setelah ETS, analisis akan diperluas dengan membandingkan data dari **Shopee** dan **Lazada**.

---

## 🗄️ Sumber Data

| No | Sumber | Jenis Produk | Kondisi | Metode |
|----|--------|-------------|---------|--------|
| 1 | Tokopedia | Smartphone (HP) | Baru & Bekas | Web Scraping |
| 2 | Tokopedia | Laptop | Baru & Bekas | Web Scraping |
| 3 | OLX *(arsip awal)* | Smartphone (HP) | Bekas | Web Scraping |

**Brand yang dicakup (contoh):**
- HP: Samsung, Xiaomi, Oppo, Vivo, iPhone, Realme
- Laptop: Asus, Acer, Lenovo, HP, Dell, MSI

> Seluruh scraping dilakukan pada rentang waktu tertentu dan hanya mengambil data yang tersedia secara publik di halaman produk Tokopedia.

---

## ⚙️ Metode Akuisisi Data

### Web Scraping Tokopedia

Scraping dilakukan secara terbagi per anggota kelompok (individual), kemudian digabungkan menjadi satu dataset utama.

**Tools yang digunakan:**
- [WebScraper.io](https://webscraper.io/) — ekstensi browser untuk scraping halaman dinamis tanpa kode
- `pandas` untuk membersihkan dan menyimpan hasil ekspor ke CSV

**Cara kerja WebScraper.io:**
1. Buat *sitemap* baru di WebScraper.io yang mengarah ke halaman pencarian Tokopedia
2. Definisikan *selector* untuk elemen produk (nama, harga, terjual, kondisi, dll.)
3. Jalankan scraping — hasilnya diekspor langsung ke **CSV**
4. File CSV mentah disimpan di `data/raw/` lalu diproses di notebook

**Atribut yang diambil per produk:**

| Atribut | Keterangan |
|---------|------------|
| `nama_produk` | Judul listing produk |
| `merek` | Brand (Samsung, Asus, dll.) |
| `kategori` | HP / Laptop |
| `kondisi` | Baru / Bekas |
| `harga` | Harga jual (Rp) |
| `terjual` | Jumlah unit terjual |
| `rating` | Rating toko / produk |
| `lokasi_penjual` | Kota/provinsi penjual |
| `url_produk` | Link listing |

### Pembagian Tugas Scraping

```
Eris   → HP (berbagai brand, fokus query tertentu)
Alfani → HP (berbagai brand, fokus query berbeda)
Gendis → Laptop (berbagai brand, fokus query tertentu)
Olive  → Laptop (berbagai brand, fokus query berbeda)
```

Masing-masing anggota menghasilkan file CSV individual di `data/processed/individual/`, kemudian digabung di notebook `02_preprocessing_tokopedia_merge_all.ipynb`.

---

## 🔎 Penilaian 5V Big Data

### 1. 📦 Volume

| Aspek | Keterangan |
|-------|------------|
| Estimasi Total Listing | Ribuan hingga puluhan ribu baris hasil scraping |
| Cakupan | Multi-brand, multi-kategori, baru & bekas |
| Format | CSV per anggota → merge menjadi `tokopedia_tech_clean.csv` |

---

### 2. ⚡ Velocity

| Aspek | Keterangan |
|-------|------------|
| Metode | Batch scraping (tidak real-time) |
| Frekuensi | Satu kali pengumpulan data per periode tugas |
| Potensi Pengembangan | Scraping berkala untuk melacak perubahan harga dari waktu ke waktu |

---

### 3. 🗂️ Variety

Data mencakup berbagai dimensi:
- **Numerik**: harga, jumlah terjual, rating
- **Kategorik**: merek, kategori produk, kondisi (baru/bekas), lokasi penjual
- **Teks bebas**: nama produk (mengandung spesifikasi, kapasitas RAM, storage, dll.)
- **Multi-platform** *(ke depan)*: Tokopedia, Shopee, Lazada untuk perbandingan lintas marketplace

---

### 4. ✅ Veracity

| Masalah | Contoh | Penanganan |
|---------|--------|------------|
| Nama produk tidak standar | "Samsung S23 Ultra 12/256" vs "Samsung Galaxy S23U" | Normalisasi teks, ekstraksi merek |
| Format harga tidak konsisten | "Rp1.500.000" vs "1500000" | Strip karakter, konversi ke integer |
| Data terjual ambigu | "1rb+" vs "500+" | Konversi ke nilai numerik |
| Duplikasi listing | Produk yang sama dijual banyak toko | Dedup berdasarkan nama + harga + toko |
| Missing value | Produk tanpa info terjual / rating | Impute atau tandai sebagai null |

---

### 5. 💡 Value

Insight yang dihasilkan dari analisis ini:
- Mengetahui **brand mana yang paling mendominasi** pasar HP & laptop di Tokopedia berdasarkan volume listing dan penjualan
- Mengidentifikasi **anomali harga** — gap tidak wajar antara produk baru dan bekas, atau outlier harga dalam satu kategori brand
- Memberikan gambaran **pola harga pasar secondhand** produk teknologi di Indonesia
- Fondasi untuk perbandingan lintas platform (Tokopedia vs Shopee vs Lazada) setelah ETS

---

## 🚀 Bagaimana Tambahan Data Baru Meningkatkan Keampuhan Model Analisis

### 1. 📈 Lebih Banyak Data → Deteksi Anomali Lebih Akurat

Deteksi anomali harga berbasis IQR sangat bergantung pada distribusi data. Semakin banyak listing yang terkumpul, semakin representatif distribusi harga "normal" per segmen:

```
Dengan 500 data:   batas IQR kasar, banyak false positive
Dengan 5.000 data: distribusi lebih stabil, anomali lebih presisi
Dengan 50.000 data: threshold per segmen sangat akurat
```

### 2. 🌐 Tambahan Platform → Perbandingan Lintas Marketplace

Setelah ETS, penambahan data dari **Shopee** dan **Lazada** akan memungkinkan:

| Pertanyaan Baru | Kebutuhan Data |
|-----------------|---------------|
| Apakah harga di Tokopedia lebih mahal dari Shopee? | Data Shopee |
| Brand apa yang lebih dominan di Lazada vs Tokopedia? | Data Lazada |
| Di platform mana anomali harga paling banyak terjadi? | Data 3 platform |

### 3. 🔄 Data Berkala → Analisis Tren Harga

Jika scraping dilakukan berulang dalam interval waktu, model dapat:
- Melacak **fluktuasi harga** produk tertentu dari waktu ke waktu
- Mendeteksi **pola musiman** (harbolnas, lebaran, back-to-school)
- Memberikan sinyal kapan waktu terbaik untuk membeli

### 4. 🧩 Fitur Tambahan → Model Gem Detection Lebih Kuat

Analisis ke-gem-an (produk "hidden gem") membutuhkan lebih banyak sinyal:

| Fitur Baru | Kontribusi |
|-----------|-----------|
| Foto produk (Computer Vision) | Menilai kualitas kondisi barang bekas |
| Deskripsi produk (NLP) | Menangkap detail spesifikasi tersembunyi |
| Histori harga | Mendeteksi produk yang harganya sedang turun |
| Rating + ulasan teks | Menilai kepercayaan penjual lebih akurat |

### 5. 🧪 Ilustrasi Peningkatan Kualitas Analisis

| Fase | Data Tersedia | Kemampuan Analisis |
|------|---------------|--------------------|
| Sekarang | Tokopedia (HP + Laptop, baru & bekas) | Brand dominance + anomali harga per platform |
| Setelah ETS | + Shopee + Lazada | Perbandingan lintas marketplace |
| Pengembangan | + Data berkala + ulasan teks | Tren harga + sentiment + gem detection |

---

## 🛠️ Tools & Library

| Kategori | Tools |
|----------|-------|
| Bahasa | Python 3.x |
| Scraping | WebScraper.io (ekstensi browser) |
| Manipulasi Data | `pandas`, `numpy` |
| Visualisasi | `matplotlib`, `seaborn` |
| Lingkungan | Jupyter Notebook |
| Version Control | Git, GitHub |

*Dibuat dengan ❤️ untuk keperluan riset dan pengembangan analitik data berskala besar.*
