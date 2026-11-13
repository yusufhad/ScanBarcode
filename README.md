# Scan Barcode (Android)

Scan barcode/QR dengan kamera, hasilnya otomatis tersimpan, lalu export ke Excel/CSV
atau kirim langsung ke nomor WhatsApp.

## Cara membuat APK

**Opsi A - Android Studio** (versi Koala 2024.1 atau lebih baru)
1. File > Open > pilih folder `ScanBarcode`, tunggu Gradle sync selesai (butuh internet).
2. Sambungkan HP (USB debugging aktif) lalu tekan Run, atau
   Build > Build App Bundle(s)/APK(s) > Build APK(s).
   APK ada di `app/build/outputs/apk/debug/app-debug.apk`.

**Opsi B - tanpa Android Studio (GitHub Actions)**
1. Upload isi folder ini ke repository GitHub.
2. Buka tab Actions > "Build APK" > run terakhir > Artifacts > `ScanBarcode-apk`.

## Cara pakai
1. Buka aplikasi, izinkan kamera, arahkan ke barcode. Bunyi "bip" = tersimpan.
2. Tekan **Export / Kirim**, pilih format, lalu:
   - **Kirim ke WhatsApp**: isi nomor tujuan (08xx atau 628xx). WhatsApp terbuka di chat
     nomor itu dengan file terlampir, tinggal tekan kirim.
   - **Simpan ke perangkat**: pilih folder penyimpanan.
   - **Bagikan ke aplikasi lain**: email, Drive, Telegram, dll.

## Struktur kode (`app/src/main/java/com/scanbarcode/app`)
| File | Isi |
|---|---|
| `MainActivity.kt` | Titik masuk aplikasi |
| `ScanViewModel.kt` | Logika: simpan hasil scan, cegah dobel, buat file export |
| `data/Scan.kt` | Database lokal (Room) |
| `ui/ScannerPreview.kt` | Kamera (CameraX) + pembaca barcode (ML Kit, offline) |
| `ui/MainScreen.kt` | Tampilan utama dan dialog export |
| `export/Exporter.kt` | Penulis CSV dan XLSX (tanpa library tambahan) |
| `share/ShareHelper.kt` | Kirim ke WhatsApp / bagikan |

## Yang mudah diubah
- Jeda scan ulang barcode yang sama: `REPEAT_WINDOW_MS` di `ScanViewModel.kt` (default 2 detik).
- Kode negara default untuk nomor berawalan 0: `normalizeNumber` di `ShareHelper.kt` (default 62).
- Judul kolom export: `buildExport` di `ScanViewModel.kt`.
