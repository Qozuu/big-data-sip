<p align="center">
  <img src="https://cdn.brandfetch.io/idoruRsDhk/theme/dark/logo.svg?c=1bxid64Mup7aczewSAYMX&t=1667561320464" alt="Tokopedia Logo" width="280">
</p>

<h1 align="center">
  Brand Dominance Mapping & Price Anomaly Detection<br>
  <small>🛍️ Produk Teknologi pada E-Commerce Indonesia 🛍️</small>
</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Ongoing-orange?style=for-the-badge" alt="Status Ongoing">
  <img src="https://img.shields.io/badge/Focus-Big%20Data-blue?style=for-the-badge" alt="Focus Big Data">
  <img src="https://img.shields.io/badge/Tools-Python%20%7C%20Pandas%20%7C%20Web%20Scraper-green?style=for-the-badge" alt="Tools">
</p>

---

## 👥 Tim Pengembang: Kelompok SIPP

Kami adalah kolaborasi mahasiswa yang berdedikasi mentransformasi data mentah e-commerce menjadi wawasan strategis di pasar digital.

| Nama Lengkap                | NPM           |
|----------------------------|--------------|
| *Eris Alfionita*         | 24083010032| 
| *Gendis Poerbodani*      | 24083010077|
| *Alfani Nur Azizah*      | 24083010048| 
| *Khairunisa Olive Ektha* | 24083010120|

---

## 📌 Latar Belakang

Produk teknologi — khususnya smartphone dan laptop — dinamis di platform e-commerce Indonesia, dengan jumlah listing yang besar, perubahan harga yang cepat, serta persaingan merek yang ketat. Pada marketplace seperti Tokopedia, konsumen dihadapkan pada beragam pilihan produk baru maupun bekas dari berbagai brand ternama, yang sering kali memiliki spesifikasi serupa namun dengan perbedaan harga yang cukup signifikan, sehingga menyulitkan dalam menentukan produk yang benar-benar sepadan dengan nilai yang ditawarkan.

Proyek ini memanfaatkan data Tokopedia untuk:
- memetakan dominasi brand per kategori dan segmen harga, dan  
- mendeteksi anomali harga (produk overpriced dan hidden gem) dengan pendekatan statistik dan machine learning ringan.

---

## 🗄️ Dataset

**Sumber Data**

| Sumber | Jenis Produk | Kondisi | Metode |
|--------|-------------|---------|--------|
| Tokopedia | Smartphone (HP) dan laptop| Baru & Bekas | Web Scraping |

Detail Data:

- Data berjumlah 10690
- Kolom utama: product_name, price, sold, rating, review_count, seller, serta konteks (category, brand, condition)

**Brand Coverage**

- Smartphone (17 brand): Samsung, Xiaomi, Redmi, Oppo, Vivo, iPhone, Realme, Infinix, Tecno, Itel, Asus, Huawei, Honor, Sony, Lenovo, Black Shark, ZTE
- Laptop (15 brand): Asus, Apple, Acer, Lenovo, HP, Dell, MSI, Axioo, Advan, Zyrex, Samsung, Huawei, Infinix, Realme, Xiaomi

---

## ⚙️ Metode Akuisisi Data

**Tools yang digunakan:**
- [WebScraper.io](https://webscraper.io/) — ekstensi browser untuk scraping halaman dinamis tanpa kode
  
---

## 🔎 5V yang Difokuskan

- *Volume*: Ribuan baris data per kategori/brand, dengan potensi puluhan ribu baris ketika semua kategori dan snapshot digabung.  
- *Variety*: Data numerik (harga, sold), kategorikal (brand, kategori, condition, seller), dan teks (nama produk, deskripsi singkat).  
- *Velocity*: Data mencerminkan snapshot pada waktu tertentu; struktur disiapkan untuk menambahkan beberapa snapshot waktu (snapshot_date).  
- *Veracity*: Banyak noise dari hasil scraping (format harga beragam, teks “rb+”, nilai kosong) sehingga butuh cleaning dan normalisasi.  
- *Value*: Dataset akhir dirancang untuk mendukung analisis dominasi brand dan deteksi anomali harga yang relevan untuk konsumen dan pelaku usaha.
  
---
## 🛠️ 3. Data Wrangling (Preprocessing)

Data mentah hasil scraping belum seragam dan tidak langsung siap dianalisis. Tahapan utama yang dilakukan:

- *Penambahan konteks*: Menambahkan kolom category, brand, dan condition (baru/bekas) berdasarkan setting scraping atau nama file.  
- *Imputasi*: Mengisi nilai kosong pada rating, review_count, dan sold dengan 0 sebagai nilai default aman.  
- *Normalisasi price*: Menghapus "Rp", titik ribuan, dan spasi, lalu mengonversi ke tipe numerik (integer).  
- *Normalisasi sold*:
  - Membuat versi teks yang seragam (sold_text).  
  - Membuat versi numerik sold_num (misalnya "3 rb+" → 3000, "30+" → 30).  
- *Deduplikasi & filtering*: Menghapus baris tanpa price atau seller, dan menghapus duplikat berdasarkan kombinasi product_link + seller.  
- *Konsolidasi*: Menyimpan hasil preprocessing per anggota di data/processed/individual/ dan menggabungkannya menjadi master_clean.csv.

## 🚀 Bagaimana Tambahan Data Baru Meningkatkan Keampuhan Model Analisis

Penambahan data baru meningkatkan keandalan model dengan memperkaya distribusi data, memungkinkan perbandingan lintas platform, mengidentifikasi dominasi brand dengan lebih akurat, serta meningkatkan akurasi deteksi anomali dan hidden gem.

---

<div align="center">
  <p><i>"Project Big Data © 2026 • Brand Dominance Mapping & Price Anomaly Detection"</i></p>
  <strong>Kelompok SIPP - UPN "Veteran" Jawa Timur</strong>
</div>
