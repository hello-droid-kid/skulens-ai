# Changelog — SkuLens AI

## v1.9.2 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.9.2** (Build 14) (*Powered by Boostech Demo Tech*) — Perbaikan Bug Tombol Kosongkan Multi-Scan & Solusi Deteksi Barang Bertumpuk (Stacked Objects).

### Fitur & Peningkatan Utama
- **Perbaikan Bug Tombol Kosongkan / Reset Sesi Multi-Scan**:
  - **Akar Masalah**: Sebelumnya, saat kasir menekan *"Ya, Kosongkan"*, background camera analysis langsung mendeteksi ulang barang yang masih berada di atas meja kasir dalam hitungan 50 milidetik dan memasukkannya kembali ke sesi laporan, sehingga tombol kosongkan tampak tidak berfungsi.
  - **Solusi**:
    - Menambahkan mekanisme penahanan akumulasi sesi (*session suppression cooldown*): setelah dikosongkan, barang yang masih berada di atas meja tidak akan langsung mengisi ulang laporan sesi selama 3,5 detik atau hingga meja dikosongkan.
    - Dialog konfirmasi kosongkan kini otomatis menutup drawer laporan secara instan (`onDismiss()`).
    - Tombol *"Kosongkan Keranjang"* pada modal keranjang belanja kini sekaligus membersihkan rekaman sesi aktif sehingga meja kasir bersih total untuk transaksi berikutnya.
- **Peningkatan Signifikan Deteksi Barang Bertumpuk (*Stacked Items Recognition*)**:
  - **Akar Masalah**: Pustaka MediaPipe bawaan sering kali hanya mendeteksi 1 kotak besar untuk barang yang bertumpuk vertikal/horizontal, dan filter NMS standar membuang kotak deteksi yang saling tumpang tindih (*IoU threshold*).
  - **Solusi Komprehensif**:
    - **Peningkatan Kapasitas Detektor**: Kuota proposal objek dinaikkan dari 12 menjadi **24 proposal**, dan ambang deteksi diturunkan ke **0.18f** agar objek bertumpuk yang sebagian tertutup tetap terdeteksi.
    - **NMS Stack-Aware**: Algoritma NMS diperbarui dengan deteksi pergeseran pusat (*center-offset awareness*). Dua objek yang bertumpuk vertikal atau bersinggungan horizontal tidak lagi dibuang oleh NMS meskipun memiliki tingkat tumpang tindih (*overlap*) tinggi.
    - **Dekomposisi Sub-Slice Otomatis**: Jika 2-3 barang bertumpuk dideteksi sebagai satu kotak tinggi/lebar, sistem otomatis mengekstrak potongan atas (*top slice*), potongan bawah (*bottom slice*), tengah (*mid slice*), serta kiri/kanan untuk mengenali masing-masing barang secara individual.
    - **Deduplikasi Cerdas**: Kotak kontainer besar otomatis disaring jika potongan-potongan barang di dalamnya telah cocok dengan produk yang terdaftar, menghasilkan perhitungan kuantitas yang presisi ($2$ barang bertumpuk terhitung $2$).
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.9.2** (Build 14) di seluruh antarmuka (`✨ v1.9.2 • On-Device`).
- **Pengujian & Instalasi Langsung**:
  - Berhasil dipasang dan diverifikasi via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13, 720x1600).

### Berkas Rilis
- `releases/SkuLens-AI-v1.9.2.apk` (`101.92 MB`)
- SHA-256: `F2EDA7CB9E9A078E2159F5DEBCF8A27A14AB47FF225A1145B0EE3830CB3AAC29`

---

## v1.9.1 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.9.1** (Build 13) (*Powered by Boostech Demo Tech*) — Penambahan Baris Kode SKU pada Struk Kasir Fisik & Fallback Cetak Multi-Scan Otomatis.

### Fitur & Peningkatan Utama
- **Penambahan Kode SKU pada Struk Thermal**:
  - Pada struk cetak kasir (baik iMin POS internal maupun Bluetooth thermal ESC/POS), setiap produk kini mencetak baris kode SKU secara eksplisit di bawah nama produk (`SKU: [kode_sku]`).
  - Memudahkan verifikasi pencocokan fisik barang di meja kasir terhadap data inventaris toko.
- **Fallback Cerdas Cetak Struk Multi-Scan**:
  - Fungsi `printSessionReportReceipt` diperbarui: jika sesi akumulasi belum tersimpan atau baru dimulai, sistem secara otomatis mengambil barang yang sedang aktif dikenali di kamera (*live items*) sebagai data struk yang dicetak.
  - Mencegah error "Belum ada barang di laporan multi-scan" saat kasir langsung menekan tombol cetak struk dari layar multi-scan.
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.9.1** (Build 13) di seluruh layar: Splash Screen, TopAppBar, Dashboard Vision AI On-Device (`✨ v1.9.1 • On-Device`), dan Tab Pengaturan.
- **Pengujian & Instalasi Nyata**:
  - Berhasil diinstal dan dijalankan langsung pada perangkat kasir **iMin Swift 2 Pro** (Android 13, 720x1600).
  - Terverifikasi pada layar utama: versi `v1.9.1`, status printer kasir internal iMin aktif (`🟢 Siap`), dan fitur cetak struk berfungsi sempurna.

### Berkas Rilis
- `releases/SkuLens-AI-v1.9.1.apk` (`101.92 MB`)
- SHA-256: `E105F73E6350DA60E341022AEAFABA2B272EF559E7B01DBD464DE117760632A7`

---

## v1.9.0 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.9.0** (Build 12) (*Powered by Boostech Demo Tech*) — Integrasi Printer Kasir Hardware iMin POS & Bluetooth Thermal ESC/POS dengan Cetak Struk Logo Boostech dari Multi-Scan.

### Fitur & Peningkatan Utama
- **Integrasi Printer Kasir Hardware iMin POS (Built-in Internal Printer)**:
  - Integrasi resmi menggunakan `IminPrinterLibrary:V2.0.0.18` yang langsung terhubung ke layanan sistem `com.imin.printerservice` via AIDL IPC.
  - Mendukung inisialisasi otomatis printer saat aplikasi dibuka (`🟢 iMin POS Internal Printer Siap`).
  - Cetak teks resolusi tinggi, feed kertas otomatis, dan potong kertas (*partial cut*).
- **Integrasi Printer Bluetooth Thermal ESC/POS Eksternal**:
  - Pengaturan koneksi printer Bluetooth standard via profil Serial Port (SPP RFCOMM `00001101-0000-1000-8000-00805F9B34FB`).
  - Fitur enumerasi perangkat paired (*bonded devices*) dengan tombol penyegaran `[ 🔄 Segarkan ]`.
  - Pilihan hubungkan/putuskan sambungan dengan status visual real-time (`🟢 Terhubung Bluetooth: [Device]` / `⚪ Belum Siap`).
  - Menangani izin runtime Bluetooth otomatis untuk Android 12 & 13 (`BLUETOOTH_CONNECT`, `BLUETOOTH_SCAN`).
- **Pilihan Lebar Kertas Thermal (58 mm & 80 mm)**:
  - Mode **58 mm**: Format standar struk kasir mini (lebar 32 kolom karakter, batas dot raster 384).
  - Mode **80 mm**: Format standar struk kasir lebar (lebar 48 kolom karakter, batas dot raster 576).
  - Pengaturan tersimpan secara persisten di SharedPreferences (`skulens_printer_prefs`).
- **Format Struk Kasir Otentik dengan Logo Boostech**:
  - Konversi gambar Logo Wordmark Boostech (`boostech_wordmark.png`) menjadi bitmap 1-bit monochrome raster ESC/POS perataan tengah (*align center*).
  - Header toko resmi: `BOOSTECH AI VISION POS` & `SKULENS KASIR PINTAR`.
  - Informasi transaksi rapi: No. Transaksi, Tanggal & Jam, Kasir, dan Metode Pembayaran.
  - Garis pemisah ganda / putus-putus.
  - Rincian belanja: Nama produk, jumlah pcs x harga satuan, dan subtotal rata kanan.
  - Grand total tebal (*bold double-size*).
  - Footer: Ucapan terima kasih, catatan garansi, dan *Powered by Boostech Demo Tech*.
- **Cetak Struk Langsung dari Meja Kasir Multi-Scan**:
  - **Drawer Laporan Hasil Multi-Scan (`MultiObjectResultsDrawer`)**: Tombol tebal `[ 🖨️ Cetak Struk Laporan (Logo Boostech) ]` untuk mencetak seluruh akumulasi item yang terbaca di sesi kasir tanpa membuka keranjang.
  - **Modal Keranjang Belanja Kasir (`SavedBasketModal`)**: Tombol `[ 🖨️ Cetak Struk Belanja (Logo Boostech) ]` untuk mencetak struk transaksi belanja kasir resmi.
  - **Menu Pengaturan / Atur (`SettingsAndIminScreen`)**: Tombol `[ 🧾 🖨️ Tes Cetak Struk Kasir (Logo Boostech) ]` untuk menguji printer kapan saja.
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.9.0** (Build 12) di Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13, 720x1600).
  - Terverifikasi pencetakan struk pengujian kasir berhasil dicetak pada hardware iMin internal (`com.imin.printerservice`) dan pemindaian bluetooth printer sukses mendeteksi `InnerPrinter`.

### Berkas Rilis
- `releases/SkuLens-AI-v1.9.0.apk` (`101.92 MB`)
- SHA-256: `26DEBD8BA0504A7A976CC11FF5A1B12B91995274910FC840A6118215F2438CE9`

---

## v1.8.0 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.8.0** (Build 11) (*Powered by Boostech Demo Tech*) — Fitur Laporan Sesi Multi-Scan Persisten ("Jangan Hilang") & Drawer Report Terbaca di Meja Kasir.

### Fitur & Peningkatan Utama
- **Akumulator Sesi Multi-Scan ("Barang Sudah Dapat Jangan Hilang")**:
  - Mengatasi keluhan saat pemindaian meja kasir (`MultiObjectScreen`), ketika kamera bergeser atau sudut berganti, barang yang sudah terbaca seringkali langsung hilang dari layar (`totalRecognizedCount` menjadi 0 dan list kosong).
  - Sistem kini memiliki **State Akumulasi Sesi** (`sessionReportItems` & `ScannedSessionItem`):
    - Seluruh barang yang berhasil dikenali oleh AI visual akan dicatat dan dipertahankan sepanjang sesi pemindaian kasir berlangsung.
    - Status deteksi dibedakan secara visual:
      - `🟢 Live di Layar`: Objek saat ini sedang berada tepat di dalam pandangan kamera.
      - `⏱️ Terbaca di Sesi`: Objek yang sudah pernah terbaca sebelumnya di area meja kasir dan tetap disimpan di memori sesi meskipun kamera sudah bergeser ke sudut lain.
- **Drawer Laporan Multi-Scan Komprehensif (`MultiObjectResultsDrawer`)**:
  - Dapat dibuka kapan saja via tombol `[ 📋 Laporan (X) ]` di HUD atas maupun bar rangkuman bawah layar.
  - **Filter Tab Navigasi**:
    - `[ 📋 Semua Terbaca (X pcs) ]`: Menampilkan seluruh barang yang berhasil tercatat di sesi meja kasir ini.
    - `[ 🟢 Live di Layar (Y) ]`: Menyaring khusus barang yang sedang aktif berada di frame kamera saat ini.
  - **Kontrol Kuantitas & Manajemen Item Langsung**:
    - Kasir dapat menyesuaikan jumlah pcs barang secara cepat dengan tombol `[ + ]` dan `[ - ]`.
    - Tombol `[ 🗑️ ]` untuk menghapus item yang tidak diinginkan dari sesi laporan.
    - Menampilkan informasi lengkap: Foto produk, nama barang, kode SKU, subtotal Rupiah, serta persentase kecocokan AI tertinggi.
  - **Aksi Cepat Transaksi**:
    - Tombol `[ 🔄 Reset Sesi ]` dengan dialog konfirmasi untuk mengosongkan rekaman pemindaian area dan memulai meja belanja berikutnya.
    - Tombol besar `[ 💾 Simpan ke Keranjang (X pcs • Rp ...) ]` untuk langsung memindahkan seluruh isi laporan sesi ke keranjang belanja lokal secara persisten.
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.8.0** (Build 11) di Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13, 720x1600).
  - Tampilan Bottom Peek Bar, Drawer Laporan Sesi, tombol reset sesi, dan tombol simpan ke keranjang terverifikasi 100% mulus dan responsif.

### Berkas Rilis
- `releases/SkuLens-AI-v1.8.0.apk` (`97.09 MB`)
- SHA-256: `12398B98BA0CEFAECE82B260A5DC42CF415C483FC2680D1155F8F069C4B2E941`

---

## v1.7.0 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.7.0** (Build 10) (*Powered by Boostech Demo Tech*) — Validasi Deteksi Kemiripan Visual AI $\ge$ 90% & Pencegahan Data Barang Ganda (Anti-Double).

### Fitur & Peningkatan Utama
- **Validasi AI Kemiripan Visual $\ge$ 90% (Pencegahan Barang Ganda)**:
  - Mengatasi risiko kasir atau staf toko mendaftarkan ulang barang yang sebenarnya sudah ada di database sistem kasir.
  - Saat kasir mengambil foto atau merekam 360° untuk mendaftarkan barang baru, sistem secara otomatis menghitung kecocokan *cosine embedding* AI terhadap seluruh produk yang telah tersimpan.
  - **Banner Peringatan Visual Mencolok (Card Amber Alert)**:
    - Muncul tepat di atas form pendaftaran barang jika kemiripan visual $\ge 90\%$.
    - Menampilkan kartu produk yang cocok: foto thumbnail, nama produk, SKU, harga, dan badge persentase kecocokan (misal `94% Cocok`).
    - **Tombol Pintas 1-Klik**: `[ ➕ Tambahkan ke "[Nama Barang]" (Cegah Double) ]` yang langsung mengalihkan ke tab *Tambah ke Barang Ada* dan memilih produk tersebut untuk memperkaya sampel sudut tanpa membuat data duplikat.
  - **Dialog Konfirmasi Duplikasi Interaktif**:
    - Jika kasir tetap menekan tombol simpan baru padahal foto barang terdeteksi mirip $\ge 90\%$, sistem memunculkan dialog konfirmasi peringatan risiko data ganda di sistem kasir.
    - Menyediakan tombol cepat `[ Tambah ke Barang Ada ]` sebagai aksi utama yang disarankan, `[ Tetap Simpan Baru ]`, serta `[ Batal ]`.
- **Validasi SKU Duplikat Real-Time**:
  - Form SKU mendeteksi secara langsung jika kode SKU yang diketikkan sudah digunakan oleh produk lain di database lokal.
  - Border input langsung berubah menjadi merah dengan pesan: `⚠️ SKU ini sudah dipakai oleh "[Nama Produk]". Gunakan SKU lain atau tab Tambah ke Barang Ada.`
  - Tombol simpan dinonaktifkan secara otomatis untuk mencegah kegagalan penyimpanan akibat pelanggaran integritas data *unique constraint*.
- **Pembaruan Versi Sistem**:
  - Nomor versi dinaikkan ke **v1.7.0** (Build 10) di Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13, 720x1600).
  - Terverifikasi peringatan kemiripan 94%, pengalihan tab otomatis, dialog konfirmasi duplikasi, dan validasi SKU duplikat berjalan 100% mulus dan responsif.

### Berkas Rilis
- `releases/SkuLens-AI-v1.7.0.apk` (`97.13 MB`)
- SHA-256: `154F624A8D04F8CE508A9814438A7F765BD7B8001C1270E4941282D2F3D83FEA`

---

## v1.6.0 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.6.0** (Build 9) (*Powered by Boostech Demo Tech*) — Fitur Penyimpanan Keranjang Multi-Barang (Persisten & Anti-Hilang).

### Fitur & Peningkatan Utama
- **Penyimpanan Keranjang Multi-Scan ("Bisa Disimpan, Jangan Hilang")**:
  - Mengatasi keluhan hasil scan area meja yang langsung hilang saat barang diangkat kasir atau saat kamera bergeser.
  - **Tombol Cepat Simpan**:
    - Tombol `[ 💾 Simpan (X pcs) ]` langsung pada Peek Summary Bar di bawah layar.
    - Tombol utama tebal `[ 💾 Simpan ke Keranjang (X pcs • Rp ...) ]` di dalam Drawer Hasil Area.
    - Sekali ketuk, semua barang yang terdaftar dan terdeteksi di area langsung tersimpan ke keranjang lokal dengan suara konfirmasi ceria (*chime*).
  - **Penyimpanan Permanen (Persisten)**:
    - Data keranjang disimpan secara lokal di SharedPreferences (`saved_multi_basket_json`).
    - **Tidak akan hilang**: Tetap tersimpan utuh meskipun kasir memindahkan barang, mengarahkan kamera ke tempat lain, berpindah tab (Home/Scan/Model/Atur), bahkan saat aplikasi ditutup dan dibuka kembali.
- **Drawer / Modal Keranjang Belanja Interaktif (`SavedBasketModal`)**:
  - Akses satu ketukan via tombol mengambang `[ 🛒 X item ]` di HUD atas dan tombol `[ 🛒 Keranjang ]` di bar bawah.
  - Menampilkan daftar lengkap: Foto thumbnail barang, Nama Produk, SKU, Harga satuan, dan Subtotal per item.
  - **Kontrol Kuantitas Lengkap**:
    - Tombol `[ + ]` untuk menambah jumlah pcs.
    - Tombol `[ - ]` untuk mengurangi jumlah pcs.
    - Tombol tong sampah merah `[ 🗑️ ]` saat kuantitas mencapai 1 untuk menghapus item secara aman.
    - Tombol `[ 🗑️ Kosongkan ]` dengan dialog konfirmasi jika transaksi kasir telah selesai.
    - Rekapitulasi otomatis: Total Kuantitas (pcs), Jumlah macam produk, dan Total Nilai Tagihan (Rupiah).
- **Indikator Titik Oranye (Badge Dot) di Navigasi**:
  - Tab **Multi** pada navbar bawah otomatis menyalakan titik oranye jika ada barang yang sedang tersimpan di keranjang, mengingatkan kasir bahwa ada transaksi yang siap diproses.
- **Tombol Pintas Daftarkan Produk Baru**:
  - Pada objek yang belum terdaftar di area, ditambahkan tombol `[ Daftarkan ]` yang langsung membuka alur scan dan pendaftaran produk.
- **Pembaruan Versi Sistem**:
  - Nomor versi aplikasi dinaikkan ke **v1.6.0** (Build 9) di Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13).
  - Terverifikasi penambahan kuantitas, kalkulasi total belanja (Rp 118.000 -> Rp 163.000), perpindahan tab tanpa kehilangan data, dan pengosongan keranjang berjalan 100% mulus.

### Berkas Rilis
- `releases/SkuLens-AI-v1.6.0.apk` (`97.06 MB`)
- SHA-256: `27773289DA56A6C9FAF31423FF8C048ABD50F4466C0BC668A066CFE54876BD7C`

---

## v1.5.0 (2026-11-13)

Rilis pembaruan **SkuLens AI v1.5.0** (Build 8) (*Powered by Boostech Demo Tech*) — Tombol Lampu Flash Hardware & Kontrol Jeda (Pause) Rekam 360°.

### Fitur & Peningkatan Utama
- **Tombol Lampu Senter / Flash Kamera Hardware**:
  - Mendeteksi ketersediaan unit lampu kilat hardware (`camera.cameraInfo.hasFlashUnit()`) secara dinamis.
  - Menampilkan tombol pill `[ ⚡ Flash ]` / `[ ⚡ Flash ON ]` di kontrol HUD kamera pada mode *Cek Barang*, *Rekam 360°*, dan *Multi-Objek*.
  - Mengontrol lampu LED senter fisik perangkat secara langsung (`enableTorch`) untuk pencahayaan optimal di kondisi meja kasir yang remang/gelap.
- **Kontrol Jeda / Pause 360° ("Supaya Tidak Semuanya Ter-capture")**:
  - **Pencegahan Tangkapan Beruntun (Burst Prevention)**: Menaikkan interval aman antar jepretan otomatis menjadi 1,4 detik dan memperketat batas kesamaan sudut visual (novelty threshold) agar kamera tidak memotret liar saat barang baru mulai diputar.
  - **Floating Control di Bawah Viewfinder**:
    - Tombol Merah `[ ⏸️ Jeda Auto (X/8) ]` untuk menghentikan pengambilan otomatis seketika saat memutar barang.
    - Tombol Hijau `[ ▶️ Lanjut Auto (X/8) ]` untuk melanjutkan auto-capture setelah sudut barang siap.
    - Tombol Kuning `[ 📸 Jepret Sisi Ini ]` untuk mengambil satu sudut foto secara manual kapan pun kasir inginkan.
  - **Panel Bawah Interaktif**: Menambahkan tombol berlabel jelas `[ ⏸️ Jeda Auto ]` / `[ ▶️ Lanjut Auto ]` serta `[ 📸 Jepret +1 ]` dengan teks panduan status visual.
- **Pembaruan Versi Sistem**:
  - Versi aplikasi dinaikkan ke **v1.5.0** (Build 8) di Splash Screen, TopAppBar, Dashboard Vision AI On-Device, dan Tab Pengaturan.
- **Pengujian & Verifikasi Langsung**:
  - Diinstal dan diuji via *Wireless Debugging* pada perangkat kasir **iMin Swift 2 Pro** (Android 13).
  - Lampu LED fisik terbukti menyala terang dan menerangi meja scanner. Tombol Jeda berfungsi membekukan auto-capture dengan aman tanpa merusak 8 SKU produk Room SQLite yang tersimpan.

### Berkas Rilis
- `releases/SkuLens-AI-v1.5.0.apk` (`97.01 MB`)
- SHA-256: `0E772C0D71A2E970E40037D28A0848B3C1C7F847E91FB39613CF6B785681F00B`

---

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
