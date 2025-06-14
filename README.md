# 🏪 Aplikasi Akuntansi Toko Modern

Aplikasi desktop untuk manajemen akuntansi toko modern dengan antarmuka grafis yang intuitif dan fitur lengkap.  
Dibangun menggunakan **Python**, **PyQt5**, dan **MySQL**, aplikasi ini dirancang untuk memudahkan pengelolaan produk, transaksi, dan laporan keuangan.

---

## 🌟 Fitur Unggulan

### 📦 Manajemen Produk
- ✅ Tambah, edit, dan hapus produk
- 📊 Menampilkan stok produk secara real-time
- 🔍 Pencarian produk cepat dan efisien

### 💰 Manajemen Transaksi
- 🧾 Mencatat transaksi penjualan
- 📅 Filter transaksi berdasarkan periode waktu
- 📈 Visualisasi riwayat transaksi

### 📊 Laporan Keuangan
- 📉 Grafik interaktif untuk laporan laba rugi
- 🔢 Analisis keuangan otomatis
- 🗓️ Laporan keuangan berdasarkan periode yang dapat disesuaikan

### 📤 Ekspor Data
- 📄 Ekspor laporan ke format Excel (.xlsx)
- 🖨️ Ekspor laporan ke format PDF profesional
- 🖼️ Termasuk grafik dalam hasil ekspor

---

## 🛠️ Teknologi

| Komponen       | Teknologi     |
|----------------|----------------|
| **Frontend**   | PyQt5          |
| **Backend**    | Python 3.8+    |
| **Database**   | MySQL          |
| **Visualisasi**| Matplotlib     |
| **Ekspor Excel**| OpenPyXL      |
| **Ekspor PDF** | FPDF           |

---

## 🚀 Instalasi

### 📦 Prasyarat
- Python 3.8 atau lebih baru
- MySQL Server
- Git (opsional)

### 🔧 Langkah-langkah
1. Clone repositori ini:
   ```bash
   git clone https://github.com/Jiepra/Akuntasi_App.git
   cd Akuntasi_App
2. Install dependensi Python:
   ```bash
   pip install -r requirements.txt
3. Setup database:
   ```bash
   Buat database MySQL bernama akuntansi
   Jalankan skema SQL yang disediakan
4. Konfigurasi koneksi:
   ```bash
   Edit DB_CONFIG di admin_app.py sesuai setting MySQL Anda.
6. Jalankan aplikasi:
   ```bash
   python admin_app.py

   python client_app.py

---

## 🏗️ Struktur Database

### 📑 Tabel: `barang`
| Kolom         | Tipe Data        | Keterangan                 |
|---------------|------------------|-----------------------------|
| `kode`        | VARCHAR(20) 🔑   | Kode unik produk (Primary Key) |
| `nama`        | VARCHAR(100)     | Nama produk                   |
| `stok`        | INT              | Jumlah stok tersedia         |
| `harga_beli`  | DECIMAL(10,2)    | Harga beli per unit          |
| `harga_jual`  | DECIMAL(10,2)    | Harga jual per unit          |

---

### 📑 Tabel: `penjualan`
| Kolom                | Tipe Data        | Keterangan                             |
|----------------------|------------------|----------------------------------------|
| `id`                 | INT 🔑 (AUTO_INCREMENT) | ID unik transaksi (Primary Key)       |
| `id_pesanan`         | VARCHAR(50)      | Nomor invoice / pesanan                |
| `tanggal`            | DATETIME         | Waktu transaksi dilakukan              |
| `pelanggan`          | VARCHAR(100)     | Nama pelanggan                         |
| `kode_barang`        | VARCHAR(20) 🔗   | Kode barang yang dijual (Foreign Key)  |
| `jumlah`             | INT              | Jumlah unit barang yang dibeli         |
| `harga_satuan`       | DECIMAL(10,2)    | Harga per unit barang saat transaksi   |
| `total`              | DECIMAL(10,2)    | Total harga (jumlah × harga satuan)    |
| `metode_pembayaran`  | VARCHAR(50)      | Metode pembayaran (QRIS / Kartu)       |
| `rating`             | INT              | Penilaian pelanggan (1–5)              |
| `komentar`           | TEXT             | Komentar atau ulasan pelanggan         |

> 🔗 `kode_barang` memiliki relasi ke `barang(kode)` dan akan diset `NULL` jika produk dihapus (`ON DELETE SET NULL`)

---

## 🛠️ SQL Query Struktur Database

Gunakan query berikut untuk membuat database dan tabel-tabel yang dibutuhkan:

```sql
   -- Buat database
   CREATE DATABASE akuntansi;
   
   -- Gunakan database
   USE akuntansi;
   
   -- Tabel produk
   CREATE TABLE barang (
       kode VARCHAR(20) PRIMARY KEY,
       nama VARCHAR(100) NOT NULL,
       stok INT NOT NULL,
       harga_beli DECIMAL(10, 2) NOT NULL,
       harga_jual DECIMAL(10, 2) NOT NULL
   );
   
   -- Tabel transaksi penjualan
   CREATE TABLE penjualan (
       id INT AUTO_INCREMENT PRIMARY KEY,
       id_pesanan VARCHAR(50) NOT NULL,
       tanggal DATETIME NOT NULL,
       pelanggan VARCHAR(100),
       kode_barang VARCHAR(20),
       jumlah INT NOT NULL,
       harga_satuan DECIMAL(10, 2) NOT NULL,
       total DECIMAL(10, 2) NOT NULL,
       metode_pembayaran VARCHAR(50),
       rating INT,
       komentar TEXT,
       FOREIGN KEY (kode_barang) REFERENCES barang(kode) ON DELETE SET NULL
   );
```

---

## 📜 Lisensi
Proyek ini dilisensikan di bawah MIT License.

© 2025 Jiepra. Dibuat dengan ❤️ untuk manajemen toko modern.
