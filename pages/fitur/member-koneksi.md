# Member & koneksi API

## Member

**Member** adalah entitas bisnis yang dapat memiliki **user** login, **saldo** (jika dipakai), status aktif/nonaktif, dan **peran** (admin vs member). Admin dapat membuat dan mengelola member dari panel.

## Koneksi API

Agar mitra bisa mengirim order, setiap member dapat memiliki satu atau lebih **koneksi API**:

- **Username API** — identitas di body order.
- **API key** — dipakai untuk menghitung **signature**; tidak boleh bocor.
- **Pembatasan IP** — opsional: hanya IP yang terdaftar yang boleh mengirim order untuk koneksi tersebut.

## Validasi saat order

Saat order masuk, sistem mencocokkan **username** dengan koneksi API, memverifikasi **signature** dengan `api_key` yang tersimpan, dan memeriksa **IP sumber** jika aturan IP diaktifkan.

## Koneksi berbasis IP

Selain kredensial API, dapat dikonfigurasi aturan berbasis **IP** untuk skenario whitelist tambahan (sesuai model data dan rute yang tersedia).
