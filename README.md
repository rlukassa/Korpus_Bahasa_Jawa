# Korpus Suara Bahasa Jawa

Korpus suara Bahasa Jawa untuk Tugas Besar Fase 1 IF4071 Pemrosesan Ucapan (Semester 1 2026/2027, STEI ITB). Korpus ini dikumpulkan sebagai data untuk pengembangan sistem pengenal ucapan (ASR) Bahasa Jawa pada Fase 2.

## Ringkasan

| Aspek | Nilai |
|---|---|
| Bahasa | Bahasa Jawa (ISO 639-3 `jav`) |
| Penutur | 10 (5 laki-laki, 5 perempuan), Speaker ID S01 sampai S10 |
| Jumlah berkas audio | 10 (satu berkas per penutur) |
| Total durasi berkas | 6.516,77 detik (108,61 menit) |
| Format audio | WAV, PCM 16-bit, 16 kHz, mono |
| Hasil QC | 8 Good, 2 Acceptable, 0 Reject |
| Anotasi | 2.188 segmen; transkripsi berstatus draf dan belum direview |

## Struktur

```
audio/Sxx/           berkas audio per penutur
metadata/            metadata.csv
annotation/          annotation-semua.csv
qc/                  qc_report.csv
consent/consent_form/
documentation/       README.txt, laporan
```

## Dokumentasi lengkap

Tujuan, spesifikasi, statistik, hasil QC, konvensi, keputusan desain, keterbatasan, dan cara penggunaan korpus dijelaskan pada [documentation/README.txt](documentation/README.txt).

## Catatan penggunaan

- Transkripsi berasal dari ASR otomatis dan wajib diperiksa manusia sebelum dipakai sebagai data latih atau data uji.
- Repositori hanya memuat Speaker ID. Data pribadi penutur tidak boleh ditambahkan.
- Penggunaan korpus dibatasi pada keperluan akademik IF4071 sampai lisensi dan cakupan informed consent dipastikan.

## Anggota kelompok

Danendra Shafi Athallah (13523136), Jonathan Kenan Budianto (13523139), Jovandra Otniel Panagalambok Siregar (13523141), Muhammad Farrel Wibowo (13523153), Lukas Raja Agripa (13523158).
