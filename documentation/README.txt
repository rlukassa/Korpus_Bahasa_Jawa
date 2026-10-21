================================================================================
KORPUS SUARA BAHASA JAWA
Dokumentasi Korpus (README)
================================================================================

Mata kuliah   : IF4071 Pemrosesan Ucapan
Tugas         : Tugas Besar Fase 1, Pengumpulan Korpus Suara Bahasa Daerah
                Indonesia
Semester      : Semester 1 2026/2027
Institusi     : Sekolah Teknik Elektro dan Informatika, Institut Teknologi
                Bandung
Bahasa        : Bahasa Jawa (ISO 639-1 jv, ISO 639-3 jav)
Repositori    : https://github.com/rlukassa/Korpus_Bahasa_Jawa
Versi README  : 1.0 (21 Oktober 2026)

Anggota kelompok:
  - Danendra Shafi Athallah               13523136
  - Jonathan Kenan Budianto               13523139
  - Jovandra Otniel Panagalambok Siregar  13523141
  - Muhammad Farrel Wibowo                13523153
  - Lukas Raja Agripa                     13523158

Dokumen ini menjelaskan tujuan, spesifikasi, isi, statistik, konvensi, dan
keterbatasan korpus pada kondisi saat dokumen disusun. Informasi yang belum
terdokumentasi oleh kelompok dinyatakan secara eksplisit sebagai "belum
terdokumentasi" dan tidak diisi dengan perkiraan.


--------------------------------------------------------------------------------
DAFTAR ISI
--------------------------------------------------------------------------------
  1. Tujuan Korpus
  2. Spesifikasi Korpus
  3. Struktur Repositori
  4. Penutur
  5. Statistik Korpus
  6. Metadata (metadata.csv)
  7. Quality Control
  8. Anotasi
  9. Konvensi
 10. Keputusan Desain (D1 sampai D5)
 11. Etika dan Informed Consent
 12. Keterbatasan dan Pekerjaan yang Belum Selesai
 13. Cara Menggunakan dan Memverifikasi Korpus
 14. Lisensi dan Penggunaan


--------------------------------------------------------------------------------
1. TUJUAN KORPUS
--------------------------------------------------------------------------------
Korpus ini dikumpulkan untuk memenuhi Tugas Besar IF4071 Fase 1, yaitu
menyediakan data suara bahasa daerah sebagai bahan pengembangan sistem
pengenal ucapan (Automatic Speech Recognition, ASR) Bahasa Jawa pada Fase 2.

Sasaran pengumpulan:
  - ucapan spontan Bahasa Jawa dari 10 penutur (5 laki-laki dan 5
    perempuan);
  - durasi sekitar 10 sampai 15 menit per penutur;
  - metadata, label kualitas, dan anotasi (transkripsi serta label lain)
    untuk setiap rekaman.

Penggunaan yang dimaksud: training, validation, dan testing sistem ASR Bahasa
Jawa pada Fase 2, serta dapat diakses oleh dosen, asisten, dan mahasiswa lain
melalui repositori GitHub. Penggunaan di luar itu hanya sah sepanjang
diizinkan oleh informed consent penutur (lihat Bagian 11).


--------------------------------------------------------------------------------
2. SPESIFIKASI KORPUS
--------------------------------------------------------------------------------
2.1 Spesifikasi menurut tugas dan kondisi aktual

  Aspek              Ketentuan tugas            Kondisi aktual
  -----------------  -------------------------  --------------------------------
  Bahasa             1 bahasa daerah            Bahasa Jawa
  Jumlah penutur     10                         10 (S01 sampai S10)
  Gender             5 laki-laki + 5 perempuan  5 M (S01-S05) + 5 F (S06-S10)
  Jenis ucapan       Spontaneous / Conversation Berbasis prompt berupa
                                                pertanyaan (lihat Bagian 12)
  Topik              Minimal 3                  4 topik pada metadata.csv
  Durasi             sekitar 10-15 menit/penutur 10,00 sampai 11,69 menit
                                                (durasi berkas)
  Sampling rate      16 kHz                     16000 Hz (10 dari 10 berkas)
  Bit depth          16-bit                     16-bit (10 dari 10 berkas)
  Channel            Mono                       1 channel (10 dari 10 berkas)
  Format             WAV                        WAV, pcm_s16le
  Lingkungan         Indoor, relatif tenang     Indoor (10 dari 10 baris)
  Metadata           Wajib                      metadata/metadata.csv
  Quality control    Good/Acceptable/Reject     8 Good, 2 Acceptable, 0 Reject
  Anotasi            Transkripsi dan label      annotation/annotation-semua.csv

Pemeriksaan format dilakukan dengan ffprobe pada seluruh 10 berkas:

  ffprobe -v error -show_entries stream=codec_name,sample_rate,channels,bits_per_sample -of default=nw=1 <berkas.wav>

2.2 Total durasi

  Total durasi berkas       : 6.516,77 detik (108,61 menit)
  Rata-rata per penutur     : 10,86 menit
  Berkas terpendek          : S09_T01_001.wav (600,00 detik)
  Berkas terpanjang         : S02_T01_001.wav (701,67 detik)
  Total ukuran audio        : sekitar 208,5 MB (10 berkas)

Catatan: angka di atas adalah durasi berkas, yang masih mencakup jeda dan
hening. Durasi ucapan bersih belum diukur secara menyeluruh (lihat Bagian 5.3
dan Bagian 12).


--------------------------------------------------------------------------------
3. STRUKTUR REPOSITORI
--------------------------------------------------------------------------------
Akar repositori adalah folder korpus itu sendiri.

  /
  |-- README.md                            ringkasan singkat dan tautan ke
  |                                        dokumen ini
  |-- audio/
  |   |-- S01/ S01_T01_001.wav
  |   |-- S02/ S02_T01_001.wav
  |   |-- ...
  |   `-- S10/ S10_T01_001.wav
  |-- metadata/
  |   `-- metadata.csv                     10 baris, satu per berkas WAV
  |-- annotation/
  |   `-- annotation-semua.csv             2.188 baris segmen, 10 berkas
  |-- qc/
  |   `-- qc_report.csv                    label dan masalah per berkas
  |-- consent/
  |   `-- consent_form/                    lihat Bagian 11
  `-- documentation/
      |-- README.txt                       dokumen ini
      |-- Laporan Tugas Besar Fase 1.docx  laporan
      `-- Laporan Tugas Besar Fase 1.pdf   laporan

Perbedaan terhadap struktur yang dirancang pada spesifikasi tugas:

  Rancangan                                   Kondisi aktual
  ------------------------------------------  ----------------------------------
  annotation/annotation.csv                   annotation/annotation-semua.csv
  documentation/qc_report.csv                 qc/qc_report.csv
  Nama berkas Sxx_Txx_nnn.wav, kode topik     Seluruh berkas bernama
  mengikuti topik utterance                   Sxx_T01_001.wav; satu berkas utuh
                                              per penutur memuat empat topik
  consent_log.csv dan templat consent         Belum ada (lihat Bagian 11)

Pola nama berkas: Sxx_Txx_nnn.wav, dengan Sxx = Speaker ID (S01 sampai S10),
Txx = kode topik, nnn = nomor urut berkas. Berkas berada pada folder audio/Sxx
dengan Speaker ID yang sama dengan awalan nama berkas.


--------------------------------------------------------------------------------
4. PENUTUR
--------------------------------------------------------------------------------
Penutur diidentifikasi hanya dengan Speaker ID. Nama asli, kontak, dan
pemetaan nama ke Speaker ID tidak boleh dimuat di repositori ini.

  Speaker  Gender  Label dialek pada anotasi
  -------  ------  -------------------------------------------------------
  S01      M       Jawa Timuran (Suroboyoan)
  S02      M       Jawa Tengahan (Semarangan)
  S03      M       Jawa Tengahan (Solo); berlabel penutur non-asli
  S04      M       Jawa Mataraman (Jogja); 2 segmen berlabel ragam krama
  S05      M       Jawa Tengahan/Mataraman (ngoko); berlabel penutur warisan
  S06      F       Jawa Tengahan (Semarangan)
  S07      F       Jawa Timuran (Suroboyoan)
  S08      F       Jawa Timuran (Suroboyoan)
  S09      F       Jawa campuran (Tengahan + Malangan); berlabel penutur
                   non-asli
  S10      F       Jawa Timuran (Trenggalekan/Mataraman wetan)

Ringkasan komposisi dialek menurut label anotasi: Jawa Timuran empat penutur
(S01, S07, S08, S10); Jawa Tengahan/Mataraman lima penutur (S02, S03, S04, S05,
S06); Jawa campuran Tengahan-Malangan satu penutur (S09).

Kolom Language pada metadata.csv bernilai "Jawa" untuk seluruh penutur dan
tidak memuat dialek. Informasi dialek hanya tersedia pada berkas anotasi.

Informasi berikut belum terdokumentasi pada berkas mana pun di repositori dan
perlu dilengkapi kelompok: daerah asal (kabupaten/kota), rentang usia, latar
belakang penggunaan bahasa, serta anggota kelompok yang menangani tiap penutur.


--------------------------------------------------------------------------------
5. STATISTIK KORPUS
--------------------------------------------------------------------------------
5.1 Durasi berkas per penutur (sumber: metadata.csv)

  Speaker  Gender  Berkas            Durasi (detik)  Durasi (menit)
  -------  ------  ----------------  --------------  --------------
  S01      M       S01_T01_001.wav          629,76           10,50
  S02      M       S02_T01_001.wav          701,67           11,69
  S03      M       S03_T01_001.wav          643,24           10,72
  S04      M       S04_T01_001.wav          701,18           11,69
  S05      M       S05_T01_001.wav          601,45           10,02
  S06      F       S06_T01_001.wav          690,94           11,52
  S07      F       S07_T01_001.wav          651,16           10,85
  S08      F       S08_T01_001.wav          607,77           10,13
  S09      F       S09_T01_001.wav          600,00           10,00
  S10      F       S10_T01_001.wav          689,60           11,49
  Total                                   6.516,77          108,61

5.2 Durasi per gender

  Gender  Jumlah penutur  Durasi (detik)  Durasi (menit)
  ------  --------------  --------------  --------------
  M                    5        3.277,30           54,62
  F                    5        3.239,47           53,99
  Selisih                          37,83            0,63  (sekitar 1,2%)

Selisih M terhadap F berada di bawah batas 10% yang diusulkan pada
spesifikasi. Seluruh penutur berdurasi berkas minimal 10 menit.

5.3 Anotasi per penutur (sumber: annotation-semua.csv)

  Speaker  Segmen  Bertrans-  Durasi bertrans-  Rata-rata       Durasi
                   kripsi     kripsi (detik)    confidence_asr  berlabel Jawa
  -------  ------  ---------  ----------------  --------------  -------------
  S01         112        112            592,95            0,881          95,9%
  S02         222        214            530,40            0,865          59,6%
  S03         370        368            509,34            0,889          91,3%
  S04         301        301            575,83            0,884          93,2%
  S05         106        106            566,44            0,825          93,6%
  S06          70         69            659,25            0,875          72,2%
  S07         527        527            649,84                -          86,0%
  S08          80         77            561,95            0,859          41,7%
  S09          73         67            508,23            0,875          76,9%
  S10         327        327            584,09            0,918          92,3%
  Total     2.188      2.168          5.738,32            0,884          80,4%

Keterangan:
  - 20 baris tidak berisi transkripsi (penanda "-" pada segment_id gap):
    S02 8 baris, S03 2, S06 1, S08 3, S09 6. Baris ini mencatat jeda panjang,
    hening digital, atau ucapan yang tidak tertranskripsi.
  - Kolom confidence_asr kosong pada seluruh 527 baris S07 dan pada 20 baris
    tanpa transkripsi.
  - Durasi bertranskripsi S09 melebihi durasi ucapan sebenarnya karena 119,5
    detik hening digital berada di dalam rentang waktu segmen bertranskripsi.

5.4 Token dan kosakata

  Jumlah token (rangkaian huruf, huruf kecil) : sekitar 12.650
  Ukuran kosakata (token berbeda)             : 2.590

Angka ini dihitung dari kolom transkripsi pada 2.168 baris bertranskripsi,
dengan tokenisasi sederhana berdasarkan rangkaian huruf. Karena transkripsi
masih berstatus draf (Bagian 8), angka ini bersifat sementara.

5.5 Label bahasa pada segmen bertranskripsi

  Label bahasa                       Durasi (detik)  Porsi
  ---------------------------------  --------------  -----
  Jawa                                      4.615,7  80,4%
  Campuran (Jawa-Indonesia)                   631,5  11,0%
  Campuran (Jawa-Inggris)                     109,5   1,9%
  Campuran (Jawa-Indonesia-Inggris)            55,5   1,0%
  Indonesia                                   303,2   5,3%
  Inggris                                      22,9   0,4%

Korpus ini tidak seluruhnya berbahasa Jawa. Porsi durasi berlabel Jawa berbeda
jauh antarpenutur, dari 41,7% (S08) sampai 95,9% (S01). Hal ini perlu
diperhatikan pada Fase 2, misalnya dengan menyaring segmen berdasarkan
label_bahasa.

5.6 Topik

metadata.csv mencatat empat topik yang sama pada setiap baris: Perkenalan,
Keluarga, Aktivitas sehari-hari, dan Makanan. Berkas anotasi memakai 16 label
topik yang lebih rinci (misalnya "Kegiatan sehari-hari", "Makanan khas daerah",
"Hobi", dan "Kuliah & jurusan"), dengan 11 sampai 15 label berbeda per berkas.
Label topik pada anotasi belum diselaraskan dengan empat topik pada metadata.
Durasi per topik belum dapat dihitung dari metadata karena posisi awal dan
akhir tiap topik tidak dicatat di sana.


--------------------------------------------------------------------------------
6. METADATA (metadata/metadata.csv)
--------------------------------------------------------------------------------
Satu baris per berkas WAV, 10 baris. Pengodean UTF-8, pemisah koma.

Kolom (delapan kolom wajib dari spesifikasi tugas):

  Kolom     Isi
  --------  ---------------------------------------------------------------
  File      Nama berkas audio, mis. S01_T01_001.wav
  Speaker   Speaker ID, S01 sampai S10
  Gender    M atau F
  Language  Bahasa; bernilai "Jawa" (lihat catatan di bawah)
  Topic     Daftar topik dipisahkan titik koma
  Duration  Durasi berkas dalam detik, dua digit desimal
  Environment  Indoor
  Quality   Good, Acceptable, atau Reject

Catatan penyimpangan:
  - Kolom keempat bernama "Language", bukan "Language/Dialect" seperti pada
    spesifikasi tugas, dan tidak memuat dialek.
  - Kolom Topic memuat empat topik dalam satu sel, sedangkan kode topik pada
    nama berkas hanya T01.
  - Kolom tambahan yang diusulkan (Session, Start, End, SpeechType, Register,
    Device, OrigSampleRate, RecordingDate, Recorder, Problem, Split) belum
    dipakai.
  - Nilai Duration pada setiap baris berselisih kurang dari 0,01 detik dari
    durasi berkas hasil ffprobe.


--------------------------------------------------------------------------------
7. QUALITY CONTROL
--------------------------------------------------------------------------------
7.1 Kriteria

Setiap rekaman diperiksa berdasarkan tujuh kriteria spesifikasi tugas:
  (1) suara terdengar jelas;
  (2) tidak terjadi clipping;
  (3) noise masih dapat diterima;
  (4) tidak ada suara orang lain yang mengganggu;
  (5) rekaman tidak terpotong;
  (6) format sesuai;
  (7) metadata lengkap.

Definisi label:
  Good        Suara jelas dan dapat dipakai tanpa masalah berarti.
  Acceptable  Ada gangguan kecil, tetapi suara masih dapat dipakai.
  Reject      Ada masalah serius (mis. suara tidak terdengar, clipping berat,
              noise sangat dominan, rekaman terpotong, berkas rusak). Rekam
              ulang jika memungkinkan.

7.2 Ambang QC acuan

Ambang berikut adalah ambang usulan dari materi acuan kelompok (RULES.md,
bagian [BP]) untuk menyeragamkan penilaian antarpemeriksa. Ambang ini bersifat
bantuan flag otomatis; label Quality tetap ditetapkan oleh manusia setelah
mendengarkan rekaman.

  Metrik                  Good           Acceptable               Reject
  ----------------------  -------------  -----------------------  ------------
  Clipping (clip_runs)    0              Sedikit, singkat, tidak  Terdengar
                                         terdengar                distorsi
  Peak                    -12 s.d. -4    -30 s.d. -12 dBFS        < -30 dBFS dan
                          dBFS                                    ucapan sulit
                                                                  didengar
  Estimasi SNR            >= 25 dB       15 s.d. 25 dB            < 15 dB dan
                                                                  noise
                                                                  mengganggu

Belum terdokumentasi: apakah ambang ini dipakai oleh pemeriksa saat memberi
label pada 10 rekaman, serta cara pemeriksaan (mis. apakah rekaman didengarkan
seluruhnya atau hanya sebagian).

7.3 Hasil QC (qc/qc_report.csv)

  Label        Jumlah  Berkas
  -----------  ------  --------------------------------------------
  Good              8  S01, S02, S04, S05, S06, S07, S08, S10
  Acceptable        2  S03, S09
  Reject            0  -
  Total            10

Label pada qc_report.csv identik dengan label pada metadata.csv untuk setiap
rekaman. Catatan masalah:

  S03  Background noise cukup tinggi, namun ucapan masih dapat dipahami.
  S09  Silence digital berulang: sekitar 14 jeda sepanjang 10 sampai 14 detik,
       karena penutur berpikir dan membaca pertanyaan terlebih dahulu.

Hasil pengukuran ulang untuk S09: terdapat 14 segmen senyap digital (amplitudo
sampel <= 1) berdurasi minimal 1 detik, yaitu satu segmen 3,3 detik di awal
rekaman dan 13 segmen berdurasi 10,7 sampai 14,6 detik. Totalnya 170,2 detik
atau 28,4% dari 600,00 detik. Angka sekitar 39% pada catatan QC mendekati
proporsi bingkai 25 milidetik dengan tingkat sinyal di bawah -60 dBFS (243,2
detik, 40,5%); metode yang dipakai pada catatan QC belum terdokumentasi. Durasi
berisi sinyal pada S09 berada di bawah 10 menit menurut kedua ukuran tersebut.

7.4 Pemeriksaan teknis tambahan: peak sampel

  Berkas             Peak (dBFS)  Sampel pada nilai maksimum
  -----------------  -----------  --------------------------
  S01_T01_001.wav            0,0                          25
  S02_T01_001.wav           -3,1                           0
  S03_T01_001.wav           -4,2                           0
  S04_T01_001.wav           -0,3                           0
  S05_T01_001.wav           -1,0                           0
  S06_T01_001.wav           -0,2                           0
  S07_T01_001.wav           -0,1                           0
  S08_T01_001.wav           -0,6                           0
  S09_T01_001.wav            0,0                           2
  S10_T01_001.wav           -0,5                           0

Peak S01 dan S09 mencapai nilai maksimum 16-bit, dan peak S04, S06, S07, S08,
serta S10 berada di atas -1,0 dBFS. Metrik ini hanya menjadi penanda untuk
didengar ulang. Ada atau tidaknya distorsi pada berkas tersebut belum diperiksa
melalui pendengaran, sehingga label Quality tidak diubah. Perubahan label hanya
dilakukan setelah anggota kelompok mendengar ulang rekaman terkait dan alasannya
dicatat.

7.5 Tindak lanjut

Tidak ada berkas berlabel Reject, sehingga tidak ada rekaman ulang yang
tercatat. Berkas S01, S04, S06, S07, S08, S09, dan S10 perlu didengar ulang
berdasarkan Bagian 7.4, dan S09 berdasarkan Bagian 7.3.


--------------------------------------------------------------------------------
8. ANOTASI (annotation/annotation-semua.csv)
--------------------------------------------------------------------------------
8.1 Skema

Berkas memuat 2.188 baris segmen untuk 10 berkas audio. Pengodean UTF-8 dengan
BOM, pemisah koma.

  Kolom            Isi
  ---------------  -------------------------------------------------------
  file             Nama berkas audio
  segment_id       Nomor segmen dalam berkas; "-gap" menandai baris tanpa
                   transkripsi
  start, end       Posisi segmen pada berkas audio (detik)
  durasi_detik     Durasi segmen (detik)
  transkripsi      Teks transkripsi
  label_speaker    Label penutur
  label_bahasa     Jawa, Indonesia, Inggris, atau campuran
  label_dialek     Label dialek
  label_topik      Label topik rinci (16 label)
  label_kejadian   Kejadian khusus; teks bebas, "-" jika tidak ada
  confidence_asr   Skor kepercayaan ASR (kosong pada S07 dan baris tanpa
                   transkripsi)

Kolom Register, Annotator, Reviewer, dan Status yang dirancang pada
spesifikasi kelompok tidak ada pada berkas ini.

8.2 Kejadian khusus

Kolom label_kejadian berisi 238 baris dengan penanda selain tanda hubung.
Penanda yang ada antara lain: pengulangan/terbata, napas/desah, filler/ragu,
batuk/deham, tawa, musik, suara hewan, hening/jeda panjang, hening digital, dan
catatan tentang ASR (ucapan terlewat, kalimat berulang, kemungkinan halusinasi).
Penanda ini berupa teks bebas dan belum mengikuti tabel tag resmi.

8.3 Status review

Status review belum dapat dilaporkan sebagai selesai. Berkas tidak memiliki
kolom Annotator, Reviewer, maupun Status, sehingga tidak diketahui siapa yang
menyusun dan memeriksa tiap baris. Kolom confidence_asr terisi pada 1.641 baris
dan beberapa catatan kejadian menyebut ASR, yang menunjukkan bahwa transkripsi
berasal dari ASR otomatis. Belum ada bukti bahwa penutur asli dalam kelompok
telah memeriksa seluruh transkripsi. Seluruh transkripsi karena itu
diperlakukan sebagai DRAF yang wajib diperiksa manusia sebelum dipakai sebagai
data latih atau data uji. Label speaker S07 diberi catatan "tanpa verifikasi
akustik".


--------------------------------------------------------------------------------
9. KONVENSI
--------------------------------------------------------------------------------
Format data:
  - CSV: UTF-8, pemisah koma, header pada baris pertama, titik desimal pada
    anotasi dan metadata.
  - Audio: WAV, pcm_s16le, 16000 Hz, 1 channel. Berkas audio korpus tidak
    diberi denoise, normalisasi, kompresi, atau efek lain.
  - Satuan waktu: detik, angka desimal tanpa satuan.
  - Gender: M atau F.
  - Quality: Good, Acceptable, atau Reject.

Kode topik global yang dirancang kelompok:

  Kode  Topik
  ----  ---------------------
  T01   Introduction (Perkenalan)
  T02   Daily (Aktivitas sehari-hari)
  T03   Family (Keluarga)
  T04   Food (Makanan)
  T05   WorkEducation (Pekerjaan/pendidikan)
  T06   Travel (Perjalanan)
  T07   Culture (Budaya daerah)

Pada korpus saat ini seluruh berkas memakai kode T01 (lihat Bagian 3).

Pedoman transkripsi: belum ada berkas transcription_guideline.md. Konvensi
ejaan, penulisan tag kejadian, dan penanganan campur kode belum terdokumentasi
secara tertulis, sehingga transkripsi pada Bagian 8 belum dapat dinilai
konsistensinya terhadap suatu pedoman.


--------------------------------------------------------------------------------
10. KEPUTUSAN DESAIN (D1 SAMPAI D5)
--------------------------------------------------------------------------------
  ID  Keputusan                        Status
  --  -------------------------------  --------------------------------------
  D1  Dialek utama atau campuran       Belum ditetapkan secara tertulis. Data
      dialek                           aktual memuat tiga kelompok dialek
                                       (Bagian 4): Jawa Timuran 4 penutur,
                                       Jawa Tengahan/Mataraman 5 penutur,
                                       campuran Tengahan-Malangan 1 penutur.
  D2  Ejaan vokal a/o                  Belum terdokumentasi.
  D3  Penanganan consent bertanda      Belum ditetapkan. Tiga formulir
      tangan pada repositori publik    bertanda tangan (S02, S09, S10) ada
                                       di repositori; lihat Bagian 11.
  D4  Porsi spontaneous vs             Belum dicatat per rekaman. Rekaman
      conversation                     berbasis pertanyaan panduan.
  D5  Perangkat rekam utama            Belum terdokumentasi. Berkas akhir
                                       bersampling rate 16 kHz; sampling rate
                                       asli rekaman tidak dicatat.

Keputusan D1 sampai D5 perlu ditetapkan atau dikonfirmasi oleh kelompok, lalu
dicatat pada bagian ini dengan menghapus pernyataan "belum" di atas.


--------------------------------------------------------------------------------
11. ETIKA DAN INFORMED CONSENT
--------------------------------------------------------------------------------
Kondisi saat ini:
  - Folder consent/consent_form/ memuat tiga formulir bertanda tangan: S02, S09,
    dan S10.
  - Formulir untuk tujuh Speaker ID lain (S01, S03, S04, S05, S06, S07, S08)
    belum ada di repositori.
  - Berkas consent_log.csv dan templat formulir kosong belum ada.

Kebijakan privasi korpus:
  - Repositori hanya boleh memuat Speaker ID. Nama asli, nomor telepon,
    alamat, dan pemetaan nama ke Speaker ID disimpan di luar repositori.
  - Formulir bertanda tangan umumnya memuat nama dan tanda tangan penutur.
    Karena repositori dapat diakses mahasiswa lain, pengunggahannya
    memerlukan keputusan D3 yang dikonfirmasi ke dosen atau asisten.
  - Formulir consent sebaiknya menyebut secara eksplisit bahwa rekaman disimpan
    di GitHub dan dapat diakses dosen, asisten, dan mahasiswa lain.

Status kepatuhan consent untuk 10 penutur belum dapat dinyatakan lengkap.


--------------------------------------------------------------------------------
12. KETERBATASAN DAN PEKERJAAN YANG BELUM SELESAI
--------------------------------------------------------------------------------
Keterbatasan yang diketahui pada korpus saat ini:

  1. Transkripsi berasal dari ASR otomatis dan belum terdokumentasi sebagai
     hasil review manusia (Bagian 8.3). Seluruhnya berstatus draf.
  2. Berkas anotasi tidak memuat Annotator, Reviewer, Status, dan Register.
  3. Struktur berkas berbeda dari rancangan: satu berkas panjang per penutur
     (10 sampai 11,7 menit), bukan utterance pendek per topik; berkas anotasi
     dan qc_report.csv berada di lokasi lain (Bagian 3).
  4. Topik pada metadata dan anotasi belum selaras (Bagian 5.6). Kesesuaian isi
     audio dengan topik belum diverifikasi.
  5. Penutur S03 dan S09 berlabel non-asli dan S05 berlabel warisan pada
     anotasi, sedangkan kriteria kelompok adalah penutur asli (L1) Bahasa Jawa
     berusia minimal 18 tahun. Status ini perlu dikonfirmasi, termasuk
     keputusan apakah ketiga rekaman tetap digunakan.
  6. Durasi ucapan bersih belum diukur menyeluruh. Pada S09, durasi berisi
     sinyal berada di bawah 10 menit (Bagian 7.3).
  7. Porsi ucapan berbahasa Jawa tidak seragam (41,7% sampai 95,9% per
     penutur) dan korpus memuat segmen Indonesia, Inggris, serta campuran
     (Bagian 5.5).
  8. Tujuh berkas perlu didengar ulang berdasarkan metrik peak (Bagian 7.4).
  9. Daerah asal, rentang usia, perangkat rekam, lokasi rekaman, tanggal
     rekaman, anggota perekam, posisi mikrofon, recording level, dan teks
     prompt belum terdokumentasi.
 10. Berkas consent untuk tujuh Speaker ID dan consent_log.csv belum ada
     (Bagian 11).
 11. Pedoman transkripsi belum ada (Bagian 9).
 12. Belum ada pembagian data (train, dev, test) untuk Fase 2.
 13. Kolom label_speaker pada anotasi memuat teks tambahan di luar Speaker ID.
     Isi kolom ini perlu diperiksa agar hanya memuat Speaker ID, sesuai
     kebijakan privasi pada Bagian 11.


--------------------------------------------------------------------------------
13. CARA MENGGUNAKAN DAN MEMVERIFIKASI KORPUS
--------------------------------------------------------------------------------
Mengambil korpus:

  git clone https://github.com/rlukassa/Korpus_Bahasa_Jawa.git

Memeriksa format seluruh audio (membutuhkan ffprobe):

  for f in audio/S*/*.wav; do
    ffprobe -v error -show_entries stream=codec_name,sample_rate,channels,bits_per_sample \
      -of csv=p=0 "$f"
  done

Hasil yang diharapkan untuk setiap berkas: pcm_s16le,16000,1,16.

Membaca metadata dan anotasi dengan Python:

  import csv

  with open("metadata/metadata.csv", encoding="utf-8", newline="") as f:
      metadata = list(csv.DictReader(f))

  # berkas anotasi memakai BOM, gunakan utf-8-sig
  with open("annotation/annotation-semua.csv", encoding="utf-8-sig", newline="") as f:
      anotasi = list(csv.DictReader(f))

Saran penggunaan pada Fase 2:
  - Perlakukan transkripsi sebagai draf; periksa dan perbaiki sebelum training
    atau evaluasi.
  - Saring segmen berdasarkan label_bahasa jika diperlukan hanya ucapan Jawa.
  - Abaikan baris tanpa transkripsi (segment_id "-gap") dan perhatikan S09,
    yang memuat hening digital pada rentang waktu segmen.
  - Jika membagi data, gunakan pembagian per penutur (speaker-disjoint) agar
    tidak ada penutur yang muncul pada lebih dari satu subset.


--------------------------------------------------------------------------------
14. LISENSI DAN PENGGUNAAN
--------------------------------------------------------------------------------
Lisensi korpus belum ditetapkan. Penggunaan korpus dibatasi pada keperluan
akademik IF4071 (Fase 1 dan Fase 2) sampai lisensi dan cakupan informed consent
dipastikan. Penggunaan lain, termasuk redistribusi, memerlukan izin dari
kelompok dan kesesuaian dengan informed consent penutur.

Rujukan dokumen terkait:
  - Laporan Tugas Besar Fase 1 : documentation/Laporan Tugas Besar Fase 1.pdf
  - Spesifikasi tugas          : IF4071 Spesifikasi Tugas Besar Fase 1
