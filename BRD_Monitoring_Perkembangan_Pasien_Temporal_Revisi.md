# BUSINESS REQUIREMENTS DOCUMENT (BRD)

## Implementasi Event-Driven Architecture dengan Durable Workflow Orchestration Menggunakan Temporal pada Sistem Monitoring Perkembangan Pasien

| Informasi                   | Keterangan                                   |
| --------------------------- | -------------------------------------------- |
| Instansi / Objek Penelitian | Klinik Darus Syifa Holistik (DSH)            |
| Program Studi               | Informatika, FASILKOM Universitas Esa Unggul |
| Versi Dokumen               | 1.3 — Draf Revisi untuk Validasi             |
| Tanggal                     | 12 November 2026                             |
| Penyusun                    | Mahasiswa Program Studi Informatika          |
| Status                      | Belum divalidasi oleh pihak klinik           |

> **Catatan dokumen:** BRD ini disusun berdasarkan konsep penelitian dan informasi awal mengenai Klinik DSH. Informasi yang belum dikonfirmasi melalui wawancara atau observasi dinyatakan sebagai asumsi atau kebutuhan validasi. Target angka pada bagian pengujian merupakan target awal yang diusulkan untuk prototipe, bukan hasil pengukuran maupun standar operasional klinik.

---

# 1. Executive Summary

Klinik Darus Syifa Holistik (DSH), berdasarkan informasi awal, masih menggunakan Microsoft Excel untuk melakukan pencatatan data pasien dan hasil pemeriksaan. Dalam kegiatan monitoring perkembangan pasien, khususnya peserta program Moslem Healthy Lifestyle (MHLS), proses pemantauan tidak hanya berkaitan dengan kunjungan dan pemeriksaan di klinik, tetapi juga dapat melibatkan aktivitas mandiri pasien berdasarkan instruksi pihak klinik. Aktivitas tersebut dapat memiliki jadwal, frekuensi, dan periode pelaksanaan yang berbeda, serta memerlukan pengingat dan laporan dari pasien.

Karakteristik tersebut menjadi dasar kebutuhan sistem yang tidak hanya berfungsi sebagai media pencatatan data, tetapi juga mampu mengelola rangkaian aktivitas monitoring yang berlangsung dalam jangka waktu tertentu. Dalam pelaksanaannya, instruksi aktivitas dapat mengalami perubahan atau pembatalan, pasien dapat mengirimkan laporan pada waktu yang berbeda, dan proses monitoring perlu memiliki mekanisme penanganan apabila terjadi gangguan teknis.

Penelitian ini mengusulkan sistem monitoring perkembangan pasien yang terdiri atas aplikasi web untuk petugas klinik dan aplikasi mobile untuk pasien. Sistem menerapkan **Event-Driven Architecture (EDA)** untuk komunikasi antarbagian sistem melalui event, serta **Durable Workflow Orchestration menggunakan Temporal** untuk mengelola siklus workflow, termasuk penjadwalan, pengingat, waktu tunggu laporan pasien, perubahan instruksi, pembatalan, retry, dan pemulihan proses setelah gangguan.

Data pasien, kunjungan, pemeriksaan, instruksi aktivitas, dan laporan tetap disimpan pada basis data aplikasi. Event digunakan untuk menyampaikan kejadian bisnis yang relevan, sedangkan Temporal mengelola eksekusi workflow yang membutuhkan penjadwalan dan waktu tunggu dalam jangka panjang.

Keberhasilan sistem akan dievaluasi melalui pengujian fungsional, pemrosesan event, ketepatan alur workflow, penanganan perubahan, serta pemulihan setelah gangguan. Evaluasi juga dapat membandingkan pendekatan workflow konvensional menggunakan Laravel Queue dan Scheduler dengan pendekatan EDA dan Temporal berdasarkan skenario pengujian yang sama. Perbandingan tersebut bertujuan mengidentifikasi perbedaan karakteristik kedua pendekatan, bukan mengasumsikan bahwa salah satunya pasti lebih unggul pada seluruh aspek.

# 2. Business Objectives & Success Metrics (SMART)

| Kode  | Business Objective                                                                         | Success Metric                                                                                                                | Target Awal                                                                                          |
| ----- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| BO-01 | Memusatkan pengelolaan data pasien dan informasi monitoring dalam satu sistem.             | Keberhasilan pencatatan dan penayangan data pasien, kunjungan, pemeriksaan, instruksi, serta laporan pada skenario pengujian. | 100% skenario fungsi inti yang ditetapkan berhasil dijalankan.                                       |
| BO-02 | Memfasilitasi pengelolaan instruksi aktivitas mandiri pasien secara terstruktur.           | Keberhasilan pembuatan instruksi beserta jadwal, frekuensi, periode, dan keterangannya.                                       | 100% skenario pengelolaan instruksi yang ditetapkan berhasil dijalankan.                             |
| BO-03 | Memfasilitasi pasien dalam menyampaikan laporan pelaksanaan aktivitas.                     | Keberhasilan penerimaan, penyimpanan, dan keterkaitan laporan dengan instruksi yang sesuai.                                   | 100% skenario pengiriman dan penyimpanan laporan pada pengujian fungsional berhasil.                 |
| BO-04 | Mengelola pengingat berdasarkan jadwal aktivitas yang masih berlaku.                       | Ketepatan pemicu pengingat dibandingkan dengan jadwal yang telah dikonfigurasi.                                               | Minimal 95% pemicu pengingat berada dalam toleransi keterlambatan 1 menit pada lingkungan pengujian. |
| BO-05 | Menjaga keberlangsungan workflow ketika terjadi gangguan pada worker atau layanan terkait. | Keberhasilan workflow melanjutkan proses setelah worker dihentikan dan dijalankan kembali.                                    | 100% skenario pemulihan yang telah ditetapkan berhasil dijalankan.                                   |
| BO-06 | Memastikan perubahan dan pembatalan instruksi diterapkan pada workflow terkait.            | Ketepatan penyesuaian atau penghentian workflow setelah instruksi diperbarui atau dibatalkan.                                 | 100% skenario perubahan dan pembatalan yang ditetapkan berhasil dijalankan.                          |
| BO-07 | Menyediakan riwayat monitoring yang dapat ditelusuri oleh pengguna berwenang.              | Kelengkapan penayangan riwayat kunjungan, pemeriksaan, instruksi, laporan, dan perubahan.                                     | Seluruh data pada skenario pengujian dapat ditelusuri sesuai hak akses.                              |

**Ketentuan pengukuran:**

1. Target di atas merupakan target awal pengujian prototipe dan dapat disesuaikan berdasarkan hasil validasi kebutuhan serta kemampuan lingkungan pengujian.
2. Keberhasilan pemulihan workflow diukur berdasarkan skenario gangguan yang didefinisikan, bukan jaminan bahwa seluruh kemungkinan gangguan sistem dapat dipulihkan tanpa pengecualian.
3. Ketepatan pengingat diukur dari waktu pemicu aktivitas pengiriman notifikasi oleh sistem, bukan jaminan notifikasi telah diterima atau dibaca oleh perangkat pasien.
4. Penelitian tidak menyimpulkan adanya pengurangan waktu kerja, penurunan kesalahan pencatatan, atau peningkatan kinerja operasional klinik tanpa pengukuran kondisi sebelum dan sesudah penerapan sistem.

# 3. Scope (In-Scope & Out-of-Scope)

## 3.1 In-Scope

Pengembangan sistem mencakup:

**A. Pengelolaan Pasien**

- Aplikasi web untuk petugas klinik.
- Aplikasi mobile untuk pasien.
- Autentikasi dan pembatasan hak akses berdasarkan peran.
- Pembuatan akun pasien oleh petugas; pendaftaran mandiri pasien tidak termasuk dalam ruang lingkup.
- Pengelolaan identitas dan informasi dasar pasien.
- Pengelompokan pasien umum dan peserta program MHLS berdasarkan ketentuan klinik.

**B. Pengelolaan Kunjungan dan Pemeriksaan**

- Pencatatan jadwal dan riwayat kunjungan pasien.
- Pencatatan hasil pemeriksaan berdasarkan indikator yang disepakati dengan pihak klinik.
- Penayangan riwayat pemeriksaan dan perkembangan pasien berdasarkan waktu pencatatan.

**C. Monitoring Aktivitas Mandiri**

- Pembuatan instruksi aktivitas mandiri oleh petugas atau pihak klinik yang berwenang.
- Pengaturan jadwal, frekuensi, tanggal mulai, dan periode aktivitas.
- Pembaruan dan pembatalan instruksi aktivitas.
- Penayangan instruksi dan jadwal kepada pasien melalui aplikasi mobile.
- Pengiriman laporan pelaksanaan aktivitas oleh pasien.
- Penayangan laporan dan status aktivitas kepada petugas.
- Penayangan ringkasan instruksi aktif dan riwayat laporan pada dashboard pasien.

**D. Event-Driven Architecture**

- Penerbitan event ketika terjadi perubahan bisnis yang relevan, seperti instruksi dibuat, diperbarui, dibatalkan, dan laporan diterima.
- Penerimaan dan pemrosesan event oleh komponen sistem.
- Pengelolaan konsistensi antara penyimpanan data dan penerbitan event.
- Penerapan mekanisme idempotensi untuk mencegah efek bisnis ganda akibat pemrosesan event berulang.

**E. Durable Workflow Orchestration**

- Inisialisasi workflow Temporal berdasarkan instruksi aktivitas yang telah disimpan.
- Pengelolaan timer dan jadwal pengingat.
- Pengelolaan waktu tunggu laporan pasien.
- Penerimaan laporan pasien sebagai pemicu kelanjutan workflow.
- Penyesuaian workflow ketika instruksi diperbarui.
- Pembatalan workflow ketika instruksi dibatalkan.
- Retry untuk aktivitas teknis yang gagal sesuai kebijakan.
- Pemulihan workflow setelah worker atau layanan terkait mengalami gangguan.

**F. Pengujian dan Evaluasi**

- Pengujian fungsional aplikasi.
- Pengujian penerbitan dan pemrosesan event.
- Pengujian urutan dan transisi workflow.
- Pengujian timer dan pengingat.
- Pengujian laporan, perubahan, dan pembatalan instruksi.
- Pengujian event duplikat dan idempotensi.
- Pengujian retry dan pemulihan workflow.
- Evaluasi komparatif dengan pendekatan workflow konvensional apabila baseline berhasil diimplementasikan.

## 3.2 Out-of-Scope

Hal-hal berikut tidak termasuk dalam ruang lingkup penelitian:

- Diagnosis medis otomatis dan rekomendasi terapi otomatis.
- Artificial Intelligence (AI) dan Machine Learning (ML).
- Pengembangan sistem rekam medis elektronik lengkap atau penggantian seluruh sistem operasional klinik.
- Pengelolaan resep, farmasi, stok obat, pembelian, dan persediaan.
- Pembayaran, kasir, tagihan, klaim, dan akuntansi.
- Integrasi dengan laboratorium, rumah sakit, perangkat medis, smartwatch, atau platform kesehatan eksternal.
- Telekonsultasi video dan layanan konsultasi real-time.
- Penentuan instruksi aktivitas pasien secara otomatis oleh sistem.
- Validasi medis terhadap instrumen pemeriksaan, diagnosis, atau ambang batas klinis.
- Pengambilan keputusan medis oleh sistem.
- Pengembangan infrastruktur microservices berskala besar atau cluster Kubernetes yang tidak diperlukan untuk evaluasi penelitian.

# 4. Stakeholder Analysis

| Stakeholder                    | Peran                                                                                                  | Kepentingan                                                                                | Influence |
| ------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | --------- |
| Pemilik / Pimpinan Klinik      | Pemilik proses dan pihak yang memberikan persetujuan penggunaan sistem serta pelaksanaan penelitian.   | Kesesuaian sistem dengan kebutuhan dan kebijakan klinik.                                   | Tinggi    |
| Petugas Klinik / Operator      | Pengguna aplikasi web untuk mengelola pasien, kunjungan, pemeriksaan, dan instruksi sesuai kewenangan. | Kemudahan pencatatan, pengelolaan jadwal, dan pemantauan laporan.                          | Tinggi    |
| Pasien Umum                    | Penerima layanan yang data dan riwayat kunjungannya dikelola sesuai ruang lingkup sistem.              | Informasi dan riwayat yang akurat serta terlindungi.                                       | Sedang    |
| Pasien Program MHLS            | Pengguna aplikasi mobile untuk melihat instruksi aktivitas dan mengirim laporan pelaksanaan.           | Instruksi yang jelas, pengingat sesuai jadwal, dan kemudahan pelaporan.                    | Sedang    |
| Pihak Klinik Pemberi Instruksi | Pihak yang menetapkan, memperbarui, atau membatalkan instruksi aktivitas sesuai kewenangan klinis.     | Instruksi tercatat dengan benar dan perubahan diterapkan pada proses monitoring.           | Tinggi    |
| Peneliti / Pengembang          | Menganalisis kebutuhan, merancang, membangun, dan menguji sistem.                                      | Kebutuhan dapat diterjemahkan menjadi artefak yang dapat diimplementasikan dan dievaluasi. | Sedang    |
| Dosen Pembimbing / Penguji     | Memberikan arahan dan menilai kelayakan akademik penelitian.                                           | Kesesuaian masalah, solusi, metode, implementasi, dan evaluasi.                            | Tinggi    |

**Catatan:** Pembagian jabatan, jumlah pengguna, dan kewenangan aktual di Klinik DSH perlu dikonfirmasi. Pemetaan ini merupakan rancangan stakeholder berdasarkan konsep sistem, bukan pernyataan bahwa seluruh pihak tersebut telah dipastikan tersedia.

# 5. Functional Requirements (FR)

Prioritas menggunakan metode MoSCoW:

- **Must:** kebutuhan inti yang wajib dipenuhi.
- **Should:** kebutuhan penting yang diimplementasikan setelah fungsi inti.
- **Could:** kebutuhan tambahan apabila waktu dan sumber daya memungkinkan.
- **Won't:** kebutuhan yang tidak dikerjakan dalam ruang lingkup penelitian.

| ID    | Requirement                                                                                                                           | Prioritas |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| FR-01 | Sistem dapat melakukan autentikasi petugas dan pasien sebelum mengakses fitur sesuai hak aksesnya.                                    | Must      |
| FR-02 | Sistem memungkinkan petugas membuat dan mengelola akun pasien; pasien tidak melakukan pendaftaran mandiri.                            | Must      |
| FR-03 | Sistem dapat menambah, melihat, memperbarui, mencari, dan mengelola data pasien.                                                      | Must      |
| FR-04 | Sistem dapat mencatat kategori pasien umum dan peserta program MHLS sesuai ketentuan klinik.                                          | Must      |
| FR-05 | Sistem dapat mencatat jadwal dan riwayat kunjungan pasien.                                                                            | Should    |
| FR-06 | Sistem dapat mencatat hasil pemeriksaan berdasarkan indikator yang disepakati dengan pihak klinik.                                    | Should    |
| FR-07 | Sistem dapat menampilkan riwayat perkembangan dan hasil pemeriksaan pasien berdasarkan waktu pencatatan.                              | Should    |
| FR-08 | Petugas atau pihak yang berwenang dapat membuat instruksi aktivitas mandiri untuk pasien MHLS.                                        | Must      |
| FR-09 | Sistem dapat menyimpan jadwal, frekuensi, tanggal mulai, dan periode aktivitas sesuai instruksi yang diberikan.                       | Must      |
| FR-10 | Petugas atau pihak yang berwenang dapat memperbarui isi maupun jadwal instruksi aktivitas.                                            | Must      |
| FR-11 | Petugas atau pihak yang berwenang dapat membatalkan instruksi aktivitas yang sedang berlaku.                                          | Must      |
| FR-12 | Pasien dapat melihat instruksi aktivitas yang aktif beserta jadwal dan keterangannya melalui aplikasi mobile.                         | Must      |
| FR-13 | Sistem dapat memicu pengingat berdasarkan jadwal instruksi yang masih aktif.                                                          | Must      |
| FR-14 | Pasien dapat mengirim laporan pelaksanaan aktivitas melalui aplikasi mobile.                                                          | Must      |
| FR-15 | Petugas dapat melihat laporan aktivitas pasien beserta waktu pengiriman dan instruksi yang terkait.                                   | Must      |
| FR-16 | Sistem dapat menampilkan status aktivitas, seperti terjadwal, menunggu laporan, dilaporkan, selesai, diperbarui, atau dibatalkan.     | Must      |
| FR-17 | Sistem dapat menampilkan ringkasan instruksi aktif dan riwayat laporan pada dashboard pasien.                                         | Should    |
| FR-18 | Sistem dapat menerbitkan event untuk kejadian bisnis penting, seperti instruksi dibuat, diperbarui, dibatalkan, dan laporan diterima. | Must      |
| FR-19 | Komponen sistem dapat menerima dan memproses event untuk memicu tindakan atau workflow yang sesuai.                                   | Must      |
| FR-20 | Sistem dapat memulai workflow Temporal setelah instruksi berhasil disimpan dan event terkait diproses.                                | Must      |
| FR-21 | Workflow dapat mengelola timer dan waktu tunggu sesuai jadwal serta aturan pelaporan aktivitas.                                       | Must      |
| FR-22 | Sistem dapat meneruskan laporan pasien yang telah tersimpan kepada workflow agar proses dapat berlanjut.                              | Must      |
| FR-23 | Workflow dapat menyesuaikan proses ketika instruksi aktivitas diperbarui.                                                             | Must      |
| FR-24 | Workflow dapat dihentikan atau dibatalkan secara terkendali ketika instruksi aktivitas dibatalkan.                                    | Must      |
| FR-25 | Sistem dapat melakukan retry terhadap aktivitas teknis yang gagal sesuai kebijakan yang ditentukan.                                   | Must      |
| FR-26 | Workflow dapat dilanjutkan setelah worker atau layanan terkait mengalami gangguan dan kembali tersedia.                               | Must      |
| FR-27 | Pengguna berwenang dapat menelusuri status workflow dan informasi kegagalan proses yang relevan.                                      | Should    |
| FR-28 | Sistem dapat mencatat riwayat perubahan instruksi, status, waktu, dan pengguna yang melakukan perubahan.                              | Should    |

## 5.1 Ketentuan Teknis Functional Requirements

1. Data pasien, kunjungan, pemeriksaan, instruksi, dan laporan disimpan pada basis data aplikasi.
2. Event digunakan untuk menyampaikan kejadian bisnis penting antarbagian sistem, bukan menggantikan basis data utama.
3. Penerbitan event perlu dirancang agar tidak terjadi ketidaksesuaian antara transaksi penyimpanan data dan pengiriman event. Salah satu pendekatan yang dapat digunakan adalah transactional outbox.
4. Pemrosesan event dan aktivitas yang dapat diulang perlu dirancang secara idempoten agar event duplikat atau retry tidak menyebabkan efek bisnis ganda.
5. Temporal bertanggung jawab mengelola eksekusi workflow jangka panjang, termasuk timer, waktu tunggu, sinyal laporan pasien, perubahan, pembatalan, dan pemulihan.
6. Pengiriman notifikasi dilakukan melalui aktivitas atau layanan notifikasi yang terintegrasi dengan workflow. Status pemicu notifikasi dibedakan dari status penerimaan notifikasi pada perangkat pasien.
7. Satu instruksi aktivitas dapat memiliki satu workflow utama yang mengelola siklus monitoring instruksi tersebut. Detail implementasi dapat disesuaikan dengan aturan aktivitas yang telah divalidasi.
8. Pembaruan dan pembatalan instruksi harus mempertimbangkan kondisi workflow saat perubahan diterima, termasuk kemungkinan laporan pasien masuk pada waktu yang bersamaan.

# 6. Non-Functional Requirements (NFR)

| Kategori        | Requirement                                                                                                          | Metrik / Kriteria Pengujian                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Performance     | Halaman utama dan fungsi pencatatan memberikan respons yang layak pada lingkungan pengujian.                         | Waktu respons p95 maksimal 3 detik pada beban uji yang ditentukan.                                                                                       |
| Performance     | Pemrosesan event tidak menghambat transaksi utama pencatatan data.                                                   | Latensi pemrosesan event p95 dicatat dan dievaluasi pada lingkungan pengujian normal.                                                                    |
| Performance     | Sistem mampu menangani jumlah pengguna dan workflow sesuai skala prototipe.                                          | Beban uji awal dapat menggunakan hingga 20 pengguna bersamaan dan 50 workflow aktif; angka ini merupakan profil uji, bukan kapasitas operasional klinik. |
| Security        | Sistem mewajibkan autentikasi dan otorisasi sesuai peran pengguna.                                                   | Seluruh skenario pengujian autentikasi dan hak akses yang ditetapkan berhasil.                                                                           |
| Security        | Pasien hanya dapat mengakses data miliknya sendiri.                                                                  | Seluruh skenario pengujian akses tidak sah ditolak.                                                                                                      |
| Security        | Komunikasi aplikasi dan server menggunakan koneksi terenkripsi pada lingkungan deployment.                           | HTTPS/TLS aktif pada lingkungan deployment.                                                                                                              |
| Security        | Kredensial dan informasi rahasia tidak disimpan dalam kode sumber atau log.                                          | Tidak ditemukan kredensial atau informasi rahasia pada pemeriksaan konfigurasi dan log.                                                                  |
| Security        | Perubahan penting dapat ditelusuri melalui audit log.                                                                | Perubahan penting mencatat identitas pengguna, waktu, dan jenis perubahan.                                                                               |
| Usability       | Antarmuka petugas menggunakan istilah sesuai proses klinik dan menyediakan validasi input.                           | Skenario tugas utama dapat diselesaikan oleh pengguna uji tanpa kesalahan kritis.                                                                        |
| Usability       | Pasien dapat melihat instruksi dan mengirim laporan melalui antarmuka mobile.                                        | Minimal 90% skenario tugas utama berhasil diselesaikan oleh pengguna uji.                                                                                |
| Usability       | Sistem menampilkan pesan kesalahan dan status proses yang dapat dipahami pengguna.                                   | Seluruh skenario kesalahan utama memiliki pesan dan status yang sesuai.                                                                                  |
| Reliability     | Workflow mempertahankan riwayat dan status eksekusi melalui mekanisme durable execution Temporal.                    | Seluruh skenario penghentian dan pemulihan worker yang ditetapkan berhasil.                                                                              |
| Reliability     | Kegagalan pemrosesan event dapat dideteksi dan ditangani melalui retry atau mekanisme error handling yang dirancang. | Seluruh skenario kegagalan event yang ditetapkan memiliki hasil penanganan yang dapat ditelusuri.                                                        |
| Reliability     | Pemrosesan event dan aktivitas yang dapat diulang dirancang idempoten.                                               | Event duplikat tidak menghasilkan efek bisnis ganda pada skenario pengujian.                                                                             |
| Reliability     | Sistem memiliki prosedur pencadangan dan pemulihan basis data.                                                       | Prosedur backup dan restore didokumentasikan dan diuji pada lingkungan deployment.                                                                       |
| Reliability     | Kegagalan layanan notifikasi tercatat dan tidak dianggap berhasil tanpa status yang sesuai.                          | Status pengiriman, kegagalan, dan hasil retry dapat ditelusuri melalui log sistem.                                                                       |
| Maintainability | Kode aplikasi, event, dan workflow memiliki struktur serta dokumentasi yang mendukung pemeliharaan.                  | Struktur proyek, kontrak event, konfigurasi, dan alur workflow terdokumentasi.                                                                           |
| Maintainability | Perubahan kode workflow tidak menyebabkan kegagalan replay pada workflow aktif.                                      | Skenario kompatibilitas workflow diuji ketika terdapat perubahan kode yang memengaruhi workflow berjalan.                                                |

**Catatan NFR:**

- Target performa dan usability merupakan target awal untuk prototipe penelitian.
- Hasil pengujian harus menyertakan spesifikasi perangkat, konfigurasi infrastruktur, jumlah pengguna uji, dan kondisi pengujian.
- Pemulihan workflow tidak berarti seluruh layanan eksternal otomatis pulih. Misalnya, kegagalan layanan notifikasi tetap membutuhkan penanganan dan retry tersendiri.
- Temporal Workflow harus mengikuti ketentuan determinisme dan kompatibilitas replay. Strategi versioning digunakan apabila terdapat perubahan kode yang berpotensi memengaruhi workflow yang masih berjalan, sesuai SDK dan strategi deployment yang digunakan.
- Pengujian reliability harus membedakan keberhasilan pemulihan workflow, keberhasilan aktivitas eksternal, dan keberhasilan efek bisnis.

# 7. Business Process As-Is vs To-Be

## 7.1 As-Is (Kondisi Saat Ini)

Berdasarkan informasi awal, Klinik DSH masih menggunakan Microsoft Excel untuk melakukan pencatatan data pasien dan hasil pemeriksaan. Pasien menjalani kunjungan dan pemeriksaan sesuai proses klinik. Pada pasien program MHLS, monitoring juga dapat melibatkan aktivitas mandiri berdasarkan instruksi pihak klinik.

Aktivitas mandiri tersebut dapat memiliki jadwal, frekuensi, dan periode yang berbeda. Pasien perlu melaksanakan aktivitas sesuai instruksi dan menyampaikan laporan pelaksanaannya. Instruksi dapat berubah atau dibatalkan sesuai kebutuhan.

Namun, detail mengenai cara pemberian instruksi, pengiriman pengingat, penerimaan laporan, penanganan pasien yang belum melapor, dan pencatatan perubahan belum dikonfirmasi secara menyeluruh. Oleh karena itu, kondisi As-Is pada dokumen ini masih merupakan gambaran awal dan harus divalidasi melalui wawancara serta observasi.

## 7.2 To-Be (Kondisi yang Diusulkan)

Petugas mengelola data pasien, kunjungan, hasil pemeriksaan, dan instruksi aktivitas melalui aplikasi web. Pasien menggunakan aplikasi mobile untuk melihat instruksi dan mengirim laporan pelaksanaan aktivitas.

Ketika instruksi aktivitas dibuat, backend menyimpan data ke basis data. Setelah transaksi berhasil, sistem menerbitkan event yang mewakili kejadian pembuatan instruksi. Komponen penerima event memproses kejadian tersebut dan memulai workflow Temporal berdasarkan identitas instruksi.

Workflow mengelola jadwal dan waktu tunggu sesuai aturan aktivitas. Ketika waktu pengingat tercapai, workflow menjalankan aktivitas pengiriman notifikasi. Pasien kemudian dapat melihat instruksi dan menyampaikan laporan melalui aplikasi mobile.

Ketika laporan diterima, backend memvalidasi dan menyimpan laporan ke basis data. Setelah laporan tersimpan, sistem meneruskan informasi laporan kepada workflow melalui mekanisme komunikasi yang sesuai, sehingga workflow dapat melanjutkan tahapan berikutnya.

Jika instruksi diperbarui, sistem menyampaikan perubahan tersebut agar workflow menyesuaikan jadwal atau proses yang masih berlaku. Jika instruksi dibatalkan, workflow dihentikan atau dibatalkan secara terkendali berdasarkan aturan yang telah ditentukan.

Apabila worker mengalami gangguan, Temporal dapat melanjutkan eksekusi workflow berdasarkan riwayat eksekusi yang tersimpan ketika worker kembali tersedia. Petugas dapat meninjau data monitoring, laporan, perubahan instruksi, dan status workflow sesuai hak akses.

## 7.3 Alur Utama To-Be

1. Petugas membuat instruksi aktivitas pasien melalui aplikasi web.
2. Backend menyimpan instruksi ke basis data.
3. Sistem menerbitkan event setelah transaksi penyimpanan berhasil.
4. Consumer menerima event dan memulai workflow Temporal.
5. Workflow mengatur timer berdasarkan jadwal aktivitas.
6. Ketika jadwal tercapai, workflow menjalankan aktivitas pengiriman pengingat.
7. Pasien melihat instruksi dan mengirim laporan melalui aplikasi mobile.
8. Backend menyimpan laporan dan meneruskan informasi laporan kepada workflow.
9. Workflow melanjutkan proses sesuai aturan aktivitas.
10. Jika instruksi berubah atau dibatalkan, sistem menyampaikan perubahan kepada workflow.
11. Jika terjadi gangguan pada worker, workflow dapat dilanjutkan setelah worker tersedia kembali.
12. Petugas meninjau riwayat monitoring dan status aktivitas pasien.

## 7.4 Perbandingan As-Is dan To-Be

| Aspek                  | As-Is                                                                                   | To-Be                                                                                                            |
| ---------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Pengelolaan data       | Informasi awal menyebut pencatatan data pasien dan hasil pemeriksaan menggunakan Excel. | Data pasien, kunjungan, pemeriksaan, instruksi, dan laporan dikelola melalui aplikasi.                           |
| Instruksi aktivitas    | Prosedur aktual pemberian dan pencatatan instruksi masih perlu dikonfirmasi.            | Instruksi aktivitas dibuat dan dikelola melalui aplikasi web oleh pihak berwenang.                               |
| Jadwal aktivitas       | Mekanisme pengelolaan jadwal aktual perlu dikonfirmasi.                                 | Jadwal, frekuensi, dan periode aktivitas dikelola secara terstruktur.                                            |
| Pengingat              | Mekanisme pengingat aktual perlu dikonfirmasi.                                          | Pengingat dipicu berdasarkan jadwal instruksi aktif melalui workflow.                                            |
| Pelaporan              | Media dan prosedur pelaporan aktivitas pasien masih perlu dikonfirmasi.                 | Pasien mengirim laporan melalui aplikasi mobile.                                                                 |
| Perubahan instruksi    | Prosedur perubahan atau pembatalan instruksi aktual perlu dikonfirmasi.                 | Perubahan instruksi diterapkan pada data dan workflow terkait.                                                   |
| Keberlangsungan proses | Mekanisme pemulihan proses aktual perlu dikonfirmasi.                                   | Temporal mengelola eksekusi workflow agar dapat dilanjutkan setelah gangguan sesuai mekanisme durable execution. |
| Penelusuran            | Penelusuran informasi bergantung pada dokumen dan proses yang digunakan saat ini.       | Riwayat data, laporan, perubahan, dan status workflow dapat ditelusuri sesuai hak akses.                         |

# 8. Assumptions & Constraints

## 8.1 Assumptions

| ID     | Asumsi                                                                                                                                                                                                                    |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ASM-01 | Klinik bersedia menjadi objek penelitian dan memberikan izin untuk pengumpulan kebutuhan, wawancara, observasi, serta validasi proses.                                                                                    |
| ASM-02 | Petugas klinik menjadi pengguna utama aplikasi web. Jumlah petugas dan pembagian tugas mengikuti hasil konfirmasi pihak klinik.                                                                                           |
| ASM-03 | Akun pasien dibuat oleh petugas, bukan melalui pendaftaran mandiri.                                                                                                                                                       |
| ASM-04 | Sebagian pasien, khususnya peserta program MHLS, memiliki instruksi aktivitas mandiri yang perlu dipantau. Jenis dan cakupan aktivitas disesuaikan dengan proses yang dikonfirmasi oleh klinik.                           |
| ASM-05 | Jadwal, frekuensi, dan periode aktivitas dapat berbeda antar-instruksi atau pasien.                                                                                                                                       |
| ASM-06 | Pasien dapat menggunakan aplikasi mobile untuk melihat instruksi dan mengirim laporan aktivitas.                                                                                                                          |
| ASM-07 | Instruksi aktivitas dapat diperbarui atau dibatalkan oleh pihak klinik yang berwenang.                                                                                                                                    |
| ASM-08 | Klinik memberikan persetujuan atas data yang digunakan untuk analisis dan pengujian. Jika izin penggunaan data nyata tidak tersedia, pengujian menggunakan data sintetis atau data anonim sesuai persetujuan.             |
| ASM-09 | Pengiriman pengingat dilakukan melalui notifikasi aplikasi mobile. Keberhasilan penerimaan notifikasi bergantung pada koneksi jaringan, izin notifikasi perangkat, dan layanan pengiriman yang digunakan.                 |
| ASM-10 | Pihak klinik memberikan definisi indikator pemeriksaan, aturan aktivitas, dan ketentuan pelaporan yang digunakan dalam sistem.                                                                                            |
| ASM-11 | Proses monitoring yang dipilih memiliki tahapan atau waktu tunggu yang cukup untuk dievaluasi menggunakan durable workflow orchestration. Asumsi ini harus dibuktikan melalui validasi proses sebelum implementasi final. |

## 8.2 Constraints

| ID     | Batasan                                                                                                                                                                                                      |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CON-01 | Penelitian berfokus pada monitoring perkembangan pasien dan aktivitas tindak lanjut, bukan seluruh sistem operasional klinik.                                                                                |
| CON-02 | Sistem tidak memberikan diagnosis atau keputusan terapi otomatis.                                                                                                                                            |
| CON-03 | Informasi proses bisnis yang belum diverifikasi tidak boleh dianggap sebagai fakta final.                                                                                                                    |
| CON-04 | Penggunaan data pasien nyata bergantung pada izin klinik dan ketentuan perlindungan data yang berlaku.                                                                                                       |
| CON-05 | Keberhasilan durable workflow bergantung pada implementasi, konfigurasi, infrastruktur, dan integrasi. Temporal tidak menghilangkan seluruh kemungkinan kegagalan sistem.                                    |
| CON-06 | Keberhasilan pemicu workflow tidak otomatis menjamin notifikasi diterima perangkat pasien karena pengiriman bergantung pada layanan dan jaringan yang digunakan.                                             |
| CON-07 | Waktu, biaya, kapasitas pengembangan, dan infrastruktur penelitian terbatas. Implementasi diprioritaskan pada kebutuhan inti dan satu alur monitoring aktivitas mandiri pasien sebagai alur utama pengujian. |
| CON-08 | Pengembangan sistem dilakukan menggunakan pendekatan Incremental Development sehingga fitur dibangun dan diuji secara bertahap.                                                                              |
| CON-09 | Penelitian menggunakan pendekatan Design Science Research (DSR) untuk merancang, membangun, dan mengevaluasi artefak sistem.                                                                                 |
| CON-10 | Arsitektur sistem dapat menggunakan backend modular dengan komunikasi berbasis event dan Temporal tanpa mewajibkan penerapan microservices secara terpisah.                                                  |
| CON-11 | Evaluasi komparatif dengan pendekatan konvensional bergantung pada ketersediaan waktu untuk membangun baseline dan menjalankan skenario pengujian yang setara.                                               |

# 9. Risk Register

| ID   | Risiko                                                                                         | Probabilitas  | Dampak | Mitigasi                                                                                                                                    |
| ---- | ---------------------------------------------------------------------------------------------- | ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| R-01 | Proses bisnis aktual berbeda dari informasi awal.                                              | Sedang        | Tinggi | Melakukan wawancara dan observasi serta memvalidasi alur As-Is sebelum kebutuhan ditetapkan.                                                |
| R-02 | Izin akses data pasien atau hasil pemeriksaan tidak diperoleh.                                 | Sedang        | Tinggi | Mengajukan izin sejak awal; menyiapkan data sintetis atau anonim dan membatasi penggunaan data sesuai persetujuan.                          |
| R-03 | Pasien tidak rutin membuka aplikasi atau mengirim laporan.                                     | Sedang        | Sedang | Merancang alur pelaporan sederhana dan memvalidasi kebutuhan pengingat serta tindak lanjut dengan pihak klinik.                             |
| R-04 | Instruksi berubah ketika workflow sedang berjalan.                                             | Sedang        | Tinggi | Mendefinisikan aturan pembaruan, pembatalan, dan versi instruksi; menguji perubahan ketika workflow aktif.                                  |
| R-05 | Event gagal diterbitkan atau diproses.                                                         | Sedang        | Tinggi | Menggunakan transactional outbox atau mekanisme setara, retry, pencatatan status, dan pemantauan event.                                     |
| R-06 | Event yang sama diproses lebih dari satu kali.                                                 | Sedang        | Sedang | Menerapkan idempotency key dan pemeriksaan status agar efek bisnis tidak terduplikasi.                                                      |
| R-07 | Worker atau layanan Temporal berhenti ketika workflow berjalan.                                | Sedang        | Tinggi | Menggunakan durable execution, konfigurasi deployment yang tepat, monitoring, dan pengujian pemulihan worker.                               |
| R-08 | Layanan notifikasi eksternal mengalami gangguan.                                               | Sedang        | Sedang | Mencatat status pengiriman, menerapkan retry yang sesuai, dan menyediakan penanganan kegagalan notifikasi.                                  |
| R-09 | Data pasien diakses oleh pengguna yang tidak berwenang.                                        | Rendah–Sedang | Tinggi | Menerapkan autentikasi, otorisasi, pembatasan akses pasien, enkripsi koneksi, dan audit log.                                                |
| R-10 | Data pemeriksaan atau laporan pasien tidak lengkap atau salah input.                           | Sedang        | Tinggi | Menerapkan validasi input, penanda data kosong, dan riwayat perubahan.                                                                      |
| R-11 | Integrasi EDA dan Temporal melebihi waktu penelitian.                                          | Sedang        | Tinggi | Mengembangkan sistem secara incremental, dimulai dari satu alur aktivitas inti, dan memprioritaskan kebutuhan Must.                         |
| R-12 | Infrastruktur pengembangan atau deployment tidak stabil.                                       | Sedang        | Sedang | Menyiapkan lingkungan uji, backup konfigurasi, dokumentasi deployment, dan prosedur pemulihan.                                              |
| R-13 | Target kinerja ditentukan tanpa baseline yang memadai.                                         | Sedang        | Sedang | Menetapkan profil beban pengujian dan metrik sejak awal serta membedakan target prototipe dari kondisi operasional klinik.                  |
| R-14 | Pengguna kesulitan beradaptasi dengan aplikasi baru.                                           | Sedang        | Sedang | Melibatkan calon pengguna dalam validasi prototipe, menyediakan panduan, dan melakukan uji tugas.                                           |
| R-15 | Jadwal pengingat tidak sesuai akibat perubahan instruksi atau perbedaan waktu pemrosesan.      | Sedang        | Tinggi | Menyimpan jadwal dan zona waktu secara konsisten, menyinkronkan perubahan dengan workflow, serta menguji perubahan jadwal.                  |
| R-16 | Laporan pasien diterima lebih dari satu kali atau tidak terhubung dengan instruksi yang benar. | Sedang        | Tinggi | Menggunakan identitas laporan dan instruksi yang unik, memvalidasi relasi data, serta menerapkan idempotensi pada penerimaan laporan.       |
| R-17 | Perubahan kode workflow menyebabkan ketidakcocokan replay pada workflow yang masih berjalan.   | Sedang        | Tinggi | Menerapkan strategi kompatibilitas dan versioning workflow sesuai SDK Temporal serta menguji replay terhadap riwayat workflow yang relevan. |
| R-18 | Proses aktual klinik ternyata tidak membutuhkan workflow jangka panjang yang kompleks.         | Sedang        | Tinggi | Memvalidasi tahapan, waktu tunggu, perubahan, dan kebutuhan pemulihan sebelum menetapkan Temporal sebagai teknologi utama penelitian.       |

# 10. Acceptance Criteria

## 10.1 Kriteria Penerimaan

Sistem dinyatakan **BERHASIL** apabila:

**A. Pengelolaan Data**

- Petugas dapat login dan mengelola data pasien sesuai hak akses.
- Petugas dapat mencatat kunjungan dan hasil pemeriksaan sesuai indikator yang disepakati.
- Riwayat perkembangan pasien dapat ditampilkan berdasarkan data yang tersimpan.

**B. Monitoring Aktivitas**

- Petugas dapat membuat instruksi aktivitas mandiri pasien.
- Petugas dapat mengatur jadwal, frekuensi, tanggal mulai, dan periode aktivitas.
- Pasien dapat melihat instruksi aktif melalui aplikasi mobile.
- Pasien dapat mengirim laporan pelaksanaan aktivitas.
- Petugas dapat melihat laporan yang terkait dengan instruksi pasien.
- Status aktivitas dapat berubah sesuai tahapan proses yang ditetapkan.

**C. Event-Driven Architecture**

- Event penting dapat diterbitkan setelah perubahan data berhasil disimpan.
- Consumer dapat menerima dan memproses event sesuai kontrak yang ditetapkan.
- Event duplikat tidak menghasilkan efek bisnis ganda pada skenario pengujian.
- Kegagalan penerbitan atau pemrosesan event dapat dideteksi dan ditangani sesuai rancangan.

**D. Durable Workflow Orchestration**

- Workflow Temporal dapat dimulai berdasarkan instruksi aktivitas yang berhasil disimpan.
- Workflow dapat mengelola timer dan waktu tunggu laporan pasien.
- Laporan yang telah disimpan dapat diteruskan kepada workflow agar proses berlanjut.
- Perubahan instruksi dapat diterapkan pada workflow yang sedang berjalan.
- Pembatalan instruksi dapat menghentikan tahapan workflow terkait secara terkendali.
- Retry aktivitas teknis berjalan sesuai kebijakan yang ditentukan.
- Workflow dapat dilanjutkan setelah worker dihentikan dan dijalankan kembali sesuai skenario pengujian.

**E. Keamanan dan Penelusuran**

- Pasien hanya dapat mengakses data miliknya sendiri.
- Petugas hanya dapat mengakses fungsi sesuai hak akses.
- Riwayat instruksi, laporan, dan perubahan dapat ditelusuri.
- Status kegagalan workflow dan informasi teknis yang relevan dapat diperiksa oleh pengguna berwenang.

**F. Evaluasi**

- Seluruh skenario pengujian prioritas Must telah dijalankan dan hasilnya terdokumentasi.
- Target NFR yang telah ditetapkan dievaluasi pada lingkungan pengujian yang didokumentasikan.
- Jika evaluasi komparatif dilaksanakan, kedua pendekatan diuji menggunakan skenario dan kondisi pengujian yang setara.

## 10.2 Skenario Pengujian Utama

| ID    | Skenario                                                          | Hasil yang Diharapkan                                                                                                     |
| ----- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| TC-01 | Petugas membuat instruksi aktivitas baru.                         | Data tersimpan dan event pembuatan instruksi diproses hingga workflow dimulai.                                            |
| TC-02 | Workflow mencapai waktu pengingat.                                | Aktivitas pengiriman notifikasi dipicu sesuai jadwal yang dikonfigurasi.                                                  |
| TC-03 | Pasien mengirim laporan aktivitas.                                | Laporan tersimpan, terhubung dengan instruksi, dan diteruskan kepada workflow.                                            |
| TC-04 | Worker dihentikan ketika workflow sedang menunggu.                | Workflow dapat dilanjutkan setelah worker tersedia kembali tanpa kehilangan state workflow yang telah tercatat.           |
| TC-05 | Event instruksi yang sama diproses lebih dari satu kali.          | Tidak terjadi efek bisnis ganda.                                                                                          |
| TC-06 | Petugas memperbarui jadwal instruksi yang masih aktif.            | Data instruksi diperbarui dan workflow menyesuaikan jadwal berdasarkan aturan perubahan.                                  |
| TC-07 | Petugas membatalkan instruksi yang masih aktif.                   | Instruksi berubah menjadi dibatalkan dan workflow tidak menjalankan tahapan berikutnya yang sudah tidak berlaku.          |
| TC-08 | Aktivitas pengiriman notifikasi mengalami kegagalan.              | Kegagalan tercatat dan retry atau penanganan lanjutan berjalan sesuai kebijakan.                                          |
| TC-09 | Laporan pasien dan perubahan instruksi terjadi hampir bersamaan.  | Sistem menerapkan aturan konsistensi sehingga laporan dan perubahan diproses tanpa menghasilkan status yang bertentangan. |
| TC-10 | Kode workflow mengalami perubahan ketika terdapat workflow aktif. | Workflow yang masih berjalan tetap dapat diproses sesuai strategi kompatibilitas dan versioning yang diterapkan.          |

## 10.3 Kriteria Belum Diterima

Sistem dinyatakan **GAGAL / BELUM DITERIMA** apabila:

- Fungsi inti pengelolaan pasien, instruksi, atau laporan tidak berjalan sesuai kebutuhan yang telah disetujui.
- Pasien dapat mengakses data pasien lain atau pengguna dapat mengakses fungsi di luar kewenangannya.
- Event penting hilang atau tidak diproses tanpa mekanisme deteksi dan penanganan yang dirancang.
- Perubahan atau pembatalan instruksi tidak diterapkan pada workflow terkait sehingga proses yang tidak berlaku tetap dijalankan.
- Workflow tidak dapat dilanjutkan pada skenario pemulihan yang telah ditetapkan.
- Pemrosesan berulang menyebabkan pencatatan atau efek bisnis ganda yang tidak ditangani.
- Pengingat tidak mengikuti jadwal instruksi aktif pada skenario pengujian yang telah ditetapkan.
- Terdapat kegagalan kritis pada skenario prioritas Must yang belum diperbaiki atau belum mendapat persetujuan pengecualian.

## 10.4 Pihak yang Memvalidasi

- Pemilik atau pimpinan Klinik DSH sebagai pihak yang memberikan persetujuan kebutuhan dan penggunaan sistem.
- Perwakilan petugas atau pihak klinik yang ditunjuk untuk memvalidasi kesesuaian proses dan kebutuhan pengguna.
- Dosen pembimbing untuk kesesuaian akademik dan metodologi penelitian.

Tanggal validasi ditentukan ketika pelaksanaan wawancara, validasi kebutuhan, dan penerimaan sistem.

---

# Catatan Akhir Pengembangan BRD

BRD ini menjadi dasar pengembangan artefak penelitian dengan pendekatan **Design Science Research (DSR)** dan model pengembangan perangkat lunak **Incremental Development**.

Implementasi diprioritaskan pada satu alur utama:

**Pembuatan instruksi → penerbitan event → inisialisasi Temporal Workflow → timer dan pengingat → laporan pasien → kelanjutan workflow → perubahan atau pembatalan instruksi.**

Alur tersebut menjadi fokus utama demonstrasi dan evaluasi teknis EDA serta Durable Workflow Orchestration.

Fitur pengelolaan pasien, kunjungan, pemeriksaan, dan dashboard berfungsi sebagai pendukung sistem monitoring. Keberhasilan penelitian tidak hanya dinilai dari tersedianya fitur aplikasi, tetapi juga dari kemampuan sistem menangani proses yang berlangsung dalam jangka waktu tertentu, menerima perubahan, menangani kegagalan, dan melanjutkan workflow berdasarkan state yang tersimpan.

Sebelum BRD ditetapkan sebagai dokumen final, proses As-Is, peran pengguna, jenis aktivitas MHLS, aturan pelaporan, serta kebutuhan pengingat dan perubahan instruksi harus divalidasi dengan pihak Klinik DSH.
