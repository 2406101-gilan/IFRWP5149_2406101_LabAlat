Aktor pada skenario adalah Peminjam, dan langkah khususnya dijalankan 
Mahasiswa; swimlane yang dipakai adalah Mahasiswa, Sistem, dan Petugas 
Laboratorium. Petugas Laboratorium muncul karena langkah Memproses 
keputusan peminjaman pada skenario dijalankan petugas.

Activity kedua lebih pendek dan melanjutkan tahap pembangunan. Swimlane 
yang dipakai sama dengan Activity Peminjaman.

Activity ini adalah alur baca tanpa perubahan data: aktor Peminjam 
memeriksa peralatan apa saja yang tersedia. Swimlane yang dipakai adalah 
Peminjam dan Sistem.

Activity ini memuat satu decision bentuk pengelolaan dengan tiga cabang 
varian. Cabang tambah memuat langkah pembeda LAB-UC08 Tambah Data 
Peralatan, cabang ubah memuat langkah pembeda LAB-UC09 Ubah Data 
Peralatan, dan cabang hapus memuat langkah pembeda LAB-UC10 Hapus Data 
Peralatan beserta syarat hapusnya: data hanya dapat dihapus untuk peralatan 
yang tidak sedang dipinjam dan tidak memiliki pengajuan aktif. Ketiga cabang 
bermuara ke satu merge, lalu alur bersama LAB-UC02 dilanjutkan. Swimlane yang 
dipakai adalah Petugas Laboratorium dan Sistem

Activity ini adalah perilaku extend terhadap LAB-UC03, sehingga alurnya tidak 
dimulai dari pengajuan baru: alur dimulai pada extension point Bukti pengajuan 
tersedia, setelah pengajuan mahasiswa tercatat dengan status Menunggu 
Keputusan, dan berjalan hanya bila condition [mahasiswa memilih cetak] 
terpenuhi. Aktornya Mahasiswa, dan swimlane yang dipakai adalah Mahasiswa 
dan Sistem. Di dalam Activity Peminjaman, perilaku yang sama muncul sebagai 
cabang bersyarat pada Tahap 3; activity ini menggambar perilaku extend tersebut 
secara utuh sebagai satu diagram tersendiri.

Activity ini memuat dua titik keputusan petugas: apakah pengajuan masih 
dapat diproses, dan apakah pengajuan disetujui atau ditolak. Status yang dipakai adalah status pada aturan model Pertemuan 4: Menunggu Keputusan, Disetujui, 
dan Ditolak. Swimlane yang dipakai adalah Petugas Laboratorium dan Sistem; 
Mahasiswa tidak digambar karena pada skenario LAB-UC06 mahasiswa tidak 
melakukan langkah apa pun.

Activity ini adalah satu-satunya activity dengan aktor Kepala Laboratorium, 
sesuai kedudukan LAB-UC07 sebagai satu-satunya use case aktor tersebut. Isi 
activity dibatasi pada langkah tabel skenario LAB-UC07: memilih periode dan 
menampilkan laporan periode tersebut, tanpa fitur tambahan apa pun. Swimlane 
yang dipakai adalah Kepala Laboratorium dan Sistem.