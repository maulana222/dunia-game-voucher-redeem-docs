# Dunia Game — dokumentasi

**Dokumentasi lengkap (browsing, pencarian, semua bab):**  
**[https://maulana222.github.io/dunia-game-voucher-redeem-docs/](https://maulana222.github.io/dunia-game-voucher-redeem-docs/)**

---

## Tentang proyek

**Dunia Game** adalah sistem untuk **redeem voucher** dan **transaksi prepaid game** (misalnya Mobile Legends, Free Fire, PUBG, Valorant, dan produk lain yang Anda daftarkan). Sistem menghubungkan **mitra atau reseller** yang mengirim order lewat API, **penyedia layanan game** yang memproses redeem di sisi infrastruktur resmi, dan **operator** yang mengelola produk, stok voucher, akun bisnis, serta pemantauan transaksi dari antarmuka web.

Tujuan utamanya adalah memberi jalur yang **terstruktur dan dapat diaudit**: setiap permintaan punya referensi unik, hasil akhir diberitahukan ke mitra lewat **callback**, dan status transaksi tersimpan untuk laporan serta troubleshooting.

## Siapa yang memakainya?

| Peran | Peran dalam sistem |
|--------|---------------------|
| **Mitra / integrator** | Mengirim order programmatically, memvalidasi signature, menerima notifikasi hasil ke URL callback mereka |
| **Operator / admin** | Mengatur member, produk, SKU, paket voucher, melihat dan mengekspor transaksi, mengelola pengaturan operasional |
| **Member (bisnis)** | Entitas yang memiliki kredensial API terpisah; dapat dibatasi berdasarkan IP sumber request |

## Fitur utama

- **API order** — endpoint untuk membuat permintaan redeem dengan ID referensi unik (`ref_id`), SKU produk, data pemain (`customer_no`), dan URL **callback** untuk hasil akhir.
- **Signature & koneksi API** — setiap order memakai **MD5(username + api_key + ref_id)** agar hanya pemegang kunci yang sah yang bisa mengirim untuk username tersebut; koneksi API dapat dikaitkan dengan **whitelist IP**.
- **Alur redeem ke penyedia** — backend menjalankan rangkaian langkah teknis ke API penyedia (ambil voucher, inquiry, transaksi, cek status), dengan **antrian**, **timeout**, dan **throttling** agar stabil di beban tinggi.
- **Callback ke mitra** — setelah sukses, gagal, atau skenario khusus (misalnya hasil parsial pada order multi-unit), sistem mengirim **HTTP POST** ke `cb_url` dengan payload yang konsisten (kode hasil, pesan, detail transaksi).
- **Panel administrasi** — antarmuka web untuk mengelola data master dan operasional: autentikasi dengan JWT, opsi **2FA**, manajemen voucher (termasuk operasi massal), produk, member, dan laporan transaksi.
- **Pembaruan realtime** — untuk monitoring di browser, tersedia saluran **Socket.IO** (misalnya pembaruan transaksi, antrean, voucher, status sistem) ke ruang admin atau per pengguna.
- **Kesehatan layanan** — endpoint ringan untuk cek apakah proses hidup dan apakah basis data serta konfigurasi kritis siap melayani.

## Integrasi untuk mitra

Mitra mengarahkan sistem mereka ke **POST /api/orders** pada URL publik instalasi Anda, mengirim body JSON sesuai kontrak (termasuk `max_price` dan `allow_dot` sesuai validasi server), lalu menangani **callback** di sisi mereka dengan idempotensi yang wajar. Detail field, alur pending, dan pemetaan kode hasil dijelaskan di dokumentasi online di tautan di atas (bab **Integrasi API** dan **Fitur**).

## Keamanan (ringkas)

Autentikasi panel memakai **JWT** (cookie httpOnly diutamakan); order publik memakai **signature** dan opsi **pembatasan IP**. Gunakan **HTTPS** di produksi untuk API dan callback. Rahasia seperti `JWT_SECRET` dan kunci API hanya di lingkungan server, tidak di repositori publik.

## Repositori ini

Repositori **dunia-game-voucher-redeem-docs** berisi **sumber dokumentasi** (Markdown di folder `pages/`, konfigurasi MkDocs). **Versi yang sudah di-build dan di-host** untuk dibaca publik ada di situs dokumentasi:

**[https://maulana222.github.io/dunia-game-voucher-redeem-docs/](https://maulana222.github.io/dunia-game-voucher-redeem-docs/)**

Untuk kode aplikasi utama (backend, frontend admin, alat uji integrasi), lihat repositori atau monorepo proyek Dunia Game tempat layanan tersebut dikembangkan.
