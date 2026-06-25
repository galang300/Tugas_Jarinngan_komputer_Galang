# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 12 — ICMP dan Asistensi Tugas Besar
### Minggu ke-12

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
1. Mahasiswa dapat menginvestigasi cara kerja protokol ICMP menggunakan Wireshark.
2. Mahasiswa dapat membuat program ICMP Pinger.
3. Melakukan asistensi dan laporan progress pengerjaan tugas besar.

## 2. Dasar Teori

**Internet Control Message Protocol (ICMP)** digunakan oleh host dan router untuk
saling bertukar informasi kontrol/kesalahan jaringan, antara lain:

| Type | Kode | Keterangan |
|---|---|---|
| 0 | 0 | Echo Reply (balasan ping) |
| 8 | 0 | Echo Request (permintaan ping) |
| 11 | 0 | Time-to-live exceeded in transit (digunakan oleh traceroute) |
| 3 | x | Destination Unreachable |

Program **Ping** menggunakan pesan ICMP *Echo Request*/*Echo Reply* untuk memeriksa apakah
sebuah host aktif (*reachable*), serta menghitung *Round Trip Time* (RTT). Program **Traceroute**
(pada Windows: `tracert`) mengirim paket dengan TTL bertingkat untuk memetakan jalur router
menuju tujuan, memanfaatkan pesan ICMP *Time-to-Live exceeded*.

## 3. Alat dan Bahan
- Wireshark
- Command Prompt/Terminal
- Python 3 (untuk membuat program ICMP Pinger)
- File trace (jika diperlukan): `icmp-ethereal-trace-1`, `icmp-ethereal-trace-2`

## 4. Langkah Percobaan

### 4.1 ICMP dan Ping
1. Jalankan Wireshark, mulai capture.
2. Jalankan: `ping -n 10 <hostname_tujuan>` (Windows) atau `ping -c 10 <hostname_tujuan>` (Linux/Mac).
3. Hentikan capture, terapkan filter `icmp`.

### 4.2 ICMP dan Traceroute
1. Jalankan Wireshark, mulai capture.
2. Jalankan: `tracert <hostname_tujuan>` (Windows) atau `traceroute <hostname_tujuan>` (Linux/Mac).
3. Hentikan capture, terapkan filter `icmp`.

### 4.3 Program ICMP Pinger (Python)
Buat program Python sederhana yang mengirimkan paket ICMP Echo Request dan menerima
Echo Reply, lalu menghitung RTT-nya (raw socket ICMP).

```python
# [Sisipkan kode program ICMP Pinger Anda di sini]
# Contoh struktur umum:
# 1. Membuat raw socket ICMP
# 2. Membentuk header ICMP (Type=8, Code=0, Checksum, Identifier, Sequence Number)
# 3. Mengirim paket Echo Request ke alamat tujuan
# 4. Menunggu dan menerima Echo Reply
# 5. Menghitung selisih waktu kirim-terima sebagai RTT
```

## 5. Hasil Pengamatan

### 5.1 Ping
```
[Sisipkan screenshot Command Prompt hasil ping di sini]
[Sisipkan screenshot Wireshark dengan filter "icmp" di sini]
```

### 5.2 Traceroute
```
[Sisipkan screenshot Command Prompt hasil tracert/traceroute di sini]
[Sisipkan screenshot Wireshark paket ICMP Time-to-live exceeded di sini]
```

### 5.3 Program ICMP Pinger
```
[Sisipkan screenshot hasil eksekusi program ICMP Pinger di sini]
```

## 6. Analisis

1. Berapa nilai Type dan Code pada paket ICMP yang dikirim oleh program Ping (request)?
   Dan pada balasannya (reply)? ......................................................................

2. Apa isi bidang *Identifier* dan *Sequence Number* pada paket ICMP Echo Request/Reply,
   dan apa fungsinya? ......................................................................

3. Berapa rata-rata RTT (Round Trip Time) hasil ping Anda? ......................................................................

4. Pada hasil traceroute, identifikasi alamat IP setiap router (hop) yang dilewati paket
   menuju tujuan. Tunjukkan paket ICMP `Time-to-live exceeded` yang dikembalikan oleh
   masing-masing router tersebut. ......................................................................

5. Pada program ICMP Pinger yang Anda buat, bandingkan hasil RTT-nya dengan hasil
   program `ping` bawaan sistem operasi. Apakah hasilnya konsisten? ......................................................................

## 7. Asistensi Tugas Besar

| Item | Keterangan |
|---|---|
| Topik Tugas Besar | ...................................... |
| Progress saat ini (%) | ...................................... |
| Modul/fitur yang sudah selesai | ...................................... |
| Modul/fitur yang belum selesai | ...................................... |
| Kendala yang dihadapi | ...................................... |
| Rencana penyelesaian | ...................................... |
| Catatan/arahan asisten | ...................................... |

## 8. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
