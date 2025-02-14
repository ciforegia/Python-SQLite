# Python-SQLite

## Ciforegia Romakoneri

### 1. Analisis Kode

#### Routing & Redirecting

##### A. Login (`/login`)
- Metode: `GET` & `POST`
- `POST`: Mengambil data login dari form dan melakukan autentikasi.
- `GET`: Menampilkan halaman login.

![image](https://github.com/user-attachments/assets/9f0f0ddf-4926-4408-bcee-d823d5f8a2a9)

##### B. Logout (`/logout`)
- Metode: `GET`
- Menghapus semua data sesi untuk logout user dan memberikan notifikasi logout berhasil.
- Redirect ke halaman index.

![image](https://github.com/user-attachments/assets/abe6a846-11d7-46b5-9096-afaa4529495d)

##### C. Tampilkan Mahasiswa (`/students`)
- Metode: `GET`
- Memastikan user sudah login.
- Mengambil semua data mahasiswa dari database dan menampilkannya.
- Jika tidak login, diarahkan ke halaman login.

![image](https://github.com/user-attachments/assets/6d4be40f-f666-47a6-bf19-c5f8c346e397)

##### D. Tambah Mahasiswa (`/add`)
- Metode: `POST`
- Memastikan user sudah login.
- Mengambil data mahasiswa dari form dan menyimpannya ke database.
- Memberikan notifikasi sukses dan redirect ke halaman mahasiswa.

![image](https://github.com/user-attachments/assets/3911ec1f-5560-4074-bd5f-68d3b25cc781)

##### E. Hapus Mahasiswa (`/delete/<id>`)
- Metode: `GET`
- Memastikan user sudah login.
- Mencari data mahasiswa berdasarkan ID dan menghapusnya dari database.
- Memberikan notifikasi sukses dan redirect ke halaman mahasiswa.

![image](https://github.com/user-attachments/assets/d5ee06f9-577a-4062-bb08-34eb3bd47347)

##### F. Edit Mahasiswa (`/edit/<id>`)
- Metode: `GET` & `POST`
- `GET`: Mengambil data mahasiswa berdasarkan ID dan menampilkan halaman edit.
- `POST`: Mengambil data dari form, memperbarui database, lalu redirect ke daftar mahasiswa.

![image](https://github.com/user-attachments/assets/26688feb-1e65-40ce-8f63-c2cdc45aa39f)

##### G. Halaman Utama (`/`)
- Metode: `GET`
- Menampilkan halaman utama.

![image](https://github.com/user-attachments/assets/eeab4a58-4e17-420c-a109-7f09a6099686)

##### H. Register User (`/users/create`)
- Metode: `GET` & `POST`
- `POST`: Mengambil data username & password dari form.
- Memastikan user belum terdaftar, lalu menyimpan ke database.
- Redirect ke halaman utama setelah berhasil.

![image](https://github.com/user-attachments/assets/dbfe6520-8b30-4ae7-8fee-41230d598dcb)

---

### 2. Class Diagram

Class diagram ini merepresentasikan struktur arsitektur aplikasi Flask yang mengelola pengguna dan data mahasiswa menggunakan autentikasi berbasis HTTP dan database SQLAlchemy.

#### **A. FlaskRoutes (Controller)**
- Mengelola berbagai endpoint dalam aplikasi Flask.
- Fungsi utama:
  - `login(request)`: Autentikasi pengguna.
  - `logout()`: Menghapus sesi pengguna.
  - `student()`: Menampilkan daftar mahasiswa.
  - `add_student(request)`: Menambahkan mahasiswa.
  - `delete_student(id)`: Menghapus mahasiswa berdasarkan ID.
  - `edit_student(id, request)`: Mengedit informasi mahasiswa.
  - `create_user_form(request)`: Mendaftarkan pengguna baru.
- Menggunakan `HTTPBasicAuth` untuk autentikasi dan `SQLAlchemy` untuk manajemen database.

#### **B. HTTPBasicAuth (Authentication)**
- Memverifikasi kredensial pengguna dengan `verify_password(username, password)`.

#### **C. SQLAlchemy (ORM - Database Management)**
- Mengelola interaksi dengan database.
- Metode utama:
  - `create_all()`: Membuat semua tabel dalam database.
  - `commit()`: Menyimpan perubahan ke database.

#### **D. User (Model - Tabel User)**
- Atribut:
  - `id`: Primary key (integer).
  - `username`: Nama pengguna (string, unik).
  - `password_hash`: Hash password (string).
- Metode:
  - `set_password(password)`: Mengubah password menjadi hash.
  - `check_password(password)`: Memeriksa password dengan hash di database.

#### **E. Student (Model - Tabel Mahasiswa)**
- Atribut:
  - `id`: Primary key (integer).
  - `name`: Nama mahasiswa (string).
  - `age`: Umur mahasiswa (integer).
  - `grade`: Nilai mahasiswa (string).

![classdiagram](https://github.com/user-attachments/assets/b9eb12db-4615-4df4-9283-d592aed25ffd)

---

### 3. Use-Case Diagram

Diagram ini menunjukkan interaksi pengguna dengan berbagai fitur aplikasi.

#### **Aktor**
- Regular/Admin: Pengguna biasa atau admin.

#### **Use Case & Relasi**
- **Login & Logout (Account)**: Pengguna masuk dan keluar dari akun.
- **CRUD (Mahasiswa)**: Operasi Create, Read, Update, dan Delete pada data mahasiswa.
- **Create (Account)**: Pendaftaran pengguna baru.

![usecase](https://github.com/user-attachments/assets/287321c3-1419-4511-bae6-a553a29bb540)

---

### 4. Sequence Diagram

Diagram ini menggambarkan urutan interaksi antara pengguna, sistem (FlaskRoutes), controller, dan database.

#### **A. Pembuatan Akun (`POST /user/create`)**
- Pengguna mengisi formulir pendaftaran.
- Sistem memeriksa username.
- Jika belum ada, akun disimpan ke database.
- Redirect ke halaman utama.

#### **B. Login (`POST /login`)**
- Validasi kredensial pengguna.
- Jika valid, diarahkan ke halaman daftar mahasiswa.

#### **C. Logout (`GET /logout`)**
- Menghapus sesi pengguna dan mengarahkan ke halaman login.

#### **D. Mengambil Data Mahasiswa (`GET /students`)**
- Mengambil daftar mahasiswa dari database dan menampilkannya.

#### **E. Menambah Mahasiswa (`POST /students/add`)**
- Validasi input, menyimpan data mahasiswa, dan menampilkan konfirmasi.

#### **F. Memperbarui Data Mahasiswa (`POST /students/<id>`)**
- Validasi dan pembaruan data mahasiswa.

#### **G. Menghapus Data Mahasiswa (`REMOVE /students/<id>`)**
- Validasi dan penghapusan data berdasarkan ID.

![sequencediagram](https://github.com/user-attachments/assets/970f9d98-226c-4f56-ba37-4bb43773fea2)

---

Dokumentasi ini menjelaskan dengan lengkap bagaimana sistem bekerja, mencakup fitur autentikasi, manajemen mahasiswa, serta alur interaksi antar komponen dalam aplikasi Flask-SQLite ini.

