# Changelog — SkuLens AI

## v1.3.0 (2026-11-13)

Pembaruan versi resmi **SkuLens AI v1.3.0** (Build 4) (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan
- **Peningkatan Versi Aplikasi**: Pembaruan penomoran versi menjadi `v1.3.0` di seluruh antarmuka (Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan).
- **Tata Letak Navbar Lega & Luas**: Bilah navigasi bawah (*Floating Wave Navbar*) memanfaatkan 100% lebar kapsul untuk 5 menu utama (**Home**, **Scan**, **Multi**, **Model**, **Atur**) dengan kubah gelombang amber yang presisi dan nyaman disentuh pada layar sentuh POS.
- **Dashboard Analitik Teranimasi**: Dual-ring donut gauge dan vertical column bar chart terintegrasi dengan data model produk real-time.

### Berkas Rilis
- `releases/SkuLens-AI-v1.3.0.apk` (`97.00 MB`)
- SHA-256: `617E56BBAE81E77B407F51852D84310CD3921F679127E8D8270F96720CAB529D`

---

## v1.2.0 (2026-11-13)

Penyempurnaan tata letak navigasi bawah (*Floating Wave Navbar*) agar lebih luas, lega, dan nyaman digunakan di layar sentuh kasir **iMin Swift 2 Pro**.

### Fitur & Peningkatan
- **Tata Letak Navbar Lebih Lega**: Logo pada bilah navigasi bawah dihilangkan sehingga seluruh lebar pill charcoal digunakan penuh secara proporsional untuk ke-5 tab.
- **Kubah Gelombang Cair Simetris**: Animasi gelombang amber (*liquid wave arch*) kini bergerak penuh dan presisi menaungi ikon tab aktif dari ujung kiri hingga ujung kanan.

### Berkas Rilis
- `releases/SkuLens-AI-v1.2.0.apk` (`97.00 MB`)
- SHA-256: `213B17507422692CEFA698532A7E254FAB50106956EC9DC5B30BD987E9FC5387`

---

## v1.1.0 (2026-11-13)

Pembaruan besar untuk estetika antarmuka, navigasi interaktif, dan analitik visual performa AI pada **SkuLens AI** (*Powered by Boostech Demo Tech*).

### Fitur & Peningkatan
- **Animasi Perpindahan Halaman (Page Transitions)**: Transisi halus arah horizontal (slide + fade + scale lembut `0.96f -> 1f`) saat berpindah antar-tab, lengkap dengan animasi vertikal pada judul dan subjudul `TopAppBar`.
- **Grafik Dashboard Teranimasi (Home Analytics)**: Dual-Ring Donut Gauge & Vertical Column Bar Chart.
- **Deteksi Multi-Objek Area**: Dukungan deteksi banyak barang sekaligus dalam satu frame kamera dengan hitungan jumlah produk (`Nx`) dan rincian bottom drawer.

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

### Berkas Rilis
- `releases/SkuLens-AI-v1.0.0.apk` (`92.85 MB`)
- SHA-256: `F079BF86D13403317640DFDF4E2A1231415511878FD0CD3E7F06AE27C47E8530`
