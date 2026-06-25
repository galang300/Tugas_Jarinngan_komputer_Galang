# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 14 — 802.11 WiFi
### Minggu ke-14

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa dapat menginvestigasi cara kerja WiFi (802.11) menggunakan Wireshark.

## 2. Dasar Teori

### 2.1 Beacon Frame
*Access Point* (AP) 802.11 secara berkala mengirimkan **Beacon Frame** untuk mengiklankan
keberadaannya, berisi informasi seperti **SSID**, **Beacon Interval (BI)**, dan **Sequence
Number (SN)**.

### 2.2 Association / Disassociation
Sebelum sebuah host dapat berkomunikasi melalui suatu AP, host harus melakukan **asosiasi**:
1. **Association Request** (Type=0, Subtype=0) → dikirim host ke AP.
2. **Association Response** (Type=0, Subtype=1) → dikirim AP ke host sebagai balasan.

Saat host berpindah AP atau melepas koneksi, terjadi proses **disasosiasi**.

### 2.3 Data Transfer
Setelah terasosiasi, data (misalnya request/response HTTP) dapat dikirim melalui AP. Frame
802.11 yang membawa data memiliki header tambahan dibandingkan frame Ethernet biasa, karena
sifat media nirkabel yang *broadcast* dan rawan kolisi/interferensi.

## 3. Alat dan Bahan
- Wireshark
- File trace: `Wireshark_802_11.pcap` (diunduh dari paket trace modul, karena tidak semua
  NIC nirkabel mendukung capture langsung frame 802.11)

## 4. Skenario pada File Trace
Berdasarkan modul, aktivitas yang terekam pada `Wireshark_802_11.pcap`:
- Host sudah terasosiasi dengan AP **"30 Munroe St"** saat capture dimulai.
- t = 24.82 s → host mengakses `http://gaia.cs.umass.edu/wireshark-labs/alice.txt`
- t = 32.82 s → host mengakses `http://www.cs.umass.edu`
- t = 49.58 s → host disasosiasi dari AP "30 Munroe St" dan mencoba ke AP `linksys_ses_24086`
  (gagal karena memerlukan kredensial/keamanan)
- t = 63.0 s → host kembali berasosiasi dengan AP "30 Munroe St"

## 5. Langkah Percobaan
1. Buka file `Wireshark_802_11.pcap` di Wireshark.
2. Amati **Beacon Frame** pertama pada daftar paket — catat SSID dan Beacon Interval-nya.
3. Telusuri paket pada t ≈ 24.82 s dan t ≈ 32.82 s untuk melihat proses pertukaran data
   (HTTP melalui 802.11).
4. Telusuri paket pada t ≈ 49.58 s dan t ≈ 63.0 s untuk mengamati proses
   Disassociation/Association Request/Response.

## 6. Hasil Pengamatan

### 6.1 Beacon Frame
```
[Sisipkan screenshot detail Beacon Frame (SSID, BI, SN) di sini]
```

### 6.2 Data Transfer (HTTP melalui 802.11)
```
[Sisipkan screenshot paket data pada t ≈ 24.82s dan t ≈ 32.82s di sini]
```

### 6.3 Association / Disassociation
```
[Sisipkan screenshot Association Request/Response dan Disassociation di sini]
```

## 7. Analisis

1. Apa nilai SSID dan Beacon Interval (BI) pada Beacon Frame yang Anda amati?
   ......................................................................

2. Berapa nilai *Type* dan *Subtype* pada Beacon Frame? ......................................................................

3. Pada t ≈ 24.82 s, tunjukkan paket yang berisi request HTTP ke `alice.txt`. Apakah frame
   tersebut dikirim langsung sebagai frame 802.11 Data, atau dibungkus dalam mekanisme lain
   (misalnya ACK setiap frame)? ......................................................................

4. Pada t ≈ 49.58 s, tunjukkan paket **Disassociation** dari AP "30 Munroe St". Apa nilai
   *Type/Subtype*-nya? ......................................................................

5. Tunjukkan paket **Association Request** dan **Association Response** saat host mencoba
   bergabung dengan AP `linksys_ses_24086`. Mengapa proses asosiasi ini gagal?
   ......................................................................

6. Bandingkan struktur frame 802.11 dengan frame Ethernet pada Modul 13. Apa bidang
   tambahan yang dimiliki frame 802.11 (misalnya 4 address field)? ......................................................................

## 8. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. IEEE Std 802.11, 1999 Edition (R2003).
3. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
