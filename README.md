# iPhone 12 mini Diagnostics & USB Reverse Tethering

Dokumentasi kerja untuk:
1. Pemeriksaan iPhone 12 mini (A2176) dengan iOS 27.2.1.
2. Investigasi Wi-Fi/Bluetooth/AirDrop dan kernel panic.
3. Reverse tethering internet dari PC Windows 11 ke iPhone melalui USB CDC-NCM dan Internet Connection Sharing (ICS).

> **Status:** dokumentasi awal berdasarkan pengujian yang dilaporkan pada 16 November 2026. Ini bukan diagnosis servis final. Gejala Wi-Fi belum membuktikan IC tertentu rusak.

## Struktur

- `docs/` — langkah diagnosis, hasil pemeriksaan, dan troubleshooting.
- `scripts/` — tempat menyimpan script asli yang sudah diverifikasi.
- `logs/` — template dan petunjuk sanitasi log.
- `requirements.txt` — dependensi Python.

## Status temuan iPhone

| Pemeriksaan | Hasil |
|---|---|
| Model | iPhone 12 mini, A2176 |
| Part number | MG663LL/A |
| iOS | 27.2.1 (24B156) |
| Wi-Fi Address | N/A |
| Wi-Fi toggle | Bisa ON; jaringan tidak muncul |
| Bluetooth Address | MAC muncul |
| Bluetooth | Terus Searching |
| AirDrop | Gagal |
| eSIM | Pernah gagal aktivasi; bukan fokus dokumentasi ini |
| Kernel panic | Dua log dengan `port enable failed: 0xe00002d6` |
| Kondisi saat panic | iPhone terhubung fisik ke laptop melalui USB |
| Aksesori lain | Tidak ada yang dilaporkan |

## Status reverse tethering Windows

Pengujian sebelumnya menggunakan Windows 11, Python 3.14.x, PyUSB 1.3.1, adaptor Ethernet Realtek sebagai uplink, dan adaptor USB CDC-NCM iPhone sebagai private interface. ICS kemudian berhasil diaktifkan ulang melalui COM `HNetCfg.HNetShare`, dan layanan `SharedAccess` berjalan.

**Penting:** script operasional asli belum disertakan dalam paket ini karena isi file sumber belum tersedia untuk diverifikasi. Jangan mengganti placeholder dengan script rekaan. Salin file asli yang sudah diuji ke `scripts/` setelah diperoleh.

## Mulai

1. Baca `docs/01-device-and-symptoms.md`.
2. Baca `docs/02-panic-log-notes.md`.
3. Ikuti `docs/03-windows-usb-reverse-tethering.md`.
4. Gunakan `docs/04-troubleshooting-checklist.md` untuk mencatat perubahan.
5. Jangan unggah log mentah yang memuat serial number, IMEI, EID, alamat MAC, nomor telepon, atau identifier pribadi.

## Disclaimer

Repositori ini merupakan catatan eksperimen dan troubleshooting komunitas, bukan panduan resmi Apple atau Microsoft. Perubahan jaringan Windows dan reset iPhone dilakukan dengan risiko sendiri. Backup data sebelum reset/perbaikan.
