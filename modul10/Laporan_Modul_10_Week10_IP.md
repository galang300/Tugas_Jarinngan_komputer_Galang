# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 10 — IP
### Minggu ke-10

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa dapat menginvestigasi cara kerja protokol IP menggunakan Wireshark, dengan fokus
pada datagram IPv4 (dasar & fragmentasi) dan IPv6.

## 2. Dasar Teori

### 2.1 Time-To-Live (TTL) dan Traceroute
`traceroute` (Linux/MacOS) atau `tracert` (Windows) mengirim datagram secara berurutan dengan
nilai TTL = 1, 2, 3, ... . Setiap router yang dilewati akan mengurangi TTL sebesar 1; jika TTL
mencapai 0, router mengirim pesan **ICMP Type 11 (TTL-exceeded)** kembali ke pengirim. Dengan
cara ini, alamat IP setiap router pada jalur ke tujuan dapat diketahui.

### 2.2 Fragmentasi IP
Jika ukuran datagram IP melebihi *Maximum Transmission Unit* (MTU) pada suatu link, datagram
akan dipecah (*fragmented*) menjadi beberapa datagram IP yang lebih kecil. Setiap fragmen memiliki
*Identification* yang sama, namun *Fragment Offset* yang berbeda, serta flag `More Fragments (MF)`
untuk menandai fragmen terakhir.

### 2.3 IPv6
IPv6 menggunakan alamat 128-bit (dibandingkan 32-bit pada IPv4) untuk mengatasi keterbatasan
ruang alamat IPv4. Resolusi nama ke alamat IPv6 menggunakan DNS record tipe **AAAA**.

## 3. Alat dan Bahan
- Wireshark
- Command Prompt/Terminal (untuk `traceroute`/`tracert`)
- File trace (jika tidak dapat capture langsung): `ip-wireshark-trace1-1.pcapng`,
  `ip-wireshark-trace2-1.pcapng`

## 4. Langkah Percobaan

1. Jalankan Wireshark, mulai *capture*.
2. Jalankan traceroute ke `gaia.cs.umass.edu` dengan ukuran paket kecil (56 byte):
   - Linux/MacOS: `traceroute gaia.cs.umass.edu 56`
   - Windows: `tracert gaia.cs.umass.edu`
3. Jalankan traceroute kedua ke tujuan yang sama dengan ukuran paket besar (3000 byte) — *khusus
   Linux/MacOS* (program `tracert` Windows tidak mendukung pengaturan ukuran paket):
   ```
   traceroute gaia.cs.umass.edu 3000
   ```
4. Hentikan capture Wireshark.
5. Terapkan filter tampilan `udp||icmp` untuk melihat seluruh paket UDP/ICMP traceroute.
6. Terapkan filter `ip.src==<IP_anda> and ip.dst==<IP_tujuan> and udp and !icmp` untuk melihat
   hanya segmen UDP yang dikirim host.
7. Terapkan filter `ip.dst==<IP_anda> and icmp` untuk melihat balasan ICMP TTL-exceeded dari router.
8. Untuk pengamatan IPv6, buka file `ip-wireshark-trace2-1.pcapng` (hasil mengakses
   `www.youtube.com`) dan amati paket DNS AAAA serta datagram IPv6.

## 5. Hasil Pengamatan

### 5.1 Bagian 1 — IPv4 Dasar

**Filter `udp||icmp`:**
```
[Sisipkan screenshot capture di sini]
```

| No. | Sumber | Tujuan | Protokol | Keterangan |
|---|---|---|---|---|
| | | | | |
| | | | | |

**Analisis:**
1. Berapa alamat IP host (sumber) Anda? .....................................
2. Berapa alamat IP tujuan (`gaia.cs.umass.edu`)? .....................................
3. Tunjukkan rangkaian segmen UDP traceroute yang dikirim host Anda
   (port sumber sama, port tujuan bertambah pada setiap kiriman). Jelaskan pola nomor portnya:
   .....................................
4. Tunjukkan paket ICMP `Time-to-live exceeded` yang dikembalikan oleh router.
   Dari alamat IP router mana saja balasan tersebut diterima (urutkan sesuai hop)?
   .....................................

### 5.2 Bagian 2 — Fragmentasi

**Capture traceroute dengan paket 3000 byte, diurutkan berdasarkan waktu:**
```
[Sisipkan screenshot capture di sini]
```

**Analisis:**
1. Apakah datagram 3000-byte tersebut terpecah menjadi beberapa fragmen IP? Berapa jumlah
   fragmennya? .....................................
2. Berapa nilai *Identification* pada seluruh fragmen tersebut (harus sama)? .....................................
3. Berapa *Fragment Offset* pada setiap fragmen, dan fragmen mana yang memiliki flag
   `More Fragments = 0` (fragmen terakhir)? .....................................
4. Berapa MTU link yang digunakan (berdasarkan ukuran maksimum fragmen)? .....................................

### 5.3 Bagian 3 — IPv6

**Capture `ip-wireshark-trace2-1.pcapng`:**
```
[Sisipkan screenshot capture di sini]
```

**Analisis:**
1. Tunjukkan paket DNS request tipe **AAAA** untuk `youtube.com`. Pada waktu (timestamp) berapa
   paket tersebut dikirim? .....................................
2. Berapa alamat IPv6 sumber dan tujuan pada paket DNS tersebut? .....................................
3. Bandingkan format alamat IPv6 dengan IPv4 yang Anda amati pada Bagian 1. Apa perbedaan
   strukturnya? .....................................

## 6. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
