# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 11 — DHCP
### Minggu ke-11

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa dapat menginvestigasi cara kerja protokol DHCP menggunakan Wireshark.

## 2. Dasar Teori

**Dynamic Host Configuration Protocol (DHCP)** digunakan untuk memberikan alamat IP serta
informasi konfigurasi jaringan lain (subnet mask, default gateway, DNS server) secara otomatis
kepada host yang terhubung ke jaringan. DHCP bekerja melalui empat jenis pesan yang biasa
disingkat **DORA**:

| Pesan | Pengirim | Keterangan |
|---|---|---|
| **D**iscover | Klien → Broadcast | Klien mencari server DHCP di jaringan |
| **O**ffer | Server → Klien | Server menawarkan sebuah alamat IP |
| **R**equest | Klien → Broadcast | Klien meminta (mengonfirmasi) alamat IP yang ditawarkan |
| **A**ck | Server → Klien | Server mengonfirmasi pemberian alamat IP tersebut |

Keempat pesan ini dibawa di atas **UDP**, dengan port tujuan **67** (server) dan port sumber **68** (klien).

## 3. Alat dan Bahan
- Wireshark
- Command Prompt/Terminal dengan hak akses administrator/root
- File trace (jika diperlukan): `dhcp-wireshark-trace1-1.pcapng`

## 4. Langkah Percobaan

**Windows:**
```
ipconfig /release
(jalankan Wireshark, mulai capture)
ipconfig /renew
(hentikan capture setelah beberapa detik)
```

**MacOS:**
```
sudo ipconfig set en0 none
(jalankan Wireshark, mulai capture)
sudo ipconfig set en0 dhcp
(hentikan capture setelah beberapa detik)
```

**Linux:**
```
sudo ip addr flush en0
sudo dhclient -r
(jalankan Wireshark, mulai capture)
sudo dhclient en0
(hentikan capture setelah beberapa detik)
```

Setelah capture berhenti, terapkan filter tampilan `dhcp` pada Wireshark untuk menampilkan
hanya keempat pesan DHCP (Discover, Offer, Request, ACK).

## 5. Hasil Pengamatan

```
[Sisipkan screenshot Wireshark dengan filter "dhcp" yang menampilkan
Discover, Offer, Request, dan ACK di sini]
```

| No. | Waktu | Sumber | Tujuan | Pesan |
|---|---|---|---|---|
| | | | | DHCP Discover |
| | | | | DHCP Offer |
| | | | | DHCP Request |
| | | | | DHCP ACK |

## 6. Analisis

1. Mengapa pesan **Discover** dan **Request** dikirim ke alamat broadcast
   (`255.255.255.255`), sedangkan **Offer** dan **ACK** ditujukan ke alamat tertentu?
   ......................................................................

2. Periksa bidang *Transaction ID* pada keempat pesan tersebut. Apakah nilainya sama
   untuk satu siklus DORA? Jelaskan fungsinya. ......................................................................

3. Pada pesan **Offer**, alamat IP apa yang ditawarkan oleh server kepada klien?
   ......................................................................

4. Pada pesan **ACK**, periksa nilai *lease time* (waktu sewa) yang diberikan. Berapa
   lamanya? ......................................................................

5. Berapa lama (dalam waktu/timestamp) yang dibutuhkan sejak pesan Discover dikirim
   hingga pesan ACK diterima oleh klien? ......................................................................

6. Apa alamat IP dan MAC address server DHCP pada jaringan Anda? ......................................................................

## 7. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
