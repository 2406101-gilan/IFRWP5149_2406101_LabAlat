Selain mahasiswa, dosen juga meminjam peralatan laboratorium untuk
kegiatan praktikum dan penelitian. Mahasiswa dan dosen sama-sama
dapat melihat ketersediaan peralatan dan mengajukan peminjaman.
Petugas laboratorium mengelola data peralatan: menambah peralatan
baru, mengubah data peralatan, dan menghapus data peralatan yang
tidak lagi dipakai. Setelah peminjaman disetujui dan alat diambil, petugas
mencatat pengembalian peralatan. Pada saat mencatat pengembalian,
petugas memeriksa dan mencatat kondisi peralatan. Dua use case utama
pada potongan model ini, Ajukan Peminjaman dan Catat Pengembalian
Peralatan, ditunjukkan realisasinya oleh collaboration yang bersesuaian.
Seluruh fungsi Pertemuan 3 tetap berlaku dan tetap digambar:
pemeriksaan ketersediaan di dalam pengajuan, pencetakan bukti
pengajuan oleh mahasiswa, proses keputusan peminjaman oleh petugas,
dan laporan peminjaman untuk kepala laboratorium. Diagram Pertemuan
4 adalah diagram Pertemuan 3 yang ditambah, bukan diagram baru yang
menggantikannya.


Batas sistem dan aturan
• Sistem mencatat dan menyediakan informasi; perpindahan fisik alat tidak
terjadi di dalam perangkat lunak (tetap dari Pertemuan 3).
• Pengguna telah terautentikasi dan memiliki hak akses sesuai peran (tetap
dari Pertemuan 3).
• Pengembalian hanya dapat dicatat untuk peminjaman berstatus Dipinjam.
Peminjaman yang masih Menunggu Keputusan atau Ditolak tidak dapat
dicatat pengembaliannya.
• Kondisi peralatan pada pengembalian dicatat dengan salah satu nilai: Baik,
Rusak Ringan, atau Rusak Berat.
• Hapus Data Peralatan hanya untuk peralatan yang tidak sedang dipinjam
dan tidak memiliki pengajuan aktif.
• Keterlambatan dan denda belum dimodelkan pada pertemuan ini. Tuliskan
sebagai pertanyaan terbuka pada berkas kebutuhan, jangan mengarang
aturan denda.
• Kriteria penerimaan model: semua kebutuhan LAB-R01 sampai LAB-R11
mempunyai representasi pada diagram kumulatif, arah generalization dan
realization benar, dan diagram konsisten dengan deskripsinya.

|                                                                               || Aktor | Kedudukan | Tujuan terhadap sistem |                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                |---|---|---|                                                                                                |
|                                | Peminjam | Umum (*general*), baru pada Pertemuan 4 | Peran umum bagi peminjam peralatan. Mewariskan fungsinya kepada Mahasiswa dan Dosen. |                                |
|| Mahasiswa | Khusus dari Peminjam, tetap dari Pertemuan 3 | Melihat ketersediaan dan mengajukan peminjaman (diwarisi dari Peminjam), ditambah mencetak bukti pengajuan sebagai asosiasi khususnya sendiri. ||
|                                     | Dosen | Khusus dari Peminjam, baru pada Pertemuan 4 | Melihat ketersediaan dan mengajukan peminjaman (diwarisi dari Peminjam). |                                      |
|                             | Petugas Laboratorium | Tetap dari Pertemuan 3 | Mengelola data peralatan, memproses keputusan peminjaman, dan mencatat pengembalian peralatan. |                              |
|                                                               | Kepala Laboratorium | Tetap dari Pertemuan 3 | Melihat laporan peminjaman. |                                                                |
|                                                                                                                                                                                                             |
|                                                                   <!-- Kerangka tabel berikutnya (isi tidak ada pada teks yang ditempel):                                                                   |
|                                                                                                                                                                                                             |
|                                                                             | ID | Nama use case | Peran dalam model | Sumber |                                                                             |
|                                                                                              |---|---|---|---|                                                                                              |
|                                                                                                                                                                                                             |
|                                                                                                     -->                                                                                                     |

Daftar Kebutuhan Use Case Laboratorium

## Tabel Kebutuhan Use Case

| ID       | Nama Use Case                | Peran dalam Model                                                                                 | Sumber Kebutuhan |
| -------- | ---------------------------- | ------------------------------------------------------------------------------------------------- | ---------------- |
| LAB-UC01 | Lihat Ketersediaan Peralatan | Tetap dari Pertemuan 3; fungsi aktor umum Peminjam                                                | LAB-R01, LAB-R07 |
| LAB-UC02 | Kelola Data Peralatan        | Tetap dari Pertemuan 3; use case umum bagi LAB-UC08, LAB-UC09, dan LAB-UC10                       | LAB-R02, LAB-R08 |
| LAB-UC03 | Ajukan Peminjaman            | Tetap dari Pertemuan 3; fungsi aktor umum Peminjam; menyertakan LAB-UC04; direalisasikan LAB-CO01 | LAB-R03, LAB-R07 |
| LAB-UC04 | Periksa Ketersediaan         | Tetap dari Pertemuan 3; perilaku yang disertakan LAB-UC03                                         | LAB-R03          |
| LAB-UC05 | Cetak Bukti Pengajuan        | Tetap dari Pertemuan 3; tambahan bersyarat pada LAB-UC03 melalui relasi `«extend»`                | LAB-R04          |
| LAB-UC06 | Proses Keputusan Peminjaman  | Tetap dari Pertemuan 3; fungsi utama Petugas                                                      | LAB-R05          |
| LAB-UC07 | Lihat Laporan Peminjaman     | Tetap dari Pertemuan 3; fungsi utama Kepala Laboratorium                                          | LAB-R06          |
| LAB-UC08 | Tambah Data Peralatan        | Baru pada Pertemuan 4; use case khusus dari LAB-UC02                                              | LAB-R08          |
| LAB-UC09 | Ubah Data Peralatan          | Baru pada Pertemuan 4; use case khusus dari LAB-UC02                                              | LAB-R08          |
| LAB-UC10 | Hapus Data Peralatan         | Baru pada Pertemuan 4; use case khusus dari LAB-UC02                                              | LAB-R08          |
| LAB-UC11 | Catat Pengembalian Peralatan | Baru pada Pertemuan 4; fungsi utama Petugas; direalisasikan LAB-CO02                              | LAB-R09          |
| LAB-UC12 | Periksa Kondisi Peralatan    | Baru pada Pertemuan 4; perilaku yang disertakan LAB-UC11                                          | LAB-R10          |



