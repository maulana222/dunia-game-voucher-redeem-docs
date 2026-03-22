# Redeem & transaksi

## Order dari mitra

Mitra mengirim permintaan transaksi ke endpoint **`POST /api/orders`**. Sistem:

- Memastikan **ID referensi** (`ref_id`) unik per mitra (jika sudah pernah dipakai, respons mengikuti status transaksi yang tersimpan).
- Memvalidasi **format data** (termasuk signature dan field wajib sesuai skema validasi di kode).
- Mengembalikan respons awal yang umumnya berstatus **menunggu (pending)** sementara redeem berjalan di latar belakang.

## Signature

Integritas permintaan dijamin dengan **signature** berbasis **MD5** dari penggabungan: `username` + `api_key` + `ref_id`, dibandingkan dengan nilai `sign` di body. Kunci API berasal dari **koneksi API** yang terdaftar untuk member terkait.

## Callback

Setelah pemrosesan selesai (atau pada titik tertentu untuk kasus khusus), sistem mengirim **HTTP POST** ke **`cb_url`** yang mitra sediakan, berisi ringkasan hasil (kode hasil, pesan, detail transaksi) agar sistem mitra dapat memperbarui status order mereka.

## Kode hasil (`rc`)

Respons dan callback memakai kode numerik string (misalnya sukses, gagal, pending, nomor tujuan salah, SKU tidak ditemukan) yang konsisten dengan logika di layanan transaksi. Mitra sebaiknya memetakan semua kode yang mereka terima di lingkungan produksi.

## Multi-unit & denom besar

Untuk order dengan **banyak unit** (denom kelipatan), pemrosesan dilakukan per unit; hasil bisa **parsial** (sebagian sukses) tergantung jenis kegagalan di penyedia — sistem dapat mempertahankan status tertentu dan memberi tahu mitra lewat callback (misalnya jumlah unit terpenuhi vs diminta).

## Pelacakan

Transaksi dapat dilihat dan difilter melalui **API terautentikasi** serta **panel operator** (riwayat, pencarian, unduhan/ekspor sesuai implementasi).
