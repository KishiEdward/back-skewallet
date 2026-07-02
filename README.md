# Skewallet Backend API

<div align="center">
  <img width="300" height="301" alt="Institut Teknologi dan Bisnis Bina Sarana Global" src="https://github.com/user-attachments/assets/1e84f66a-135b-4cf2-b07a-b2a9098ce119" width="200"/>
</div>

<div align="center">
Institut Teknologi dan Bisnis Bina Sarana Global <br>
FAKULTAS TEKNOLOGI INFORMASI & KOMUNIKASI <br>
https://global.ac.id/
</div>

## Project UAS

- Nim : 1123150045
- Nama : Dzidan Rafi Habibie
- Mata Kuliah : Pemrograman Mobile Lanjutan
- Kelas : TI-SE 23 SH

## Deskripsi Project

Project ini adalah backend API untuk sistem Skewallet yang digunakan untuk mendukung autentikasi pengguna, verifikasi OTP, manajemen akun, serta proses pembayaran (payment) secara aman. Backend ini juga berperan sebagai penghubung deep link dengan aplikasi Skenaid, sehingga proses pembayaran dari aplikasi e-commerce dapat diarahkan dan diproses melalui Skewallet secara langsung. Aplikasi ini dibangun menggunakan Go, MySQL, Redis, dan Firebase Authentication.

## Demo Video

Lihat demo aplikasi dan alur fitur yang tersedia dalam video berikut.

**[Watch Full Demo on YouTube]()**

Alternative link: **[Google Drive Demo]()**

## Fitur Utama

- Autentikasi pengguna dengan Firebase Authentication
- Verifikasi OTP untuk keamanan transaksi
- Manajemen akun dan profil pengguna
- Proses pembayaran (payment) terintegrasi
- Deep link integration dengan aplikasi Skenaid untuk alur checkout dan callback pembayaran
- Middleware autentikasi JWT dan logging request
- Notifikasi email untuk aktivitas akun/transaksi
- Caching dan session management menggunakan Redis

## Teknologi yang Digunakan

- **[Go](https://go.dev/)** - Bahasa pemrograman backend
- **[MySQL](https://www.mysql.com/)** - Database relasional
- **[Redis](https://redis.io/)** - In-memory data store untuk caching/session
- **[Firebase](https://firebase.google.com/)** - Authentication
- **[JWT](https://jwt.io/)** - Token autentikasi
- **[godotenv](https://github.com/joho/godotenv)** - Manajemen environment variable

## Persyaratan Sistem

Pastikan perangkat Anda sudah memiliki:

- Go (versi terbaru yang kompatibel dengan modul ini)
- MySQL Server
- Redis Server
- Firebase project dengan service account
- Git
- Postman (opsional untuk testing API, koleksi tersedia di folder `postman/`)

## Cara Menjalankan Project

### 1. Clone Repository

```bash
git clone https://github.com/Frientia/skewallet-backend.git
cd skeback
```

### 2. Install Dependency

```bash
go mod tidy
```

### 3. Siapkan Environment

Buat file `.env` berdasarkan konfigurasi yang dibutuhkan, contohnya:

```env
APP_PORT=8081
APP_ENV=development
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=
DB_NAME=skewallet
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
JWT_SECRET=1234567890abcdef1234567890abcdef
JWT_EXPIRE_HOURS=24
FIREBASE_CREDENTIALS_PATH=./firebase_service_account.json
GOOGLE_APPLICATION_CREDENTIALS=./firebase_service_account.json
```

### 4. Siapkan Firebase

- Buat project Firebase
- Aktifkan Authentication
- Download file service account JSON
- Simpan sebagai `firebase_service_account.json` di root project

### 5. Siapkan Database MySQL & Redis

Pastikan MySQL dan Redis sudah berjalan dan database yang digunakan sudah tersedia sebelum menjalankan server.

### 6. Jalankan Server

```bash
go run main.go
```

Server akan berjalan di:

```bash
http://localhost:8081
```

## Struktur Project

```bash
skeback/
├── config/                         # Konfigurasi aplikasi
│   └── config.go
├── database/                       # Koneksi Firebase, MySQL, dan Redis
│   ├── firebase.go
│   ├── mysql.go
│   └── redis.go
├── handlers/                       # Handler HTTP untuk endpoint API
│   ├── auth.go
│   ├── health.go
│   ├── otp.go
│   └── payment.go
├── middleware/                     # Middleware autentikasi dan logging
│   ├── jwt.go
│   └── logger.go
├── models/                         # Struktur data model untuk account, otp, user
│   ├── account.go
│   ├── otp.go
│   └── user.go
├── postman/                        # Koleksi Postman untuk testing API
├── routes/                         # Routing API
│   └── routes.go
├── services/                       # Logika bisnis aplikasi
│   ├── email.go
│   ├── firebase_rest.go
│   ├── jwt.go
│   └── otp.go
├── main.go                         # Entry point aplikasi
├── go.mod                          # Modul Go
├── go.sum                          # Checksum dependency Go
├── .env                            # Konfigurasi environment
├── .gitignore
└── firebase_service_account.json   # Kredensial Firebase Admin SDK
```

## Dokumentasi API

Base URL:

```bash
http://localhost:8081/v1
```

### Authentication

- `POST /v1/auth/verify-token` - Verifikasi Firebase ID Token dan menghasilkan JWT backend

### OTP

- `POST /v1/otp/send` - Kirim kode OTP ke pengguna
- `POST /v1/otp/verify` - Verifikasi kode OTP

### Payment

- `POST /v1/payment/pay` - Proses pembayaran (dipanggil melalui deep link `skewallet://pay` dari aplikasi Skenaid)
- `GET /v1/payment/:id` - Ambil detail status pembayaran

### Health Check

- `GET /v1/health` - Cek status service

## Integrasi Deep Link

Backend ini mendukung alur pembayaran lintas aplikasi bersama Skenaid:

- Aplikasi Skenaid memanggil skema `skewallet://pay` untuk membuka aplikasi Skewallet dan memproses pembayaran.
- Setelah transaksi selesai, Skewallet mengarahkan callback kembali ke Skenaid melalui skema `skenaid://payment-callback`.

## Lisensi

Project ini dilisensikan di bawah MIT License.

## Ucapan Terima Kasih

- [Firebase](https://firebase.google.com/)
- [MySQL](https://www.mysql.com/)
- [Redis](https://redis.io/)
- [Go](https://go.dev/)

---

<div align="center">
  <p>© 2026 Skewallet Backend API. All rights reserved.</p>
</div>
