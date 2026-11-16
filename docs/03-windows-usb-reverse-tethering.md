# 03 — Windows 11 USB Reverse Tethering (CDC-NCM + ICS)

## Tujuan

Membagikan koneksi internet PC Windows ke iPhone melalui kabel USB. PC menggunakan koneksi Ethernet sebagai uplink; iPhone terdeteksi sebagai USB Ethernet/CDC-NCM.

## Lingkungan yang dilaporkan

- OS PC: Windows 11
- Shell: PowerShell Administrator
- Uplink: adapter `Ethernet` — Realtek Gaming GbE Family Controller
- Kecepatan link yang terlihat: 100 Mbps
- Python: 3.14.x x64
- PyUSB: 1.3.1
- Folder kerja: `C:\Users\Administrator\Desktop\iPhone-Reverse-Tethering-Ethernet`

## Persiapan sesi PowerShell

```powershell
$env:Path = "$env:LOCALAPPDATA\Programs\Python\Python314;$env:LOCALAPPDATA\Programs\Python\Python314\Scripts;$env:Path"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
```

## Perintah yang pernah dijalankan

```powershell
cd "$env:USERPROFILE\Desktop\iPhone-Reverse-Tethering-Ethernet"
.\USB-Share.ps1 on
```

Script pernah melaporkan timeout menunggu NCM adapter. Namun pemeriksaan berikutnya menunjukkan `Ethernet 4` berstatus Up dengan IP `192.168.137.1`, sedangkan `Ethernet 5` Not Present. Jadi timeout script tidak selalu berarti adaptor sama sekali tidak muncul.

## Pemeriksaan adapter

```powershell
Get-NetAdapter -IncludeHidden |
  Format-Table Name, InterfaceDescription, Status, MacAddress -Auto
```

Periksa konfigurasi IPv4:

```powershell
Get-NetIPConfiguration -InterfaceAlias "Ethernet 4"
```

Nilai yang pernah terlihat pada private interface:
- IP: `192.168.137.1`
- DHCP: disabled
- Default gateway: kosong (normal untuk interface private ICS)

## Refresh Internet Connection Sharing melalui COM

> Sesuaikan nama adapter jika berbeda. `Ethernet` adalah uplink publik dan `Ethernet 4` adalah interface iPhone pada sesi yang didokumentasikan.

Jalankan PowerShell sebagai Administrator:

```powershell
$ics = New-Object -ComObject HNetCfg.HNetShare
$public = $null
$private = $null

foreach ($c in $ics.EnumEveryConnection) {
    $p = $ics.NetConnectionProps($c)

    if ($p.Name -eq "Ethernet") {
        $public = $ics.INetSharingConfigurationForINetConnection($c)
    }

    if ($p.Name -eq "Ethernet 4") {
        $private = $ics.INetSharingConfigurationForINetConnection($c)
    }
}

if ($null -eq $public -or $null -eq $private) {
    throw "Adapter uplink/private tidak ditemukan. Periksa nama adapter."
}

try { $public.DisableSharing() } catch {}
try { $private.DisableSharing() } catch {}
Start-Sleep -Seconds 3

$public.EnableSharing(0)  # 0 = public/uplink
$private.EnableSharing(1) # 1 = private/home interface

Start-Sleep -Seconds 5
Get-Service SharedAccess
```

Hasil yang pernah dilaporkan: `SharedAccess` menjadi `Running` dan pengguna menyatakan koneksi USB kembali bisa digunakan.

## Pemeriksaan DNS ICS

Pernah terlihat iPhone menggunakan IP `192.168.137.146` dan mengirim DNS ke `192.168.137.1:53`. Sebelum ICS diperbaiki, Windows mengembalikan ICMP port unreachable. Setelah refresh ICS, listener UDP port 53 terlihat pada Windows.

```powershell
Get-NetUDPEndpoint -LocalPort 53
Get-Service SharedAccess
```

## Catatan penting

- Nama adapter `Ethernet 4` dapat berubah setelah re-enumeration USB.
- Jangan menganggap timeout script sebagai kegagalan total sebelum memeriksa `Get-NetAdapter`.
- Jangan menghapus perangkat PnP, mengedit registry, atau menginstal ulang driver tanpa alasan dan backup.
- Jangan mengulang setup/install script yang sudah berhasil hanya untuk mengatasi status ICS.
- Script asli `USB-Share.ps1`, `Setup.ps1`, `Uninstall.ps1`, dan `iphone_mode.py` belum disertakan dalam paket awal ini; salin dari folder kerja asli setelah diverifikasi.
