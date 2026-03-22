# Panel administrasi

Antarmuka web untuk **operator** mengelola sistem tanpa mengubah kode.

## Autentikasi

Operator masuk dengan **username dan password**. Sistem mendukung **verifikasi dua faktor (2FA)** untuk menguatkan akun. Sesi memakai **token** yang dikirim lewat cookie aman (dan dapat diakses juga lewat header, sesuai implementasi).

## Pengaturan sistem

Mengubah parameter operasional (misalnya batas antrian, timeout, integrasi penyedia) sesuai yang diizinkan oleh layanan konfigurasi — nilai sensitif biasanya disamarkan di tampilan.

## Log & audit

Akses ke **log aplikasi** untuk diagnosis (bergantung pada hak akses dan fitur yang diaktifkan).

## Manajemen voucher (operasional)

Entri voucher massal, penghapusan, atau operasi lain yang disediakan rute admin untuk menjaga stok redeem.
