# 01 — Spesifikasi Perangkat dan Gejala

## Identifikasi perangkat

- Perangkat: iPhone 12 mini
- Model identifier: iPhone13,1
- Model number: A2176
- Part number yang dilaporkan: MG663LL/A
- iOS: 27.2.1
- Build: 24B156

## Gejala yang dilaporkan

| Item | Hasil |
|---|---|
| Wi-Fi Address di Settings > General > About | N/A |
| Wi-Fi toggle | Dapat ON |
| Daftar jaringan Wi-Fi | Tidak ada jaringan muncul |
| Bluetooth Address | MAC masih tampil |
| Bluetooth | Searching terus |
| AirDrop | Gagal |
| Wi-Fi Address historis | Sebelum upgrade iOS 27 pernah tampil sebagai strip `-`; setelah upgrade sempat muncul sebentar lalu kembali N/A |
| Restart | Pernah membuat alamat Wi-Fi muncul sementara, kemudian N/A lagi |
| Kondisi panas/restart | Pernah restart sendiri setelah digunakan jogging dan terasa hangat, tidak dilaporkan sangat panas |

## Interpretasi yang aman

- Wi-Fi Address N/A dan tidak adanya hasil pemindaian menguatkan dugaan bahwa antarmuka Wi-Fi tidak terinisialisasi/terdeteksi dengan normal.
- Bluetooth Address yang tetap tampil menunjukkan identitas Bluetooth masih tersedia, tetapi tidak membuktikan radio Bluetooth bekerja normal.
- Bluetooth Searching dan AirDrop gagal adalah gejala tambahan, bukan bukti mandiri bahwa chip gabungan Wi-Fi/Bluetooth rusak.
- Gangguan bisa berasal dari software/firmware, modul, jalur daya, komunikasi pada logic board, atau komponen RF/antena. Pemeriksaan pengukuran diperlukan untuk membedakannya.

## Riwayat uji tanpa USB

Pada satu pengujian, kabel USB dilepas. Wi-Fi tetap dapat diaktifkan, tetapi tidak menemukan jaringan; Wi-Fi Address tetap N/A. Hasil ini tidak mengisolasi seluruh faktor penyebab dan tidak membuktikan kerusakan komponen tertentu.
