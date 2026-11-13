# SYSTEMATIC LITERATURE REVIEW (SLR)

## Implementasi Event-Driven Architecture dengan Durable Workflow Orchestration Menggunakan Temporal pada Sistem Monitoring Perkembangan Pasien

Rentang publikasi: 2021–2026\
Pedoman pelaporan: PRISMA 2020\
Status dokumen: Protokol SLR dan sintesis literatur awal\
Jumlah studi utama yang menjadi fokus telaah awal: 12 paper

# 1. Research Questions (RQ SLR)

## 1.1 Kerangka PICOS

| Elemen           | Definisi                                                                                                                                                                                                                                                                   |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Population (P)   | Sistem informasi kesehatan atau digital health yang mendukung monitoring pasien, aktivitas mandiri, kunjungan, pemeriksaan, pelaporan perkembangan, dan tindak lanjut pasien.                                                                                              |
| Intervention (I) | Event-Driven Architecture (EDA), event-based communication, workflow orchestration, dan durable execution. Temporal menjadi teknologi utama yang akan diterapkan, sedangkan penelitian tentang workflow engine lain digunakan sebagai pembanding konseptual maupun teknis. |
| Comparison (C)   | Proses manual atau konvensional, komunikasi sistem secara sinkron, workflow tanpa durable execution, atau perbandingan antar-workflow engine. Perbandingan tidak harus tersedia pada setiap penelitian.                                                                    |
| Outcomes (O)     | Keberhasilan pemrosesan event, konsistensi alur proses, pengelolaan timer dan waktu tunggu, penanganan laporan, perubahan dan pembatalan instruksi, retry, pemulihan workflow, serta keterlacakan proses.                                                                  |
| Context (S)      | Sistem monitoring pasien, digital health, sistem informasi klinik, dan sistem terdistribusi yang memiliki proses jangka panjang atau melibatkan interaksi berulang antara sistem dan pengguna.                                                                             |

## 1.2 Pertanyaan Penelitian

RQ disusun untuk menjawab tiga kebutuhan utama penelitian: bagaimana komunikasi berbasis event diterapkan, bagaimana workflow jangka panjang dikelola, dan bagaimana kedua pendekatan tersebut relevan untuk monitoring pasien.

| Kode | Research Question                                                                                                                                                                         | Fokus Analisis                                                                                                          |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| RQ1  | Bagaimana Event-Driven Architecture diterapkan untuk mengelola komunikasi dan integrasi proses pada sistem informasi kesehatan maupun sistem informasi terdistribusi?                     | Pola event, producer-consumer, event broker, event schema, konsistensi, dan observabilitas.                             |
| RQ2  | Bagaimana workflow orchestration dan durable execution digunakan untuk mengelola proses jangka panjang yang melibatkan penjadwalan, waktu tunggu, respons pengguna, dan perubahan proses? | Workflow engine, timer, penyimpanan state, signal/message, retry, update, cancellation, dan recovery.                   |
| RQ3  | Bagaimana penelitian terdahulu mengevaluasi keandalan event-driven system dan workflow orchestration?                                                                                     | Metrik evaluasi, skenario pengujian, keberhasilan pemrosesan, duplikasi event, latensi, dan pemulihan setelah gangguan. |
| RQ4  | Bagaimana temuan penelitian terdahulu dapat menjadi dasar perancangan integrasi EDA dan durable workflow orchestration pada sistem monitoring perkembangan pasien?                        | Kebutuhan monitoring, pengingat, pelaporan mandiri, kesinambungan proses, serta gap penerapan dan evaluasi.             |

Alasan penyusunan RQ: RQ1–RQ3 mengkaji aspek teknis arsitektur dan keandalan sistem. RQ4 menghubungkan temuan teknis tersebut dengan kebutuhan monitoring pasien. Dengan demikian, SLR tidak hanya membahas EDA, Temporal, atau digital health secara terpisah, tetapi mengarahkan sintesisnya pada kebutuhan penelitian.

# 2. Search Strategy

## 2.1 Database dan Sumber Pencarian

Pencarian literatur direncanakan melalui sumber berikut:

| Sumber         | Fokus pencarian                                                                                                       |
| -------------- | --------------------------------------------------------------------------------------------------------------------- |
| Scopus         | Artikel ilmiah tentang EDA, workflow orchestration, reliability, dan digital health.                                  |
| IEEE Xplore    | Penelitian teknis tentang arsitektur sistem, event-driven system, workflow, dan reliability.                          |
| ScienceDirect  | Penelitian tentang sistem terdistribusi, workflow, dan aplikasi digital health.                                       |
| Google Scholar | Penelusuran tambahan, termasuk artikel yang mungkin tidak ditemukan melalui sumber sebelumnya dan penelusuran sitasi. |

Google Scholar digunakan sebagai sumber penelusuran tambahan, bukan disamakan dengan basis data bibliografis terindeks seperti Scopus.

## 2.2 Rentang Tahun dan Bahasa

- Rentang publikasi: 1 Januari 2021–31 Desember 2026, atau sampai tanggal pencarian terakhir jika pencarian dilakukan sebelum akhir tahun.
- Bahasa publikasi: Inggris dan Indonesia.
- Jenis publikasi: artikel jurnal dan prosiding konferensi ilmiah.
- Artikel harus memiliki identitas bibliografis yang dapat diverifikasi.
- Artikel harus menyediakan informasi yang dapat digunakan untuk menjawab setidaknya satu RQ.

Tanggal pencarian terakhir: [Isi berdasarkan tanggal pencarian aktual].

## 2.3 Kelompok Kata Kunci

Kata kunci dikelompokkan berdasarkan empat konsep utama.

| Kelompok                  | Kata kunci                                                                                                           |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Event-Driven Architecture | `"event-driven architecture"`, `"event-based architecture"`, `"event-driven microservices"`, `"event-driven system"` |
| Workflow Orchestration    | `"workflow orchestration"`, `"durable execution"`, `"long-running workflow"`, `"workflow engine"`                    |
| Patient Monitoring        | `"patient monitoring"`, `"patient-reported outcome"`, `"digital health"`, `"clinical workflow"`, `"self-monitoring"` |
| Reliability and Recovery  | `"fault recovery"`, `"failure recovery"`, `"retry"`, `"resilience"`, `"reliability"`, `"process recovery"`           |

## 2.4 Boolean Search String

Pencarian dilakukan melalui beberapa kelompok query. Pemisahan query diperlukan agar penelitian teknis tentang EDA atau workflow tidak terlewat hanya karena tidak menggunakan istilah monitoring pasien, dan sebaliknya.

A. Event-Driven Architecture dan pengelolaan event

```
("event-driven architecture" OR "event-based architecture"
OR "event-driven microservices" OR "event-driven system")
AND
(reliability OR resilience OR "event management"
OR "event consistency" OR "event processing")
```

B. Workflow orchestration dan durable execution

```
("workflow orchestration" OR "durable execution"
OR "durable workflow" OR "long-running workflow"
OR "workflow engine")
AND
(timer OR retry OR recovery OR reliability
OR "fault tolerance" OR "failure handling")
```

C. Event-driven system dan workflow orchestration

```
("event-driven architecture" OR "event-driven system"
OR "event-based communication")
AND
("workflow orchestration" OR "workflow engine"
OR "long-running workflow" OR "durable workflow")
```

D. Patient monitoring dan pelaporan

```
("patient monitoring" OR "self-monitoring"
OR "patient-reported outcome" OR "patient-reported data")
AND
(reminder OR notification OR adherence OR reporting
OR "longitudinal monitoring")
AND
("digital health" OR healthcare OR clinical)
```

E. Temporal dan durable workflow

```
(Temporal OR "durable execution"
OR "durable workflow" OR "workflow orchestration engine")
AND
(timer OR retry OR recovery OR "long-running process"
OR "fault tolerance")
```

Query E digunakan untuk menemukan penelitian yang secara eksplisit membahas Temporal atau konsep durable execution. Dokumentasi vendor, blog, forum, dan halaman produk tidak dihitung sebagai artikel ilmiah yang memenuhi kriteria inklusi.

## 2.5 Prosedur Pencarian dan Seleksi

Proses pencarian dan seleksi dilakukan melalui tahapan berikut:

1. Menjalankan query pada setiap sumber pencarian sesuai kelompok kata kunci.
2. Mencatat nama sumber, tanggal pencarian, query, filter, dan jumlah hasil.
3. Mengekspor metadata artikel, meliputi judul, penulis, tahun, DOI, abstrak, dan sumber publikasi.
4. Menggabungkan hasil pencarian dan menghapus artikel duplikat berdasarkan DOI, judul, dan penulis.
5. Melakukan screening berdasarkan judul dan abstrak.
6. Memeriksa full-text artikel yang lolos screening awal.
7. Mencatat alasan eksklusi pada tahap pemeriksaan full-text.
8. Melakukan ekstraksi data dari artikel yang memenuhi kriteria.
9. Melakukan quality assessment berdasarkan rubrik yang telah ditetapkan.
10. Mengelompokkan hasil penelitian berdasarkan tema dan pertanyaan penelitian.

Setiap keputusan inklusi dan eksklusi perlu memiliki catatan agar proses seleksi dapat ditelusuri. Jika screening dilakukan oleh satu peneliti, keterbatasan tersebut perlu dinyatakan. Apabila memungkinkan, hasil seleksi dapat diperiksa oleh penilai kedua.

# 3. Inclusion and Exclusion Criteria

Kriteria inklusi dan eksklusi digunakan untuk memastikan bahwa penelitian yang dianalisis memiliki keterkaitan dengan pertanyaan penelitian.

| Kode | Inclusion Criteria                                                                                                                                     | Kode | Exclusion Criteria                                                                             |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---- | ---------------------------------------------------------------------------------------------- |
| I1   | Publikasi berada pada rentang tahun 2021–2026.                                                                                                         | E1   | Publikasi berada di luar rentang tahun penelitian.                                             |
| I2   | Membahas EDA, event-based communication, workflow orchestration, durable execution, atau reliability sistem.                                           | E2   | Tidak membahas konsep yang relevan dengan RQ.                                                  |
| I3   | Membahas sistem kesehatan, digital health, patient monitoring, atau aspek teknis sistem terdistribusi yang mendukung analisis arsitektur dan workflow. | E3   | Konteks dan kontribusinya tidak relevan dengan ruang lingkup penelitian.                       |
| I4   | Memiliki informasi bibliografis yang dapat diverifikasi.                                                                                               | E4   | Metadata publikasi tidak dapat diverifikasi.                                                   |
| I5   | Full-text dapat diperoleh untuk pemeriksaan metodologi dan hasil.                                                                                      | E5   | Full-text tidak berhasil diperoleh setelah upaya penelusuran yang wajar.                       |
| I6   | Menyajikan metode, rancangan, implementasi, evaluasi, atau temuan yang dapat dianalisis.                                                               | E6   | Hanya berupa opini atau promosi produk tanpa metode dan hasil penelitian yang dapat dinilai.   |
| I7   | Berupa artikel jurnal atau prosiding ilmiah.                                                                                                           | E7   | Berupa blog, forum, berita, materi pemasaran, atau halaman vendor nonilmiah.                   |
| I8   | Ditulis dalam bahasa Inggris atau Indonesia.                                                                                                           | E8   | Ditulis dalam bahasa selain Inggris atau Indonesia dan tidak tersedia terjemahan yang memadai. |

Ketentuan relevansi: Artikel teknis di luar bidang kesehatan tetap dapat dimasukkan apabila memberikan kontribusi terhadap RQ1, RQ2, atau RQ3. Namun, artikel tersebut tidak dapat digunakan sebagai bukti langsung efektivitas penerapan EDA dan durable workflow orchestration pada monitoring pasien.

# 4. PRISMA Flow Diagram

Seleksi studi dilaporkan menggunakan alur PRISMA 2020 yang mencakup identifikasi, penghapusan duplikasi, screening, pemeriksaan kelayakan full-text, dan penentuan studi yang dimasukkan ke dalam sintesis.

Angka PRISMA harus berasal dari catatan pencarian dan screening aktual. Angka contoh seperti 180 artikel ditemukan, 35 duplikat, atau 12 studi terpilih tidak boleh dipertahankan jika belum dapat dibuktikan.

## 4.1 Diagram Alur Seleksi

```
IDENTIFICATION
      |
      v
Records identified from databases
Scopus (n = ...)
IEEE Xplore (n = ...)
ScienceDirect (n = ...)
Google Scholar (n = ...)
      |
      v
Total records identified (n = ...)
      |
      v
Duplicate records removed (n = ...)
      |
      v
SCREENING
      |
      v
Records screened by title and abstract (n = ...)
      |
      +------------------------------+
      |                              |
      v                              v
Records excluded              Reports sought for retrieval
(n = ...)                     (n = ...)
                                     |
                                     v
ELIGIBILITY
                                     |
                                     v
Full-text reports assessed for eligibility
(n = ...)
                                     |
                    +----------------+----------------+
                    |                                 |
                    v                                 v
             Full-text excluded              Studies included
             with reasons                    in the review
             (n = ...)                       (n = ...)
```

## 4.2 Tabel Rekapitulasi PRISMA

| Tahapan                                             | Jumlah |
| --------------------------------------------------- | ------ |
| Records dari Scopus                                 | [Isi]  |
| Records dari IEEE Xplore                            | [Isi]  |
| Records dari ScienceDirect                          | [Isi]  |
| Records dari Google Scholar                         | [Isi]  |
| Total records ditemukan                             | [Isi]  |
| Duplikat yang dihapus                               | [Isi]  |
| Records setelah duplikasi dihapus                   | [Isi]  |
| Records yang disaring berdasarkan judul dan abstrak | [Isi]  |
| Records yang dikeluarkan pada screening             | [Isi]  |
| Full-text yang dicari                               | [Isi]  |
| Full-text yang tidak berhasil diperoleh             | [Isi]  |
| Full-text yang dinilai kelayakannya                 | [Isi]  |
| Full-text yang dikeluarkan beserta alasan           | [Isi]  |
| Studi yang dimasukkan dalam sintesis                | [Isi]  |

## 4.3 Pemeriksaan Konsistensi Jumlah Artikel

Jumlah pada setiap tahap harus memenuhi hubungan berikut:

| Tahapan                          | Hubungan                                                                        |
| -------------------------------- | ------------------------------------------------------------------------------- |
| Total records ditemukan          | Jumlah seluruh records dari sumber pencarian.                                   |
| Setelah duplikasi                | Total ditemukan − duplikat.                                                     |
| Screening judul dan abstrak      | Records setelah duplikasi = records dikeluarkan + laporan yang dicari.          |
| Pemeriksaan full-text            | Full-text yang diperoleh = full-text yang dikeluarkan + studi yang dimasukkan.  |
| Studi untuk sintesis kuantitatif | Diisi hanya jika sintesis kuantitatif atau meta-analisis benar-benar dilakukan. |

Jika penelitian menggunakan sintesis naratif atau tematik tanpa meta-analisis, hal tersebut dinyatakan secara eksplisit. Jangan membuat kategori sintesis kuantitatif hanya untuk melengkapi diagram.

# 5. Data Extraction Form

## 5.1 Variabel Ekstraksi Data

Data diekstraksi dari full-text artikel yang memenuhi kriteria inklusi. Informasi yang dikumpulkan mencakup:

| Variabel                      | Informasi yang Diekstraksi                                                                           |
| ----------------------------- | ---------------------------------------------------------------------------------------------------- |
| Identitas studi               | Penulis, tahun, judul, DOI, dan sumber publikasi.                                                    |
| Tujuan penelitian             | Permasalahan dan tujuan utama penelitian.                                                            |
| Konteks penelitian            | Domain, objek, dan lingkungan penerapan.                                                             |
| Metode                        | Metode penelitian, pendekatan arsitektur, algoritma, atau teknologi yang digunakan.                  |
| Dataset atau objek pengujian  | Sumber data, karakteristik data, objek penelitian, atau workload yang digunakan.                     |
| Evaluasi                      | Skenario pengujian, metrik, dan prosedur evaluasi.                                                   |
| Hasil utama                   | Temuan yang secara langsung dilaporkan oleh penulis.                                                 |
| Keterbatasan                  | Limitasi yang dinyatakan penulis atau keterbatasan yang dapat diidentifikasi dari desain penelitian. |
| Relevansi terhadap penelitian | Kontribusi artikel terhadap RQ1, RQ2, RQ3, atau RQ4.                                                 |

## 5.2 Daftar 12 Studi Utama

Kedua belas paper berikut dipertahankan sesuai daftar studi utama yang telah kamu tetapkan. Tabel ini merupakan peta ekstraksi awal berdasarkan identitas dan fokus publikasi, bukan pengganti pemeriksaan full-text.

| Kode | Penulis dan Tahun                    | Judul                                                                                                                                                                                                                                                  | Fokus Telaah                                                         |
| ---- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| S1   | Nagpal (2026) [7]                    | A Reproducible Benchmark Harness for Comparing Workflow Orchestration Engines: Temporal, Conductor, and Apache Airflow                                                                                                                                 | Perbandingan workflow orchestration engine, termasuk Temporal.       |
| S2   | Ardawan et al. (2026) [18]           | Perancangan Failure-Aware Self-Healing Workflow pada Sistem Event-Driven untuk Pemulihan Proses Layanan Digital Secara Otomatis                                                                                                                        | Pemulihan workflow pada sistem event-driven.                         |
| S3   | Guan et al. (2026) [13]              | iDDS: Intelligent Distributed Dispatch and Scheduling for Workflow Orchestration                                                                                                                                                                       | Penjadwalan dan distribusi workflow terdistribusi.                   |
| S4   | Yasini et al. (2025) [6]             | Clinical Events as Building Blocks for Smart Workflows and Decision Support                                                                                                                                                                            | Clinical events dan pembentukan workflow klinis.                     |
| S5   | Syarif & Pizaini (2022) [15]         | Penerapan Event-Driven Microservices pada Aplikasi Layanan Penerimaan Peserta Didik Baru                                                                                                                                                               | Penerapan event-driven microservices.                                |
| S6   | Laigner et al. (2026) [10]           | An Empirical Study on Challenges of Event Management in Microservice Architectures                                                                                                                                                                     | Tantangan pengelolaan event pada microservices.                      |
| S7   | Bação & Guerreiro (2026) [11]        | Consistency Challenges in Event-Driven Microservices: A Literature Review on Data, Process, and System Evolution                                                                                                                                       | Tantangan konsistensi pada event-driven microservices.               |
| S8   | Wibowo (2023) [16]                   | Arsitektur Event Driven untuk Mendukung Implementasi CRM Pada Aplikasi E-Commerce                                                                                                                                                                      | Penerapan arsitektur event-driven pada CRM.                          |
| S9   | Soegaard Ballester et al. (2021) [5] | A Mobile, Electronic Health Record-Connected Application for Managing Team Workflows in Inpatient Care                                                                                                                                                 | Aplikasi mobile yang terhubung dengan EHR untuk workflow perawatan.  |
| S10  | Tyagi et al. (2025) [1]              | Exploring User Behavior, Profiles, and Generation of Missed Reading Alerts in Long-Term Users of a Technology-Enabled Intervention for Self-Monitoring of Blood Pressure in Public Primary Care Setting in Singapore: Longitudinal Observational Study | Monitoring tekanan darah mandiri, perilaku pengguna, dan pengingat.  |
| S11  | Stratil et al. (2026) [3]            | A Longitudinal Analysis of Real World Symptom Tracking and Patient-Reported Outcomes in Brisa, a German Digital Health App for Multiple Sclerosis                                                                                                      | Monitoring gejala dan patient-reported outcomes secara longitudinal. |
| S12  | Nowell et al. (2023) [2]             | Participant Engagement and Adherence to Providing Smartwatch and Patient-Reported Outcome Data: Digital Tracking of Rheumatoid Arthritis Longitudinally (DIGITAL) Real-World Study                                                                     | Keterlibatan dan kepatuhan peserta dalam penyediaan data monitoring. |

## 5.3 Formulir Ekstraksi Hasil Penelitian

| Kode | Metode Penelitian                                                                                                                                                      | Dataset/Objek Pengujian                                                                                                                                                                            | Hasil Utama                                                                                                                                                                                                                                                            | Limitasi                                                                                                                                                                                                                   | RQ       |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| S1   | Pengembangan benchmark harness dengan adapter untuk Temporal, Conductor OSS, dan Apache Airflow. Pengujian mencakup workload dan fault injection.                      | Tujuh workload workflow orchestration, Docker Compose, dan PostgreSQL.                                                                                                                             | Menghasilkan benchmark yang dapat direproduksi untuk menguji low-latency execution, high-throughput, sequential chains, durable waits, retry, timer scheduling, dan long-wait/resume. Pengujian juga menemukan pengaruh host contention dan masalah scheduler Airflow. | Angka perbandingan performa setiap engine perlu diperiksa langsung pada tabel hasil eksperimen full-text.                                                                                                                  | RQ2, RQ3 |
| S2   | Prototyping Model dengan integrasi n8n, Apache Kafka, Docker, dan finite state machine berbasis JavaScript.                                                            | Lima skenario kegagalan, dua kondisi baseline, dan 30 pengulangan untuk setiap skenario.                                                                                                           | Sistem mencapai akurasi klasifikasi kegagalan 100% pada 150 iterasi. Success rate pemulihan mencapai 100% pada skenario dengan jalur fallback, sedangkan waktu pemulihan turun 29,90% dibandingkan baseline tanpa pemulihan.                                           | Pengujian terbatas pada prototipe dan lima skenario kegagalan tertentu. Belum membuktikan efektivitas pada monitoring pasien atau penggunaan Temporal.                                                                     | RQ1, RQ3 |
| S3   | Pengembangan dan pemaparan arsitektur Intelligent Distributed Dispatch and Scheduling (iDDS).                                                                          | Workflow komputasi ilmiah terdistribusi, termasuk pemrosesan data ATLAS dan Rubin Observatory. Salah satu contoh workflow memiliki lebih dari 100.000 job.                                         | iDDS mendukung workflow berbasis DAG, conditional execution, message-driven communication, monitoring, dan penjadwalan terdistribusi. Sistem juga menyediakan database polling sebagai fallback ketika event tidak diterima.                                           | Konteks penelitian adalah komputasi ilmiah terdistribusi, bukan monitoring pasien. Dukungan workflow interaktif, cloud-native, dan serverless masih memerlukan pengembangan.                                               | RQ2, RQ3 |
| S4   | Analisis jalur klinis lintas spesialisasi oleh tim multidisiplin, dilanjutkan validasi iteratif dan konsensus ahli.                                                    | 168 clinical events dari sembilan domain klinis. Setiap event memiliki definisi, data payload, dan indikator kinerja.                                                                              | Menghasilkan katalog clinical events terstruktur yang dapat digunakan sebagai pemicu workflow, dokumentasi klinis, dan pemantauan proses.                                                                                                                              | Penerapan pada sistem nyata masih direncanakan. Penelitian berfokus pada katalog event, bukan evaluasi implementasi workflow klinis secara operasional.                                                                    | RQ1, RQ4 |
| S5   | Tahapan analisis, perancangan, implementasi, pengujian, kesimpulan, dan saran. Evaluasi arsitektur menggunakan Software Architecture Analysis Method (SAAM).           | Aplikasi PPDB dengan API Gateway dan beberapa layanan, termasuk Registration, Announcement, Payment, dan Mail Service. Komunikasi menggunakan event-driven choreography, Redis Stream, dan Docker. | Perbandingan microservices dan monolith menunjukkan nilai modification cost sebesar 5,94 untuk microservices dan 78,335 untuk monolith. Penulis menyimpulkan microservices lebih sesuai untuk aplikasi yang diteliti.                                                  | Modification cost didasarkan pada evaluasi skenario dan estimasi tingkat kesulitan perubahan oleh system architect, bukan pengukuran performa operasional atau ketahanan workflow melalui fault injection.                 | RQ1      |
| S6   | Empirical study menggunakan pendekatan repository mining terhadap pertanyaan pengembang di Stack Overflow.                                                             | Lebih dari 8.000 pertanyaan Stack Overflow terkait pengelolaan event pada arsitektur microservices.                                                                                                | Mengidentifikasi permasalahan seperti payload event berukuran besar, pemodelan event schema, audit dan debugging event flow, serta ketergantungan dan urutan pemrosesan event.                                                                                         | Data berasal dari Stack Overflow sehingga merepresentasikan permasalahan yang dibahas pada platform tersebut, bukan keseluruhan praktik industri.                                                                          | RQ1, RQ3 |
| S7   | Literature review dengan prosedur systematic review yang mengacu pada pendekatan Kitchenham.                                                                           | Literatur mengenai konsistensi dalam arsitektur microservices.                                                                                                                                     | Menghasilkan tiga kategori konsistensi, yaitu data consistency, process consistency, dan system evolution consistency, beserta pendekatan penanganannya.                                                                                                               | Pemilihan digital libraries dan pengecualian grey literature dapat membatasi cakupan review. Penulis menyarankan perluasan dataset dan validasi model.                                                                     | RQ1, RQ3 |
| S8   | Perancangan konseptual hubungan dua arah antara penjual dan pembeli dengan Event-Driven Architecture, dijelaskan melalui use case, activity, dan sequence diagram.     | Aplikasi e-commerce dengan data jenis produk yang dibeli, motivasi pembelian, karakteristik pembeli, serta informasi pemasaran.                                                                    | Menghasilkan rancangan CRM berbasis EDA yang merekam karakteristik pembeli dan mencocokkannya dengan informasi pemasaran agar promosi dapat dikirimkan kepada pembeli yang sesuai.                                                                                     | Tidak menyajikan implementasi sistem operasional, pengujian performa, pengukuran keberhasilan pengiriman event, maupun evaluasi kuantitatif peningkatan penjualan.                                                         | RQ1      |
| S9   | User-centered design dan Agile development. Evaluasi menggunakan usage metrics, observasi pengguna, time-motion study, dan survei.                                     | Aplikasi Carelign yang terhubung dengan EHR pada tiga rumah sakit dengan total 1.616 tempat tidur.                                                                                                 | Pada Juli 2016, aplikasi digunakan pada 152 dari 169 layanan rawat inap, dengan rata-rata 3.275 pengguna unik dan 26.981 sesi akses per minggu. Penggunaan tetap stabil selama empat tahun berikutnya.                                                                 | Berfokus pada workflow tim klinis rumah sakit dan pengelolaan informasi EHR, bukan aktivitas mandiri pasien, timer, atau pemulihan workflow menggunakan workflow engine.                                                   | RQ4      |
| S10  | Longitudinal observational study menggunakan data backend PTEC-HT. Analisis mencakup logistic regression, latent class analysis, dan generalized estimating equations. | 491 peserta program pemantauan tekanan darah dengan data missed-reading alert, tekanan darah, karakteristik peserta, dan interaksi pesan selama 12 bulan.                                          | Sebanyak 93 peserta (18,9%) menghasilkan missed-reading alert pada bulan indeks. Penelitian menemukan tiga kelompok pola kepatuhan dan perbedaan karakteristik pengingat antarkelompok.                                                                                | Data tidak mencakup sejumlah faktor psikososial seperti motivasi dan literasi teknologi. Tidak dilakukan perhitungan ukuran sampel formal dan generalisasi perlu memperhatikan konteks layanan kesehatan primer Singapura. | RQ4      |
| S11  | Retrospective analysis menggunakan data pengguna aplikasi dan analisis longitudinal, termasuk Cox proportional hazards regression.                                     | 4.194 pengguna aplikasi Brisa yang memenuhi kriteria dari 8.441 pengguna yang memberikan persetujuan. Data mencakup aktivitas aplikasi, pelaporan gejala, dan patient-reported outcomes.           | Sekitar 76% pengguna mencatat setidaknya satu gejala atau PRO. Pada pengguna dengan setidaknya satu tahun pelacakan, skor gejala dan PRO cenderung stabil. Penelitian juga menemukan perbedaan risiko disengagement.                                                   | Terdapat potensi selection bias dan attrition bias. Diagnosis dan penggunaan obat sebagian didasarkan pada laporan mandiri, sementara skala gejala menggunakan skala emotikon 1–5.                                         | RQ4      |
| S12  | Studi real-world dengan periode run-in 14 hari dan periode utama 84 hari. Pengumpulan data dilakukan melalui aplikasi dan smartwatch.                                  | Program DIGITAL dengan 470 peserta yang menunjukkan minat awal; 278 peserta menyelesaikan run-in dan memenuhi syarat untuk periode utama.                                                          | Kepatuhan pelaporan mingguan ePRO mencapai 87,4%, harian ePRO 57,2%, dan data smartwatch 81,7%. Kepatuhan gabungan mencapai 52,9%. Pengingat dan pemantauan koordinator digunakan untuk menangani data yang belum dikirim.                                             | Hasil berasal dari peserta yang berhasil melewati tahap run-in sehingga tidak otomatis mewakili seluruh calon pengguna. Temuan berkaitan dengan periode dan protokol penelitian tertentu.                                  | RQ4      |

# 6. Synthesis and Thematic Analysis

Sintesis literatur dikelompokkan ke dalam empat tema utama. Pengelompokan dilakukan berdasarkan kontribusi masing-masing penelitian terhadap kebutuhan arsitektur, pengelolaan workflow, keandalan sistem, dan monitoring pasien.

## 6.1 Tema 1 — Event-Driven Architecture dan Pengelolaan Event

Event-Driven Architecture merupakan pendekatan komunikasi antarkomponen sistem dengan menggunakan event sebagai representasi kejadian. Pendekatan ini memungkinkan komponen yang menghasilkan event dan komponen yang memproses event berkomunikasi secara asinkron.

Namun, penggunaan event tidak otomatis menjamin konsistensi proses. Pengelolaan event perlu mempertimbangkan struktur pesan, perubahan skema, urutan kejadian, duplikasi pesan, serta keterlacakan proses.

Studi S5 dan S8 menjadi referensi penerapan arsitektur event-driven pada sistem aplikasi. Sementara itu, S6 dan S7 memberikan fokus telaah terhadap tantangan pengelolaan event dan konsistensi pada sistem terdistribusi. S4 memberikan perspektif penerapan clinical events sebagai komponen pembentuk workflow klinis.

Dalam konteks penelitian ini, event dapat merepresentasikan perubahan kondisi proses monitoring, seperti:

- Instruksi aktivitas pasien dibuat.
- Instruksi aktivitas diperbarui.
- Instruksi aktivitas dibatalkan.
- Pasien mengirim laporan aktivitas.
- Jadwal aktivitas mencapai waktu pelaksanaan.
- Periode monitoring diselesaikan.

Event-event tersebut menjadi dasar komunikasi antara backend aplikasi dan komponen yang menjalankan workflow. Setiap event perlu memiliki identitas dan informasi yang memadai agar dapat diproses serta ditelusuri.

## 6.2 Tema 2 — Durable Workflow Orchestration

Workflow orchestration digunakan untuk mengatur urutan aktivitas yang saling berkaitan dalam suatu proses. Pada proses jangka panjang, beberapa aktivitas tidak selalu dijalankan dalam satu transaksi atau satu interaksi pengguna.

Monitoring aktivitas pasien dapat memiliki tahapan berupa pembuatan instruksi, penentuan jadwal, pengiriman pengingat, penantian laporan pasien, dan kelanjutan monitoring pada periode berikutnya.

S1 menjadi studi utama untuk menelaah perbandingan workflow orchestration engine, termasuk Temporal. S3 memberikan perspektif tambahan mengenai penjadwalan dan distribusi workflow terdistribusi.

Dari perspektif penelitian, aspek yang perlu diperhatikan bukan hanya kemampuan memulai workflow, tetapi juga kemampuan mempertahankan status proses selama menunggu aktivitas atau respons pengguna.

Dalam implementasinya, Temporal akan digunakan untuk mengelola workflow yang memiliki:

1. Penjadwalan aktivitas berdasarkan waktu atau frekuensi.
2. Timer dan waktu tunggu.
3. Penerimaan laporan pasien sebagai respons terhadap workflow.
4. Perubahan instruksi selama workflow berjalan.
5. Pembatalan workflow ketika instruksi tidak lagi berlaku.
6. Kelanjutan workflow setelah gangguan pada worker.

Aspek tersebut perlu dibuktikan melalui implementasi dan pengujian, bukan hanya berdasarkan klaim kemampuan teknologi.

## 6.3 Tema 3 — Failure Handling dan Reliability Workflow

Sistem berbasis event dan workflow terdistribusi memiliki kemungkinan mengalami gangguan pada berbagai tahapan. Gangguan dapat terjadi ketika event diterbitkan, ketika consumer memproses event, ketika worker menjalankan aktivitas, atau ketika layanan eksternal tidak tersedia.

S2 secara khusus relevan untuk menelaah pemulihan proses pada sistem event-driven. S6 dan S7 memberikan landasan untuk mengkaji tantangan pengelolaan event dan konsistensi pada sistem terdistribusi. S1 dapat digunakan untuk menelaah evaluasi workflow orchestration engine.

Penelitian ini mengarahkan evaluasi reliability pada beberapa kondisi:

- Event gagal diproses.
- Event yang sama diterima lebih dari satu kali.
- Worker berhenti ketika workflow masih berjalan.
- Layanan notifikasi mengalami kegagalan.
- Instruksi diperbarui ketika workflow aktif.
- Instruksi dibatalkan ketika workflow masih berjalan.

Pengujian perlu membedakan antara pemulihan eksekusi workflow dan pemulihan efek bisnis. Workflow yang berhasil dilanjutkan belum tentu menjamin bahwa notifikasi atau pencatatan bisnis tidak terjadi dua kali. Oleh karena itu, implementasi perlu memperhatikan mekanisme idempotency.

Pengujian penghentian dan pengaktifan kembali worker dapat digunakan untuk memeriksa apakah workflow melanjutkan proses berdasarkan status yang tersimpan. Hasil pengujian kemudian dianalisis berdasarkan keberhasilan kelanjutan proses dan waktu pemulihan.

## 6.4 Tema 4 — Patient Monitoring dan Pelaporan Longitudinal

Monitoring pasien melalui aplikasi digital dapat melibatkan pencatatan perkembangan dan pelaporan mandiri yang dilakukan berulang dalam periode tertentu.

S9 memberikan perspektif penggunaan aplikasi mobile yang terhubung dengan EHR untuk mendukung workflow perawatan. S10 membahas perilaku pengguna dan missed-reading alerts dalam konteks pemantauan tekanan darah mandiri. S11 mengkaji symptom tracking dan patient-reported outcomes secara longitudinal. S12 membahas keterlibatan dan kepatuhan peserta dalam penyediaan data smartwatch serta patient-reported outcomes.

Keempat studi tersebut relevan untuk memahami kebutuhan kesinambungan monitoring, keterlibatan pasien, pengingat, dan pelaporan mandiri. Namun, fokusnya tidak boleh disamakan dengan evaluasi arsitektur EDA atau durable execution.

Dalam konteks penelitian DSH, aspek monitoring yang menjadi perhatian adalah pengelolaan instruksi aktivitas mandiri pasien, jadwal pelaksanaan, laporan pasien, dan riwayat perkembangan. Sistem ditujukan untuk mendukung proses monitoring, bukan menentukan diagnosis atau memberikan rekomendasi terapi medis.

## 6.5 Sintesis Lintas Tema

| Tema                                    | Sintesis Literatur                                                                                                                          | Implikasi terhadap Penelitian                                                                                 | Evaluasi yang Diperlukan                                                         |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Event-driven communication              | Studi EDA membahas penerapan komunikasi berbasis event, sedangkan studi event management dan consistency membahas tantangan pengelolaannya. | Merancang event bisnis, kontrak payload, consumer, dan pencatatan status proses.                              | Keberhasilan event diterbitkan, diterima, dan diproses; penanganan duplikasi.    |
| Workflow orchestration                  | Studi workflow orchestration membahas pengelolaan dan penjadwalan proses melalui workflow engine.                                           | Menggunakan Temporal untuk mengelola proses monitoring yang memiliki timer, waktu tunggu, dan respons pasien. | Ketepatan transisi workflow, timer, update, cancellation, dan resume.            |
| Failure handling                        | Literatur membahas pemulihan workflow serta tantangan konsistensi sistem terdistribusi.                                                     | Merancang mekanisme retry, idempotency, dan pemulihan workflow.                                               | Keberhasilan pemulihan setelah worker berhenti dan pencegahan efek bisnis ganda. |
| Patient monitoring                      | Studi digital health membahas monitoring longitudinal, patient-reported outcomes, pengingat, dan kepatuhan pengguna.                        | Menyediakan instruksi aktivitas, pelaporan mandiri, serta riwayat monitoring pasien.                          | Kesesuaian fungsi sistem dengan proses monitoring pasien.                        |
| Integrasi EDA dan durable orchestration | Studi-studi tersebut memiliki fokus yang berbeda antara komunikasi event, workflow engine, reliability, dan monitoring pasien.              | Mengintegrasikan komunikasi event dengan durable workflow orchestration dalam satu artefak sistem monitoring. | Pengujian terpadu pada skenario monitoring pasien.                               |

# 7. Quality Assessment

Quality Assessment (QA) dilakukan untuk menilai kualitas metodologis dan kekuatan pelaporan setiap artikel yang telah lolos seleksi. Penilaian ini berbeda dari relevansi artikel: relevansi menentukan apakah artikel sesuai dengan ruang lingkup SLR, sedangkan QA menilai seberapa kuat bukti yang disajikan artikel tersebut.

## 7.1 Kriteria Penilaian

Saya menyarankan menggunakan lima kriteria dengan skor 0–2. Skema ini lebih mudah diterapkan secara konsisten daripada memberikan skor 1–5 tanpa indikator yang terukur.

| Kode | Kriteria                             | Skor 0                                                    | Skor 1                                        | Skor 2                                                                        |
| ---- | ------------------------------------ | --------------------------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------- |
| QA1  | Kejelasan tujuan penelitian          | Tujuan tidak jelas.                                       | Tujuan disebutkan tetapi kurang spesifik.     | Tujuan jelas dan terarah.                                                     |
| QA2  | Kejelasan metodologi                 | Metode tidak dijelaskan.                                  | Metode dijelaskan sebagian.                   | Metode dijelaskan secara sistematis.                                          |
| QA3  | Kejelasan objek atau data penelitian | Objek atau data tidak dijelaskan.                         | Objek atau data dijelaskan sebagian.          | Objek atau data dijelaskan dengan memadai.                                    |
| QA4  | Evaluasi dan penyajian hasil         | Tidak terdapat evaluasi atau hasil yang dapat dianalisis. | Evaluasi atau hasil tersedia tetapi terbatas. | Evaluasi dan hasil dijelaskan dengan jelas serta mendukung tujuan penelitian. |
| QA5  | Keterbatasan dan validitas           | Tidak ada pembahasan keterbatasan atau validitas.         | Dibahas secara terbatas.                      | Keterbatasan atau validitas dijelaskan secara memadai.                        |

Skor maksimal setiap artikel adalah 10.

## 7.2 Interpretasi Skor

| Skor | Interpretasi         |
| ---- | -------------------- |
| 0–3  | Kualitas rendah      |
| 4–6  | Kualitas sedang      |
| 7–8  | Kualitas baik        |
| 9–10 | Kualitas sangat baik |

Artikel dengan skor rendah tidak otomatis dikeluarkan jika masih memberikan kontribusi yang relevan terhadap RQ. Namun, kualitas bukti yang disajikan harus dipertimbangkan saat melakukan sintesis.

## 7.3 Lembar Penilaian 12 Studi Utama

Untuk mengubah penilaian lama menjadi rubrik baru, saya gunakan indikator yang sudah kamu tetapkan:

- QA1: Kejelasan tujuan penelitian.
- QA2: Kejelasan metodologi.
- QA3: Kejelasan objek atau data penelitian.
- QA4: Evaluasi dan penyajian hasil.
- QA5: Keterbatasan dan validitas.

Berikut penilaian yang disesuaikan dengan informasi hasil ekstraksi sebelumnya.

| Kode | Studi                                | QA1 | QA2 | QA3 | QA4 | QA5 | Total               |
| ---- | ------------------------------------ | --- | --- | --- | --- | --- | ------------------- |
| S1   | Nagpal (2026) [7]                    | 2   | 2   | 2   | 1   | 1   | 8/10 – Baik         |
| S2   | Ardawan et al. (2026) [18]           | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |
| S3   | Guan et al. (2026) [13]              | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |
| S4   | Yasini et al. (2025) [6]             | 2   | 2   | 2   | 1   | 1   | 8/10 – Baik         |
| S5   | Syarif & Pizaini (2022) [15]         | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |
| S6   | Laigner et al. (2026) [10]           | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |
| S7   | Bação & Guerreiro (2026) [11]        | 2   | 2   | 2   | 2   | 2   | 10/10 – Sangat baik |
| S8   | Wibowo (2023) [16]                   | 2   | 1   | 2   | 1   | 0   | 6/10 – Sedang       |
| S9   | Soegaard Ballester et al. (2021) [5] | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |
| S10  | Tyagi et al. (2025) [1]              | 2   | 2   | 2   | 2   | 2   | 10/10 – Sangat baik |
| S11  | Stratil et al. (2026) [3]            | 2   | 2   | 2   | 2   | 2   | 10/10 – Sangat baik |
| S12  | Nowell et al. (2023) [2]             | 2   | 2   | 2   | 2   | 1   | 9/10 – Sangat baik  |

Catatan penting tentang skor: tabel ini merupakan penyesuaian penilaian berdasarkan ringkasan hasil ekstraksi yang sudah kita susun. Skor QA5 khususnya perlu dicocokkan kembali dengan bagian keterbatasan dan validitas masing-masing full-text. Skor 2 tidak boleh diberikan hanya karena artikel menyebut keterbatasan secara singkat; pembahasannya harus memadai sesuai rubrik.

# 8. Research Gap Matrix

Research gap diidentifikasi dengan membandingkan fokus penelitian terdahulu berdasarkan empat dimensi: metodologis, skenario evaluasi, konteks penerapan, serta performa dan keandalan.

## 8.1 Matriks Research Gap

| Dimensi Gap            | Fokus Penelitian Terdahulu                                                                                                                                                                                                    | Kesenjangan yang Menjadi Fokus Penelitian                                                                                                                                  | Kontribusi yang Diusulkan                                                                                                                    |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Metodologis            | Studi EDA membahas komunikasi berbasis event [15], [16], pengelolaan event [10], dan konsistensi sistem [11]. Studi workflow membahas orkestrasi proses [7], [13], sedangkan studi recovery membahas pemulihan workflow [18]. | Fokus-fokus tersebut perlu dikaji dalam satu rancangan implementasi yang menghubungkan komunikasi event dengan pengelolaan workflow jangka panjang pada monitoring pasien. | Merancang integrasi EDA dan durable workflow orchestration menggunakan Temporal dalam artefak sistem monitoring pasien.                      |
| Skenario Evaluasi      | Penelitian workflow dan recovery memiliki fokus evaluasi teknis [7], [13], [18], sementara penelitian monitoring pasien berfokus pada perilaku, pelaporan, dan keterlibatan pengguna [1], [2], [3].                           | Diperlukan evaluasi terpadu yang menguji proses monitoring sekaligus perilaku sistem ketika terjadi gangguan, perubahan instruksi, dan penerimaan laporan.                 | Menyusun skenario pengujian workflow normal, timer, laporan pasien, update, cancellation, duplikasi event, dan worker recovery.              |
| Konteks                | Penelitian EDA yang digunakan sebagai referensi mencakup domain pendidikan dan e-commerce [15], [16]. Penelitian kesehatan membahas workflow perawatan dan monitoring digital [5], [1], [3], [2].                             | Masih diperlukan pembahasan penerapan integrasi arsitektur tersebut pada proses monitoring aktivitas pasien yang melibatkan interaksi berulang dalam periode tertentu.     | Menerapkan rancangan pada sistem monitoring perkembangan pasien dengan konteks operasional Klinik DSH, setelah proses aktual dikonfirmasi.   |
| Performa dan Keandalan | Literatur membahas tantangan pengelolaan event dan konsistensi [10], [11], serta workflow orchestration dan pemulihan proses [7], [13], [18].                                                                                 | Dampak integrasi terhadap kelanjutan proses monitoring, penanganan duplikasi, dan pemulihan workflow perlu dibuktikan melalui skenario pengujian yang terukur.             | Mengukur keberhasilan pemrosesan event, ketepatan transisi workflow, keberhasilan recovery, recovery time, dan pencegahan efek bisnis ganda. |

## 8.2 Sintesis Rumusan Research Gap

Berdasarkan fokus kedua belas studi utama, penelitian terdahulu telah membahas beberapa aspek yang saling berkaitan, tetapi dengan penekanan yang berbeda. Penelitian tentang Event-Driven Architecture membahas komunikasi asinkron, pengelolaan event, dan tantangan konsistensi pada sistem terdistribusi [15], [16], [10], [11]. Penelitian workflow orchestration membahas pengelolaan dan penjadwalan proses terdistribusi, termasuk perbandingan workflow engine [7], [13]. Sementara itu, penelitian mengenai pemulihan workflow memberikan perspektif terhadap penanganan kegagalan pada sistem event-driven [18].

Pada bidang kesehatan, penelitian terdahulu membahas penggunaan aplikasi digital untuk mendukung workflow perawatan, monitoring pasien, pengingat, serta pelaporan perkembangan secara longitudinal [5], [1], [3], [2]. Penelitian tersebut memberikan landasan mengenai kebutuhan kesinambungan monitoring dan keterlibatan pasien, tetapi memiliki fokus yang berbeda dari evaluasi keandalan arsitektur sistem.

Berdasarkan perbedaan fokus tersebut, penelitian ini diarahkan pada perancangan dan evaluasi integrasi Event-Driven Architecture dengan durable workflow orchestration menggunakan Temporal untuk mengelola proses monitoring perkembangan pasien. Fokus implementasi meliputi pengelolaan instruksi aktivitas, penjadwalan, pengingat, penerimaan laporan pasien, perubahan atau pembatalan instruksi, serta pemulihan workflow setelah terjadi gangguan. Kontribusi penelitian terletak pada penerapan dan evaluasi integrasi tersebut dalam satu artefak sistem, bukan pada klaim bahwa setiap teknologi atau mekanisme yang digunakan belum pernah diteliti sebelumnya.

Batas klaim gap: rumusan tersebut merupakan gap awal berdasarkan fokus 12 studi utama. Klaim bahwa belum ada penelitian sejenis secara keseluruhan baru dapat diperkuat setelah hasil pencarian sistematis dan pemeriksaan full-text selesai.

# 9. Kesimpulan dan Rekomendasi

## 9.1 Kesimpulan

Berdasarkan pengelompokan literatur awal, terdapat empat kelompok penelitian yang menjadi landasan bagi penelitian ini.

1. Event-Driven Architecture dan pengelolaan event. Penelitian terdahulu membahas komunikasi berbasis event, penerapan event-driven system, serta tantangan pengelolaan dan konsistensi event [15], [16], [10], [11]. Temuan tersebut menjadi dasar perancangan komunikasi antarkomponen sistem menggunakan event.
2. Workflow orchestration dan pemulihan proses. Penelitian terdahulu membahas workflow orchestration, penjadwalan proses terdistribusi, perbandingan workflow engine, dan pemulihan workflow [7], [13], [18]. Temuan tersebut menjadi landasan untuk mengkaji penggunaan Temporal dalam pengelolaan workflow jangka panjang.
3. Monitoring pasien dan pelaporan longitudinal. Penelitian digital health membahas penggunaan aplikasi untuk mendukung workflow perawatan, pengingat, pemantauan mandiri, dan pelaporan perkembangan pasien [5], [1], [3], [2]. Temuan tersebut menjadi dasar kebutuhan monitoring aktivitas dan pelaporan pasien secara berkelanjutan.
4. Arah penelitian yang diusulkan. Berdasarkan perbedaan fokus tersebut, penelitian ini diarahkan pada implementasi integrasi EDA dan durable workflow orchestration menggunakan Temporal untuk mengelola proses monitoring perkembangan pasien. Evaluasi akan difokuskan pada pemrosesan event, pengelolaan workflow, perubahan instruksi, pembatalan, dan pemulihan proses setelah gangguan.

Dengan demikian, penelitian tidak berfokus pada pengembangan fitur pencatatan pasien semata, tetapi pada bagaimana proses monitoring yang berlangsung dalam beberapa tahapan dan periode waktu dapat dikelola secara lebih terstruktur dan andal melalui integrasi arsitektur dan teknologi orkestrasi workflow.

## 9.2 Rekomendasi Tindak Lanjut

Untuk meningkatkan kekuatan SLR dan memastikan kesesuaiannya dengan penelitian, diperlukan beberapa tindak lanjut.

1. Validasi pencarian dan seleksi literatur. Melengkapi dokumentasi pencarian dari setiap sumber, mencatat tanggal dan jumlah hasil, melakukan screening, serta menyusun diagram PRISMA berdasarkan hasil aktual.
2. Pemeriksaan full-text 12 studi utama. Melengkapi data ekstraksi yang meliputi metode, dataset atau objek penelitian, hasil evaluasi, dan keterbatasan berdasarkan isi artikel.
3. Pelaksanaan Quality Assessment. Memberikan skor setiap studi menggunakan lima kriteria QA yang telah ditetapkan setelah seluruh informasi yang dibutuhkan diperiksa.
4. Validasi proses monitoring Klinik DSH. Memastikan apakah proses aktual memang melibatkan instruksi aktivitas dengan jadwal dan frekuensi, penantian laporan pasien, perubahan instruksi, pembatalan, serta kebutuhan tindak lanjut. Hasil konfirmasi ini akan menentukan kesesuaian penggunaan Temporal.
5. Penyusunan skenario evaluasi sistem. Pengujian implementasi dapat mencakup:
   - Pembuatan instruksi aktivitas dan dimulainya workflow.
   - Pemicu timer sesuai jadwal aktivitas.
   - Pengiriman laporan pasien dan kelanjutan workflow.
   - Perubahan instruksi ketika workflow sedang berjalan.
   - Pembatalan instruksi dan workflow.
   - Penanganan event duplikat.
   - Penghentian dan pengaktifan kembali Temporal Worker.
   - Pemulihan workflow setelah gangguan.
6. Pengukuran keandalan. Evaluasi dapat menggunakan keberhasilan pemrosesan event, ketepatan transisi workflow, keberhasilan pemulihan, recovery time, dan jumlah efek bisnis ganda. Hasil pengukuran harus dilaporkan sesuai hasil eksperimen, bukan berdasarkan target yang diasumsikan tercapai.
