# Dokumentasi Dunia Game

Selamat datang. Di sini dijelaskan **aplikasi Dunia Game** secara menyeluruh: tujuan sistem, **fitur** untuk operator dan mitra, cara **memulai**, serta **integrasi API** untuk penerimaan order redeem voucher game.

## Isi cepat

| Halaman | Apa yang Anda dapat |
|---------|---------------------|
| [Tentang aplikasi](tentang.md) | Gambaran sistem dan pengguna |
| [Fitur](fitur/redeem-transaksi.md) | Kemampuan per area (transaksi, admin, voucher, dll.) |
| [Memulai](memulai.md) | Prasyarat dan menjalankan sistem secara lokal |
| [Integrasi API](integrasi-api.md) | Order, signature, callback untuk mitra |
| [Keamanan](keamanan.md) | Prinsip perlindungan data dan akses |

## Dokumentasi vs kode

Isi ini menggambarkan perilaku yang diimplementasikan di repositori proyek. Jika ada perbedaan dengan kode, utamakan **kode sumber** dan perbarui dokumentasi.

## Membangun situs statis

Dari **akar proyek** (folder yang berisi `mkdocs.yml`):

```bash
pip install -r requirements-docs.txt
mkdocs serve
```

Pratinjau di browser sesuai URL yang ditampilkan. Build produksi:

```bash
mkdocs build
```

Hasil berada di **`docs/site/`** (folder ini diabaikan oleh Git).
