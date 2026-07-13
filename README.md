# 💍 Undangan Pernikahan Digital Premium (Batak-Chinese Fusion)

Undangan pernikahan digital satu halaman (Single Page Application) yang elegan, responsif, memiliki animasi kelas dunia (tren web 2026), dan **100% gratis selamanya untuk dideploy online**.

Proyek ini menggunakan arsitektur statis murni (HTML/CSS/JS) dengan satu file konfigurasi terpusat untuk memudahkan pengeditan data tanpa perlu menyentuh struktur kode program.

---

## 📂 Struktur Folder Proyek

```text
undangan-digital/
├── assets/                  # Tempat menyimpan foto, logo, & musik latar
│   ├── groom.jpg            # Foto mempelai pria (Albert)
│   ├── bride.jpg            # Foto mempelai wanita (Grace)
│   ├── wedding-song.mp3     # File musik latar belakang (Romantis)
│   ├── bca.png              # Logo Bank BCA
│   └── mandiri.png          # Logo Bank Mandiri
├── config.js                # FILE UTAMA: Pengaturan teks, tanggal, & rekening
├── index.html               # Struktur halaman web & SEO meta tags
├── style.css                # Desain CSS, Glassmorphism, & Animasi 2026
├── app.js                   # Logika partikel, countdown, RSVP & efek 3D tilt
└── README.md                # Panduan instalasi dan deployment ini
```

---

## 🛠️ Cara Mengedit & Kustomisasi Isi Undangan

Anda hanya perlu membuka file `config.js` dengan text editor (misal: VS Code, Notepad++, atau Notepad biasa) dan mengubah nilai-nilai teks di dalamnya:

1. **Ubah Data Mempelai**: 
   Edit bagian `groom` (pria) dan `bride` (wanita). Anda bisa mengubah nama lengkap, panggilan, nama orang tua, deskripsi biografi, dan link Instagram.
2. **Ubah Tanggal Acara**:
   Ganti `weddingDate` dengan format `YYYY-MM-DDTHH:mm:ss` (Contoh: `"2026-10-18T09:00:00"`). Ini otomatis mengatur waktu countdown di website.
3. **Ubah Alamat & Link Google Maps**:
   Ganti `venue`, `address`, `mapsUrl` (link tombol petunjuk arah), dan `mapsEmbedUrl` (link iframe peta) untuk acara Pemberkatan dan Resepsi.
4. **Kado Digital (Rekening)**:
   Ubah data bank, nomor rekening, nama pemilik rekening, dan alamat pengiriman kado fisik pada bagian `gifts`.
5. **Ganti Foto & Musik**:
   - Taruh foto pengantin Anda ke dalam folder `assets/` dengan nama `groom.jpg` dan `bride.jpg`.
   - Taruh file lagu pernikahan berformat `.mp3` ke dalam folder `assets/` dengan nama `wedding-song.mp3`.

---

## 🚀 Cara Online-kan / Deploy Gratis Tanpa Ribet

Untuk meng-online-kan undangan ini tanpa bayar sepeser pun dan mendapatkan URL yang bagus dan cepat, berikut adalah cara terbaik:

### Opsi A: Netlify Drop (Paling Direkomendasikan - Tanpa Koding & Tanpa Akun Git)

1. Buka situs [Netlify Drop](https://app.netlify.com/drop) di browser Anda.
2. Seret (Drag & Drop) folder proyek `undangan-digital` Anda langsung ke kotak yang tersedia di layar.
3. Tunggu beberapa detik, situs Anda langsung online!
4. **Kustomisasi URL**: 
   - Buat akun gratis di Netlify untuk menyimpan situs tersebut.
   - Masuk ke dashboard Netlify Anda > pilih situs Anda > **Site configuration** > **Change site name**.
   - Ubah nama situs menjadi nama pernikahan Anda (contoh: `albert-grace-wedding.netlify.app`).

### Opsi B: Vercel (Cepat & Handal)

Jika Anda ingin menggunakan Vercel (sangat populer di tahun 2026 karena CDN globalnya yang sangat cepat):
1. Buka [Vercel](https://vercel.com/) dan masuk/buat akun gratis.
2. Hubungkan Vercel dengan repositori Git Anda (GitHub/GitLab) atau gunakan Vercel CLI untuk deploy instan lewat terminal command line:
   ```bash
   npm install -g vercel
   vercel
   ```
3. URL undangan Anda akan aktif dengan format: `nama-proyek.vercel.app`.

---

## 📊 Setup Database Buku Tamu (RSVP) Gratis lewat Google Sheets

Secara default, data RSVP tamu yang dikirim via formulir akan langsung disimpan di browser pengirim (`localStorage`). Supaya Anda bisa melihat rekapitulasi kehadiran dan ucapan tamu secara online secara real-time, ikuti panduan Google Sheets gratis ini:

### Langkah 1: Buat Spreadsheet Baru
1. Buka [Google Sheets](https://sheets.google.com) dan buat spreadsheet kosong baru.
2. Beri nama spreadsheet tersebut (misal: "Rekap RSVP Undangan").
3. Di baris pertama (Row 1), buat 5 kolom dengan nama header berikut:
   - Kolom A: `Timestamp`
   - Kolom B: `Nama`
   - Kolom C: `Status`
   - Kolom D: `Jumlah Tamu`
   - Kolom E: `Ucapan`

### Langkah 2: Pasang Apps Script
1. Di menu atas Google Sheets, klik **Extensions** (Ekstensi) > **Apps Script**.
2. Hapus semua kode bawaan yang ada di editor, lalu paste kode berikut:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var name = e.parameter.name;
    var status = e.parameter.status;
    var guests = e.parameter.guests;
    var message = e.parameter.message;
    var timestamp = new Date();
    
    // Tambahkan baris baru berisi data kiriman dari web
    sheet.appendRow([timestamp, name, status, guests, message]);
    
    // Kirim respon sukses
    return ContentService.createTextOutput("SUCCESS")
                         .setMimeType(ContentService.MimeType.TEXT);
  } catch (err) {
    return ContentService.createTextOutput("ERROR: " + err.message)
                         .setMimeType(ContentService.MimeType.TEXT);
  }
}
```

3. Klik ikon 💾 **Save Project** (Simpan).

### Langkah 3: Deploy Apps Script sebagai Web App
1. Klik tombol **Deploy** (Terapkan) di kanan atas > pilih **New Deployment** (Terapkan baru).
2. Klik ikon gerigi (Select Type) > pilih **Web App** (Aplikasi Web).
3. Isi konfigurasi sebagai berikut:
   - *Description*: `RSVP Pernikahan`
   - *Execute as*: **Me (Email Anda)**
   - *Who has access*: **Anyone** (Siapa saja - ini sangat penting agar formulir web bisa mengirim data).
4. Klik **Deploy**.
5. Google mungkin akan meminta otorisasi keamanan. Klik **Authorize Access**, pilih akun Google Anda, klik **Advanced** (Lanjutan), lalu klik **Go to Untitled project (unsafe)** dan setujui izinnya.
6. Setelah selesai, Google akan memberikan **Web App URL** (URL Aplikasi Web). **Salin URL tersebut**.

### Langkah 4: Hubungkan ke Web Undangan
1. Buka kembali file `config.js`.
2. Temukan variabel `googleSheetsUrl` di bagian bawah.
3. Paste URL web app Google Anda di sana. Contoh:
   ```javascript
   googleSheetsUrl: "https://script.google.com/macros/s/AKfycb.../exec"
   ```
4. Simpan file `config.js` Anda dan upload ulang/re-deploy folder undangan ke server Netlify/Vercel.
5. Sekarang, setiap ada tamu yang mengisi RSVP di web undangan Anda, data dan ucapan doa restu mereka akan langsung masuk secara otomatis ke spreadsheet Google Sheets Anda secara real-time!

---

## 🎯 Cara Membagikan Undangan dengan Nama Tamu Spesifik

Anda bisa membagikan link undangan ini kepada teman/keluarga secara spesifik dengan menambahkan parameter `?to=Nama+Tamu` di akhir URL website Anda.

**Contoh Format Link:**
- Link Utama: `https://pernikahan-albert-grace.netlify.app`
- Dikirim ke Bpk. Joko & Istri: `https://pernikahan-albert-grace.netlify.app?to=Bpk.+Joko+%26+Istri`
- Dikirim ke Sdr. Daniel: `https://pernikahan-albert-grace.netlify.app?to=Sdr.+Daniel`

Teks "Kepada Yth. Bapak/Ibu/Saudara/i:" di halaman depan akan otomatis berubah mengikuti nama yang Anda cantumkan di dalam parameter link tersebut.
