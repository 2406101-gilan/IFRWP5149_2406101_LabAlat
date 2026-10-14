Skenario tugas:
Mahasiswa mengajukan KRS dengan memilih mata kuliah. Setiap
pengajuan menjalankan validasi KRS yang memeriksa kelengkapan,
prasyarat mata kuliah, dan benturan jadwal. Jika validasi berhasil,
sistem menyimpan pengajuan berstatus menunggu persetujuan dosen
wali. Pada konfirmasi penyimpanan, mahasiswa dapat memilih
mengunduh bukti pengajuan. Dosen wali menyetujui atau menolak KRS
dan memberikan catatan keputusan.

2. Kebutuhan yang dimodelkan 

|ID         | Kebutuhan                                                                |
|--------------------------------------------------------------------------------------|
|SIA-R01    |Mahasiswa dapat melihat jadwal                                            | 
|SIA-R02    | Admin akademik dapat mengelola jadwal kuliah                             |
|SIA-R03	| Mahasiswa dapat mengajukan KRS                                           |
|SIA-R04	| Sistem memvalidasi KRS sebagai bagian pengajuan                          |
|SIA-R05	| ahasiswa dapat mengunduh bukti jika memilihnya pada konfirmasi pengajuan |
|SIA-R06	| Dosen wali dapat memproses persetujuan atau penolakan KRS                |
                                                                                   

3. Asumsi dan batas
Pengguna telah terautentikasi.
Data mata kuliah, prasyarat, dan jadwal tersedia.
Validasi gagal menyebabkan pengajuan belum berhasil tersimpan.
Unduh bukti tidak menjadi syarat keberhasilan pengajuan.
KRS tersimpan belum berarti disetujui.
Di luar tugas: pembayaran, pengisian nilai, implementasi basis data.

<!-- Katalog use case -->
ID	Nama use case	Aktor terkait	Sumber kebutuhan	Peran dalam model
SIA-UC01	Ajukan KRS	Mahasiswa	SIA-R03, SIA-R05	Fungsi utama mahasiswa
SIA-UC02	Validasi KRS	— (dijalankan oleh UC01)	SIA-R04	Perilaku yang disertakan UC01
SIA-UC03	Unduh bukti pengajuan KRS	Mahasiswa	SIA-R05	Tambahan bersyarat pada UC01
SIA-UC04	Proses keputusan KRS	Dosen wali	SIA-R06	Fungsi utama dosen wali

<!-- SIA-UC01 «include» SIA-UC02 -->

Sumber: Ajukan KRS. Tujuan: Validasi KRS.
Alasan: skenario menyatakan setiap pengajuan menjalankan validasi (SIA-R04: bagian pengajuan). Pemeriksaan kelengkapan, prasyarat, dan benturan jadwal selalu dilakukan pada langkah 4; hasil "valid/tidak valid" menentukan apakah pengajuan disimpan. Gagalnya validasi tidak membuatnya opsional.
Letak pemanggilan: langkah 4 alur utama UC01. Hasil: valid -> lanjut simpan; tidak valid -> alur alternatif 5a.
Bukan include: autentikasi. Itu prasyarat ("Pengguna telah terautentikasi"), bukan bagian pelaksanaan fungsi, sehingga tidak ada use case Login.

<!-- SIA-UC03 «extend» SIA-UC01 -->

Use case dasar: Ajukan KRS. Use case tambahan: Unduh bukti pengajuan KRS.
Extension point: Bukti pengajuan tersedia (langkah 6 UC01).
Kondisi: [mahasiswa memilih unduh].
Alasan: pengajuan tetap berhasil tersimpan tanpa unduhan (aturan 4); UC01 tetap bermakna tanpa UC03.
Pembeda: validasi gagal bukan extend, melainkan alur alternatif UC01 (5a), karena tidak punya tujuan pemodelan terpisah.