## **1. Kerangka PICOS**

| Komponen                              | Formulasi                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **P – Platform / Target User**        | Sistem informasi monitoring perkembangan pasien berbasis web dan mobile. Pengguna sistem terdiri atas admin klinik yang mengelola data dan proses monitoring, serta pasien yang mengakses informasi, melihat instruksi aktivitas mandiri, dan mengirimkan laporan perkembangan.                                                                                                                                                    |
| **I – Intervention / Metode**         | Implementasi Event-Driven Architecture untuk komunikasi antarkomponen sistem berbasis event serta Durable Workflow Orchestration menggunakan Temporal untuk mengelola workflow monitoring aktivitas mandiri pasien MHLS yang berlangsung dalam jangka waktu tertentu. Workflow mencakup penjadwalan, timer, waktu tunggu laporan pasien, perubahan instruksi, pembatalan, retry, dan pemulihan proses.                             |
| **C – Comparison / Baseline**         | Tidak menetapkan metode pembanding eksperimental secara khusus. Sistem dan mekanisme yang berjalan secara konvensional, seperti pengelolaan proses secara manual atau workflow tanpa mekanisme persistensi dan pemulihan, dapat digunakan sebagai konteks analisis kebutuhan dan pembahasan. Penelitian tidak berfokus pada perbandingan performa Temporal dengan teknologi workflow lainnya.                                      |
| **O – Outcome / Metrik Evaluasi**     | Keberhasilan implementasi komunikasi event, ketepatan transisi workflow, pelaksanaan timer dan aktivitas terjadwal, penanganan perubahan dan pembatalan instruksi, pencegahan efek pemrosesan ganda, serta kemampuan melanjutkan workflow setelah worker mengalami gangguan. Evaluasi juga mencakup kesesuaian fungsi sistem melalui pengujian fungsional dan integrasi, serta usability menggunakan System Usability Scale (SUS). |
| **S – Subject / Subjek Domain Kasus** | Proses monitoring perkembangan pasien pada layanan kesehatan holistik, khususnya pasien yang mengikuti program Moslem Healthy Lifestyle (MHLS) di Klinik Darus Syifa Holistik (DSH), dengan fokus pada monitoring aktivitas mandiri pasien.                                                                                                                                                                                        |

**Catatan:** Dalam PICOS ini, komponen C tidak harus berupa algoritma atau sistem pembanding. Karena penelitian berorientasi pada implementasi dan evaluasi artefak, pembanding eksperimental tidak menjadi keharusan. Namun, kondisi proses yang berjalan saat ini tetap perlu dikaji sebagai dasar kebutuhan sistem.

## **2. Research Questions (RQ)**

Ketiga RQ berikut disusun agar berurutan dari identifikasi kebutuhan, implementasi solusi, hingga evaluasi hasil implementasi.

### **RQ 1.1 – Kebutuhan dan Karakteristik Sistem**

**Apa saja kebutuhan fungsional, karakteristik proses, dan kebutuhan pengelolaan data dalam sistem monitoring perkembangan pasien yang melibatkan aktivitas mandiri, penjadwalan, pelaporan pasien, serta perubahan proses monitoring?**

Fokus kajian:

- Kebutuhan admin dan pasien dalam proses monitoring.
- Karakteristik workflow yang memiliki tahapan, jadwal, waktu tunggu, dan respons pasien.
- Kebutuhan pengelolaan instruksi aktivitas mandiri, laporan perkembangan, serta riwayat monitoring.
- Potensi kondisi seperti keterlambatan laporan, perubahan instruksi, pembatalan aktivitas, dan gangguan teknis.

### **RQ 1.2 – Implementasi Teknis dan Proses Bisnis**

**Bagaimana Event-Driven Architecture dan Durable Workflow Orchestration menggunakan Temporal diimplementasikan untuk mengelola komunikasi antarkomponen serta workflow monitoring aktivitas mandiri pasien MHLS yang berlangsung dalam jangka waktu tertentu?**

Fokus kajian:

- Penerapan komunikasi antarkomponen berbasis event.
- Integrasi event dengan workflow Temporal.
- Pengelolaan timer, waktu tunggu laporan, dan respons pasien.
- Penanganan perubahan serta pembatalan instruksi.
- Penerapan retry, idempotency, dan pemulihan workflow ketika terjadi gangguan.

### **RQ 1.3 – Evaluasi Implementasi dan Usability**

**Bagaimana hasil evaluasi implementasi sistem dalam memenuhi kebutuhan fungsional dan keandalan workflow monitoring, serta bagaimana tingkat usability sistem berdasarkan penilaian pengguna?**

Fokus kajian:

- Pengujian fungsional pada fitur utama sistem.
- Pengujian integrasi komunikasi event dan workflow.
- Pengujian skenario timer, keterlambatan laporan, perubahan instruksi, pembatalan, event duplikat, retry, dan pemulihan workflow.
- Evaluasi usability menggunakan System Usability Scale (SUS).

## **3. Keterkaitan PICOS dan Research Questions**

| RQ     | Komponen PICOS yang dominan | Hasil yang diharapkan                                                     |
| ------ | --------------------------- | ------------------------------------------------------------------------- |
| RQ 1.1 | P dan S                     | Daftar kebutuhan sistem dan karakteristik workflow monitoring pasien.     |
| RQ 1.2 | I                           | Rancangan dan implementasi integrasi EDA dengan Temporal.                 |
| RQ 1.3 | O                           | Hasil pengujian fungsional, integrasi, keandalan workflow, dan usability. |

## **4. Penegasan Batas Penelitian**

Agar ruang lingkup penelitian tidak melebar, terdapat tiga batasan yang perlu dipertahankan:

1. **Cakupan sistem:** Sistem tetap menyediakan pengelolaan pasien, kunjungan, pemeriksaan, instruksi aktivitas mandiri, laporan, dan dashboard perkembangan pasien.
2. **Cakupan EDA dan Temporal:** EDA digunakan untuk komunikasi antarkomponen, sedangkan Temporal secara khusus mengelola workflow jangka panjang pada monitoring aktivitas mandiri pasien MHLS. Temporal tidak digunakan untuk mengelola seluruh operasional klinik.
3. **Cakupan evaluasi:** Penelitian mengevaluasi keberhasilan implementasi dan perilaku sistem melalui skenario pengujian, serta usability melalui SUS. Penelitian tidak mengklaim bahwa Temporal lebih unggul daripada teknologi workflow lain karena tidak melakukan pengujian komparatif.

