# Log privat

Simpan salinan asli log di tempat privat. Jangan commit log mentah ke repository publik.

Sebelum membagikan log, sanitasi:
- Serial number
- IMEI / MEID
- EID / ICCID
- Nomor telepon
- Wi-Fi/Bluetooth MAC address
- Identifier akun atau perangkat lain

Gunakan placeholder seperti `[REDACTED]`. Jangan mengubah `panicString`, backtrace, timestamp, atau informasi teknis yang dibutuhkan untuk analisis, kecuali informasi tersebut mengandung identifier pribadi.
