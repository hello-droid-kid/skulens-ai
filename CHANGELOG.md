# Changelog — SkuLens AI

## v1.4.1 (2026-11-13)

Pembaruan optimalisasi transisi cold start & splash screen **SkuLens AI v1.4.1** (Build 7) (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan
- **Perbaikan Glitch "Double Kuning" / Blank Yellow pada Splash Screen**:
  - Menghilangkan *transparent icon* lama pada `themes.xml` yang sebelumnya menyebabkan layar Android menampilkan bidang kuning polos kosong selama 2–3 detik saat aplikasi baru dibuka.
  - Memasang **Splash Screen Terintegrasi** (`@drawable/splash_background` dan `windowSplashScreenAnimatedIcon` = `@drawable/app_logo`) sehingga logo **SkuLens AI** langsung tampil di tengah sejak milidetik pertama icon aplikasi ditekan tanpa menunggu Compose.
  - Menyelaraskan skala logo dan transisi *fade-in* teks ("SkuLens AI", versi, dan kata logo Boostech) secara halus tanpa efek lompat (*jumpy scale*).
  - Mempersingkat durasi tunggu splash agar transisi langsung masuk ke dashboard dengan mulus (~1 detik).
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.4.1** (Build 7) pada Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Atur.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji *cold-start* di perangkat kasir **iMin Swift 2 Pro** (Android 13). Terverifikasi logo langsung tampil instan sejak awal proses dibuka dan seluruh data 8 SKU Room SQLite tetap utuh.

### Berkas Rilis
- `releases/SkuLens-AI-v1.4.1.apk` (`97.01 MB`)
- SHA-256: `1C13D5DBC316F9331447A990F80ADE3ECAADE5194A9F28D84698573B3B45A3A4`

---

## v1.4.0 (2026-11-13)

Rilis pembaruan besar **SkuLens AI v1.4.0** (Build 6) (*Powered by Boostech Demo Tech*) — Pemisahan Alur Kerja Cek Kasir vs Studio Rekam 360°.

### Fitur & Peningkatan Utama
- **Pemisahan Mode "Cek Barang (Kasir)" vs "Rekam 360° (Daftar)"**:
  - Mengganti tombol ganda yang membingungkan (`1 Sisi`, `Scan 360°`, `Rekam 360°`) dengan **Segmented Mode Switcher** modern di atas frame kamera:
    - **Mode Cek Barang (Kasir)**: Dikhususkan untuk kasir membaca dan mencocokkan barang yang sudah terdaftar secara instan. Menampilkan nama produk, SKU, harga, dan skor kecocokan %. Jika barang belum dikenal, muncul kartu *"BARANG TIDAK DIKENAL"* dengan satu tombol jelas: `[ 🎥 Daftarkan & Rekam 360° ]`.
    - **Mode Rekam 360° (Daftar)**: Dikhususkan untuk enrollment produk baru. Membuka studio panduan 360° dengan cincin progres 8 segmen melingkar, skor ketajaman visual, auto/manual capture saat rotasi, dan form input SKU.
- **Peningkatan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.4.0** (Build 6) pada Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Atur.
- **Pembersihan Antarmuka Kamera**:
  - Area kamera menjadi jauh lebih lega, bersih, dan bebas tombol yang tumpang-tindih.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diverifikasi melalui *Wireless Debugging* di perangkat kasir **iMin Swift 2 Pro** (Android 13) dengan seluruh data 8 SKU produk Room SQLite tetap aman dan utuh.

### Berkas Rilis
- `releases/SkuLens-AI-v1.4.0.apk` (`97.01 MB`)
- SHA-256: `B9CF08976BA06348DB97E4EDB6ED3B3DE6D69F952C48491C7182C9F6420EE2C0`

---

## v1.3.1 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.3.1** (Build 5) (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan
- **Pembaruan Versi Produksi**: Menaikkan nomor versi menjadi `v1.3.1` (Build 5) di seluruh lapisan aplikasi (Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan).
- **Floating Wave Navbar Dioptimalkan**: Menghilangkan logo bawah sehingga seluruh lebar bar dialokasikan penuh secara simetris ke 5 menu (**Home**, **Scan**, **Multi**, **Model**, **Atur**) dengan kubah gelombang amber responsif.
- **Pembaruan Terverifikasi di iMin Swift 2 Pro**: Aplikasi langsung dipasang dan diuji pada perangkat POS iMin dengan data produk dan sampel vektor lokal yang tetap utuh.

### Berkas Rilis
- `releases/SkuLens-AI-v1.3.1.apk` (`97.00 MB`)
- SHA-256: `03BB6BD899A935BBCA53118BC19661F8ED97BDB6BB0F0FD67AA6A4917F0388EC`

---

## v1.3.0 (2026-11-13)

Pembaruan versi resmi **SkuLens AI v1.3.0** (Build 4).

### Fitur & Peningkatan
- Indikator versi aplikasi diperbarui ke `v1.3.0`.
- Optimasi tata letak navigasi bawah dan dashboard analitik.

### Berkas Rilis
- `releases/SkuLens-AI-v1.3.0.apk` (`97.00 MB`)
- SHA-256: `617E56BBAE81E77B407F51852D84310CD3921F679127E8D8270F96720CAB529D`

---

## v1.2.0 (2026-11-13)

Penyempurnaan tata letak navigasi bawah (*Floating Wave Navbar*) agar lebih luas, lega, dan nyaman digunakan di layar sentuh kasir **iMin Swift 2 Pro**.

---

## v1.1.0 (2026-11-13)

Pembaruan besar untuk estetika antarmuka, navigasi interaktif, dan analitik visual performa AI pada **SkuLens AI** (*Powered by Boostech Demo Tech*).

---

## v1.0.0 (2026-11-12)

Rilis publik pertama **SkuLens AI** (*Powered by Boostech Demo Tech*).
