# WargaHub Praktikum 04

UX, RecyclerView, Fragment, dan navigasi.

```text
Nama        : Noor Azkia Salsabila
NIM         : 240104040183
Kelas       : TI24B
Mata kuliah : Pemrograman Mobile
Dosen       : Muhayat, M.IT
```

## Ringkasan aplikasi

WargaHubP04 menampilkan 15 laporan lingkungan fiktif melalui satu Activity dan tiga Fragment: Beranda, Daftar Laporan, serta Rincian Laporan. Daftar menggunakan RecyclerView, ListAdapter, dan DiffUtil. Navigation Component mengirim ID Long untuk menampilkan rincian yang sesuai. Kondisi daftar kosong memiliki petunjuk serta tombol pemulihan; ID yang tidak tersedia menghasilkan pesan aman.

## Konfigurasi source saat ini

- Root Android Studio: WargaHubP04.
- Namespace dan application ID: id.antasari.p04.wargahub.
- Bahasa dan UI: Kotlin, XML Views, dan ViewBinding.
- Minimum SDK: API 26.
- Target SDK: API 36.
- Compile SDK: API 37.
- Target Java: 11.
- Android Gradle Plugin pada source saat diperiksa: 9.5.1.
- Gradle wrapper: 9.4.1.
- RecyclerView: 1.4.0.
- Fragment KTX: 1.8.9.
- Navigation Fragment KTX dan Navigation UI KTX: 2.9.5.

Laporan pengujian sumber mencatat AGP 9.2.1. Perbedaan ini dicatat tanpa mengubah konfigurasi source. Proyek menggunakan dukungan Kotlin bawaan AGP. Perangkat pengujian sumber adalah emulator Pixel 7, Android 17/API 37, APK debug versi 1.0. Variasi kondisi mencakup portrait, landscape, font 1,0x sampai 1,5x, layar 360 x 640dp, serta TalkBack.

## Cara membuka dan menjalankan

1. Ekstrak ZIP, kemudian buka folder WargaHubP04 di Android Studio.
2. Tunggu Gradle Sync dan siapkan SDK sesuai konfigurasi proyek.
3. Pilih emulator atau perangkat Android yang memenuhi minSdk, lalu jalankan app.
4. Tekan Lihat Daftar Laporan, gulir daftar, dan pilih satu laporan.
5. Cocokkan judul, kategori, status, dan deskripsi dengan laporan yang dipilih.
6. Gunakan Kembali ke Daftar, Up toolbar, atau Back sistem untuk memeriksa alur kembali.
7. Gunakan Uji Daftar Kosong, lalu Tampilkan Data Contoh untuk memulihkan daftar.

## Struktur dan tanggung jawab

| Lokasi atau komponen | Peran |
| --- | --- |
| WargaHubP04/MainActivity dan activity_main.xml | Wadah NavHostFragment, Toolbar, NavController, dan insets. |
| HomeFragment | Beranda dan action_home_to_list. |
| ListFragment | RecyclerView, mode kosong, pemulihan data, dan pengiriman ID. |
| DetailFragment | Pembacaan laporan_id, rincian, kondisi tidak ditemukan, dan navigateUp. |
| Laporan dan LaporanContoh | Model laporan serta 15 data fiktif di memori. |
| LaporanAdapter | ViewHolder, binding item, DiffUtil, dan contentDescription baris. |
| res/navigation/nav_graph.xml | Tiga tujuan, dua action, dan argumen laporan_id bertipe Long. |
| res/layout-land/fragment_list.xml | Variasi layout daftar untuk ruang landscape yang lebih lega. |
| docs | Laporan, sketsa, ringkasan validasi, dan arsip log pengujian sumber. |
| screenshots | Dokumentasi asli pengujian yang disertakan dalam paket sumber. |

ViewBinding Fragment dibuat ketika View tersedia dan dilepas pada onDestroyView. ListFragment juga melepas adapter. Pemeriksaan currentDestination mencegah navigasi ganda saat ketukan cepat. Navigasi kembali menggunakan back stack, bukan sengaja membuat daftar baru. Flag contohKosong disimpan dalam savedInstanceState.

## Hasil pengujian T01 sampai T16

Hasil berikut mengikuti laporan sumber. Penyesuaian identitas tidak disertai pengujian runtime baru. T13 ditulis Sebagian untuk menegaskan bahwa pembacaan dan aktivasi berhasil, sedangkan gulir TalkBack belum berhasil pada emulator.

| ID | Skenario | Hasil aktual | Status | Bukti pada folder screenshots |
| --- | --- | --- | --- | --- |
| T01 | Beranda | Beranda tunggal memuat judul, pengantar, catatan simulasi, dan tombol daftar. | Lulus | 01_beranda.png |
| T02 | Daftar | Indikator 15 laporan contoh dan baris judul, kategori, serta status Simulasi tampil. | Lulus | 02_daftar.png |
| T03 | Gulir | Daftar dapat digulir sampai zona 15 dan item terakhir dapat dipilih. | Lulus | 23_daftar_zona_15.png |
| T04 | Rincian | Pilihan zona 1, 10, dan 15 menampilkan rincian yang sesuai ID masing-masing. | Lulus | 03, 04, dan 24 |
| T05 | Tombol kembali | Kembali ke Daftar memanggil navigateUp dan kembali tanpa layar daftar baru. | Lulus | 02_daftar.png |
| T06 | Up toolbar | Panah Up memindahkan Rincian ke Daftar, kemudian ke Beranda. | Lulus | 02 dan 01 |
| T07 | Back sistem | Back mengikuti Rincian, Daftar, Beranda, lalu launcher tanpa crash. | Lulus | 12_back_dari_beranda.png |
| T08 | Mode kosong | Jumlah berubah menjadi 0; daftar disembunyikan dan pesan serta tombol pemulihan tampil. | Lulus | 07_kosong.png |
| T09 | Pulihkan data | Tampilkan Data Contoh mengembalikan indikator serta seluruh 15 laporan. | Lulus | 26_pulihkan_akhir.png |
| T10 | Rotasi rincian | Toolbar dan data rincian tetap sesuai ID terpilih setelah rotasi. | Lulus | 05_rotasi_rincian.png |
| T11 | Rotasi mode kosong | Mode 0 laporan dan tombol Tampilkan Data Contoh bertahan setelah rotasi. | Lulus | 06 dan 25 |
| T12 | Font dan layar kecil | Tiga layar tetap terbaca dan dapat digulir pada landscape, font 1,3x sampai 1,5x, serta 360 x 640dp. | Lulus | 08-10 dan 14-19 |
| T13 | TalkBack | Pembacaan judul, kategori, status, serta Buka rincian dikonfirmasi penguji. Aktivasi baris dan kembali berhasil; gulir belum berhasil pada emulator. | Sebagian | 21, 22; konfirmasi manual |
| T14 | Ketukan cepat | Enam ketukan berulang tidak menyebabkan crash atau duplikasi layar. | Lulus | 13_ketukan_cepat_rincian.png |
| T15 | Mulai ulang | Setelah force-stop, daftar 15 contoh dibentuk kembali saat aplikasi dibuka; bukan bukti database. | Lulus | 01 dan 02 |
| T16 | ID salah | Versi uji -99L menampilkan pesan aman dan tombol kembali berfungsi. Source akhir kembali mengirim laporan.id. | Lulus | 11; log uji ID salah |

## Uji usability dan tindak lanjut

Rekan penguji usability adalah Hafidzatun Aulia Safitri (240104040184). Tugasnya menemukan rincian laporan zona latihan 10, kemudian kembali ke daftar. Waktu yang dicatat adalah 7,3 detik sejak Beranda siap sampai rincian zona 10 terbuka. Perjalanan kembali tidak termasuk dalam angka waktu tersebut. Penguji belum terbiasa menggunakan emulator.

Ketidakbiasaan memakai emulator merupakan konteks utama yang dicatat. Penyesuaian gerakan klik-tahan dan geser, penempatan kursor pada baris yang tepat, serta pembacaan label zona merupakan faktor lain yang mungkin memengaruhi waktu. Faktor tambahan ini merupakan kemungkinan penjelasan, bukan pengamatan baru yang sudah diukur. Tidak tersedia pengukuran durasi per langkah.

Pada landscape 360 x 640dp dengan font 1,5x, ruang daftar awal pendek sehingga status baris pertama tidak langsung terlihat. Variasi layout-land menempatkan jumlah dan tombol berdampingan agar baris pertama lebih lengkap. Bukti sebelum dan sesudah ada pada screenshot 15 dan 16. Tidak tersedia waktu sebelum perbaikan dengan prosedur dan penguji yang sama, sehingga tidak disimpulkan ada peningkatan kecepatan dari waktu 7,3 detik tersebut.

Pengujian lanjutan dapat menyediakan pengenalan emulator lebih dahulu, menggunakan titik awal/akhir yang konsisten, dan memisahkan waktu mencari item dari waktu membuka rincian.

TalkBack merupakan pengujian teknis pada dokumentasi sumber: pembacaan informasi, klik dua kali, dan kembali dilaporkan berhasil, sedangkan gulir saat TalkBack aktif belum berhasil pada emulator. Hasil suara berasal dari konfirmasi manual sumber, bukan screenshot atau pengukuran waktu tugas rekan.

## Batas data simulasi

Seluruh 15 laporan dibentuk di memori oleh LaporanContoh. Munculnya kembali data setelah force-stop berasal dari inisialisasi kode, bukan penyimpanan database. P04 tidak menyediakan CRUD atau pengiriman laporan ke server. Source akhir yang diperiksa mengirim laporan.id; -99L hanya digunakan pada versi eksperimen yang didokumentasikan.

## Identitas dan arsip pengujian

Identitas penyusun pada README, dokumen validasi, sketsa SVG, dan laporan PDF telah disesuaikan ke Noor Azkia Salsabila. Tidak ada identitas mahasiswa pada resource aplikasi P04 yang perlu diganti. Source Kotlin, XML aplikasi, dan konfigurasi build dipertahankan.

Identitas dan waktu uji rekan telah diperbarui menjadi Hafidzatun Aulia Safitri (240104040184), 7,3 detik, dengan konteks belum terbiasa memakai emulator. Data pengujian teknis lainnya tetap mengikuti dokumentasi sumber. Log build/lint/ADB serta hasil_uji_akhir.json merupakan arsip asli pengujian sebelum penyesuaian identitas; jalur komputer lama dan hash APK di dalam arsip tetap mengikuti sumber. Tidak ada build atau pengujian runtime baru pada salinan ini.

## Pengumpulan

Paket berisi README, docs/Laporan_P04.pdf, docs/HASIL_VALIDASI.md, docs/SKETSA_ALUR.svg, arsip log, screenshots, serta source WargaHubP04 dengan Gradle wrapper. Cache, output build, local.properties, dan salinan Word laporan lama tidak disertakan. Laporan PDF yang sama juga disediakan terpisah sebagai Laporan_P04_240104040183.pdf.
