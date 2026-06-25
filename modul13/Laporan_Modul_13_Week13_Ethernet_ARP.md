# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 13 — Ethernet and ARP
### Minggu ke-13

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa dapat menginvestigasi cara kerja Ethernet dan ARP menggunakan Wireshark.

## 2. Dasar Teori

### 2.1 Frame Ethernet
Frame Ethernet adalah unit data pada *link layer* yang membawa datagram IP (dan protokol
lapisan atas lainnya). Bagian utamanya meliputi: **Destination MAC Address**, **Source MAC
Address**, **Type** (mengindikasikan protokol lapisan jaringan di dalamnya, mis. `0x0800`
untuk IPv4), **Data/Payload**, dan **Frame Check Sequence (FCS)**.

### 2.2 Address Resolution Protocol (ARP)
ARP (RFC 826) digunakan oleh perangkat IP untuk menentukan **MAC address** dari sebuah
**alamat IP** pada jaringan lokal yang sama. Mekanismenya:
1. Host mengirim **ARP Request** secara *broadcast* ("Who has IP X? Tell IP Y").
2. Host yang memiliki alamat IP tersebut membalas dengan **ARP Reply** secara *unicast*,
   berisi MAC address miliknya.
3. Hasil pemetaan IP-ke-MAC disimpan sementara pada **ARP cache** untuk efisiensi (tidak perlu
   broadcast berulang).

Perintah `arp` (bukan protokol ARP) digunakan untuk melihat/memanipulasi isi ARP cache:
- `arp -a` (Windows) atau `arp` tanpa argumen → menampilkan isi cache.
- `arp -d *` (Windows) atau `arp -d *` dengan hak akses root (Linux/Mac) → menghapus cache.

## 3. Alat dan Bahan
- Wireshark
- Browser web
- Command Prompt/Terminal dengan hak akses administrator/root (untuk menghapus ARP cache)

## 4. Langkah Percobaan

### 4.1 Capture dan Analisis Frame Ethernet
1. Bersihkan cache browser.
2. Mulai capture Wireshark.
3. Akses: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html`
4. Hentikan capture.
5. Nonaktifkan protokol di atas Ethernet (Analyze → Enabled Protocols → uncheck **IP**)
   agar hanya frame Ethernet yang ditampilkan.

### 4.2 ARP Caching dan Observasi
1. Lihat isi ARP cache: `arp -a` (Windows) atau `arp` (Linux/Mac).
2. Kosongkan ARP cache: `arp -d *` (perlu hak akses admin/root).
3. Bersihkan cache browser, lalu mulai capture Wireshark.
4. Akses kembali: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-lab-file3.html`
5. Hentikan capture, nonaktifkan protokol IP (sama seperti langkah 4.1.5) agar terlihat
   pesan ARP Request/Reply sebelum frame IP dikirim.

## 5. Hasil Pengamatan

### 5.1 Frame Ethernet
```
[Sisipkan screenshot detail frame Ethernet (Source MAC, Destination MAC, Type) di sini]
```

### 5.2 ARP Cache Sebelum Dihapus
```
[Sisipkan screenshot hasil "arp -a" di sini]
```

### 5.3 ARP Request/Reply
```
[Sisipkan screenshot Wireshark menampilkan ARP Request (broadcast) dan ARP Reply (unicast) di sini]
```

## 6. Analisis

1. Sebutkan alamat MAC sumber dan tujuan pada frame Ethernet yang membawa pesan HTTP
   GET Anda. ......................................................................

2. Berapa nilai bidang *Type* pada frame Ethernet tersebut, dan apa artinya?
   ......................................................................

3. Pada ARP Request, ke alamat MAC berapa pesan tersebut dikirim (broadcast)? Apa isi
   pertanyaan dalam pesan tersebut ("Who has ... Tell ...")? ......................................................................

4. Pada ARP Reply, siapa pengirim dan siapa penerimanya? Apakah dikirim secara unicast
   atau broadcast? ......................................................................

5. Bandingkan ARP cache sebelum dan sesudah Anda mengakses halaman web. Apakah muncul
   entry baru? ......................................................................

6. Mengapa ARP hanya bekerja pada jaringan lokal (satu segmen/subnet) dan tidak dapat
   digunakan untuk menentukan MAC address host pada jaringan lain? ......................................................................

## 7. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. RFC 826 — *An Ethernet Address Resolution Protocol*.
3. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
