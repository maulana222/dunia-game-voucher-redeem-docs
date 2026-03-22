# Notifikasi & realtime

## Callback HTTP

Cara utama mitra menerima hasil akhir transaksi adalah **callback** ke `cb_url` (POST). Ini bekerja meskipun mitra tidak menjaga koneksi tetap ke server Anda.

## Pembaruan langsung di panel

Antarmuka operator dapat menerima **pembaruan langsung** saat transaksi berubah status (misalnya dari menunggu menjadi sukses atau gagal), tanpa menyegarkan halaman secara manual. Hal ini memakai **koneksi realtime** ke server yang sama dengan API.

## Ruang (room) notifikasi

Koneksi realtime dapat bergabung ke **ruang admin** (semua pembaruan operasional) atau **ruang per pengguna** (pembaruan terkait username API tertentu), sehingga panel mitra hanya melihat data relevan.

## Event sistem

Selain transaksi, sistem dapat mengirim sinyal untuk **antrean**, **perubahan voucher**, **status sistem**, atau **error** — berguna untuk monitoring operasional.
