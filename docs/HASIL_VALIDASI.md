# Hasil Validasi Praktikum 04

```text
Nama        : Noor Azkia Salsabila
NIM         : 240104040183
Kelas       : TI24B
Mata kuliah : Pemrograman Mobile
Dosen       : Muhayat, M.IT
```

Proyek: WargaHubP04, namespace id.antasari.p04.wargahub.

Rekap berikut mempertahankan hasil pengujian sumber pada 7 sampai 9 November 2026. Perubahan identitas penyusun tidak disertai pengujian runtime baru. Catatan uji tugas rekan diperbarui untuk Hafidzatun Aulia Safitri (240104040184); waktu 7,3 detik dan konteks belum terbiasa menggunakan emulator dicatat terpisah dari rekap teknis sumber. Lingkungan sumber: Pixel 7, Android 17/API 37, portrait/landscape, font 1,0x sampai 1,5x, layar 360 x 640dp, dan TalkBack.

## 1. Ringkasan Build & Pemeriksaan Kode

- Proyek dibuka di Android Studio dan **Gradle Sync** berhasil tanpa kesalahan.
- Eksekusi perintah `.\gradlew.bat assembleDebug lintDebug` menghasilkan **BUILD SUCCESSFUL** dengan **0 error**.
- Seluruh komponen inti tersedia dan sesuai dengan Modul Praktikum 04:
  - **7 File Kotlin**: `MainActivity.kt`, `HomeFragment.kt`, `ListFragment.kt`, `DetailFragment.kt`, `Laporan.kt`, `LaporanContoh.kt`, dan `LaporanAdapter.kt`.
  - **6 File Layout XML**: `activity_main.xml`, `fragment_home.xml`, `fragment_list.xml` (*portrait*), `layout-land/fragment_list.xml` (variasi *landscape* hasil perbaikan UX), `item_laporan.xml`, dan `fragment_detail.xml`.
  - **Resource & Navigasi**: `strings.xml`, `colors.xml`, `dimens.xml`, `styles.xml`, `themes.xml` (mode terang konsisten pada `values` dan `values-night`), `nav_graph.xml`, serta `AndroidManifest.xml`.
- Laporan lengkap praktikum tersimpan pada `docs/Laporan_P04.pdf` dan bukti gambar pengujian tersimpan pada folder `screenshots/`.

## 2. Matriks Hasil Aktual Skenario Pengujian Wajib (T01–T16)

| ID & Kondisi | Lingkungan Uji | Aksi Uji & Hasil yang Diharapkan | Hasil Aktual pada Perangkat Uji | Status | Bukti Screenshot | Tindak Lanjut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **T01 Beranda** | Pixel 7, API 37, Portrait, Font 1.0x | Buka aplikasi dari *launcher*. Diharapkan satu Beranda dan penjelasan data contoh terlihat. | Layar Beranda tampil satu kali memuat judul `WargaHub`, teks pengantar, catatan data contoh simulasi, dan tombol *Lihat Daftar Laporan*. | **Lulus** | `screenshots/01_beranda.png` | Tidak diperlukan perubahan. |
| **T02 Daftar** | Pixel 7, API 37, Portrait, Font 1.0x | Tekan *Lihat Daftar Laporan*. Diharapkan jumlah 15 dan baris berisi judul, kategori, serta status tampil. | Tampil teks `15 laporan contoh` beserta daftar kartu yang memuat judul, kategori, dan `Status contoh: Simulasi`. | **Lulus** | `screenshots/02_daftar.png` | Tidak diperlukan perubahan. |
| **T03 Gulir** | Pixel 7, API 37, Portrait, Font 1.0x | Gulir ke laporan zona latihan 10–15. Diharapkan daftar lancar dan item bawah dapat dipilih. | Daftar dapat digulir mulus hingga laporan terbawah (zona latihan 10 sampai 15) dan setiap baris dapat diketuk. | **Lulus** | `screenshots/23_daftar_zona_15.png` | Tidak diperlukan perubahan. |
| **T04 Rincian** | Pixel 7, API 37, Portrait, Font 1.0x | Pilih dua atau lebih laporan berbeda secara bergantian. Diharapkan rincian sesuai ID masing-masing. | Saat memilih zona latihan 1, 10, dan 15 secara bergantian, layar Rincian menampilkan judul, kategori, status, dan deskripsi yang tepat sesuai ID `Long`. | **Lulus** | `screenshots/03_rincian_1.png`, `04_rincian_10.png`, `24_rincian_15.png` | Tidak diperlukan perubahan. |
| **T05 Tombol kembali** | Pixel 7, API 37, Portrait, Font 1.0x | Dari rincian tekan *Kembali ke Daftar*. Diharapkan kembali tanpa menambah daftar baru. | Memanggil `navigateUp()` dan kembali ke *instance* daftar sebelumnya pada posisi semula tanpa menduplikasi layar di *back stack*. | **Lulus** | `screenshots/02_daftar.png` | Tidak diperlukan perubahan. |
| **T06 Up toolbar** | Pixel 7, API 37, Portrait, Font 1.0x | Tekan ikon *Up* di rincian lalu di daftar. Diharapkan alur `Rincian -> Daftar -> Beranda`. | Tombol panah *Up* pada Toolbar mengarahkan dari Rincian Laporan ke Daftar Laporan, lalu kembali ke Beranda. | **Lulus** | `screenshots/02_daftar.png`, `01_beranda.png` | Tidak diperlukan perubahan. |
| **T07 Back sistem** | Pixel 7, API 37, Portrait, Font 1.0x | Ulangi alur lalu gunakan *Back* sistem. Diharapkan urutan kembali masuk akal dan tidak *crash*. | Tombol *Back* sistem kembali berurutan dari `Rincian -> Daftar -> Beranda` hingga keluar ke *launcher* tanpa *crash*. | **Lulus** | `screenshots/12_back_dari_beranda.png` | Tidak diperlukan perubahan. |
| **T08 Kosong** | Pixel 7, API 37, Portrait, Font 1.0x | Tekan *Uji Daftar Kosong*. Diharapkan jumlah 0, pesan kosong, dan aksi pemulihan terlihat. | Teks berubah menjadi `0 laporan contoh`, daftar disembunyikan, pesan kosong muncul, dan label tombol berubah menjadi *Tampilkan Data Contoh*. | **Lulus** | `screenshots/07_kosong.png` | Tidak diperlukan perubahan. |
| **T09 Pulihkan** | Pixel 7, API 37, Portrait & Landscape, Font 1.0x | Tekan *Tampilkan Data Contoh*. Diharapkan jumlah menjadi 15 dan baris kembali tampil. | Jumlah kembali menjadi `15 laporan contoh` dan seluruh 15 baris laporan tampil kembali di `RecyclerView`. | **Lulus** | `screenshots/26_pulihkan_akhir.png` | Tidak diperlukan perubahan. |
| **T10 Rotasi rincian** | Pixel 7, API 37, Portrait -> Landscape, Font 1.0x | Putar perangkat saat rincian terbuka. Diharapkan layar rincian dan data ID tetap sesuai. | Pada saat dirotasi ke *landscape*, judul Toolbar dan rincian laporan yang sedang dibuka tetap terjaga sesuai argumen ID. | **Lulus** | `screenshots/05_rotasi_rincian.png` | Tidak diperlukan perubahan. |
| **T11 Rotasi kosong** | Pixel 7, API 37, Portrait <-> Landscape, Font 1.0x | Aktifkan mode kosong lalu putar perangkat. Diharapkan mode kosong dan label tombol tetap sesuai. | Flag `contoh_kosong` pada `savedInstanceState` menjaga tampilan tetap pada mode 0 laporan dan tombol *Tampilkan Data Contoh* saat rotasi. | **Lulus** | `screenshots/06_kosong_landscape.png`, `25_rotasi_kosong_akhir.png` | Tidak diperlukan perubahan. |
| **T12 Font dan landscape** | Pixel 7 & Layar Kecil `360x640 dp`, Landscape, Font 1.3x–1.5x | Perbesar font; uji ketiga layar dalam *landscape* & layar kecil. Diharapkan teks terbaca serta daftar dan rincian dapat digulir. | Diuji pada skala font 1.3x–1.5x dan layar `360x640 dp` *landscape*; seluruh teks terbaca jelas dan halaman dapat digulir hingga tombol bawah. | **Lulus** | `screenshots/08` s.d. `10_font_besar_*.png`, `14` s.d. `19_layar_kecil_*.png` | Ditambahkan `res/layout-land/fragment_list.xml` agar ruang daftar *landscape* lebih lega. |
| **T13 TalkBack** | Pixel 7, TalkBack aktif | Baca baris dan buka rincian | Penguji mengonfirmasi judul, kategori, Simulasi, Buka rincian terbaca; klik dua kali dan kembali berhasil. Gulir TalkBack belum berhasil. | Lulus pembacaan/aktivasi; keterbatasan gulir | screenshot 21 dan 22; konfirmasi penguji 9 November 2026 | Uji lanjutan gulir diperlukan |
| **T14 Ketukan cepat** | Pixel 7, API 37, Portrait, Font 1.0x | Ketuk aksi dan item cepat berulang. Diharapkan tidak *crash* atau membuat layar duplikat. | Enam ketukan cepat beruntun tidak menyebabkan `IllegalArgumentException` atau layar ganda berkat pemeriksaan `currentDestination?.id`. | **Lulus** | `screenshots/13_ketukan_cepat_rincian.png` | Tidak diperlukan perubahan. |
| **T15 Mulai ulang** | Pixel 7, API 37, Portrait, Font 1.0x | Tutup paksa proses aplikasi (*force-stop*) lalu buka dari *launcher*. Diharapkan data contoh tetap tersedia saat daftar dibuka. | Setelah aplikasi di-*force-stop* dan dibuka ulang, objek `LaporanContoh` membentuk kembali ke-15 data simulasi di memori (bukan bukti database). | **Lulus** | `screenshots/01_beranda.png`, `02_daftar.png` | Tidak diperlukan perubahan. |
| **T16 Cabang laporan tidak ditemukan** | Pixel 7, API 37, Portrait, Font 1.0x (Uji Sementara `-99L`) | Ganti sementara `bundleOf` menjadi `-99L`, pilih baris, lalu kembalikan ke `laporan.id`. Diharapkan pesan aman tampil dan tombol kembali bekerja. | Pada versi uji `-99L`, tampil pesan *"Laporan tidak ditemukan. Kembali ke daftar dan pilih data contoh."* tanpa *crash*, dan tombol kembali berfungsi normal. Kode akhir telah dikembalikan ke `laporan.id`. | **Lulus** | `screenshots/11_id_tidak_ditemukan.png` | Kode akhir telah dipulihkan ke `laporan.id` dan dibangun ulang. |


## 3. Uji tugas Hafidzatun Aulia Safitri

- Nama penguji: Hafidzatun Aulia Safitri.
- NIM: 240104040184.
- Tugas: menemukan rincian laporan zona latihan 10, lalu kembali ke daftar.
- Awal pencatatan waktu: Beranda siap digunakan.
- Akhir pencatatan waktu: rincian zona latihan 10 terbuka.
- Durasi tercatat: 7,3 detik; perjalanan kembali tidak termasuk.
- Konteks pengalaman: belum terbiasa menggunakan emulator.

Durasi menunjukkan waktu interaksi dan pencarian item pada percobaan yang dicatat, bukan waktu respons aplikasi semata. Penyesuaian cara gulir melalui klik-tahan dan geser, penempatan kursor, serta pembacaan label zona dapat menjadi faktor tambahan. Ketiganya merupakan kemungkinan penjelasan dan tidak dinyatakan sebagai kejadian yang telah diukur secara terpisah.

Perbaikan landscape tetap didukung screenshot 15 dan 16: jumlah dan tombol dibuat berdampingan sehingga status baris pertama terlihat bersama judul serta kategori. Tidak tersedia pengukuran waktu sebelum perbaikan dengan prosedur dan penguji yang sama. Karena itu, waktu 7,3 detik tidak digunakan untuk menyimpulkan bahwa layout mempercepat atau memperlambat tugas.

Untuk pengujian berikutnya, berikan pengenalan emulator, tetapkan batas awal dan akhir yang sama, serta catat waktu mencari dan membuka rincian secara terpisah. Keterbatasan gulir TalkBack pada dokumentasi teknis tetap perlu ditindaklanjuti.
