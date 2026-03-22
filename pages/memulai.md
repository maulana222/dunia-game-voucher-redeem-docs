# Memulai

## Prasyarat

- **Node.js** 18 atau lebih baru  
- **MySQL** 8+ (atau kompatibel)  
- **npm**  

## Basis data

Buat database lalu impor skema SQL yang disertakan proyek (file skema penuh di folder basis data backend).

## Menjalankan layanan API

Di folder **backend** proyek: pasang dependensi (`npm install`), siapkan file **`.env`** (koneksi MySQL, rahasia JWT, URL API penyedia, dll.), lalu jalankan **seed** data awal bila tersedia. Setelah itu start server pengembangan atau produksi sesuai skrip di `package.json` (misalnya `npm run dev`). Port default biasanya **3000** kecuali diubah.

## Menjalankan antarmuka admin

Di folder **frontend** admin: `npm install` dan `npm start`. Port bawaan pengembangan biasanya **6969**. Proxy development mengarahkan `/api` dan Socket ke URL backend (dapat diatur lewat variabel lingkungan `REACT_APP_*`).

## Uji integrasi tanpa penyedia produksi

Proyek menyertakan **server tiruan** yang meniru respons API penyedia untuk pengembangan. Jalankan dari foldernya, arahkan **URL API penyedia** di `.env` backend ke alamat tiruan (misalnya `http://localhost:3636`), lalu uji order end-to-end.

## Cek kesehatan

- **`GET /health`** — server hidup  
- **`GET /ready`** — kesiapan basis data dan konfigurasi penting  

## Dokumentasi situs

Lihat halaman [Beranda](index.md) untuk membangun dokumentasi statis ke **`docs/site/`**.
