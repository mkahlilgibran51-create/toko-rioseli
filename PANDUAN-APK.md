# Aplikasi Android Toko Silawati Rioseli

Folder ini berisi proyek Android lengkap. File APK dibangun otomatis oleh GitHub (gratis), jadi Anda
tidak perlu memasang Android Studio.

## A. Membuat APK (sekali, lalu setiap ada pembaruan)

1. Buat akun di github.com, lalu buat repository baru bernama `toko-rioseli-sila`. **Pilih Private.**
2. Unggah seluruh isi folder ini ke repository tersebut, termasuk folder `.github` dan `android`.
   - Cara mudah: di halaman repository klik **uploading an existing file**, lalu seret semua isi folder.
   - Jangan unggah folder `node_modules` (tidak ada di paket ini).
3. Buka tab **Actions**, pilih **Bangun APK**, lalu klik **Run workflow**.
4. Tunggu 5–10 menit sampai tanda centang hijau. Klik hasil build tersebut, lalu unduh
   **toko-rioseli-sila-apk** di bagian Artifacts. Ekstrak zip-nya, di dalamnya ada `app-release.apk`.

## B. Memasang di tablet Samsung

1. Pindahkan `app-release.apk` ke tablet (Google Drive, kabel USB, atau WhatsApp ke diri sendiri).
2. Buka file itu di tablet. Jika diminta, izinkan **Instal aplikasi tidak dikenal** untuk aplikasi
   yang Anda pakai membuka file.
3. Buka **Toko Silawati Rioseli**. Izinkan akses **Kamera** bila ingin scan barcode lewat kamera.
4. Buat akun pemilik (PIN 6 angka) dan **catat kode pemulihan** yang muncul.

## C. Memperbarui aplikasi

1. Ganti **seluruh isi proyek** di GitHub dengan isi zip terbaru (bukan hanya `src/App.jsx`). Sejak versi 2.15 ada berkas
   tambahan, `public/katalog-ipos5.tsv`, dan nomor versi di `android/app/build.gradle` ikut naik. Jangan hapus `firebase-config.js`
   milik Anda; isi ulang bila terganti.
2. Commit di GitHub, lalu jalankan **Bangun APK** lagi dan tunggu centang hijau.
   Cek versinya di aplikasi: Pengaturan, Perangkat, "Versi aplikasi".
3. Pasang APK baru **di atas** yang lama (jangan uninstall). Data tetap ada karena tanda tangan aplikasi sama.

## D. Hal penting

- **Setiap membuat APK baru, naikkan `versionCode`** (angka bulat) di `android/app/build.gradle`, misalnya dari 15 ke 16.
  Jika angkanya sama atau lebih kecil dari yang terpasang, Android bisa menolak pemasangan di atas aplikasi lama.

- **Berkas `android/app/rioseli.keystore` adalah kunci tanda tangan aplikasi.** Kata sandinya ada di
  `android/app/build.gradle`. Simpan salinan keystore di tempat aman. Jika hilang, pembaruan harus
  dilakukan dengan uninstall dulu, dan **data lokal di tablet ikut hilang**. Karena itu repository harus Private.
- **Jangan uninstall aplikasi** sebelum mengunduh cadangan (Pengaturan, Unduh cadangan) atau memastikan
  cloud Firebase sudah sinkron. Menghapus aplikasi menghapus data lokalnya.
- Menu **Unduh cadangan** dan ekspor CSV di aplikasi Android membuka menu Bagikan: pilih Drive, WhatsApp,
  atau simpan ke penyimpanan.
- Layar tablet dibuat tetap menyala selama aplikasi terbuka.
- Cetak struk: sejak versi 2.7 aplikasi mencetak **langsung ke printer thermal Bluetooth**, tanpa RawBT. Lihat bagian D6.
- Aplikasi ini **belum pernah dibangun menjadi APK dan dicoba di tablet** oleh pembuatnya. Bagian web-nya
  sudah diuji di browser, tetapi pembangunan APK dan perilaku di perangkat nyata (kamera, cetak, penyimpanan)
  perlu Anda cek pada percobaan pertama. Jika build gagal, kirim teks error dari tab Actions.

## D2. Layar pelanggan (monitor kedua, versi 2.4)

Fitur ini menampilkan barang, diskon, total harga, dan gambar promosi di monitor yang menghadap pelanggan (misalnya layar 10,1 inci).

1. Sambungkan monitor ke tablet. Syaratnya, tablet dan kabel/adaptornya mendukung keluaran video
   (HDMI atau USB-C DisplayPort). Layar USB yang hanya berupa "layar tambahan lewat driver" biasanya
   **tidak** dikenali Android sebagai monitor kedua.
2. Monitor harus bekerja sebagai **layar tambahan (extend)**. Bila tablet hanya menyalin layar kasir (mirror),
   layar pelanggan tidak akan muncul.
3. Buka aplikasi, Pengaturan, bagian **Layar pelanggan**. Nyalakan, lalu pilih "Daftar barang, diskon, total" atau "Total saja".
   Di bagian **Gambar promosi** tekan **Tambah gambar** (maksimal 8, ukuran paling pas 1280 x 768). Gambar tampil layar penuh saat kasir kosong
   dan di sisi kanan daftar belanja saat ada transaksi. Gambar tersimpan di tablet itu saja, tidak ikut cloud atau cadangan.
4. Lencana akan berubah menjadi "Layar kedua terdeteksi". Tekan **Kirim contoh** untuk melihat tampilannya.

Bagian ini **belum pernah dicoba di monitor sungguhan** oleh pembuatnya. Jika lencana tetap "tidak terdeteksi"
padahal monitor menyala, berarti tablet menganggapnya bukan layar tambahan. Beri tahu merek tablet dan jenis
kabelnya agar bisa dicarikan jalan lain.

## D3. Yang baru di versi 2.5

- **Tiga jenis akun.** Pemilik (semua fitur), Kasir (hanya berjualan, izin tambahan bisa diatur), Gudang (stok, barang masuk,
  pembelian; tidak bisa berjualan atau melihat laporan). Atur di Pengaturan, bagian Akun, tombol **Tambah akun** dan **Atur akses**.
- **Jual saat stok habis** diizinkan secara bawaan. Stok dicatat minus dan dibetulkan saat barang masuk atau stok opname.
  Bisa dimatikan di Pengaturan, bagian Aturan penjualan.
- **Tombol Scan barcode** besar di layar Kasir. Scanner fisik (USB atau Bluetooth) cukup langsung di-scan tanpa menekan tombol.
  Bila barcode belum terdaftar, pemilik (atau kasir yang diberi izin) bisa langsung mengisi nama dan harga; barang itu
  ditandai "belum dicek" di menu Stok. Modal barang seperti ini masih 0, jadi labanya terlihat terlalu besar sampai dilengkapi.
- **Daftar cek shift.** Tampil saat kasir memulai dan menutup shift. Isi daftarnya diubah di Pengaturan.
- **Laporan harian ke WhatsApp.** Satu ketukan membuka WhatsApp dengan isi laporan, lalu tekan kirim. Aplikasi tidak bisa
  mengirim sendiri tanpa ditekan; itu butuh layanan WhatsApp berbayar dan server.
- **Settlement QRIS.** Aplikasi mengingatkan bila ada hari dengan penjualan QRIS yang CSV settlement-nya belum diunggah.
  Unggahnya tetap manual: buka email ShopeePay, unduh CSV, lalu Laporan, tab QRIS, Unggah.

## D4. Cloud (Firebase) yang ditanam di aplikasi

Sejak versi 2.6 sambungan cloud bisa ditanam saat membangun APK. Setelah itu tidak ada yang perlu diisi di Pengaturan:
setiap HP atau tablet yang memasang APK langsung tersambung ke data toko saat pertama dibuka.

**Sekali saja, membuat Firebase (sekitar 10 menit, gratis):**

1. Buka console.firebase.google.com dengan akun Google Anda, buat project baru (paket Spark).
2. Build, Firestore Database, Create database (mode produksi, lokasi asia-southeast2 Jakarta).
3. Build, Authentication, Get started, aktifkan Email/Password. Tab Users, Add user: buat email dan password khusus toko.
4. Firestore, tab Rules. Tempel aturan di bawah (ganti emailnya dengan email toko), lalu Publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /toko_rec/{doc} {
      allow read, write: if request.auth != null
                         && request.auth.token.email == "EMAIL-TOKO-ANDA";
    }
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

5. Project settings (ikon roda gigi), tab General: catat **Project ID** dan **Web API Key**.

**Menanam ke aplikasi:**

6. Buka berkas `public/firebase-config.js` di proyek ini dengan Notepad. Isi empat nilainya (apiKey, projectId, email, password). Simpan.
7. Di folder proyek jalankan `npm run build` lalu `npx cap sync android`, kemudian bangun APK seperti biasa.
   (Bila membangun lewat GitHub Actions, cukup simpan berkasnya dan push.)
8. Pasang APK. Di tablet yang sudah berisi data, data lama digabung ke cloud. Di perangkat baru, data toko langsung muncul.
9. Pemilik: Pengaturan, Cloud dan cadangan, tekan **Uji keamanan**. Hasilnya harus "Aman".

**Yang perlu dijaga:** password akun toko ikut tersimpan di dalam APK. Jangan bagikan APK atau proyek ke orang luar, dan
repository harus Private. Bila ada perangkat hilang, ganti password di Firebase (Authentication, Users), ubah di
`firebase-config.js`, lalu bangun dan pasang APK baru.

Bila berkas itu dibiarkan kosong, aplikasi tetap jalan seperti biasa dan cloud bisa disambungkan lewat Pengaturan.

Perkiraan pemakaian kuota gratis Firebase dengan 8.000 barang dan 3 perangkat (hitungan, belum diukur di Firebase asli):
unggah pertama sekitar 8.000 tulis (batas 20.000 per hari), tiap perangkat baru sekitar 8.000 baca, dan pemakaian harian
sekitar 20.000 baca (batas 50.000 per hari).

## D5. Yang berubah di versi 2.6

- Pengaturan dibagi menjadi bagian: Toko, Kasir dan struk, Akun, Perangkat, Cloud dan cadangan.
- Ringkasan di menu Analitik dihitung sendiri oleh aplikasi. Sambungan ke LLM dihapus.
- Panel pengingat di Beranda dihapus. Daftar cek saat mulai dan tutup shift tetap ada.
- Kasir boleh mendaftarkan barcode yang belum terdaftar (bisa dimatikan per akun lewat Atur akses).

## D6. Cetak struk langsung ke printer (versi 2.7)

1. Nyalakan printer thermal. Di tablet buka Pengaturan Android, Bluetooth, lalu pasangkan printernya (PIN biasanya 0000 atau 1234).
2. Buka aplikasi, Pengaturan, **Kasir dan struk**. Di "Cara mencetak" pilih **Langsung ke printer**, lalu **Pilih printer**.
   Saat pertama kali, Android meminta izin "Perangkat di sekitar". Izinkan.
3. Tekan **Cetak tes**. Bila struk keluar, selesai.

- Struk **tercetak sendiri untuk transaksi mulai Rp50.000**. Batasnya bisa diubah (semua transaksi, 20 ribu, 50 ribu, 100 ribu)
  atau dimatikan. Transaksi di bawah batas tetap bisa dicetak lewat tombol Cetak struk.
- Sambungan ke printer dibiarkan terbuka, jadi struk berikutnya keluar tanpa jeda. Bila printer sempat mati, aplikasi menyambung ulang sendiri.
- **RawBT** adalah aplikasi perantara dari Play Store. Dulu dipakai karena aplikasi belum bisa bicara langsung dengan printer.
  Sekarang hanya cadangan: pilih "Lewat RawBT" bila cetak langsung tidak cocok dengan printer Anda.
- Dengan scanner fisik, setelah bayar tidak perlu menekan "Transaksi baru": langsung scan barang pembeli berikutnya.
- Bagian cetak langsung ini **belum pernah dicoba dengan printer sungguhan** oleh pembuatnya. Bila tidak keluar, kirim merek printer
  dan pesan galat yang muncul.

## D7. Nama kategori di struk (versi 2.8)

Barang dari kategori **Rokok** ditulis "Rokok" saja di struk, dengan harga masing-masing. Merek tidak dicetak.

- Syaratnya, kategori barang rokok di menu Stok harus **Rokok** (huruf besar atau kecil tidak masalah).
- Berlaku untuk struk cetak, cetak ulang, dan struk yang dikirim lewat WhatsApp. Layar kasir, Riwayat, Laporan, dan Stok tetap memakai nama asli.
- Kategori lain bisa ditambah atau Rokok dimatikan di Pengaturan, Kasir dan struk, bagian "Tulis nama kategori saja di struk", lalu Simpan.
- Sejak versi 2.9: barang kategori terpilih yang harganya **di bawah Rp25.000** dicetak tanpa nama, hanya jumlah dan harga
  (contoh: `1 x 12.000   12.000`). Batasnya diubah di kolom "Tanpa tulisan nama bila harga di bawah"; isi 0 untuk mematikan.
  Barang seharga tepat Rp25.000 masih ditulis "Rokok".

## D8. Kasir cepat untuk semi-grosir (versi 2.10)

- **Jumlah dulu, baru barang.** Di atas daftar barang ada baris "Jumlah": 1, 2, 3, 5, 10, 12, 24, dan "Angka lain".
  Tekan angkanya, lalu tekan barangnya (atau scan). Barang masuk sejumlah itu, dan angka kembali ke 1.
  Barang bersatuan besar membuka pilihan pcs/dus dengan jumlah yang sudah terisi. Barang curah langsung masuk sebagai kg atau liter.
  Tanpa menekan angka, semuanya seperti biasa: satu ketukan atau satu scan berarti satu barang.
- **Papan "Paling sering dibeli".** Tampil di atas daftar barang. Isinya dihitung dari berapa kali barang masuk struk dalam
  30 hari terakhir; penjualan terbaru berbobot lebih besar. Sejak versi 2.11 papan dihitung **sekali saat ganti hari**
  (atau saat aplikasi dibuka), bukan tiap transaksi, supaya kasir tidak terbebani saat ramai dan posisi tombol tetap sepanjang hari.
  Sejak versi 2.12 tidak ada pengecualian: toko yang baru mulai melihat papannya terisi pada hari berikutnya.
- **Penyimpanan lebih ringan (versi 2.12).** Setiap penjualan sekarang hanya menulis struk hari itu dan catatan stok kecil,
  bukan seluruh data barang dan ringkasan setahun. Ringkasan harian ditulis tiap 10 menit atau saat aplikasi disembunyikan,
  dan dihitung ulang dari struk bila aplikasi tertutup mendadak. Sinkron cloud tidak lagi menulis ulang data barang tiap 8 detik.
- **Laci uang.** Dengan cetak langsung dan "Buka laci uang otomatis" menyala, laci terbuka pada setiap pembayaran tunai,
  termasuk transaksi kecil yang struknya tidak dicetak. Lewat RawBT, laci hanya terbuka saat struk dicetak.

## D9. Cadangan otomatis dan layar pelanggan (versi 2.13)

- **Cadangan otomatis harian ke tablet.** Aplikasi menulis sendiri berkas cadangan sekali sehari saat masuk, dan menulis ulang
  saat tutup shift supaya penjualan hari itu ikut. Tidak pernah berjalan di tengah melayani pembeli.
  Lokasinya folder **Documents/TokoRioseli** di penyimpanan tablet, dengan nama `cadangan-otomatis-TANGGAL.json`. Tujuh berkas
  terakhir disimpan. Bila folder Documents tidak bisa ditulis, dipakai folder aplikasi (yang ikut terhapus bila aplikasi dihapus);
  statusnya terlihat di Pengaturan, Cloud dan cadangan.
- **Isi cadangan otomatis:** semua barang dan stok, pelanggan, kasbon, supplier, akun, pengaturan, ringkasan penjualan semua hari,
  dan struk rinci 14 hari terakhir. Struk rinci yang lebih lama hanya ada di cadangan penuh (tombol Unduh cadangan) atau di cloud.
- **Memulihkan:** Pengaturan, Cloud dan cadangan, Pulihkan dari cadangan, lalu pilih berkasnya di Documents/TokoRioseli.
- **Cadangan ke server** adalah Firebase (bagian D4). Setelah aktif, seluruh data termasuk semua struk tersalin ke server terus-menerus.
- Tablet yang rusak atau hilang tetap membawa pergi folder Documents. Salin berkasnya ke Drive sesekali, atau aktifkan Firebase.
- **Layar pelanggan** sekarang mengikuti aturan struk: rokok tampil sebagai "Rokok", dan yang di bawah batas harga tampil tanpa nama.
- Bagian tulis berkas ini belum pernah dicoba di tablet sungguhan.

## D10. Satuan bertingkat, jejak penghapusan, dan saran harga (versi 2.14)

- **Satuan bertingkat.** Satu barang boleh punya beberapa satuan besar (renceng, dus, karton, slop, bal). Tiap satuan punya isi,
  harga jual, dan barcode sendiri. Atur di Stok, Ubah barang, bagian "Satuan besar".
  - Scan barcode dus langsung memasukkan 1 dus, scan barcode pcs memasukkan 1 pcs. Scan tidak pernah membuka dialog pilihan.
  - Ketuk barang di layar tetap membuka pilihan satuan.
  - Barang masuk dan pembelian bisa dicatat per satuan mana pun.
  - Barang lama yang hanya punya satu satuan besar tetap berjalan tanpa perlu diubah.
- **Jejak penghapusan.** Aplikasi mencatat diam-diam, tanpa dialog di kasir: barang yang dihapus dari keranjang, jumlah yang dikurangi,
  keranjang yang dikosongkan, antrian yang dihapus, dan keranjang yang ditinggal saat aplikasi dikunci. Pemilik melihatnya di
  Analitik, kartu "Barang dihapus dan keranjang dibatalkan", per kasir, dengan rincian per hari. Catatan ini tidak mengubah omzet,
  kas, stok, atau nomor struk.
- **Saran harga jual.** Saat barang masuk atau pembelian dicatat dengan harga beli yang berbeda, aplikasi menampilkan margin barunya
  dan menawarkan harga jual baru yang menjaga margin lama. Harga satuan besar dan harga grosir ikut berubah sebanding.
  Pembulatan ke atas: Rp50 di bawah Rp1.000, Rp100 di bawah Rp20.000, Rp500 di atasnya. Hanya pemilik, atau gudang yang diberi izin
  ubah harga jual, yang bisa menerapkannya.

## D11. Katalog barcode iPOS 5 (versi 2.15)

File iPOS 5 (50.601 baris) isinya barcode dan nama saja. Harga pokok, harga jual, stok, dan satuan semuanya 0 atau kosong, jadi
file itu tidak bisa mengisi Stok. Aplikasi memakainya sebagai **katalog barcode** yang terpisah dari Stok.

- **Bawaan APK.** Berkas `public/katalog-ipos5.tsv` (50.581 barang, 20 barcode kembar digabung) masuk ke aplikasi sendiri pada
  pemakaian pertama, sekitar 5 detik setelah layar siap. Tidak perlu impor manual.
- **Di kasir.** Scan barcode yang belum ada di Stok: kotak "Barang baru" terbuka dengan nama sudah terisi dan kursor di harga jual.
  Ketik harga lalu Enter, barang tersimpan dan masuk keranjang.
- **Barcode 12 digit dan 13 digit dianggap sama.** Katalog iPOS banyak berisi bentuk 12 digit (UPC), sedangkan scanner bisa membaca
  13 digit berawalan 0. Pencocokan mengabaikan angka 0 di depan, juga untuk barang yang sudah ada di Stok.
- **Tambah barang.** Mengetik 3 huruf nama memunculkan 5 saran dari katalog. Ketuk satu untuk mengisi nama dan barcode. Mengetik atau
  scan barcode juga mengisi nama.
- **Isi cepat (Stok, tombol petir).** Untuk memasukkan barang yang sudah ada di rak: scan, nama muncul, ketik harga jual, harga beli,
  dan stok dengan Enter di tiap kolom. Enter di kolom terakhir menyimpan dan kursor kembali ke kolom barcode. Barang yang sudah ada di
  Stok bisa diperbarui lewat jalur yang sama.
- **Memperbarui berkala.** Pengaturan, Katalog barcode, Perbarui dari file. Pilih file CSV: di Excel buka file iPOS terbaru, biarkan
  sheet pertama ("DATA ITEM 1 HARGA") yang aktif, Simpan Sebagai, jenis CSV. Aplikasi menampilkan pratinjau (berapa barang baru, berapa
  nama berubah), lalu Anda menerapkannya. Barang katalog tidak pernah dihapus, dan Stok serta harga jual tidak tersentuh.
  File .xls langsung ditolak dengan petunjuk, karena 23 MB terlalu berat dibuka di tablet.
- Katalog tersimpan per perangkat dan tidak ikut cadangan atau sinkron cloud (bisa diisi ulang dari file atau dari APK).

## D12. Catat stok bisa dimatikan, dan barang katalog langsung bisa dijual (versi 2.16)

- **Sakelar "Catat stok barang"** (Pengaturan, Kasir dan struk, bagian aturan penjualan; hanya pemilik). Mati: stok tidak berubah
  dan tidak pernah menolak penjualan; tampilan stok hilang dari kasir, daftar barang, form barang, Isi cepat, beranda, Analitik
  (stok diperkirakan habis dan barang tidak laku), dan laporan WhatsApp; menu Stok berganti nama menjadi Barang.
  Pembelian tetap mencatat harga beli dan hutang supplier. Angka stok lama tidak dihapus: bila dinyalakan lagi, angkanya tampil kembali
  tetapi tidak mengikuti penjualan selama mati.
- **Bawaan.** Mulai versi 2.17, stok mati untuk semua toko, termasuk yang sudah berjalan, sampai pemilik menyalakannya di sakelar
  tadi. Pilihan ini ikut tersinkron ke semua perangkat.
- **Barang katalog di kasir.** Mengetik 3 huruf atau lebih di kolom cari memunculkan barang katalog yang belum ada di Stok (maksimal 8,
  hanya bila hasil biasa sedikit). Ketuk, isi harga jual, Enter: barang tersimpan dan masuk keranjang. Hanya barang yang pernah
  dijual atau didaftarkan yang masuk ke daftar Barang, jadi daftar tidak penuh 50 ribu barang tanpa harga.
- **File CSV iPOS (titik koma)** bisa dipakai langsung di Pengaturan, Katalog barcode, Perbarui dari file.

## D13. Menentukan harga jual barang katalog (versi 2.18)

Katalog iPOS hanya berisi barcode dan nama, jadi harga jual ditentukan di aplikasi. Tiga jalan, boleh dipakai bersamaan:
1. **Saat pertama kali dijual.** Scan atau cari barangnya di kasir, isi harga jual satu kali, Enter. Barang itu sudah punya harga seterusnya.
2. **Isi cepat** (tombol petir di menu Barang): scan barang di rak, isi harga jual dan harga beli dengan Enter. Cocok untuk barang yang laris.
3. **Sekaligus lewat Excel.** Buka CSV iPOS di Excel, hapus baris barang yang tidak Anda jual, isi kolom HARGA JUAL (dan HARGA POKOK bila
   ada), Simpan Sebagai CSV, lalu Impor CSV di menu Barang. Baris tanpa harga jual dilewati.

## D14. Keyboard untuk kasir (versi 2.21)

Keyboard fisik (USB atau Bluetooth) bisa dipakai di layar Kasir. Tekan **F1** atau tombol bergambar keyboard untuk daftar pintasan.
Yang paling sering: ketik kode lalu Enter (tambah barang), `12` lalu `*` (jumlah barang berikutnya), Enter (bayar), Enter lagi (uang pas),
F4 bayar, F6 diskon, F8 tahan, F9 antrian. Scanner tetap bekerja seperti biasa.

## D15. Laci uang dan printer Bluetooth (versi 2.22)

Untuk printer Bluetooth dengan port laci (misalnya Iware XH-58PRO) dan laci RJ11 (misalnya Iware CD-339).

**Menyiapkan**

1. Colok kabel RJ11 laci ke port laci di belakang printer. Pasangkan printer di Pengaturan Bluetooth tablet.
2. Di aplikasi: Pengaturan, Kasir dan struk. Pilih **Langsung ke printer**, lalu **Pilih printer**.
3. Tekan **Tes sambungan**. Harus muncul "Tersambung".
4. Nyalakan **Laci uang tersambung ke printer**, lalu tekan **Tes buka laci**.
   Bila laci tidak terbuka, ganti **Jalur perintah laci** ke Pin 5 atau Keduanya dan tes lagi.
5. Tekan **Simpan**.

**Kapan laci terbuka**

- Setiap pembayaran tunai, walau struknya tidak dicetak.
- Pembayaran kasbon tunai, retur dan batal struk tunai, kas masuk dan kas keluar (bisa dimatikan).
- Tombol **Buka laci untuk menghitung** di layar buka shift dan tutup shift.
- Tombol **Buka laci** di atas keranjang (atau F5). Kasir wajib memilih alasan, dan pembukaan ini dicatat.

**Pengawasan**

- Analitik, kartu "Barang dihapus dan keranjang dibatalkan": jumlah laci dibuka tanpa penjualan per kasir, dan rincian per hari
  berisi jam, kasir, dan alasannya.
- Izin per akun kasir: Pengaturan, Akun, "Boleh buka laci tanpa penjualan".

**Printer dipakai bersama aplikasi lain**

Bila Mitra Bukalapak (atau aplikasi lain di tablet yang sama) mencetak ke printer yang sama, nyalakan
**Printer dipakai bersama aplikasi lain**. Aplikasi kasir melepas printer sesudah tiap cetakan. Tanpa ini, aplikasi kasir menahan
sambungan dan aplikasi lain bisa gagal mencetak.

**Aplikasi top up**: pilih Mitra Bukalapak atau Mitra Shopee di Pengaturan, Kasir dan struk. Tombolnya ada di Beranda.

## D16. Kasir lebih cepat (versi 2.23)

- **Uang pembeli**: di bawah Total ada tombol nominal (misalnya 20.000, 50.000, 100.000). Sekali ketuk, transaksi tunai selesai
  dan kembalian tampil besar.
- **Layar berhasil tertutup sendiri** setelah 3 detik bila tidak ada kembalian (uang pas, QRIS). Bila ada kembalian, layar tetap
  terbuka. Atur di Pengaturan, Perangkat.
- **Ulangi belanja**: pilih pelanggan saat keranjang kosong, lalu ketuk "Ulangi belanja ini". Dari Riwayat juga bisa lewat tombol
  "Belanja lagi". Harga memakai harga sekarang.
- **Ctrl+Z** membatalkan barang yang terakhir ditambahkan (salah scan atau scan dobel).
- **Kolom cari**: panah atas/bawah memilih barang, Enter menambahkannya.

## D17. Stok bertahap, PDA, keyboard dan mouse, beberapa kasir (versi 2.24)

**Mulai mencatat stok di toko yang barangnya sudah banyak**

1. Pengaturan, Kasir dan struk, nyalakan **Catat stok barang**, lalu pilih **Hitung bertahap**.
2. Semua barang berstatus "belum dihitung". Barang ini tetap bisa dijual tanpa batas dan tidak memicu peringatan stok.
3. Hitung pelan-pelan lewat Stok, **Hitung stok**: scan barang, ketik jumlahnya, Enter. Barang yang sama di beberapa rak
   dijumlahkan selama layar itu terbuka. Progresnya tampil di layar Stok.
4. Mode **Barang masuk** di layar yang sama menambah stok saat barang datang. Barcode yang belum terdaftar bisa langsung
   didaftarkan (nama terisi dari katalog bila ada).

**PDA Android scanner**

- Pasang APK yang sama di PDA, masuk dengan akun Gudang atau Pemilik, sambungkan ke cloud yang sama.
- Atur scanner PDA ke keluaran **keyboard / keystroke** (paling mudah). Lalu di aplikasi: Pengaturan, Perangkat,
  Scanner PDA, pilih **Seperti keyboard**, dan coba scan di kotak "Coba scan".
- Bila PDA hanya bisa mengirim **broadcast/intent**, pilih **Broadcast**, pilih mereknya (Zebra, Urovo, iData, Sunmi, Newland)
  atau isi nama action dan extra sendiri, lalu **Simpan dan nyalakan**. Cocokkan dengan setelan scanner di PDA.

**Keyboard dan mouse**: Pengaturan, Perangkat, nyalakan **Mode keyboard dan mouse**. Klik kanan barang untuk mengetik jumlahnya,
klik kanan baris keranjang untuk mengubah jumlah, ketik huruf untuk langsung mencari. Di layar sentuh, tahan lama barang juga
membuka dialog jumlah. Pintasan lengkap: F1 di layar Kasir.

**Beberapa kasir bersamaan**

- Tiap perangkat kasir punya shift, modal awal, laci, dan huruf nomor struk sendiri. Stok dan omzet tetap tergabung lewat cloud.
- Beri huruf struk yang berbeda untuk tiap perangkat (Pengaturan, Perangkat). Bila sama, layar buka shift menawarkan huruf lain.
- Pemilik melihat semua kasir yang sedang buka, omzet, dan isi laci seharusnya di Beranda.

## D18. Layar pelanggan baru dan QRIS di layar (versi 2.25)

Dirancang untuk mesin kasir dua layar seperti **Iware PXA-02D** (layar kasir 15,6 inci, layar pelanggan 11 inci, Android 11).

- **Kiri**: nama toko dan ucapan, tanggal dan jam, nama kasir, tabel Nama Barang, Harga, Qty, Hemat, Total (barang terbaru
  disorot), lalu kotak **Hemat** (selisih harga grosir atau harga per dus ditambah diskon) dan **Total**.
- **Kanan**: gambar promosi. Saat kasir memilih **QRIS** di layar Bayar, QRIS toko tampil besar dengan nominalnya.
  Saat tunai, tampil uang diterima dan kembalian. Sesudah bayar, tampil Terima kasih dan kembalian.
- **Bawah kanan**: tulisan metode pembayaran yang diterima (bisa diubah).

**Menyiapkan di PXA-02D**

1. Pasang APK di mesin, buka Pengaturan, Perangkat, nyalakan **Aktifkan layar pelanggan**.
2. Pastikan tanda **Layar kedua terdeteksi** muncul. Bila tidak, layar 11 inci belum dikenali sebagai layar kedua oleh Android
   mesin itu; hubungi penjual (Iware) soal pengaturan layar kedua.
3. Tekan **Kirim contoh** dan **Kirim contoh bayar QRIS** untuk melihat hasilnya.

**QRIS di layar**

1. Di Pengaturan, Perangkat, tekan **Unggah gambar QRIS** dan pilih gambar QR toko Anda (misalnya hasil unduh dari aplikasi
   merchant). Gambar ditampilkan apa adanya, tidak diubah.
2. Saat kasir memilih QRIS di layar Bayar, gambar itu tampil besar dengan nominal belanja di bawahnya. Pelanggan scan,
   lalu mengetik nominalnya.
3. Tetap cek dana masuk (speaker QRIS / aplikasi merchant) sebelum menekan Selesai.

## D19. Menu PDA (versi 2.26)

**Menyiapkan PDA**

1. Pasang APK yang sama di PDA dan sambungkan ke cloud toko.
2. Masuk dengan akun **Inventory Admin** (dulu Gudang). Akun ini **selalu langsung membuka menu PDA**, di perangkat mana pun,
   tanpa perlu setelan apa pun.
3. Bila scanner PDA mengirim lewat broadcast (bukan seperti keyboard), atur di Pengaturan, Perangkat, **Scanner PDA**,
   lalu coba scan di kotak "Coba scan".
4. Setelan **Perangkat ini adalah PDA** hanya perlu bila PDA dipakai dengan akun Owner atau Cashier.

**Isi menu PDA**

- **Hitung stok** dan **Barang masuk**: scan, ketik jumlah, Enter. Keyboard layar tidak muncul saat scan.
  - **Tiap scan = 1**: tidak perlu mengetik, setiap scan menambah 1. Cocok untuk barang yang sedikit per rak.
  - **Rak / area**: tulis lokasinya (misalnya "Rak A1"), ikut tercatat di riwayat stok dan CSV.
  - **Batal**: membatalkan entri terakhir, termasuk mengembalikan stok dan status "belum dihitung".
  - Hitungan yang jauh berbeda dari catatan sebelumnya diberi tanda **selisih**, supaya dihitung ulang.
  - **CSV**: unduh hasil sesi untuk dicek pemilik.
  - Barcode belum terdaftar: akun tanpa izin harga mencatat nama dan jumlahnya; barang disimpan **menunggu harga**.
- **Cek harga**: scan untuk melihat harga per satuan, harga per dus, harga grosir, dan stok.
- **Isi harga** (pemilik atau gudang dengan izin harga): sama dengan Isi cepat.
- **Menunggu harga** (pemilik): isi harga barang yang dicatat dari PDA, lalu barang langsung aktif dijual.
  Pengingatnya juga muncul di layar Stok.

## D20. Tombol scan PDA, satuan kemasan, dan penerimaan barang (versi 2.27)

**Tombol scan di badan PDA**

- Di menu PDA, tekan tombol scan: Cek harga langsung terbuka untuk barang itu.
- Di Hitung stok dan Barang masuk, tombol scan tetap bekerja walau kursor tidak di kolom barcode (misalnya sesudah mengetuk
  tombol), dan scan yang tertembak saat kursor di kolom jumlah atau rak dianggap barang berikutnya.

**Satuan dan kemasan (pcs, pack, renteng, dus, karton, slop, sak, ...)**

- Barcode baru, pilihan **Barang baru**: pilih satuan barcode itu (ketuk pilihan), isi harga, lalu **Tambah satuan besar**
  untuk pack, renteng, dus beserta isi dan harganya.
- Barcode baru, pilihan **Kemasan barang yang ada**: cari barangnya, pilih kemasannya (misalnya dus), isi berapa satuan kecil,
  simpan. Barcode dus itu langsung dikenali di kasir dan di PDA.
- Barang bersatuan banyak dihitung **campuran**: isi jumlah karton, dus, pack, dan pcs sekaligus; aplikasi menjumlahkan
  ke satuan terkecil.
- Form barang di tablet juga punya pilihan satuan yang sama.

**Penerimaan barang (Barang masuk)**

- Isi jumlah per kemasan, **harga beli** per kemasan (memperbarui modal rata-rata), dan **tanggal kedaluwarsa**.
- Semua entri bisa dibatalkan satu per satu (tombol Batal) dan diunduh sebagai CSV.

## D21. PDA sebagai scanner kasir untuk barang besar (versi 2.28)

Untuk barang yang berat atau besar (beras karung, minyak dus, galon, gas) yang susah dibawa ke meja kasir: barang di-scan
dengan PDA di tempatnya, lalu langsung masuk ke keranjang kasir yang dipilih.

**Syarat**

- PDA dan tablet kasir **tersambung ke Cloud yang sama** dan online. Scan dikirim lewat internet, bukan Bluetooth.
- Tablet kasir sudah **membuka shift**. Yang bisa dipilih hanya kasir dengan shift terbuka di perangkat lain.

**Di PDA**

1. Menu PDA, ketuk **Scan untuk kasir**.
2. Pilih kasir tujuan (Kasir A, Kasir B, ...). Kalau hanya satu kasir yang buka, langsung terpilih. Pilihan diingat.
3. Atur **Jumlah scan berikut** bila perlu (misalnya 5 karung), lalu tekan tombol scan di barang.
4. PDA berbunyi dan menampilkan **Masuk keranjang** setelah kasir menerima. Barcode yang tidak terdaftar tidak dikirim.
5. Salah scan: tombol **Batal** di atas mengurangi barang terakhir dari keranjang kasir.
6. Di bawah ada daftar yang sudah dikirim dan perkiraan totalnya, untuk diberitahukan ke pembeli.

**Di tablet kasir**

- Selama PDA tersambung, muncul tanda biru **PDA (nama)** di atas. Barang dari PDA masuk keranjang dengan label **PDA nama**.
- Kalau kasir sedang di layar **Bayar** atau memilih jumlah, barang dari PDA **menunggu** (tanda "1 menunggu") dan masuk
  setelah layar itu ditutup, supaya total yang sedang dibayar tidak berubah diam-diam.
- Stok tetap dicek di kasir. Kalau stok kurang, PDA menerima pesan ditolak.

**Kecepatan dan kuota**

- Kasir hanya mengecek cepat (tiap 1,5 detik) selama ada PDA yang tersambung, dan berhenti sendiri setelah layar
  Scan untuk kasir ditutup, atau bila PDA tidak dipakai lebih dari 10 menit. Tanpa PDA tidak ada tambahan pemakaian kuota Firebase.
- Barang pertama biasanya sampai dalam beberapa detik setelah kasir dipilih; berikutnya sekitar 1 sampai 2 detik.
- Scan yang tertahan lebih dari 15 menit (misalnya tablet kasir mati) diabaikan, supaya tidak masuk ke pembeli lain.

## D22. Perbaikan tampilan dan kecepatan (versi 2.29)

- **Masuk lebih cepat:** PIN 6 angka langsung masuk tanpa menekan tombol Masuk. Dengan keyboard fisik, PIN bisa diketik.
- **Buka shift:** di tablet mendatar, angka modal di kiri dan pengingat serta tombol Mulai di kanan, jadi tidak perlu
  menggulir. Keyboard: ketik modal lalu Enter. Tutup shift juga bisa diketik dengan keyboard.
- **Bayar:** tunai tanpa mengetik nominal berarti uang pas. Tombolnya langsung bertuliskan "Tunai pas · Bayar Rp...".
  Kalau nominal kurang, tombol menunjukkan kekurangannya.
- **QRIS di tablet kasir:** gambar QRIS yang diunggah (Pengaturan, Perangkat) tampil di layar Bayar saat memilih QRIS,
  jadi pembeli bisa scan langsung dari tablet walau tanpa layar pelanggan.
- **Form barang:** form Tambah/Ubah barang sebelumnya melebar keluar layar (kolom kanan dan pilihan Curah tidak terlihat).
  Sudah diperbaiki; pilihan satuan sekarang tersusun rapi.
- **Menu Stok di HP/PDA:** tombol tanpa nama diganti satu tombol **Lainnya** berisi menu berlabel dan penjelasan.
- Kolom cari di kasir lebih lebar, dan Beranda menampilkan keterangan bila belum ada penjualan.

## D23. Pembagian akun dan menu Top-up dengan baca struk otomatis (versi 2.30)

**Empat jenis akun** (Pengaturan, Akun, Tambah akun):

| Akun | Isi | Layar pertama |
|---|---|---|
| Owner | semua menu dan izin | Beranda |
| Cashier | menjual barang, Top-up (bisa dimatikan per akun) | Kasir |
| Inventory Admin (dulu "Gudang") | menu PDA: hitung stok, barang masuk, cek harga, scan untuk kasir | PDA |
| Top-up Officer | hanya menu Top-up | Top-up |

Nama jabatan sengaja berbahasa Inggris (tampil di layar masuk dan daftar akun); menu aplikasi tetap berbahasa Indonesia.
Cashier dan Top-up Officer membuka shift sendiri (modal laci) dan menutupnya dengan hitung laci.

**Mencatat top-up dan PPOB**

1. Lakukan transaksi seperti biasa di Mitra Bukalapak.
2. Ambil tangkapan layar halaman detail transaksi atau struk, lalu di menu Top-up tekan **Baca struk (gambar)**.
   Boleh memilih beberapa gambar sekaligus. Struk kertas: **Foto struk**.
3. Aplikasi membaca jenis, nomor tujuan, nominal, admin, total, nomor referensi, token listrik, dan status. Pembacaan
   berjalan di perangkat ini, tanpa internet, sekitar 1 sampai 2 detik per struk.
4. Cocokkan angkanya dengan gambar di sebelahnya, pilih Tunai/QRIS/Transfer, lalu **Simpan**.
5. Struk yang sudah pernah dicatat (nomor referensi sama) diberi peringatan merah supaya tidak tercatat dua kali.

**Uang di laci:** pembayaran tunai menambah laci, tarik tunai mengurangi laci (uang diberikan ke pembeli) dan biaya
adminnya menambah. Semua ini ikut di "Seharusnya di laci" saat tutup shift. Bila laci tersambung ke printer, laci
terbuka sendiri saat catatan tunai disimpan.

**Untung:** isi "Modal / saldo terpotong" (lihat riwayat di aplikasi Mitra) atau langsung isi "Untung". Pemilik bisa
mengatur **Untung bawaan per jenis** (misalnya pulsa Rp2.000) supaya terisi otomatis bila struk tidak memuat modal.

**Saldo deposit:** tekan **Isi saldo awal** dan ketik saldo yang tampil di aplikasi Mitra. Setelah itu aplikasi
menghitung perkiraan saldo (dikurangi modal tiap transaksi, ditambah isi saldo dan tarik tunai). Tekan **Cocokkan saldo**
kapan saja, misalnya saat ganti shift; selisihnya tercatat dan bisa dilihat pemilik. Isi saldo deposit hanya oleh pemilik.

**Keamanan:** catatan yang sudah disimpan hanya bisa diubah atau dibatalkan oleh Owner (atau Top-up Officer yang diberi izin
"Boleh ubah dan batalkan catatan top-up"). Yang dibatalkan tetap terlihat dengan tanda Dibatalkan.

**Laporan:** Beranda, Laporan (kartu Top-up dan PPOB per jenis), laporan WhatsApp, dan tutup shift menampilkan jumlah
transaksi, uang dari pembeli, untung, dan pengaruh ke laci. Angka ini terpisah dari omzet dan laba penjualan barang.

**Catatan:** contoh struk yang dipakai untuk menguji pembaca masih buatan sendiri. Bila struk Mitra Bukalapak asli
terbaca kurang tepat, kirim satu atau dua tangkapan layar struk asli untuk menyesuaikan pembacanya.

## D24. Hitung buta saat tutup shift (versi 2.32)

- Saat Cashier atau Top-up Officer menutup shift, angka "Seharusnya di laci" beserta rinciannya **tidak ditampilkan**
  sebelum uang dihitung dan shift ditutup. Petugas hanya melihat modal awal dan mengetik hasil hitungnya.
- Setelah ditutup, hasil (pas, lebih, kurang), angka seharusnya, dan ringkasan shift tampil seperti biasa, termasuk
  jumlah top-up dan pengaruhnya ke laci.
- Owner tetap melihat semua angka saat menutup shift.

## D25. Cetak label harga ke printer thermal 58 mm (versi 2.33)

Label harga rak dicetak ke printer yang sama dengan struk (Iware XH-58PRO, kertas 58 mm, lebar cetak 48 mm). Cara cetaknya mengikuti setelan struk: langsung ke printer, lewat RawBT, atau dialog cetak.

- **Membuka**: menu Barang, tombol Label harga (di layar kecil ada di menu Lainnya). Bisa juga dari menu PDA (kotak Label harga), dari Cek harga (tombol Cetak label), atau dengan memilih beberapa barang lalu Cetak label.
- **Memilih barang**: scan barcode barang di rak, cari namanya, atau ketuk Harga berubah dan Belum pernah dicetak. Setiap barang bisa dicetak lebih dari satu lembar. Barang yang punya satuan dus bisa dicetak sebagai label eceran atau label per dus.
- **Isi label**: nama toko, tanggal harga, nama barang, harga besar dengan satuannya, harga grosir dan harga per dus, serta barcode. Semua bisa dinyalakan atau dimatikan.
- **Ukuran**: Kecil 30 mm, Rak 40 mm, dan Besar 50 mm, semua selebar kertas 58 mm.
- **Kertas**: Kertas struk biasa dicetak berurutan dengan garis potong. Stiker label thermal 58 mm juga bisa, dengan pengaturan celah dan koreksi supaya cetakan pas di stiker. Printer struk biasa tidak membaca celah stiker, jadi coba 3 sampai 5 label dulu.
- **Harga berubah**: aplikasi mengingat harga saat label dicetak. Bila harga, nama, satuan, atau barcode berubah sesudahnya, menu Barang menampilkan pita "... barang berubah harga sejak labelnya dicetak". Ketuk pitanya untuk langsung mencetak label pengganti.
- **Label dus**: label per dus hanya memakai barcode dus itu sendiri. Bila dus belum punya barcode, labelnya dicetak tanpa barcode, supaya scan di kasir tidak salah terbaca sebagai harga eceran.
- **Bila hasil cetak rusak**: nyalakan Kirim pelan. Bila masih acak, pilih cara cetak Teks (printer lama), yang memakai huruf dan barcode bawaan printer.
- **Izin akun**: Owner selalu bisa. Inventory Admin bisa secara bawaan. Cashier hanya bila izin "Boleh cetak label harga" dinyalakan pemilik di Pengaturan, Akun.

Catatan: fitur ini belum dicoba di printer sungguhan. Hasil cetak di atas dicek lewat simulasi data yang dikirim ke printer.

## D26. Tampilan HP dan tablet, serta bagian Printer dan struk (versi 2.34)

- **iPhone dan HP layar penuh**: kepala layar, menu bawah, dialog, dan pesan sudah memperhitungkan poni atau Dynamic Island dan garis home di bawah layar. Tombol menu bawah tidak lagi terjepit, dan tombol di bagian bawah dialog (Simpan, Cetak, Bayar) tidak lagi tertutup bilah browser.
- **Ukuran tombol**: semua tombol minimal 44 piksel, ukuran sentuh yang disarankan Apple dan Google. Tombol kecil yang dulu susah dipencet (hapus kategori, tambah dan kurang jumlah, tombol hari di Top-up) sudah diperbesar.
- **Kolom isian tidak membuat layar membesar sendiri** di iPhone saat diketuk.
- **HP dimiringkan dan tablet pendek**: menu tetap di samping, kepala layar dan dialog dibuat ringkas, dan keranjang kasir disederhanakan supaya tombol Bayar selalu terlihat. Pelanggan kasbon dipilih lewat ikon orang di kepala keranjang.
- **Keranjang di HP**: harga total tiap barang ditulis di bawah namanya, dan ada tombol tutup (X).
- **Pengaturan di HP**: semua bagian tampil sebagai kotak dua kolom, tidak perlu digeser ke samping.
- **Printer dan struk sekarang bagian tersendiri** di Pengaturan, dibagi menjadi Printer, Tampilan struk, Cetak otomatis dan laci uang, serta Label harga. Perubahannya tersimpan otomatis, tanpa tombol Simpan. Bagian **Aturan kasir** berisi aplikasi top-up, catat stok, aturan retur, dan pengingat shift.
- Petunjuk lama di panduan ini yang menyebut "Pengaturan, Kasir dan struk" sekarang ada di **Printer dan struk** (printer, struk, laci) atau **Aturan kasir** (stok, retur, aplikasi top-up).

## D27. Struk tarik tunai (versi 2.35)

- **Membuka**: menu Top-up, tombol **Cetak struk tarik tunai** (di bawah tombol Baca struk). Bisa dipakai pemilik, kasir yang boleh top-up, dan Top-up Officer.
- **Isi struk**: ketik nominal sendiri (atau ketuk 50 rb sampai 1 jt), biaya admin bila ada, lalu nama pelanggan dan keterangan bila perlu (misalnya bank pengirim atau nomor referensi). Tulisan layanan bisa diganti: Tarik Tunai, Tarik Tunai QRIS, Setor Tunai, atau ketik sendiri.
- **Biaya admin**: bawaannya ditambahkan (pelanggan membayar nominal + admin, menerima nominal). Nyalakan **Admin dipotong dari uang tunai** bila pelanggan menerima nominal dikurangi admin. Angka besar di struk selalu uang tunai yang diterima pelanggan.
- **Jam sampai detik**: jam di layar berjalan setiap detik. Jam yang tercetak adalah saat tombol Cetak ditekan, lengkap dengan WIB. Nomor struk berurutan per hari, misalnya TT-101126-001.
- **2 lembar**: pilih 2 untuk lembar pelanggan dan lembar toko (bertulisan SALINAN TOKO).
- **Struk terakhir**: 30 struk terakhir di perangkat itu bisa dicetak ulang. Cetak ulang memakai jam aslinya dan diberi tulisan Cetak ulang.
- **Mengatur tampilan**: Pengaturan, Printer dan struk, bagian **Struk tarik tunai** (atau ikon roda gigi di layar struk, khusus pemilik). Bisa mengubah tulisan di atas layanan, layanan bawaan, baris tambahan di bawah nama toko (misalnya "Agen resmi Mitra Bukalapak"), tulisan di atas angka besar, pesan di bawah struk, serta menampilkan atau menyembunyikan alamat, nama petugas, tulisan TRANSAKSI BERHASIL, dan kolom tanda tangan.
- Struk ini hanya bukti untuk pelanggan dan **tidak mengubah catatan uang**. Transaksinya tetap dicatat di Top-up (Baca struk atau Catat manual) supaya laci dan saldo cocok.

## E. Mencoba di komputer (opsional)

    npm install
    npm run dev
