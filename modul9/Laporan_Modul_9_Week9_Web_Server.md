# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 9 — Web Server
### Minggu ke-9

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
Mahasiswa bisa membuat program web server sederhana berbasis TCP socket programming.

## 2. Dasar Teori

Sebuah web server pada dasarnya adalah **server TCP** yang:
1. Membuka *welcoming socket* dan mendengarkan koneksi pada port tertentu.
2. Menerima request HTTP (umumnya metode `GET`) dari klien (browser).
3. Mengurai (*parse*) baris request untuk mendapatkan nama file yang diminta.
4. Membuka file tersebut dari sistem berkas server.
5. Jika file ditemukan → mengirim *header* HTTP `200 OK` diikuti isi file.
6. Jika file tidak ditemukan → mengirim respons `404 Not Found`.
7. Menutup koneksi.

Format umum baris status HTTP yang dikirim server:
```
HTTP/1.1 200 OK
```
atau
```
HTTP/1.1 404 Not Found
```

## 3. Alat dan Bahan
- Python 3
- Browser web
- File HTML uji (contoh: `HelloWorld.html`)
- Komputer/host pada jaringan yang sama untuk mengakses server dari luar (opsional)

## 4. Kode Web Server

Berikut kode lengkap web server (`HTTPServer.py`) hasil pelengkapan kerangka kode
pada modul, beserta penjelasannya:

```python
# import socket module
from socket import *
import sys  # In order to terminate the program

serverPort = 6789
serverSocket = socket(AF_INET, SOCK_STREAM)

# Prepare a server socket
serverSocket.bind(('', serverPort))
serverSocket.listen(1)

while True:
    # Establish the connection
    print('Ready to serve...')
    connectionSocket, addr = serverSocket.accept()

    try:
        message = connectionSocket.recv(1024).decode()
        filename = message.split()[1]
        f = open(filename[1:])
        outputdata = f.readlines()

        # Send one HTTP header line into socket
        connectionSocket.send("HTTP/1.1 200 OK\r\n\r\n".encode())

        # Send the content of the requested file to the client
        for i in range(0, len(outputdata)):
            connectionSocket.send(outputdata[i].encode())
        connectionSocket.send("\r\n".encode())
        connectionSocket.close()

    except IOError:
        # Send response message for file not found
        connectionSocket.send("HTTP/1.1 404 Not Found\r\n\r\n".encode())
        connectionSocket.send("<html><body><h1>404 Not Found</h1></body></html>\r\n".encode())

        # Close client socket
        connectionSocket.close()

serverSocket.close()
sys.exit()  # Terminate the program after sending the corresponding data
```

**Penjelasan bagian penting:**
- `serverSocket.bind(('', serverPort))` → mengikat socket ke seluruh interface (`''`) pada port 6789.
- `serverSocket.listen(1)` → server siap menerima maksimal 1 koneksi dalam antrian.
- `serverSocket.accept()` → menunggu dan menerima koneksi dari klien, menghasilkan `connectionSocket` baru khusus untuk klien tersebut.
- `message.split()[1]` → mengambil token kedua dari baris request HTTP (`GET /namafile HTTP/1.1`), yaitu path file yang diminta.
- `filename[1:]` → menghapus karakter `/` di awal path agar menjadi nama file relatif.
- Blok `try/except IOError` → menangani kasus file tidak ditemukan dengan mengirim `404 Not Found`.

## 5. Langkah Menjalankan Server
1. Letakkan file `HelloWorld.html` pada folder yang sama dengan `HTTPServer.py`.
2. Jalankan server: `python HTTPServer.py`
3. Catat alamat IP host yang menjalankan server (`ipconfig` / `ifconfig`): ......................
4. Dari browser (komputer lain atau komputer yang sama), akses:
   ```
   http://<alamat_IP_server>:6789/HelloWorld.html
   ```
5. Uji juga dengan file yang **tidak ada** untuk memverifikasi respons `404 Not Found`.

## 6. Hasil Pengamatan

### 6.1 Tampilan Terminal Server saat Menerima Request
```
[Sisipkan screenshot terminal server di sini]
```

### 6.2 Tampilan Browser saat Request Berhasil (200 OK)
```
[Sisipkan screenshot browser menampilkan isi HelloWorld.html di sini]
```

### 6.3 Tampilan Browser saat File Tidak Ditemukan (404 Not Found)
```
[Sisipkan screenshot browser menampilkan 404 Not Found di sini]
```

## 7. Analisis

1. Apa yang terjadi jika nomor port pada URL browser dihilangkan (tanpa `:6789`)? Mengapa?
   ......................................................................

2. Bagaimana server menentukan apakah harus mengirim `200 OK` atau `404 Not Found`?
   ......................................................................

3. Pada kode di atas, server hanya dapat melayani **satu klien pada satu waktu**.
   Jelaskan mengapa hal ini bisa menjadi masalah pada server dengan banyak pengguna.
   ......................................................................

## 8. Latihan Tambahan

### 8.1 Web Server Multithreading
Modifikasi server agar dapat melayani beberapa klien secara bersamaan menggunakan modul `threading`.

```python
# [Sisipkan kode server multithreaded Anda di sini]
```

```
[Sisipkan screenshot pengujian beberapa klien secara bersamaan di sini]
```

### 8.2 Membuat HTTP Client Sendiri (`client.py`)
Format menjalankan: `client.py server_host server_port filename`

```python
# [Sisipkan kode client.py Anda di sini]
```

```
[Sisipkan screenshot hasil eksekusi client.py di sini]
```

## 9. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
