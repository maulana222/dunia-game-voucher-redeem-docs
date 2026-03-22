# Tentang aplikasi

## Apa itu Dunia Game (proyek ini)?

Ini adalah **sistem lengkap** untuk **redeem voucher** dan **transaksi prepaid game** (misalnya Mobile Legends, Free Fire, PUBG, Valorant, dan judul lain yang Anda konfigurasi sebagai produk). Sistem menghubungkan:

- **Mitra / reseller** yang mengirim permintaan transaksi lewat API.
- **Penyedia layanan game (DG)** untuk menyelesaikan redeem secara teknis.
- **Operator** yang mengelola produk, stok voucher, member, dan memantau transaksi lewat antarmuka web.

## Siapa penggunanya?

| Peran | Kegiatan utama |
|-------|----------------|
| **Mitra** | Mengintegrasikan `POST` order, menerima callback hasil transaksi |
| **Operator / admin** | Mengatur produk, voucher, member, melihat laporan transaksi |
| **Member (akun bisnis)** | Bisa memiliki koneksi API sendiri dan batasan IP |

## Alur bisnis inti (sederhana)

1. Mitra mengirim **order** dengan ID referensi unik, data pemain, dan URL **callback**.
2. Sistem memvalidasi permintaan, mengantrekan pemrosesan, dan berkomunikasi dengan **API penyedia** untuk menyelesaikan redeem.
3. Hasil **sukses atau gagal** dikirim ke **callback** mitra dan tercatat untuk audit di sistem.

## Komponen teknis (satu kalimat)

Proyek kode mencakup **layanan API** (Node.js, basis data MySQL), **antarmuka administrasi** berbasis web, dan alat bantu pengujian yang meniru API penyedia — tanpa perlu memisahkan penjelasan fitur per nama folder di dokumentasi ini; detail jalan cepat ada di halaman [Memulai](memulai.md).
