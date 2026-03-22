# Keamanan

Ringkasan prinsip keamanan yang diterapkan sistem. Untuk audit formal, gabungkan dengan kebijakan organisasi Anda.

## Autentikasi panel & API internal

- **JWT** ditandatangani dengan rahasia kuat (`JWT_SECRET` di lingkungan server).  
- Token disimpan sebagai **cookie httpOnly** (dengan fallback header), mengurangi risiko pencurian dari skrip di browser.  
- **2FA** opsional untuk akun operator.  
- **Batas percobaan login** dan **rate limit** per IP mengurangi brute force.

## Order publik (tanpa JWT)

- **Signature MD5** memastikan hanya pemegang `api_key` yang valid bisa mengirim order untuk `username` tersebut.  
- **Whitelist IP** opsional pada koneksi API.  
- **Produk** harus aktif; SKU tidak valid ditolak.

## Jaringan & transport

- Gunakan **HTTPS** di produksi untuk API dan callback.  
- Backend mempercayai header proxy (`trust proxy`) agar IP asli benar di belakang reverse proxy — pastikan proxy Anda **men-set** `X-Forwarded-For` dengan benar.

## CORS

Akses dari browser ke API dibatasi **asal (origin)** tertentu di mode produksi; mode pengembangan biasanya lebih longgar.

## Rahasia & konfigurasi

- Jangan commit file **`.env`** ke repositori.  
- Putar kunci API dan JWT secara berkala jika ada kebocoran.  
- Batasi siapa yang memiliki **password admin tambahan** untuk operasi sensitif (jika fitur dipakai).

## Logging

- Request API dicatat; endpoint login tidak mencatat body penuh.  
- Di produksi, **detail error internal** tidak dikembalikan ke klien umum.

## Validasi Game ID (opsional)

Jika fitur pemeriksaan ID pemain ke layanan pihak ketiga diaktifkan, kredensial tersebut harus dikelola sebagai **rahasia** (idealnya variabel lingkungan, bukan kode terbuka).
