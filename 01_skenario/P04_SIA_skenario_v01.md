Skenario (fiktif, untuk praktikum). Mahasiswa dan Dosen sama-sama Civitas Akademika yang dapat melihat kalender akademik. Dosen menginput nilai mata kuliah yang diampunya setelah masa perkuliahan berakhir. Mahasiswa melihat KHS untuk semester yang nilainya sudah dipublikasikan. Admin Akademik menambah, mengubah, dan menghapus data mahasiswa. Dua use case utama (Input Nilai Mata Kuliah dan Lihat KHS) direalisasikan oleh collaboration yang bersesuaian.

ID	Kebutuhan
SIA-R07	Mahasiswa dan Dosen, sebagai Civitas Akademika, dapat melihat kalender akademik.
SIA-R08	Dosen dapat menginput nilai mata kuliah yang diampunya.
SIA-R09	Mahasiswa dapat melihat KHS untuk semester yang nilainya sudah dipublikasikan.
SIA-R10	Admin Akademik dapat mengelola data mahasiswa.
SIA-R11	Pengelolaan data mahasiswa terdiri dari tiga bentuk khusus: tambah, ubah, dan hapus data mahasiswa.
SIA-R12	Model menunjukkan collaboration yang merealisasikan Input Nilai Mata Kuliah dan Lihat KHS.

Batas dan asumsi

Kode kebutuhan dimulai dari SIA-R07 agar SIA-R01–R02 (Pertemuan 2) dan SIA-R03–R06 (Pertemuan 3) tetap berbeda identitasnya.
Pengguna sudah terautentikasi dan memiliki hak akses sesuai peran.
Kalender akademik = agenda resmi institusi (awal semester, batas KRS, masa ujian, dst.), bukan jadwal kuliah (Pertemuan 2).
Nilai hanya dapat diinput oleh dosen pengampu mata kuliah tersebut. Nilai yang baru diinput berstatus belum terpublikasi; KHS hanya menampilkan nilai yang sudah dipublikasikan.
Hapus Data Mahasiswa hanya untuk mahasiswa tanpa data akademik aktif (ketentuan fiktif).
Pengajuan KRS tetap digambar sebagai bagian diagram kumulatif Pertemuan 3. Pembayaran dan perancangan basis data di luar tugas.
Asumsi penulis: berkas P2/P3 tidak tersedia pada saat pengerjaan ini, sehingga aktor pada SIA-UC01–UC06 direkonstruksi (lihat catatan di tabel katalog). Sesuaikan dengan diagram P3 asli bila berbeda.
Langkah 2 – Katalog gabungan aktor dan use case

Aktor: Civitas Akademika (umum, baru), Mahasiswa (khusus, baru sebagai spesialisasi), Dosen (khusus, baru sebagai spesialisasi), Admin Akademik (tetap), Dosen Wali (tetap).

ID	Nama use case	Aktor terkait	Sumber kebutuhan	Status
SIA-UC01	Lihat Jadwal Kuliah	Mahasiswa, Dosen*	SIA-R01	Tetap
SIA-UC02	Kelola Jadwal Kuliah	Admin Akademik	SIA-R02	Tetap
SIA-UC03	Ajukan KRS	Mahasiswa	SIA-R03	Tetap
SIA-UC04	Validasi KRS (di-include oleh UC03)	– (bagian dari UC03)	SIA-R04	Tetap
SIA-UC05	Unduh Bukti Pengajuan KRS (extend UC03)	Mahasiswa	SIA-R05	Tetap
SIA-UC06	Proses Keputusan KRS	Dosen Wali	SIA-R06	Tetap
SIA-UC07	Lihat Kalender Akademik	Civitas Akademika (→ Mahasiswa, Dosen)	SIA-R07	Baru
SIA-UC08	Input Nilai Mata Kuliah	Dosen	SIA-R08	Baru
SIA-UC09	Lihat KHS	Mahasiswa	SIA-R09	Baru
SIA-UC10	Kelola Data Mahasiswa (umum)	Admin Akademik	SIA-R10	Baru
SIA-UC11	Tambah Data Mahasiswa	Admin Akademik	SIA-R11	Baru
SIA-UC12	Ubah Data Mahasiswa	Admin Akademik	SIA-R11	Baru
SIA-UC13	Hapus Data Mahasiswa	Admin Akademik	SIA-R11	Baru

Langkah 3 – Generalization aktor
Civitas Akademika  (aktor umum)
 ├── Mahasiswa     (aktor khusus)
 └── Dosen         (aktor khusus)
Fungsi yang diwarisi: SIA-UC07 Lihat Kalender Akademik.
Fungsi khusus: Mahasiswa: UC01, UC03, UC05, UC09. Dosen: UC01, UC08.
Alasan: Mahasiswa dan Dosen berbagi fungsi yang sama persis (kalender akademik). Asosiasi untuk fungsi bersama digambar satu kali dari Civitas Akademika, sehingga tidak ada garis ganda, dan penambahan peran civitas lain (mis. tendik) cukup dengan satu generalization baru. Admin Akademik dan Dosen Wali bukan bagian hierarki ini.
Langkah 4 – Generalization use case

Use case umum: SIA-UC10 Kelola Data Mahasiswa (diasosiasikan dengan Admin Akademik satu kali).

Use case khusus	Perilaku pembeda
SIA-UC11 Tambah Data Mahasiswa	Membuat catatan mahasiswa baru dengan identitas unik (mis. NIM) yang belum terdaftar.
SIA-UC12 Ubah Data Mahasiswa	Memperbarui atribut data mahasiswa yang sudah ada tanpa mengganti identitas uniknya.
SIA-UC13 Hapus Data Mahasiswa	Menghapus catatan mahasiswa hanya jika mahasiswa tidak memiliki data akademik aktif, dengan konfirmasi sebelum penghapusan.
Langkah 5 – Collaboration
ID	Nama collaboration	Merealisasikan
SIA-CO01	Input Nilai Mata Kuliah	SIA-UC08 Input Nilai Mata Kuliah
SIA-CO02	Lihat KHS	SIA-UC09 Lihat KHS

Kebutuhan terkait: SIA-R12.

Langkah 6 – Use case description
SIA-UC08 Input Nilai Mata Kuliah
Elemen	Isi
ID	SIA-UC08
Nama	Input Nilai Mata Kuliah
Collaboration	SIA-CO01 Input Nilai Mata Kuliah
Aktor utama	Dosen
Sumber kebutuhan	SIA-R08
Deskripsi	Dosen memasukkan nilai mahasiswa pada mata kuliah yang diampunya setelah masa perkuliahan berakhir.
Prasyarat	(1) Dosen sudah terautentikasi. (2) Dosen adalah pengampu mata kuliah tersebut. (3) Masa perkuliahan mata kuliah telah berakhir.
Pemicu	Dosen memilih menu input nilai.
Alur utama	1. Sistem menampilkan daftar mata kuliah yang diampu dosen.
2. Dosen memilih mata kuliah.
3. Sistem menampilkan daftar mahasiswa peserta.
4. Dosen mengisi nilai tiap mahasiswa.
5. Sistem memeriksa bahwa nilai berada dalam rentang yang sah.
6. Dosen menyimpan nilai.
7. Sistem menyimpan nilai dengan status belum terpublikasi dan menampilkan konfirmasi.
Alur alternatif	A1 – Nilai di luar rentang sah (langkah 5): sistem menolak nilai tersebut, menandai kolom yang salah, dan meminta perbaikan; tidak ada nilai yang disimpan sampai semua nilai sah. Kembali ke langkah 4.
A2 – Dosen membatalkan (langkah 4–6): tidak ada perubahan data.
Pascakondisi berhasil	Nilai tersimpan pada mata kuliah terkait dengan status belum terpublikasi (belum tampil di KHS).
Pascakondisi gagal	Tidak ada nilai yang tersimpan atau berubah; data nilai tetap seperti sebelum proses; sistem menampilkan pesan alasan penolakan.
SIA-UC09 Lihat KHS (ringkas)
Elemen	Isi
ID / Nama	SIA-UC09 Lihat KHS
Collaboration	SIA-CO02 Lihat KHS
Aktor	Mahasiswa
Deskripsi	Mahasiswa memilih semester dan sistem menampilkan KHS yang hanya memuat nilai yang sudah dipublikasikan; semester yang nilainya belum dipublikasikan tidak ditampilkan nilainya.
Sumber kebutuhan	SIA-R09