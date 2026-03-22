# Antrian & pemrosesan

## Mengapa ada antrian?

Order redeem bisa memakan waktu (beberapa langkah ke penyedia, polling status, penanganan error). **Antrian** mencegah server kelebihan beban dan membantu mengatur **konkurensi** serta **throttling** ke API penyedia.

## Timeout

Tiap tahap dapat memiliki **batas waktu** (dikonfigurasi lewat variabel lingkungan). Jika batas terlampaui, transaksi diperlakukan sesuai aturan gagal atau sukses parsial di layanan.

## Throttling

Permintaan ke penyedia dapat dibatasi (misalnya maksimum per detik, mode urut) agar tidak melanggar kebijakan rate limit pihak penyedia.

## Beberapa instansi

Untuk skala besar, layanan API dapat dijalankan **beberapa instansi** di port berbeda di belakang **load balancer** — konfigurasi khusus menandai mode tersebut agar log dan perilaku konsisten.

## Status antrian

Endpoint khusus (tergantung deployment) dapat menampilkan **ringkasan antrian** untuk observabilitas.
