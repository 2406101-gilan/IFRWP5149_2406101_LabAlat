# P03_NIM_SIA_deskripsi_v01 — Use Case Description (SIA)

Status: LATIHAN USE CASE DIAGRAM. Batas sistem: **Sistem Informasi Akademik**. Diagram: `P03_NIM_SIA_usecase_v01.drawio` / `.png`.

## Langkah 2 — Katalog use case
| ID | Nama use case | Aktor terkait | Sumber kebutuhan | Peran dalam model |
|---|---|---|---|---|
| SIA-UC01 | Ajukan KRS | Mahasiswa | SIA-R03, SIA-R05 | Fungsi utama mahasiswa |
| SIA-UC02 | Validasi KRS | — (dijalankan oleh UC01) | SIA-R04 | Perilaku yang disertakan UC01 |
| SIA-UC03 | Unduh bukti pengajuan KRS | Mahasiswa | SIA-R05 | Tambahan bersyarat pada UC01 |
| SIA-UC04 | Proses keputusan KRS | Dosen wali | SIA-R06 | Fungsi utama dosen wali |

Cakupan: SIA-R03 -> UC01; SIA-R04 -> UC02; SIA-R05 -> UC03 (dan titik extend di UC01); SIA-R06 -> UC04. Semua kebutuhan tugas punya representasi.

## Langkah 3 — Include
**SIA-UC01 «include» SIA-UC02**
- Sumber: Ajukan KRS. Tujuan: Validasi KRS.
- Alasan: skenario menyatakan *setiap pengajuan* menjalankan validasi (SIA-R04: bagian pengajuan). Pemeriksaan kelengkapan, prasyarat, dan benturan jadwal selalu dilakukan pada langkah 4; hasil "valid/tidak valid" menentukan apakah pengajuan disimpan. Gagalnya validasi tidak membuatnya opsional.
- Letak pemanggilan: langkah 4 alur utama UC01. Hasil: valid -> lanjut simpan; tidak valid -> alur alternatif 5a.
- Bukan include: autentikasi. Itu **prasyarat** ("Pengguna telah terautentikasi"), bukan bagian pelaksanaan fungsi, sehingga tidak ada use case Login.

## Langkah 4 — Extend
**SIA-UC03 «extend» SIA-UC01**
- Use case dasar: Ajukan KRS. Use case tambahan: Unduh bukti pengajuan KRS.
- Extension point: **Bukti pengajuan tersedia** (langkah 6 UC01).
- Kondisi: **[mahasiswa memilih unduh]**.
- Alasan: pengajuan tetap berhasil tersimpan tanpa unduhan (aturan 4); UC01 tetap bermakna tanpa UC03.
- Pembeda: validasi gagal bukan extend, melainkan alur alternatif UC01 (5a), karena tidak punya tujuan pemodelan terpisah.

## Langkah 5 — Deskripsi

### a. SIA-UC01 — Ajukan KRS
| Bagian | Isi |
|---|---|
| ID dan nama | SIA-UC01 — Ajukan KRS |
| Sumber kebutuhan | SIA-R03, SIA-R05 |
| Tujuan | Menghasilkan pengajuan KRS yang tersimpan |
| Aktor utama | Mahasiswa |
| Aktor pendukung | Tidak ada |
| Pemicu | Mahasiswa memilih fungsi pengajuan KRS |
| Prasyarat | Mahasiswa telah terautentikasi; data mata kuliah, prasyarat, dan jadwal tersedia |
| Include | SIA-UC02 — Validasi KRS (dipanggil pada langkah 4) |
| Extension point | Bukti pengajuan tersedia, pada langkah 6 |
| Extend | SIA-UC03 jika [mahasiswa memilih unduh] |
| Pascakondisi berhasil | Pengajuan KRS tersimpan dengan nomor dan status Menunggu persetujuan dosen wali |
| Pascakondisi gagal | Tidak ada pengajuan KRS baru yang berhasil tersimpan |
| Aturan bisnis/asumsi | Validasi gagal -> tidak tersimpan; unduh bukti bukan syarat keberhasilan; tersimpan belum berarti disetujui; Q3 |

Alur utama:
| Langkah | Tindakan mahasiswa | Respons sistem |
|---|---|---|
| 1 | Membuka pengajuan KRS | Menampilkan daftar mata kuliah dan formulir pengajuan |
| 2 | Memilih mata kuliah | Menampung pilihan |
| 3 | Mengirim pengajuan | Menerima pengajuan |
| 4 | — | Menjalankan SIA-UC02 (validasi KRS) |
| 5 | — | Jika valid, menyimpan pengajuan, memberi nomor, status Menunggu persetujuan dosen wali |
| 6 | Melihat konfirmasi | Menampilkan nomor dan status; mencapai extension point *Bukti pengajuan tersedia* |
| 7 | Mengakhiri pengajuan | Menutup proses pengajuan |

Alur alternatif/pengecualian:
| Rujukan | Kondisi | Tindakan | Hasil akhir |
|---|---|---|---|
| 2a | Mahasiswa membatalkan sebelum mengirim | Sistem menutup formulir tanpa menyimpan | Gagal: tidak ada pengajuan tersimpan |
| 5a | SIA-UC02 menghasilkan "tidak valid" (tidak lengkap, prasyarat belum terpenuhi, atau jadwal bentrok) | Sistem tidak menyimpan dan menampilkan alasan. Mahasiswa memperbaiki pilihan -> kembali ke langkah 2, atau membatalkan | Gagal: tidak ada pengajuan tersimpan. Jika diperbaiki dan valid, lanjut ke langkah 5 |
| 6a | Mahasiswa memilih unduh (extension point; kondisi [mahasiswa memilih unduh]) | Sistem menjalankan SIA-UC03, lalu kembali ke langkah 7 | Berhasil: pengajuan tersimpan + bukti diunduh |
| 6b | Mahasiswa tidak memilih unduh | Lanjut ke langkah 7 | Berhasil: pengajuan tersimpan, tanpa bukti |

### b. SIA-UC02 — Validasi KRS
| Bagian | Isi |
|---|---|
| ID dan nama | SIA-UC02 — Validasi KRS |
| Sumber kebutuhan | SIA-R04 |
| Tujuan | Menentukan apakah pilihan mata kuliah layak disimpan sebagai pengajuan |
| Aktor utama | Mahasiswa (melalui SIA-UC01; tidak dijalankan langsung oleh aktor) |
| Aktor pendukung | Tidak ada |
| Pemicu | SIA-UC01 mencapai langkah 4 (disertakan pada setiap pengajuan) |
| Prasyarat | Pilihan mata kuliah telah dikirim; data mata kuliah, prasyarat, dan jadwal tersedia |
| Pascakondisi berhasil | Hasil "valid" dikembalikan ke SIA-UC01; tidak ada data yang diubah |
| Pascakondisi gagal | Hasil "tidak valid" beserta alasan dikembalikan ke SIA-UC01; tidak ada pengajuan tersimpan |
| Aturan bisnis/asumsi | Tiga pemeriksaan: kelengkapan, prasyarat, benturan jadwal; Q5; tidak ada batas SKS (tidak ditambahkan tanpa sumber) |

Alur utama:
| Langkah | Tindakan mahasiswa | Respons sistem |
|---|---|---|
| 1 | — | Menerima pilihan mata kuliah dari UC01 |
| 2 | — | Memeriksa kelengkapan pilihan |
| 3 | — | Memeriksa prasyarat setiap mata kuliah terpilih |
| 4 | — | Memeriksa benturan jadwal antarmata kuliah terpilih |
| 5 | — | Menetapkan hasil "valid" dan mengembalikannya ke UC01 |

Alur alternatif/pengecualian:
| Rujukan | Kondisi | Tindakan | Hasil akhir |
|---|---|---|---|
| 2a | Pilihan kosong atau tidak lengkap | Mencatat temuan "tidak lengkap" | Tidak valid |
| 3a | Prasyarat suatu mata kuliah belum terpenuhi | Mencatat temuan beserta mata kuliah terkait | Tidak valid |
| 4a | Dua mata kuliah atau lebih berbenturan jadwal | Mencatat temuan beserta mata kuliah terkait | Tidak valid |
| 5a | Ada minimal satu temuan dari 2a/3a/4a | Mengembalikan "tidak valid" + semua temuan ke UC01 (lanjut ke 5a UC01) | Gagal |

### c. SIA-UC03 — Unduh bukti pengajuan KRS
| Bagian | Isi |
|---|---|
| ID dan nama | SIA-UC03 — Unduh bukti pengajuan KRS |
| Sumber kebutuhan | SIA-R05 |
| Tujuan | Mahasiswa memperoleh bukti pengajuan KRS yang sudah tersimpan |
| Aktor utama | Mahasiswa |
| Aktor pendukung | Tidak ada |
| Pemicu | Pada extension point *Bukti pengajuan tersedia*, mahasiswa memilih unduh |
| Prasyarat | Pengajuan KRS telah tersimpan dan konfirmasi (nomor, status) ditampilkan |
| Use case dasar | SIA-UC01 — Ajukan KRS |
| Extension point | Bukti pengajuan tersedia (langkah 6 UC01) |
| Kondisi extend | [mahasiswa memilih unduh] |
| Pascakondisi berhasil | Berkas bukti diterima mahasiswa; kendali kembali ke UC01 langkah 7 |
| Pascakondisi gagal | Bukti tidak terunduh; pengajuan KRS **tetap tersimpan** |
| Aturan bisnis/asumsi | Unduh bukan syarat keberhasilan pengajuan; format berkas belum ditetapkan (Q2) |

Alur utama:
| Langkah | Tindakan mahasiswa | Respons sistem |
|---|---|---|
| 1 | Memilih unduh bukti pengajuan | Menyiapkan bukti yang memuat nomor, status, dan daftar mata kuliah pengajuan |
| 2 | — | Menyediakan berkas bukti untuk diunduh |
| 3 | Menerima berkas | Mengembalikan alur ke SIA-UC01 langkah 7 |

Alur alternatif/pengecualian:
| Rujukan | Kondisi | Tindakan | Hasil akhir |
|---|---|---|---|
| 2a | Bukti gagal disiapkan | Sistem menampilkan pesan; mahasiswa dapat mencoba lagi atau kembali ke UC01 langkah 7 | Gagal: pengajuan tetap tersimpan |

### d. SIA-UC04 — Proses keputusan KRS
| Bagian | Isi |
|---|---|
| ID dan nama | SIA-UC04 — Proses keputusan KRS |
| Sumber kebutuhan | SIA-R06 |
| Tujuan | Menetapkan KRS mahasiswa menjadi disetujui atau ditolak dengan catatan keputusan |
| Aktor utama | Dosen wali |
| Aktor pendukung | Tidak ada |
| Pemicu | Dosen wali memilih fungsi pemrosesan keputusan KRS |
| Prasyarat | Dosen wali telah terautentikasi; ada KRS berstatus Menunggu persetujuan dosen wali |
| Pascakondisi berhasil | KRS berstatus Disetujui atau Ditolak, beserta catatan keputusan |
| Pascakondisi gagal | Status KRS tetap Menunggu persetujuan dosen wali |
| Aturan bisnis/asumsi | Hanya KRS berstatus menunggu yang diproses; catatan wajib saat menolak, opsional saat menyetujui (Q1); tindak lanjut setelah keputusan belum dimodelkan (Q4); pembayaran di luar cakupan |

Alur utama (persetujuan):
| Langkah | Tindakan dosen wali | Respons sistem |
|---|---|---|
| 1 | Membuka daftar KRS menunggu keputusan | Menampilkan daftar KRS berstatus Menunggu persetujuan |
| 2 | Memilih satu KRS | Menampilkan rincian KRS (mata kuliah terpilih) |
| 3 | Memilih Setujui | Menampung pilihan keputusan |
| 4 | Mengisi catatan keputusan (opsional untuk persetujuan) dan mengonfirmasi | Menyimpan keputusan dan catatan, mengubah status menjadi Disetujui |
| 5 | Melihat konfirmasi | Menampilkan status akhir dan catatan |

Alur alternatif/pengecualian:
| Rujukan | Kondisi | Tindakan | Hasil akhir |
|---|---|---|---|
| 2a | Dosen wali membatalkan tanpa memilih KRS | Sistem menutup proses | Gagal: tidak ada perubahan |
| 3a | Dosen wali memilih Tolak (**penolakan**) | Sistem meminta catatan penolakan; lanjut ke langkah 4 dengan catatan wajib; status menjadi Ditolak | Berhasil: KRS Ditolak + catatan |
| 4a | Catatan kosong saat menolak | Sistem meminta catatan; kembali ke langkah 4 | Belum ada perubahan status |
| 4b | Keputusan gagal disimpan | Sistem menampilkan pesan kegagalan | Gagal: status tetap Menunggu persetujuan |

## Langkah 7 — Uji konsistensi
| Situasi | Menurut diagram | Menurut deskripsi | Konsisten? |
|---|---|---|---|
| a. Validasi berhasil, tidak unduh | UC01 -> include UC02 (valid) -> selesai; UC03 tidak dijalankan | UC01: 4 (valid) -> 5 simpan -> 6b -> 7. Pascakondisi berhasil terpenuhi tanpa UC03 | Ya |
| b. Validasi gagal | UC01 include UC02; extension point tidak tercapai | UC02 5a -> UC01 5a: tidak disimpan, tidak mencapai langkah 6 sehingga UC03 tidak dapat berjalan. Pascakondisi gagal | Ya |
| c. Validasi berhasil, unduh | UC03 extend UC01 pada *Bukti pengajuan tersedia*, kondisi [mahasiswa memilih unduh] | UC01 6a -> UC03 -> kembali ke 7. Pengajuan tersimpan + bukti diunduh | Ya |

Kesimpulan: ketiga situasi menghasilkan hasil yang sama pada diagram dan deskripsi.

## Checklist
- [x] Setiap aktor punya interaksi jelas (Mahasiswa: UC01, UC03; Dosen wali: UC04)
- [x] Use case sesuai kebutuhan dan berada di dalam batas sistem
- [x] Include mengarah ke perilaku yang disertakan (UC01 -> UC02)
- [x] Extend mengarah ke use case dasar (UC03 -> UC01)
- [x] Extension point berada pada use case dasar (UC01)
- [x] Kondisi extend tercantum di diagram (catatan) dan deskripsi
- [x] Pengajuan tetap berhasil tanpa perilaku tambahan
- [x] Prasyarat (terautentikasi) dibedakan dari include
- [x] Alur alternatif menjelaskan kegagalan dan hasil akhirnya
- [x] Diagram dan deskripsi memakai nama serta ID yang sama
- [x] Sumber dapat dibuka kembali (.drawio)
- [x] Ekspor (.png) sesuai sumber v01
- [x] Kebutuhan belum dimodelkan ditandai: SIA-R01/R02 di luar potongan; Q1–Q5 terbuka