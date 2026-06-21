<p align="center">
  <img src="https://cdn.brandfetch.io/idoruRsDhk/theme/dark/logo.svg?c=1bxid64Mup7aczewSAYMX&t=1667561320464" alt="Tokopedia Logo" width="220" style="padding: 0 20px;">
  <img src="https://cdn.brandfetch.io/idgVhUUiaD/w/820/h/262/theme/dark/logo.png?c=1bxid64Mup7aczewSAYMX&t=1781707152710" alt="Shopee Logo" width="200" style="padding: 0 20px;">
  <img src="https://cdn.brandfetch.io/idE6z9vRnM/theme/dark/logo.svg?c=1bxid64Mup7aczewSAYMX&t=1775496902207" alt="Blibli Logo" width="220" style="padding: 0 20px;">
</p>

<h1 align="center">
  Brand Dominance, Price Anomaly, dan Resale Value Analysis pada Produk Teknologi di E-Commerce Indonesia<br>
  <small>🛍️ Produk Teknologi pada E-Commerce Indonesia 🛍️</small>
</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Ongoing-orange?style=for-the-badge" alt="Status Completed">
  <img src="https://img.shields.io/badge/Focus-Big%20Data-blue?style=for-the-badge" alt="Focus Big Data">
  <img src="https://img.shields.io/badge/Tools-Python%20%7C%20Pandas%20%7C%20Web%20Scraper-green?style=for-the-badge" alt="Tools">
</p>

---

## 👥 Tim Pengembang: Kelompok SIPP

Kami adalah kolaborasi mahasiswa yang berdedikasi mentransformasi data mentah e-commerce menjadi wawasan strategis di pasar digital.

| Nama Lengkap               | NPM         |
| -------------------------- | ----------- |
| *Eris Alfionita*         | 24083010032 |
| *Gendis Poerbodani*      | 24083010077 |
| *Alfani Nur Azizah*      | 24083010048 |
| *Khairunisa Olive Ektha* | 24083010120 |

---

## 📌 Latar Belakang

Produk teknologi — khususnya smartphone dan laptop — dinamis di platform e-commerce Indonesia, dengan jumlah listing yang besar, perubahan harga yang cepat, serta persaingan merek yang ketat. Pada marketplace seperti Tokopedia, Shopee, dan Blibli, konsumen dihadapkan pada beragam pilihan produk baru maupun bekas dari berbagai brand ternama, yang sering kali memiliki spesifikasi serupa namun dengan perbedaan harga yang cukup signifikan, sehingga menyulitkan dalam menentukan produk yang benar-benar sepadan dengan nilai yang ditawarkan.

Proyek ini memanfaatkan data dari 3 platform e-commerce untuk:
Memetakan dominasi brand per kategori dan segmen harga
Mendeteksi anomali harga (produk overpriced dan hidden gem) dengan pendekatan statistik
Menganalisis resale value dan likuiditas pasar bekas per brand

---

## 🗄️ Dataset

**Sumber Data**

| Sumber    | Jenis Produk               | Kondisi      | Metode        |
| --------- | -------------------------- | ------------ | ------------- |
| Tokopedia | Smartphone (HP) dan laptop | Baru & Bekas | Web Scraping  |
| Shopee    | Smartphone (HP) dan laptop | Baru & Bekas | Simplescraper |
| BliBli    | Smartphone (HP) dan laptop | Baru         | Web Scraping  |

Detail Data:

- Total data: **34.646** baris
- Distribusi per platform: Tokopedia (11.636) · Shopee (11.634) · Blibli (11.384)
- Kolom utama: nama_produk, harga, jumlah terjual, rating, brand, kategori, kondisi, lokasi_penjual, platform

**Brand Coverage**

- Smartphone (20 brand): Samsung, Apple, Poco, Xiaomi, Infinix, Realme, Vivo, Nokia, Tecno, Oppo, Itel, ZTE, Sony, Lenovo, HP, Advan, Huawei, Asus, Blackshark, Honor
- Laptop (17 brand): Asus, Acer, Lenovo, Apple, HP, Dell, MSI, Axioo, Advan, Zyrex, Samsung, Huawei, Infinix, Realme, Xiaomi, Microsoft, Tecno

---

## ⚙️ Metode Akuisisi Data

**Tools yang digunakan:**

- [WebScraper.io](https://webscraper.io/) — ekstensi browser untuk scraping halaman dinamis tanpa kode pada platform Tokopedia dan BliBli
- [Simplescraper](https://simplescraper.io/) - ekstensi browser untuk scraping pada platform Shopee

---

## 🔎 8V yang Difokuskan

- **Volume**: 97.166 baris data hasil scraping dari 3 platform, menjadi 34.646 setelah cleaning. Distribusi data antar platform relatif seimbang (~33% per platform) sehingga hasil analisis lebih representatif.
- **Variety**: Data numerik (harga, jumlah terjual, rating), kategorikal (brand, kategori, kondisi, platform), dan teks (nama produk, lokasi penjual).
- **Velocity**: Secara konseptual, sumber datanya memiliki velocity tinggi karena harga, stok, dan jumlah terjual berubah cepat akibat promo dan dinamika permintaan. Velocity juga tercermin dari seberapa laku suatu produk, diukur melalui `jumlah_terjual` dan estimasi revenue (`harga × jumlah_terjual`). Penambahan snapshot di waktu berbeda memungkinkan analisis perubahan harga dan penjualan dari waktu ke waktu.
- **Veracity**: Data mengandung sejumlah noise dan inkonsistensi seperti typo nama brand dan platform, format harga tidak seragam, nilai rating di luar rentang valid, serta produk yang salah kategori. Proses cleaning dilakukan untuk meningkatkan kepercayaan data sebelum dianalisis.
- **Value**: Dataset memberikan nilai penting dalam analisis, antara lain mengidentifikasi platform e-commerce mana yang paling dominan, membandingkan performa kategori HP dan Laptop, serta menganalisis resale value produk bekas untuk membantu konsumen menentukan merek yang paling worth it untuk dibeli dan dijual kembali.
- **Variability**: Dataset menunjukkan dinamika brand dan harga yang bervariasi antar platform. Samsung dominan di Shopee (325K unit), Poco & Xiaomi kuat di Tokopedia, Apple merata di semua platform. Blibli konsisten memiliki median harga tertinggi (~Rp 4,9 juta), Shopee paling terjangkau (~Rp 3,4 juta). Brand populer seperti Samsung dan Apple memiliki variasi harga lebih besar karena menjangkau segmen entry hingga flagship sekaligus.
- **Validity**: Akurasi analisis dijaga melalui validasi manual sampel produk, verifikasi brand via fuzzy matching (`rapidfuzz`, threshold skor <70), dan filter harga tidak wajar (<Rp 100.000). Deteksi anomali harga menggunakan metode IQR per brand — bukan pengamatan visual — sehingga threshold batas wajar bersifat objektif dan proporsional terhadap distribusi harga masing-masing brand. Divalidasi silang dengan Z-score (|z| > 3). Total anomali terdeteksi: 2.379 listing (6,9%).
- **Visualization**: Hasil analisis divisualisasikan dalam dashboard ringkas mencakup KPI cards (total produk, top brand, jumlah anomali), treemap dominasi brand, histogram distribusi harga, boxplot median harga per brand, heatmap harga per brand × platform, dan bar chart anomali per brand.

---

## 🛠️ 3. Data Wrangling (Preprocessing)

Data mentah hasil scraping belum seragam dan tidak langsung siap dianalisis. Tahapan utama yang dilakukan:

- *Penambahan konteks*: Menambahkan kolom category, brand, dan condition (baru/bekas) berdasarkan setting scraping atau nama file.
- *Imputasi*: Mengisi nilai kosong pada rating, review_count, dan sold dengan 0 sebagai nilai default aman.
- *Menghapus baris tidak releva*: Drop placeholder "Akan Hadir", baris pre-order kosong, dan baris tanpa nama_produk atau harga.
- *Menghapus duplikat dan menangani missing values* - kondisi kosong diisi "Baru", lokasi_penjual kosong diisi "Tidak Diketahui"
- *Normalisasi price*: Menghapus "Rp", titik ribuan, dan spasi, lalu mengonversi ke tipe numerik (integer).
- *Normalisasi sold*:
  - Membuat versi teks yang seragam (sold_text).
  - Membuat versi numerik sold_num (misalnya "3 rb+" → 3000, "30+" → 30).
- *Fix typo & inkonsistensi kategorikal*: "Iphone" → "Apple", sub-brand alias (Nubia, Redmagic → ZTE), "Bliblii" → "Blibli".
- *Standarisasi tipe data & format*: Normalisasi harga (strip "Rp", filter < Rp100.000), rating (konversi ke numerik, nilai di luar 1–5 → NaN), jumlah terjual (parse format "10rb+" → integer), serta teks kategorikal menggunakan .strip().str.title().
- *Deduplikasi & filtering*: Menghapus baris tanpa price atau seller, dan menghapus duplikat berdasarkan kombinasi product_link + seller.
- *Validasi brand dengan Fuzzy Matching *: Menggunakan rapidfuzz, bandingkan brand vs nama produk; jika skor < 70 ekstrak ulang dari known_brands.
- *Drop produk di luar scope*: Smartwatch yang masuk kategori HP/Laptop dan brand minor (Blackview, Doogee, Motorola)
- *Konsolidasi*: Menyimpan hasil preprocessing per anggota di data/processed/individual/ dan menggabungkannya menjadi master_clean.csv.

## 📊 Analisis

**Analisis Gabungan**

- *Sebaran Data per Platform*
  Distribusi jumlah listing dan persentase produk di setiap platform. Shopee dan Tokopedia mendominasi volume transaksi (duopoli pasar), sementara Blibli tertinggal jauh dalam kuantitas namun rating kepuasan konsumen merata di semua platform.
- *Komparasi Performa Kategori (HP vs Laptop)*
  HP unggul di volume penjualan (2,47 juta unit vs 1,17 juta unit), namun Laptop menghasilkan estimasi omset lebih besar (~Rp 9,99 T vs ~Rp 9,53 T) berkat rata-rata harga yang hampir 2× lebih tinggi (Rp 8,49 juta vs Rp 3,86 juta).

**Analisis Kategori Handphone**

1. **Brand Dominance** — Samsung, Apple, Poco menguasai 46% total unit terjual. Poco paling efisien (listing 5,47% tapi terjual 14,17%). Oppo oversupply: listing terbesar kedua tapi terjual hanya 2,55%.
2. **Price Anomaly Detection** — 1.263 dari 19.557 listing (6,46%) terdeteksi anomali, mayoritas overpriced (1.230). Kasus ekstrem: listing dipasang Rp 90–110 juta jauh di atas batas wajar brand.
3. **Depresiasi & Likuiditas Pasar Bekas** — Samsung terbaik: depresiasi 43,71% dengan likuiditas tertinggi (93,12%). Apple depresiasi tertinggi (59,76%) tapi volume bekas terbesar. Poco & Tecno depresiasi negatif (harga bekas ≥ baru).
4. **Herfindahl-Hirschman Index (HHI)** — HHI = 1.059 → Pasar Kompetitif, tidak ada brand yang mendominasi secara signifikan.
5. **Price Positioning Matrix** — Segmen mid-low (Poco, Xiaomi, Infinix) mendominasi volume. Samsung dan Apple membuktikan harga premium tetap bisa meraih market share tinggi.
6. **Disparitas Harga Antar Platform** — Blibli cenderung segmen menengah-atas, Shopee paling ekonomis. Outlier ekstrem paling banyak ditemukan di Tokopedia.
7. **Hidden Gems** — iPhone bekas generasi lama (X, XR, 11 Pro Max) dan Poco C71 baru menjadi produk dengan value terbaik.

**Analisis Kategori Laptop**

1. **Brand Dominance** — Lenovo raja pasar dengan 30,84% total unit terjual meski bukan listing terbanyak. Apple dan MSI segmen premium (harga >Rp 13 juta) dengan market share rendah.
2. **Price Anomaly Detection** — Top overpriced didominasi laptop ultra-flagship (MSI Titan RTX5090, Dell Pro Max) yang memang merupakan segmen premium, bukan kesalahan input.
3. **Depresiasi & Likuiditas Pasar Bekas** — Asus dan Acer depresiasi tertinggi (73,99% dan 71,78%). Tecno anomali: depresiasi negatif (-21,09%), harga bekas lebih tinggi dari baru. Lenovo likuiditas tertinggi (91,80%).
4. **Disparitas Harga Antar Platform** — Blibli dominasi produk high-end (median harga baru Rp 11,3 juta). Tokopedia dan Shopee lebih mass-market (~Rp 6 juta).
5. **Hidden Gems** — Infinix Xpad 20, Axioo Hype 10, dan MacBook Air M1 second menjadi produk value terbaik di kategori laptop.

## 🚀 Bagaimana Tambahan Data Baru Meningkatkan Keampuhan Model Analisis

Penambahan data baru (lebih banyak platform, lebih banyak snapshot waktu) meningkatkan keandalan model dengan:

- Memperkaya distribusi data dan mengurangi bias satu platform
- Memungkinkan perbandingan lintas platform secara lebih adil
- Mengidentifikasi dominasi brand dengan lebih akurat
- Meningkatkan akurasi deteksi anomali harga dan hidden gem
- Memungkinkan analisis tren harga dan penjualan dari waktu ke waktu

---

<div align="center">
  <p><i>"Project Big Data © 2026 • Brand Dominance Mapping & Price Anomaly Detection"</i></p>
  <strong>Kelompok SIPP - UPN "Veteran" Jawa Timur</strong>
</div>
