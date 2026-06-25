# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 3 — HTTP
### Minggu ke-3

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa dapat menginvestigasi cara kerja protokol HTTP menggunakan Wireshark.

## 2. Dasar Teori

**HyperText Transfer Protocol (HTTP)** adalah protokol lapisan aplikasi yang digunakan
untuk transfer dokumen web, berjalan di atas **TCP**. Beberapa konsep penting:

- **GET/Response** — klien mengirim request `GET` dan server membalas dengan status
  (mis. `200 OK`) beserta isi dokumen.
- **Conditional GET** — browser yang memiliki salinan tersimpan (*cache*) akan menyertakan
  header `If-Modified-Since`. Jika dokumen belum berubah, server membalas `304 Not Modified`
  tanpa mengirim ulang isi dokumen.
- **Dokumen besar** — jika ukuran respons melebihi *Maximum Segment Size* (MSS) TCP,
  Wireshark akan menampilkannya sebagai beberapa segmen dengan info
  `[TCP segment of a reassembled PDU]`.
- **Embedded Objects** — satu halaman HTML dapat memuat beberapa objek lain (gambar, dll.)
  yang masing-masing memerlukan request HTTP `GET` terpisah.
- **HTTP Authentication** — otentikasi dasar (*Basic Authentication*) mengirim kredensial
  dalam header `Authorization: Basic <string Base64>`. Base64 **bukan enkripsi**, hanya
  encoding, sehingga kredensial mudah didekode kembali.

## 3. Alat dan Bahan
- Wireshark
- Browser web

## 4. Langkah Percobaan

### 4.1 Basic HTTP GET/Response
1. Bersihkan cache browser.
2. Mulai capture Wireshark, filter tampilan `http`.
3. Akses: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html`
4. Hentikan capture.

### 4.2 HTTP Conditional GET/Response
1. Bersihkan cache browser.
2. Mulai capture Wireshark.
3. Akses: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html`
4. Akses kembali (refresh) URL yang sama.
5. Hentikan capture, filter `http`.

### 4.3 Retrieving Long Documents
1. Bersihkan cache browser, mulai capture.
2. Akses: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html` (Bill of Rights)
3. Hentikan capture, filter `http` lalu hapus filter untuk melihat seluruh segmen TCP.

### 4.4 HTML Documents dengan Embedded Objects
1. Bersihkan cache browser, mulai capture.
2. Akses: `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html`
3. Hentikan capture, filter `http`.

### 4.5 HTTP Authentication
1. Bersihkan cache browser, mulai capture.
2. Akses: `http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html`
   (username: `wireshark-students`, password: `network`)
3. Hentikan capture, filter `http`.
4. Decode string Base64 pada header `Authorization` melalui
   `http://www.motobit.com/util/base64-decoder-encoder.asp`.

## 5. Hasil Pengamatan

### 5.1 Basic GET/Response
```
[Sisipkan screenshot Wireshark di sini]
```
**Analisis:**
1. Apa nomor urut (no. paket) pesan `GET` dan pesan respons `200 OK`? .....................................
2. Sebutkan isi header request (Host, User-Agent, Accept, dll.) dan header respons
   (Content-Type, Content-Length, Date, dll.) yang Anda temukan. .....................................

### 5.2 Conditional GET/Response
```
[Sisipkan screenshot Wireshark untuk request pertama dan kedua di sini]
```
**Analisis:**
1. Pada request **kedua**, header tambahan apa yang muncul dibandingkan request pertama?
   .....................................
2. Apa status code yang dikembalikan server pada respons kedua? Mengapa demikian?
   .....................................
3. Apa fungsi mekanisme *Conditional GET* ini bagi efisiensi jaringan? .....................................

### 5.3 Retrieving Long Documents
```
[Sisipkan screenshot Wireshark menampilkan beberapa segmen TCP untuk satu respons HTTP di sini]
```
**Analisis:**
1. Berapa banyak segmen TCP yang digunakan untuk membawa satu respons HTTP tersebut?
   .....................................
2. Apa arti info `[TCP segment of a reassembled PDU]` yang muncul pada kolom Info?
   .....................................

### 5.4 HTML dengan Embedded Objects
```
[Sisipkan screenshot Wireshark menampilkan beberapa pasangan request/response HTTP di sini]
```
**Analisis:**
1. Berapa banyak request `GET` total yang dikirim browser untuk menampilkan halaman ini?
   .....................................
2. Apakah seluruh objek (gambar) diambil dari server yang sama? Jelaskan. .....................................

### 5.5 HTTP Authentication
```
[Sisipkan screenshot header Authorization pada request GET di sini]
```
**Analisis:**
1. Apa isi string Base64 pada header `Authorization: Basic ...` yang Anda temukan?
   .....................................
2. Setelah didekode, apa username dan password yang terungkap? .....................................
3. Mengapa metode otentikasi dasar (Basic Authentication) ini dikatakan **tidak aman**
   jika dikirim tanpa HTTPS? .....................................

## 6. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
