# 🎓 SIMA - Sistem Informasi Mahasiswa Universitas Semarang

![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white)

> Praktikum Mata Kuliah Pemrograman Framework — Sistem Informasi Akademik Mahasiswa berbasis Laravel 9 dengan fitur manajemen data Program Studi, Data Pribadi Mahasiswa, dan Data Mahasiswa USM.

---

## 📋 Deskripsi Proyek

SIMA adalah aplikasi web berbasis **Laravel Framework 9** untuk mengelola data akademik mahasiswa Universitas Semarang. Sistem ini dilengkapi dengan dashboard statistik, manajemen program studi, data pribadi mahasiswa, serta status daftar ulang mahasiswa.

---

## ✨ Fitur Utama

- 📊 **Dashboard (Home)** — Grafik bar chart statistik jumlah calon mahasiswa dan data daftar ulang
- 🏫 **Data Program Studi** — CRUD data fakultas dan program studi dengan pagination
- 👤 **Data Pribadi Mahasiswa** — CRUD data pribadi mahasiswa (NIK, nama, tempat/tanggal lahir) dengan pagination
- 🎓 **Data Mahasiswa USM** — Manajemen data mahasiswa dengan fitur pencarian keyword serta status daftar ulang (Blm DU / Sudah DU)

---

## 🖥️ Tampilan Aplikasi

### Dashboard — `/home`
Menampilkan grafik bar chart statistik **Jumlah Calon** mahasiswa dan **Daftar Ulang**.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5dcd13a2-6f06-4e99-a96a-f84bd94da3cb" />


### Halaman Data Program Studi — `/progdi`
Tabel data program studi dengan kolom: No, Nama Fakultas, Nama Program Studi, dan Action (Edit / Delete). Dilengkapi tombol **Tambah Progdi** dan pagination.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7f8fe73f-ba02-44b7-9926-dca3382f2993" />


### Halaman Data Pribadi Mahasiswa — `/pribadi`
Tabel data pribadi mahasiswa dengan kolom: No, NIK, Nama Mahasiswa, Tempat/Tgl Lahir, dan Action (Edit / Delete). Dilengkapi tombol **Add Data** dan pagination.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4c47a4ba-237f-4282-99dc-7d856a94de53" />


### Halaman Mahasiswa USM — `/mahasiswa`
Tabel data mahasiswa dengan fitur pencarian keyword. Kolom: No, NIM, Nama Mahasiswa, Fakultas/Progdi, dan status daftar ulang (**Blm DU** / **Sudah DU**).
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f64b4cbf-e831-47e0-87ad-a63e248c027c" />


---

## 🛠️ Teknologi yang Digunakan

| Teknologi | Versi | Keterangan |
|-----------|-------|------------|
| Laravel | 9.52.20 | PHP Framework (MVC) |
| PHP | >= 8.0 | Backend / server-side scripting |
| MariaDB / MySQL | — | Database management |
| Blade Template | — | Template engine Laravel |
| Bootstrap | — | Framework CSS responsif |
| Chart.js | — | Library grafik statistik dashboard |
| Composer | — | Package manager PHP |

---

## ⚙️ Cara Instalasi & Menjalankan

### Prasyarat
Pastikan sudah menginstall:
- PHP >= 8.0
- [Composer](https://getcomposer.org/)
- [XAMPP](https://www.apachefriends.org/) atau [Laragon](https://laragon.org/)

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
DB_DATABASE=akademik_db
DB_USERNAME=root
DB_PASSWORD=
```

**6. Jalankan migrasi database**
```bash
php artisan migrate
```

**7. Jalankan aplikasi**
```bash
php artisan serve
```

Buka browser dan akses: `http://127.0.0.1:8000/home`

---

## 📊 Struktur Database

Nama database: **`akademik_db`**

### Tabel `pribadis`

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id_pribadi | bigint unsigned — PK, AUTO_INCREMENT | ID unik data pribadi |
| nik | varchar(255) | Nomor Induk Kependudukan |
| nama_mahasiswa | varchar(255) | Nama lengkap mahasiswa |
| tempat_lahir | varchar(255) | Kota tempat lahir |
| tanggal_lahir | date | Tanggal lahir |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

### Tabel `progdis`

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id_progdi | bigint unsigned — PK, AUTO_INCREMENT | ID unik program studi |
| nm_fakultas | varchar(255) | Nama fakultas |
| nm_progdi | varchar(255) | Nama program studi |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

### Tabel `mahasiswas`

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | bigint unsigned — PK, AUTO_INCREMENT | ID unik mahasiswa |
| nim | varchar(255) | Nomor Induk Mahasiswa |
| id_pri | varchar(255) | Referensi ke id_pribadi |
| id_pro | varchar(255) | Referensi ke id_progdi |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diperbarui |

---

## 🔗 Routing Aplikasi

```php
// Welcome page
Route::get('/', function () { return view('welcome'); });

// Resource routes
Route::resource('progdi', ProgdiController::class);
Route::resource('pribadi', PribadiController::class);
Route::resource('mahasiswa', MahasiswaController::class);
Route::resource('home', HomeController::class);

// Pencarian mahasiswa
Route::get('/search', [MahasiswaController::class, 'search'])->name('search');

// Daftar ulang mahasiswa
Route::get('/mahasiswa/daftar/{id}', 'App\Http\Controllers\MahasiswaController@daftar');
```

| Method | URL | Controller | Keterangan |
|--------|-----|------------|------------|
| GET | `/home` | HomeController | Dashboard & grafik statistik |
| GET | `/progdi` | ProgdiController@index | Daftar program studi |
| POST | `/progdi` | ProgdiController@store | Tambah program studi |
| GET | `/progdi/{id}/edit` | ProgdiController@edit | Form edit program studi |
| PUT | `/progdi/{id}` | ProgdiController@update | Update program studi |
| DELETE | `/progdi/{id}` | ProgdiController@destroy | Hapus program studi |
| GET | `/pribadi` | PribadiController@index | Daftar data pribadi |
| POST | `/pribadi` | PribadiController@store | Tambah data pribadi |
| GET | `/pribadi/{id}/edit` | PribadiController@edit | Form edit data pribadi |
| PUT | `/pribadi/{id}` | PribadiController@update | Update data pribadi |
| DELETE | `/pribadi/{id}` | PribadiController@destroy | Hapus data pribadi |
| GET | `/mahasiswa` | MahasiswaController@index | Daftar mahasiswa USM |
| GET | `/search` | MahasiswaController@search | Pencarian mahasiswa |
| GET | `/mahasiswa/daftar/{id}` | MahasiswaController@daftar | Proses daftar ulang |

---

## 👨‍💻 Informasi Pengembang

| | |
|--|--|
| **Nama** | Moh Irsan Nur Khayan |
| **NIM** | G.211.23.0026 |
| **Mata Kuliah** | Pemrograman Framework |
| **Universitas** | Universitas Semarang |
| **Semester** | 3 |

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan tugas akhir mata kuliah Pemrograman Framework. Bebas digunakan sebagai referensi belajar.

---

> ⭐ Jika repositori ini bermanfaat, jangan lupa beri bintang!
