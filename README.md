# MONSPJ BOK – UPTD Puskesmas Sawan II Kabupaten Buleleng

Aplikasi monitoring kelengkapan SPJ Dana Bantuan Operasional Kesehatan (BOK) dengan:
- Frontend statis: GitHub Pages
- Database: Google Sheets
- Penyimpanan berkas: Google Drive
- Backend/API: Google Apps Script

## A. Instalasi Google Sheets dan Google Drive
1. Buka https://script.google.com/ lalu buat project baru.
2. Salin seluruh isi `Code.gs` ke editor Apps Script.
3. Jalankan fungsi `setupSystem()` satu kali dan berikan izin akses Spreadsheet serta Drive.
4. Buka **Project Settings > Script Properties**. Pastikan `SPREADSHEET_ID` dan `ROOT_FOLDER_ID` sudah terisi (dibuat otomatis oleh setup).
5. Buka spreadsheet yang dibuat. Pada sheet `ANGGARAN`, masukkan pagu:
   `TAHUN | PAGU | KETERANGAN`
   Contoh: `2026 | 250000000 | Pagu BOK tahun 2026` (ganti dengan pagu resmi).
6. Periksa folder Drive yang dibuat. Atur akses folder sesuai kebijakan instansi; jangan menjadikan folder dokumen SPJ publik.
7. Pilih **Deploy > New deployment > Web app**. Execute as: **Me**. Who has access: untuk uji coba pilih sesuai kebijakan akun Google Workspace/instansi. Salin URL berakhiran `/exec`.

## B. Publikasi GitHub Pages
1. Buat repository GitHub baru, misalnya `monspj-bok-sawan-ii`.
2. Unggah `index.html`, `style.css`, `app.js`, dan `config.js` ke root repository.
3. Edit `config.js`, ganti `PASTE_URL_WEB_APP_APPS_SCRIPT_DI_SINI` dengan URL Web App `/exec`.
4. Aktifkan **Settings > Pages > Deploy from a branch > main > /(root)**.
5. Buka URL GitHub Pages.

## C. Struktur Google Sheets
- `SPJ`: data transaksi, checklist, file Drive, status verifikasi.
- `ANGGARAN`: pagu tahunan.
- `PENGGUNA`: disediakan untuk pengembangan pengelolaan akun/otorisasi.
- `LOG`: catatan input dan verifikasi.

## D. Struktur Google Drive
Folder utama `MONSPJ BOK - Dokumen SPJ UPTD Puskesmas Sawan II` akan berisi folder tahun, kemudian folder per nomor SPJ. File yang diunggah dicatat URL dan ID-nya di sheet `SPJ`.

## E. Checklist awal dokumen
Daftar checklist pada aplikasi adalah template awal dan wajib disesuaikan dengan juknis BOK, standar biaya, kebijakan daerah, serta jenis kegiatan/transaksi yang berlaku. Checklist: Surat Tugas; Undangan/jadwal; Daftar hadir; Notulen/laporan; Kuitansi/bukti pembayaran; Nota/faktur; Bukti pajak jika ada; Dokumentasi; SPJ perjalanan dinas jika ada; Bukti setor/transfer jika ada.

## F. Catatan penting sebelum operasional
**Versi ini adalah prototipe awal untuk konfigurasi dan uji coba, bukan sistem produksi yang sudah diaudit.** Endpoint Apps Script dan akses Google Drive perlu diuji dengan akun organisasi. Kebijakan CORS/redirect Google Apps Script dapat berbeda menurut akun dan deployment; jika browser menolak respons API dari GitHub Pages, solusi yang disarankan adalah menyajikan frontend melalui Apps Script HTML Service atau menambahkan lapisan API terautentikasi yang mendukung CORS.

Sebelum digunakan untuk dokumen keuangan resmi:
- Batasi akses aplikasi dan Drive hanya kepada petugas berwenang.
- Implementasikan autentikasi dan otorisasi server-side berbasis akun Google/daftar pengguna; jangan mengandalkan penyembunyian menu di browser.
- Tambahkan validasi file, batas ukuran, dan pemeriksaan MIME type di server.
- Uji alur input, upload, verifikasi, dan ekspor dengan data dummy.
- Sesuaikan seluruh checklist dan format SPJ dengan ketentuan BOK yang berlaku.
- Jangan memasukkan data pribadi sensitif yang tidak diperlukan.

## G. Troubleshooting
- **URL API belum diatur**: periksa `config.js`.
- **Gagal otorisasi**: jalankan `setupSystem()` dan deploy ulang Web App dengan akun pemilik yang benar.
- **Upload gagal**: cek izin Drive dan ukuran file.
- **Data kosong**: pastikan filter tahun sama dengan tahun pada sheet `SPJ`.
- **Pagu Rp0**: isi sheet `ANGGARAN` dengan tahun dan pagu numerik.
