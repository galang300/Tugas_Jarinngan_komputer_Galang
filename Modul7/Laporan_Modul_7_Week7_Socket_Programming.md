# LAPORAN PRAKTIKUM JARINGAN KOMPUTER
## Modul 7 — Socket Programming: Membuat Aplikasi Jaringan
### Minggu ke-7

| | |
|---|---|
| **Nama** | ............................................ |
| **NIM** | ............................................ |
| **Kelas** | ............................................ |
| **Tanggal Praktikum** | ............................................ |
| **Asisten Praktikum** | ............................................ |

---

## 1. Tujuan Praktikum
1. Mahasiswa bisa membuat program berbasis socket UDP.
2. Mahasiswa bisa membuat program berbasis socket TCP.

## 2. Dasar Teori

### 2.1 Socket
Socket adalah antarmuka (pintu) yang menghubungkan proses aplikasi dengan layanan
transport-layer (TCP/UDP) pada sistem operasi. Developer aplikasi memiliki kendali penuh
atas sisi aplikasi dari socket, tetapi tidak memiliki kendali atas sisi transport-layer-nya.

### 2.2 Perbedaan UDP dan TCP

| Aspek | UDP | TCP |
|---|---|---|
| Sifat koneksi | *Connectionless* (tanpa koneksi) | *Connection-oriented* (berorientasi koneksi, *three-way handshake*) |
| Keandalan | Tidak menjamin data sampai/berurutan | Menjamin data sampai secara utuh dan berurutan |
| Alamat tujuan | Harus dilampirkan ke setiap paket (`sendto`) | Cukup sekali saat `connect()`, selanjutnya data dikirim seperti aliran byte |
| Kecepatan/overhead | Lebih cepat, overhead kecil | Lebih lambat, overhead lebih besar karena ada kontrol |
| Contoh penggunaan | DNS, streaming, SNMP | HTTP, FTP, email |

### 2.3 Konsep Aplikasi Client-Server
Pada praktikum ini dibuat aplikasi client-server sederhana:
1. Klien membaca satu baris karakter dari keyboard dan mengirimkannya ke server.
2. Server menerima data tersebut dan mengubahnya menjadi huruf besar (*uppercase*).
3. Server mengirimkan kembali data yang sudah dimodifikasi ke klien.
4. Klien menerima dan menampilkan data yang sudah dimodifikasi tersebut.

## 3. Alat dan Bahan
- Python 3 (sudah terinstall)
- Text editor / IDE (VS Code, dsb.)
- 1–2 komputer/terminal yang terhubung pada jaringan yang sama
- Wireshark (opsional, untuk mengamati segmen yang dikirim)

## 4. Langkah Percobaan

### 4.1 Program Socket dengan UDP

**UDPClient.py**
```python
from socket import *
serverName = 'hostname'
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_DGRAM)
message = input('Input lowercase sentence:')
clientSocket.sendto(message.encode(), (serverName, serverPort))
modifiedMessage, serverAddress = clientSocket.recvfrom(2048)
print(modifiedMessage.decode())
clientSocket.close()
```

**UDPServer.py**
```python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET, SOCK_DGRAM)
serverSocket.bind(('', serverPort))
print("The server is ready to receive")
while True:
    message, clientAddress = serverSocket.recvfrom(2048)
    modifiedMessage = message.decode().upper()
    serverSocket.sendto(modifiedMessage.encode(), clientAddress)
```

**Langkah pengujian:**
1. Jalankan `UDPServer.py` pada komputer/terminal server.
2. Jalankan `UDPClient.py` pada komputer/terminal klien (sesuaikan `serverName` dengan alamat IP/hostname server).
3. Ketikkan kalimat pada klien, lalu amati hasil yang dikembalikan server.

### 4.2 Program Socket dengan TCP

**TCPClient.py**
```python
from socket import *
serverName = 'servername'
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_STREAM)
clientSocket.connect((serverName, serverPort))
sentence = input('Input lowercase sentence:')
clientSocket.send(sentence.encode())
modifiedSentence = clientSocket.recv(1024)
print('From Server:', modifiedSentence.decode())
clientSocket.close()
```

**TCPServer.py**
```python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET, SOCK_STREAM)
serverSocket.bind(('', serverPort))
serverSocket.listen(1)
print('The server is ready to receive')

while True:
    connectionSocket, addr = serverSocket.accept()
    sentence = connectionSocket.recv(1024).decode()
    capitalizedSentence = sentence.upper()
    connectionSocket.send(capitalizedSentence.encode())
    connectionSocket.close()
```

**Langkah pengujian:**
1. Jalankan `TCPServer.py` di sisi server.
2. Jalankan `TCPClient.py` di sisi klien.
3. Ketikkan kalimat pada klien, amati hasil dari server.
4. Bandingkan proses koneksi TCP (ada *three-way handshake* via `connect()`/`accept()`) dengan UDP yang tidak memerlukan koneksi.

## 5. Hasil Pengamatan

### 5.1 Hasil Eksekusi UDP
```
[Sisipkan screenshot terminal server & client UDP di sini]
```

### 5.2 Hasil Eksekusi TCP
```
[Sisipkan screenshot terminal server & client TCP di sini]
```

### 5.3 (Opsional) Capture Wireshark
```
[Sisipkan screenshot Wireshark yang menunjukkan segmen UDP/TCP yang terkirim di sini]
```

## 6. Analisis

1. Jelaskan fungsi setiap baris kode pada `UDPClient.py` dan `UDPServer.py`
   (gunakan kata-kata sendiri):
   - `socket(AF_INET, SOCK_DGRAM)` → ......................................
   - `bind(('', serverPort))` → ......................................
   - `sendto()` / `recvfrom()` → ......................................

2. Jelaskan fungsi setiap baris kode pada `TCPClient.py` dan `TCPServer.py`:
   - `socket(AF_INET, SOCK_STREAM)` → ......................................
   - `connect()` → ......................................
   - `listen()` / `accept()` → ......................................
   - `send()` / `recv()` → ......................................

3. Apa perbedaan utama yang Anda amati antara proses komunikasi UDP dan TCP
   pada percobaan ini? ......................................

4. Mengapa pada UDP, server harus melampirkan alamat tujuan (`clientAddress`)
   secara eksplisit ke setiap paket balasan, sedangkan pada TCP tidak perlu? 
   ......................................

## 7. Tugas Pengembangan (Opsional)
Modifikasi salah satu program (UDP atau TCP) sehingga, misalnya, server menghitung
jumlah kemunculan huruf tertentu (mis. huruf 's') pada kalimat yang dikirim, alih-alih
mengubahnya menjadi huruf besar.

```python
# [Sisipkan kode modifikasi Anda di sini]
```

```
[Sisipkan screenshot hasil pengujian program modifikasi di sini]
```

## 8. Kesimpulan
......................................................................
......................................................................
......................................................................

## Daftar Pustaka
1. Kurose, J.F., Ross, K.W. *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2021.
2. Modul Praktikum Jaringan Komputer, S1 Informatika, Telkom University, Semester Genap 2025/2026.
