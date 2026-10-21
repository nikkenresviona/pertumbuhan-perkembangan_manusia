# Petualangan Sains — Pertumbuhan dan Perkembangan Manusia

Media pembelajaran IPA kelas IX dengan kuis 10 soal, QR Code untuk bergabung, sesi kelas, dan dashboard nilai guru.

## Status dan arsitektur

- Halaman statis: GitHub Pages.
- Basis data dan sinkronisasi nilai: Firebase Realtime Database.
- Login guru: Firebase Authentication (Email/Password).
- Siswa: Firebase Authentication (Anonymous).
- QR Code dibuat di browser dan mengarah ke URL publik dengan parameter sesi.
- Dashboard dirancang untuk kelas minimal 20 siswa; kapasitas akhir bergantung pada kuota dan aturan Firebase proyek.

**Penting:** fitur kelas daring belum aktif sampai Firebase dikonfigurasi dan aturan basis data dipasang. Jangan bagikan kredensial Firebase Admin atau kata sandi guru di repositori.

## 1. Terbitkan website melalui GitHub Pages

1. Buka Settings pada repositori GitHub.
2. Pilih Pages.
3. Pada Build and deployment, pilih Deploy from a branch.
4. Pilih branch `main` dan folder `/ (root)), lalu Save.
5. Tunggu sampai GitHub menampilkan alamat situs. Biasanya berbentuk `https://NAMA-PEMILIK.github.io/pertumbuhan-perkembangan_manusia/`.

## 2. Siapkan Firebase

1. Buat proyek di https://console.firebase.google.com/.
2. Tambahkan aplikasi Web dan salin konfigurasi Firebase.
3. Pada Authentication > Sign-in method, aktifkan **Email/Password** dan **Anonymous**.
4. Pada Realtime Database, buat database. Konfigurasi saat ini menggunakan region Asia Tenggara; sesuaikan `databaseURL` dengan URL yang Firebase berikan.
5. Buat akun Email/Password untuk guru. Email yang diizinkan harus sama dengan konstanta `TEACHER_EMAIL` di `index.html` (default: `guru@sekolah.sch.id`). Ganti konstanta tersebut dengan email guru yang benar.
6. Ganti nilai placeholder `GANTI_DENGAN_...` pada `firebaseConfig` di `index.html` dengan konfigurasi aplikasi web Firebase Anda.
7. Pada Realtime Database > Rules, salin isi `database.rules.json` dan klik Publish.

Konfigurasi web Firebase bukan kredensial Admin, tetapi aturan database tetap wajib dipasang agar akses dibatasi sesuai peran.

## 3. Mulai kuis

1. Buka website publik dan pilih **Ruang Guru**.
2. Masuk menggunakan akun guru yang telah dibuat.
3. Buat kode kelas baru.
4. Masukkan URL GitHub Pages ke kolom alamat web publik jika belum terisi otomatis.
5. Bagikan QR Code atau tautan kepada siswa.
6. Siswa membuka tautan, memasukkan nama, lalu mengerjakan kuis. Dashboard guru menerima hasil yang tersimpan di Firebase.

## Data dan privasi

Papan peringkat kelas menampilkan nama, nilai, dan status penyelesaian kepada peserta yang masuk ke sesi tersebut. Gunakan nama yang sesuai kebijakan sekolah dan hindari meminta data pribadi sensitif. Guru harus menjaga akun dan kata sandinya. Jangan memakai konfigurasi database dengan akses baca/tulis global.

## Pemecahan masalah

- **Firebase belum dikonfigurasi:** pastikan placeholder konfigurasi sudah diganti dan halaman dimuat ulang.
- **Siswa tidak bisa masuk:** pastikan Anonymous Authentication aktif, kode kelas benar, dan sesi belum ditutup.
- **Guru tidak bisa login:** pastikan Email/Password aktif dan email akun cocok dengan `TEACHER_EMAIL`.
- **Tidak ada sinkronisasi:** periksa Firebase Realtime Database URL dan Rules, lalu lihat Console browser untuk pesan kesalahan.
- **QR tidak membuka website:** pastikan kolom URL publik berisi alamat GitHub Pages lengkap dan situs sudah selesai diterbitkan.
