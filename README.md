# 🎓 SIMA - Sistem Informasi Mahasiswa Universitas Semarang

![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white)

> Tugas Akhir Mata Kuliah Pemrograman Framework — Sistem Informasi Akademik Mahasiswa berbasis Laravel dengan fitur manajemen data Program Studi, Data Pribadi Mahasiswa, dan Data Mahasiswa USM.

---

## 📋 Deskripsi Proyek

SIMA adalah aplikasi web berbasis **Laravel Framework** untuk mengelola data akademik mahasiswa Universitas Semarang. Sistem ini dilengkapi dengan dashboard statistik, manajemen program studi, data pribadi mahasiswa, serta status daftar ulang mahasiswa.

---

## ✨ Fitur Utama

- 📊 **Dashboard** — Grafik statistik jumlah calon mahasiswa dan data daftar ulang
- 🏫 **Data Program Studi** — CRUD data fakultas dan program studi dengan pagination
- 👤 **Data Pribadi Mahasiswa** — CRUD data pribadi mahasiswa (NIK, nama, tempat/tanggal lahir) dengan pagination
- 🎓 **Data Mahasiswa USM** — Manajemen data mahasiswa dengan fitur pencarian (NIM, Fakultas/Prodi, status daftar ulang)
- 🔐 **Autentikasi** — Sistem login untuk keamanan akses aplikasi

---

## 🖥️ Tampilan Aplikasi

### Dashboard (Home)
Menampilkan grafik bar chart statistik jumlah calon mahasiswa dan data daftar ulang.

### Halaman Data Program Studi (`/progdi`)
Tabel data program studi dengan kolom: No, Nama Fakultas, Nama Program Studi, dan Action (Edit/Delete). Dilengkapi fitur tambah data dan pagination.

### Halaman Data Pribadi Mahasiswa (`/pribadi`)
Tabel data pribadi dengan kolom: No, NIK, Nama Mahasiswa, Tempat/Tgl Lahir, dan Action (Edit/Delete). Dilengkapi fitur tambah data dan pagination.

### Halaman Mahasiswa USM (`/mahasiswa`)
Tabel data mahasiswa dengan fitur pencarian keyword, kolom: No, NIM, Nama Mahasiswa, Fakultas/Progdi, dan status daftar ulang (Blm DU / Sudah DU).

---

## 🛠️ Teknologi yang Digunakan

| Teknologi | Keterangan |
|-----------|------------|
| Laravel | PHP Framework (MVC) |
| PHP | Backend / server-side scripting |
| MySQL / MariaDB | Database management |
| Blade Template | Template engine Laravel |
| Bootstrap | Framework CSS responsif |
| Chart.js | Library grafik statistik dashboard |
| Composer | Package manager PHP |
| Artisan | CLI tool Laravel |

---

## ⚙️ Cara Instalasi & Menjalankan

### Prasyarat
Pastikan sudah menginstall:
- [PHP](https://www.php.net/) >= 8.0
- [Composer](https://getcomposer.org/)
- [XAMPP](https://www.apachefriends.org/) atau [Laragon](https://laragon.org/)
- [Node.js](https://nodejs.org/) (opsional, untuk asset bundling)

### Langkah Instalasi

**1. Clone repositori ini**
```bash
git clone https://github.com/mohirsannurkhayan/laravel-app.git
cd laravel-app
```

**2. Install dependencies PHP**
```bash
composer install
```

**3. Salin file environment**
```bash
cp .env.example .env
```

**4. Generate application key**
```bash
php artisan key:generate
```

**5. Konfigurasi database**

Buka file `.env` dan sesuaikan:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nama_database
DB_USERNAME=root
DB_PASSWORD=
```

**6. Jalankan migrasi & seeder**
```bash
php artisan migrate
php artisan db:seed
```

**7. Jalankan aplikasi**
```bash
php artisan serve
```

Buka browser dan akses: `http://127.0.0.1:8000`

---

## 🔑 Akun Default

| Username | Password |
|----------|----------|
| admin    | password |

---

## 📊 Struktur Database

### Tabel `progdis` (Program Studi)

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | bigint — PK, AUTO_INCREMENT | ID unik |
| nama_fakultas | varchar | Nama fakultas |
| nama_progdi | varchar | Nama program studi |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

### Tabel `pribadis` (Data Pribadi Mahasiswa)

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | bigint — PK, AUTO_INCREMENT | ID unik |
| nik | varchar | Nomor Induk Kependudukan |
| nama_mahasiswa | varchar | Nama lengkap mahasiswa |
| tempat_lahir | varchar | Kota tempat lahir |
| tgl_lahir | date | Tanggal lahir |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

### Tabel `mahasiswas` (Data Mahasiswa USM)

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | bigint — PK, AUTO_INCREMENT | ID unik |
| nim | varchar | Nomor Induk Mahasiswa |
| progdi_id | bigint — FK | Relasi ke tabel progdis |
| pribadi_id | bigint — FK | Relasi ke tabel pribadis |
| status_du | enum | Status daftar ulang (sudah/belum) |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

---

## 🗂️ Struktur Direktori Laravel

```
laravel-app/
├── app/
│   ├── Http/
│   │   ├── Controllers/      # Controller (Home, Progdi, Pribadi, Mahasiswa)
│   │   └── Middleware/
│   └── Models/               # Model Eloquent
├── database/
│   ├── migrations/           # File migrasi database
│   └── seeders/              # Data awal (seeder)
├── resources/
│   └── views/                # Blade template (home, progdi, pribadi, mahasiswa)
├── routes/
│   └── web.php               # Definisi routing aplikasi
├── public/                   # Asset publik (CSS, JS, gambar)
├── .env.example              # Template konfigurasi environment
├── composer.json             # Dependency PHP
└── README.md                 # Dokumentasi proyek
```

---

## 🔗 Routing Aplikasi

| Method | URL | Keterangan |
|--------|-----|------------|
| GET | `/home` | Dashboard & grafik statistik |
| GET | `/progdi` | Halaman daftar program studi |
| POST | `/progdi` | Tambah program studi |
| PUT | `/progdi/{id}` | Edit program studi |
| DELETE | `/progdi/{id}` | Hapus program studi |
| GET | `/pribadi` | Halaman data pribadi mahasiswa |
| POST | `/pribadi` | Tambah data pribadi |
| PUT | `/pribadi/{id}` | Edit data pribadi |
| DELETE | `/pribadi/{id}` | Hapus data pribadi |
| GET | `/mahasiswa` | Halaman data mahasiswa USM |

---

## 👨‍💻 Informasi Pengembang

| | |
|--|--|
| **Nama** | [Nama Lengkap Kamu] |
| **NIM** | [NIM Kamu] |
| **Mata Kuliah** | Pemrograman Framework |
| **Universitas** | Universitas Semarang |
| **Tahun** | 2024/2025 |

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan tugas akhir mata kuliah Pemrograman Framework. Bebas digunakan sebagai referensi belajar.

---

> ⭐ Jika repositori ini bermanfaat, jangan lupa beri bintang!