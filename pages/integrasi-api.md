# Integrasi API (mitra)

Halaman ini merangkum kontrak integrasi untuk **menerima order** dari sistem mitra. Detail field mengikuti validasi di kode (validator order).

## Endpoint

- **POST** `{BASE}/api/orders`  
- `BASE` = URL publik layanan API Anda (contoh `https://api.contoh.com`).

## Header & isi

- **`Content-Type: application/json`**
- **Body JSON** (semua field wajib sesuai skema validasi saat ini), antara lain:

| Field | Fungsi |
|-------|--------|
| `username` | Username **koneksi API** yang terdaftar |
| `ref_id` | ID unik per mitra untuk idempotensi |
| `sign` | Hash **MD5** heksadesimal 32 karakter dari `username` + `api_key` + `ref_id` |
| `buyer_sku_code` | SKU produk |
| `customer_no` | ID pemain / nomor tujuan (string digit) |
| `cb_url` | URL **HTTPS/HTTP** untuk callback hasil |
| `max_price` | Angka (wajib di skema Joi saat ini) |
| `allow_dot` | Boolean (wajib di skema Joi saat ini) |

## Respons singkat HTTP

- Order baru yang diterima biasanya mendapat status **pending** di respons pertama (`rc` **03**).  
- **`ref_id`** yang sudah ada mengembalikan snapshot sesuai status tersimpan.

## Callback

Sistem akan **POST** ke `cb_url` dengan payload hasil (sukses/gagal) menggunakan pemetaan kode **`rc`** dan pesan. Mitra harus:

- Merespons HTTP dengan cepat (idealnya **2xx**).  
- Memproses **idempoten** jika callback sama dikirim ulang.  

## Keamanan integrasi

- Simpan **`api_key`** hanya di server mitra, jangan di aplikasi klien.  
- Gunakan **HTTPS** untuk `cb_url`.  
- Jika **pembatasan IP** aktif di koneksi API, pastikan IP keluar server order mitra terdaftar.

## Kesehatan & SLA

Gunakan **`/health`** dan **`/ready`** untuk monitoring infrastruktur Anda.
