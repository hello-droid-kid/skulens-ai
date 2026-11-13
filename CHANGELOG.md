# Changelog — SkuLens AI

## v1.1.0 (2026-11-13)

Pembaruan besar untuk estetika antarmuka, navigasi interaktif, dan analitik visual performa AI pada **SkuLens AI** (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan Baru
- **Animasi Perpindahan Halaman (Page Transitions)**: Transisi halus arah horizontal (slide + fade + scale lembut `0.96f -> 1f`) saat berpindah antar-tab, lengkap dengan animasi vertikal pada judul dan subjudul `TopAppBar`.
- **Indikator Versi Aplikasi**: Menampilkan badge `v1.1.0` di `TopAppBar`, teks versi di Splash Screen, hero header dashboard, dan kartu detail **"Tentang Aplikasi & Versi"** di tab Pengaturan.
- **Grafik Dashboard Teranimasi (Home Analytics)**:
  - **Grafik Performa AI (Dual-Ring Donut Gauge)**: Cincin teranimasi untuk *Avg Sukses %* (gradasi oranye-kuning) dan *Kemiripan AI %* (charcoal), rasio scan *Cocok vs Gagal*, serta tombol *Reset Statistik*.
  - **Grafik Sudut Data Model (Vertical Column Bar Chart)**: Diagram kolom batang naik bertingkat (*staggered*) menampilkan kelengkapan sudut model 360° per produk dengan garis target kesiapan `4` sudut (*Siap 360°*) hingga `8` sudut. Kolom dapat diketuk langsung untuk menambah sudut foto produk.
- **Deteksi Multi-Objek Area**: Dukungan deteksi banyak barang sekaligus dalam satu frame kamera dengan hitungan jumlah produk (`Nx`) dan rincian bottom drawer.
- **Floating Liquid Wave Navbar**: Bilah navigasi melayang berbentuk kapsul charcoal gelap dengan kubah gelombang amber dinamis mengikuti tab yang dipilih.

### Berkas Rilis
- `releases/SkuLens-AI-v1.1.0.apk` (`97.31 MB`)
- SHA-256: `01A3990D3C929BCF448838644F2BD704C3E82A9DE5543C99F8B2C6B72825BB9B`

---

## v1.0.0 (2026-11-12)

Rilis publik pertama **SkuLens AI** (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan
- Pengenalan barang real-time offline berbasis MobileNetV3 (*on-device computer vision*) tanpa GMS.
- Database lokal Room SQLite untuk menyimpan **Nama Barang**, **SKU**, **Harga**, **Kategori**, **Catatan**, dan multi-sampel foto AI.
- Slide-up **Recognized Product Drawer** otomatis ketika barang cocok ditemukan.
- Mode **Rekam 360° Otomatis** (hingga 8 sudut berbeda) lengkap dengan dialog instruksi sebelum perekaman dimulai.
- Pembacaan barcode SKU otomatis (ZXing) & dukungan USB HID scanner.
- Pemilih kamera bawaan / eksternal USB UVC untuk berbagai tipe perangkat **iMin POS**.
- Preset kepekaan visual (**Peka 58%**, **Normal 64%**, **Ketat 74%**) dan pengaturan ukuran kotak fokus.
- Identitas visual tema **Amber-Oranye (`#F59E0B`) + Charcoal (`#18181B`)**, splash screen tunggal dengan logo **SkuLens AI** dan wordmark resmi **Boostech Demo Tech**.

### Berkas Rilis
- `releases/SkuLens-AI-v1.0.0.apk` (`92.85 MB`)
- SHA-256: `F079BF86D13403317640DFDF4E2A1231415511878FD0CD3E7F06AE27C47E8530`
