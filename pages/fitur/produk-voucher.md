# Produk & voucher

## Produk

**Produk** diidentifikasi dengan **SKU** (`buyer_sku_code` di order). Tiap produk memiliki harga, status aktif/nonaktif, dan metadata game (tipe game, denom, dll.) sesuai skema basis data. Produk nonaktif menolak order.

## Paket voucher

Voucher dapat dikelompokkan dalam **paket** per game atau kategori, memudahkan stok dan pelaporan.

## Stok voucher

Voucher memiliki siklus hidup: tersedia, terpakai, atau status error. Sistem memilih voucher untuk redeem dengan mekanisme yang **mengurangi race condition** saat banyak transaksi bersamaan.

## Pembaruan harga

Tersedia operasi **pembaruan harga massal** untuk produk melalui API terautentikasi, sehingga penyesuaian cepat tanpa edit manual per baris.
