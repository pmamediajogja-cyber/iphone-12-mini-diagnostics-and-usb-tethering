# 04 — Checklist Troubleshooting

## Windows USB reverse tethering

- [ ] iPhone terdeteksi di Device Manager.
- [ ] CDC-NCM adapter muncul di `Get-NetAdapter -IncludeHidden`.
- [ ] Uplink Ethernet berstatus Up.
- [ ] Private iPhone adapter berstatus Up.
- [ ] Private adapter memiliki alamat IPv4 ICS (contoh terdahulu: `192.168.137.1`).
- [ ] `SharedAccess` berstatus Running.
- [ ] UDP DNS listener pada port 53 terlihat.
- [ ] Safari di iPhone dapat membuka situs melalui USB.

## iPhone wireless

- [ ] Wi-Fi Address di About.
- [ ] Wi-Fi toggle state.
- [ ] Apakah jaringan sekitar terlihat.
- [ ] Bluetooth Address di About.
- [ ] Bluetooth discovery/connect behavior.
- [ ] AirDrop behavior.
- [ ] Apakah gejala berubah setelah restart (catat, jangan ulangi berkali-kali).
- [ ] Catat apakah panic terjadi dan kondisi USB saat itu.

## Catatan tiap percobaan

| Tanggal/waktu | Perubahan yang dilakukan | Hasil | Panic/restart? | Catatan |
|---|---|---|---|---|
| YYYY-MM-DD HH:MM |  |  |  |  |
