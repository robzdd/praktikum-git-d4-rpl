# LAPORAN PRAKTIKUM SISTEM TERDISTRIBUSI
## PERTEMUAN 2: VERSION CONTROL SYSTEM (VCS) MENGGUNAKAN GIT DAN GITHUB

---

### IDENTITAS MAHASISWA
- **Nama Mahasiswa** : [Nama Lengkap Anda]
- **NIM**            : [NIM Anda]
- **Kelas / Prodi**   : [Kelas / D4 Rekayasa Perangkat Lunak]
- **Mata Kuliah**     : Sistem Terdistribusi
- **Dosen Pengampu**  : [Nama Dosen Pengampu]
- **Tanggal Praktikum**: [Isi Tanggal Pelaksanaan]

---

## I. TUJUAN PRAKTIKUM

1. Memahami konsep dasar *Version Control System* (VCS) dan peran Git dalam manajemen kode sumber.
2. Mampu melakukan instalasi dan konfigurasi awal identitas pengguna pada Git.
3. Mampu membuat repository lokal baru serta memahami siklus kerja dasar (*Working Directory*, *Staging Area*, dan *Repository*).
4. Mampu melakukan operasi dasar Git seperti `git init`, `git status`, `git add`, `git commit`, dan `git log`.
5. Memahami dan mengimplementasikan konsep percabangan (*branching*) dan penggabungan (*merging*) untuk isolasi fitur baru.
6. Mampu menghubungkan repository lokal ke *remote repository* di GitHub/GitLab.
7. Mampu mensimulasikan alur kolaborasi tim secara terdistribusi menggunakan perintah `clone`, `push`, dan `pull`.

---

## II. DASAR TEORI

### 1. Version Control System (VCS)
*Version Control System* (VCS) adalah perangkat lunak yang mencatat riwayat perubahan file dari waktu ke waktu sehingga pengguna dapat melacak riwayat revisi, membandingkan perbedaan kode, mengembalikan file ke kondisi sebelumnya, serta berkolaborasi dengan pengembang lain tanpa menimpa pekerjaan satu sama lain secara destruktif.

### 2. Git sebagai Distributed VCS (DVCS)
Git adalah sistem kontrol versi terdistribusi (*Distributed Version Control System*). Berbeda dengan sistem terpusat (CVCS) seperti SVN, pada Git setiap *developer* memiliki salinan lokal (*local clone*) lengkap dari seluruh riwayat proyek. Hal ini memungkinkan pekerjaan dilakukan secara *offline* serta meningkatkan redundansi dan keandalan data.

### 3. Tiga Status Utama (Three States) pada Git
Siklus hidup file pada repositori lokal Git terbagi ke dalam 3 area kerja:
1. **Working Directory:** Area kerja tempat file fisik dibuat, diedit, atau dihapus secara langsung oleh pengguna.
2. **Staging Area (Index):** Area perantara tempat file yang telah diubah ditandai untuk dimasukkan ke dalam rekaman (*commit*) berikutnya.
3. **Repository (.git directory):** Basis data permanen tempat Git menyimpan metadata dan rekaman snapshot dari proyek.

```
+-------------------+      git add       +-------------------+     git commit     +-------------------+
| Working Directory | -----------------> |   Staging Area    | -----------------> |    Repository     |
|  (Modified files) |                    |  (Prepared files) |                    |     (.git db)     |
+-------------------+ <----------------- +-------------------+                    +-------------------+
                          git checkout / git restore
```

### 4. Percabangan (Branching) dan Penggabungan (Merging)
*Branching* memungkinkan pengembang membuat alur kerja terisolasi dari basis kode utama (*main* / *master*). Hal ini penting dalam pengembangan tim agar penambahan fitur atau perbaikan *bug* tidak mengganggu kestabilan kode produksi. Setelah fitur selesai diuji, alur cabang tersebut disatukan kembali ke cabang utama melalui proses *merging*.

### 5. Remote Repository dan Kolaborasi
*Remote repository* adalah versi repositori yang di-hosting di server internet atau jaringan privat (seperti GitHub atau GitLab). Kolaborasi dilakukan dengan menyinkronkan repositori lokal dan remote menggunakan perintah:
- `git push`: Mengunggah commit lokal ke remote repository.
- `git fetch` / `git pull`: Mengambil dan menggabungkan perubahan terbaru dari remote repository ke repositori lokal.
- `git clone`: Mengunduh dan menyalin seluruh repositori remote beserta seluruh riwayatnya ke lingkungan lokal baru.

---

## III. ALAT DAN BAHAN

1. **Hardware:** Komputer / Laptop dengan koneksi internet aktif.
2. **Operating System:** Windows / Linux / macOS.
3. **Software:**
   - Git CLI (Git Bash / Command Prompt / Terminal).
   - Teks Editor / IDE (Visual Studio Code).
   - Web Browser.
4. **Akun Platform:** Akun GitHub / GitLab yang telah terverifikasi.

---

## IV. LANGKAH-LANGKAH PRAKTIKUM

### BAGIAN 1: 20 LANGKAH PRAKTIKUM DASAR GIT

---

#### Praktikum 1. Mengecek Instalasi Git
- **Deskripsi:** Memastikan aplikasi Git telah terpasang dengan baik pada sistem operasi dan memeriksa versi yang digunakan.
- **Perintah:**
  ```bash
  git --version
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot terminal hasil perintah `git --version` di bawah ini)*
  
  ![Screenshot Praktikum 1 - Cek Versi Git](assets/praktikum-01-git-version.png)
  
- **Penjelasan & Analisis:**
  Perintah ini membaca *binary* Git yang terdaftar pada sistem PATH. Output menampilkan versi Git yang terinstal (misalnya `git version 2.x.x.windows.1`). Jika versi muncul, terminal telah siap digunakan untuk menjalankan perintah-perintah Git berikutnya.

---

#### Praktikum 2. Konfigurasi Identitas Git
- **Deskripsi:** Mengatur identitas pengguna berupa nama dan email secara global. Identitas ini akan tersemat secara permanen di setiap *commit metadata*.
- **Perintah:**
  ```bash
  git config --global user.name "Nama Mahasiswa"
  git config --global user.email "email@mahasiswa.ac.id"
  git config --list
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot terminal konfigurasi identitas dan output `git config --list`)*
  
  ![Screenshot Praktikum 2 - Konfigurasi Identitas](assets/praktikum-02-git-config.png)
  
- **Penjelasan & Analisis:**
  Opsi `--global` menyimpan konfigurasi pada file `~/.gitconfig` di direktori profil pengguna. Parameter `user.name` dan `user.email` digunakan untuk mengidentifikasi kontributor pada setiap commit. Perintah `git config --list` menampilkan seluruh daftar konfigurasi aktif untuk memvalidasi bahwa nama dan email telah tercatat dengan benar.

---

#### Praktikum 3. Membuat Repository Pertama
- **Deskripsi:** Membuat folder proyek baru dan menginisialisasikannya sebagai repositori lokal Git.
- **Perintah:**
  ```bash
  mkdir praktikum-git
  cd praktikum-git
  git init
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan folder dan output inisialisasi Git)*
  
  ![Screenshot Praktikum 3 - Git Init](assets/praktikum-03-git-init.png)
  
- **Penjelasan & Analisis:**
  Perintah `mkdir` membuat direktori baru bernama `praktikum-git`, lalu perintah `cd` digunakan untuk berpindah ke direktori tersebut. Perintah `git init` menginisialisasi direktori tersebut menjadi repositori Git dengan membuat subdirektori tersembunyi bernama `.git/`. Direktori `.git/` berisi struktur internal data kontrol versi (objek, referensi, konfigurasi repositori).

---

#### Praktikum 4. Membuat File Pertama (`README.md`)
- **Deskripsi:** Membuat file dokumentasi awal proyek yang memuat informasi identitas mahasiswa (Judul, Nama, NIM, dan Program Studi).
- **Perintah / Isi File:**
  Buat file `README.md` menggunakan editor teks atau perintah terminal:
  ```markdown
  # Praktikum Git - Sistem Terdistribusi
  - **Nama**  : [Nama Mahasiswa]
  - **NIM**   : [NIM Mahasiswa]
  - **Prodi** : D4 Rekayasa Perangkat Lunak
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot file `README.md` yang telah dibuat pada editor teks atau via terminal)*
  
  ![Screenshot Praktikum 4 - Membuat File README](assets/praktikum-04-create-readme.png)
  
- **Penjelasan & Analisis:**
  File `README.md` berfungsi sebagai berkas pengantar atau dokumentasi utama dari suatu repositori. Pada tahap ini, berkas baru berada pada lingkungan fisik *Working Directory* dan belum terdaftar ke dalam pelacakan Git.

---

#### Praktikum 5. Memeriksa Status Repository (`git status`)
- **Deskripsi:** Memeriksa status berkas pada *working tree* untuk melihat berkas mana yang belum terlacak (*untracked*).
- **Perintah:**
  ```bash
  git status
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot output status yang menampilkan status `Untracked files: README.md`)*
  
  ![Screenshot Praktikum 5 - Status Untracked](assets/praktikum-05-git-status-untracked.png)
  
- **Penjelasan & Analisis:**
  Perintah `git status` menampilkan status cabang saat ini (`branch master` atau `main`) dan daftar berkas. File `README.md` tertera dalam kategori *Untracked files* (berwarna merah pada Git Bash), yang artinya Git mendeteksi adanya berkas baru tetapi belum didaftarkan untuk dilacak perubahannya.

---

#### Praktikum 6. Melakukan Staging Berkas (`git add`)
- **Deskripsi:** Memindahkan berkas `README.md` dari *Working Directory* ke *Staging Area* (Index) agar siap di-commit.
- **Perintah:**
  ```bash
  git add README.md
  git status
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot perintah `git add` dan perubahan status menjadi `Changes to be committed`)*
  
  ![Screenshot Praktikum 6 - Git Add Staging](assets/praktikum-06-git-add.png)
  
- **Penjelasan & Analisis:**
  Perintah `git add README.md` menambahkan snapshot berkas ke *Staging Area*. Ketika diverifikasi kembali dengan `git status`, status berkas berubah menjadi *Changes to be committed: new file: README.md* (berwarna hijau), menandakan berkas sudah siap dibungkus dalam commit.

---

#### Praktikum 7. Melakukan Commit Pertama
- **Deskripsi:** Menyimpan snapshot berkas dari *Staging Area* ke riwayat database Git lokal dengan menyertakan pesan commit yang jelas.
- **Perintah:**
  ```bash
  git commit -m "Membuat README"
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot eksekusi commit dan informasi ringkasan commit)*
  
  ![Screenshot Praktikum 7 - Git Commit](assets/praktikum-07-git-commit.png)
  
- **Penjelasan & Analisis:**
  Perintah `git commit` dengan flag `-m` menyimpan berkas secara permanen ke repositori lokal. Output menampilkan hash commit (misal `[master (root-commit) a1b2c3d]`), jumlah berkas yang diubah (`1 file changed`), serta jumlah baris yang dimasukkan (`insertions(+)`).

---

#### Praktikum 8. Melihat Riwayat Commit (`git log`)
- **Deskripsi:** Melihat riwayat rekaman commit yang telah tersimpan pada repositori.
- **Perintah:**
  ```bash
  git log --oneline
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot riwayat commit ringkas)*
  
  ![Screenshot Praktikum 8 - Git Log](assets/praktikum-08-git-log.png)
  
- **Penjelasan & Analisis:**
  Opsi `--oneline` menampilkan riwayat commit secara ringkas dalam format satu baris per commit, yang memuat 7 karakter awal hash commit (checksum SHA-1) beserta pesan commit. Hal ini mempermudah audit alur kerja revisi proyek.

---

#### Praktikum 9. Membuat Perubahan Kedua pada Berkas
- **Deskripsi:** Mengedit kembali berkas `README.md` dengan menambahkan informasi mata kuliah, kemudian memantau perubahan statusnya.
- **Perintah / Modifikasi File:**
  Tambahkan baris berikut pada `README.md`:
  ```markdown
  - **Mata Kuliah**: Sistem Terdistribusi
  ```
  Kemudian periksa dengan:
  ```bash
  git status
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot status file setelah diedit - status modified)*
  
  ![Screenshot Praktikum 9 - Modifikasi Berkas](assets/praktikum-09-modify-readme.png)
  
- **Penjelasan & Analisis:**
  Karena berkas `README.md` sudah pernah dilacak oleh Git sebelumnya, modifikasi berkas akan terdeteksi dengan status *Changes not staged for commit: modified: README.md*. Ini membuktikan bahwa Git secara aktif melacak perbedaan isi berkas (*diff*).

---

#### Praktikum 10. Commit Perubahan Kedua
- **Deskripsi:** Memasukkan seluruh perubahan terkini ke *Staging Area* dan membuat commit kedua.
- **Perintah:**
  ```bash
  git add .
  git commit -m "Menambahkan informasi mata kuliah"
  git log --oneline
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot staging, commit kedua, dan daftar riwayat commit terbaru)*
  
  ![Screenshot Praktikum 10 - Commit Kedua](assets/praktikum-10-commit-kedua.png)
  
- **Penjelasan & Analisis:**
  Perintah `git add .` menambahkan semua berkas yang termodifikasi di direktori kerja ke staging area. Commit kedua berhasil dibuat, dan saat diverifikasi dengan `git log --oneline`, kini terdapat dua buah riwayat commit yang tersusun kronologis dari yang terbaru ke yang terlama.

---

#### Praktikum 11. Membuat dan Berpindah ke Branch Baru
- **Deskripsi:** Memeriksa daftar cabang aktif, lalu membuat cabang baru bernama `fitur-profil` sekaligus berpindah ke cabang tersebut.
- **Perintah:**
  ```bash
  git branch
  git switch -c fitur-profil
  git branch
  ```
  *(Catatan: Perintah `git checkout -b fitur-profil` memiliki fungsi yang setara)*
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan branch dan indikator branch aktif)*
  
  ![Screenshot Praktikum 11 - Branching](assets/praktikum-11-git-branch.png)
  
- **Penjelasan & Analisis:**
  Perintah `git branch` menampilkan seluruh cabang lokal; tanda bintang (*) dan warna hijau menunjukkan cabang aktif. Perintah `git switch -c fitur-profil` membuat pointer cabang baru yang bertolak dari commit terakhir dan langsung mengalihkan pointer `HEAD` ke cabang `fitur-profil`.

---

#### Praktikum 12. Bekerja pada Branch Fitur
- **Deskripsi:** Membuat berkas baru bernama `profil.html` pada cabang `fitur-profil`, lalu menyimpannya ke dalam commit cabang tersebut.
- **Perintah / Isi File:**
  Buat berkas `profil.html`:
  ```html
  <!DOCTYPE html>
  <html lang="id">
  <head>
      <meta charset="UTF-8">
      <title>Profil Mahasiswa</title>
  </head>
  <body>
      <h1>Profil Mahasiswa</h1>
      <p>Nama: [Nama Anda]</p>
      <p>NIM: [NIM Anda]</p>
  </body>
  </html>
  ```
  Simpan dan lakukan commit:
  ```bash
  git add .
  git commit -m "Menambahkan halaman profil"
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan file dan commit pada branch `fitur-profil`)*
  
  ![Screenshot Praktikum 12 - Commit Branch Fitur](assets/praktikum-12-branch-commit.png)
  
- **Penjelasan & Analisis:**
  Perubahan ini hanya dicatat pada cabang `fitur-profil`. Cabang utama (`master`/`main`) belum terpengaruh oleh berkas `profil.html` ini, sehingga pekerjaan pengembangan fitur baru tidak mengganggu kode yang stabil.

---

#### Praktikum 13. Kembali ke Branch Utama (Master/Main)
- **Deskripsi:** Berpindah kembali ke cabang utama untuk melihat efek isolasi percabangan Git.
- **Perintah:**
  ```bash
  git switch master
  ls
  ```
  *(Atau `git switch main` sesuai nama default branch)*
- **Screenshot Hasil:**
  > *(Sisipkan screenshot perpindahan branch dan daftar file yang menunjukkan `profil.html` tidak ada di master)*
  
  ![Screenshot Praktikum 13 - Switch Master](assets/praktikum-13-switch-master.png)
  
- **Penjelasan & Analisis:**
  Setelah berpindah kembali ke `master`, berkas `profil.html` otomatis tidak terlihat di direktori kerja (hilang sementara). Hal ini membuktikan bahwa Git secara dinamis mengatur struktur *working directory* sesuai dengan snapshot commit cabang yang sedang aktif.

---

#### Praktikum 14. Melakukan Penggabungan Branch (Merge)
- **Deskripsi:** Menggabungkan perubahan dari cabang `fitur-profil` ke cabang `master`.
- **Perintah:**
  ```bash
  git merge fitur-profil
  ls
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot proses merge dan verifikasi kemunculan berkas `profil.html`)*
  
  ![Screenshot Praktikum 14 - Merge Branch](assets/praktikum-14-git-merge.png)
  
- **Penjelasan & Analisis:**
  Karena tidak ada commit baru di `master` sejak `fitur-profil` dibuat, Git melakukan penggabungan dengan metode *Fast-forward*. Pointer `master` dimajukan ke posisi commit terakhir cabang `fitur-profil`, dan kini berkas `profil.html` telah resmi tergabung ke dalam cabang utama.

---

#### Praktikum 15. Membuat Remote Repository di Platform Online
- **Deskripsi:** Membuat repositori baru di platform online (GitHub) dengan nama `praktikum-git-d4-rpl` tanpa mencentang inisialisasi README (kosong).
- **Langkah:**
  1. Buka browser dan masuk ke akun GitHub Anda.
  2. Klik tombol **New Repository**.
  3. Isi **Repository name**: `praktikum-git-d4-rpl`.
  4. Atur visibilitas ke **Public** (atau Private).
  5. Jangan centang "Add a README file", lalu klik **Create repository**.
  6. Salin URL repositori (misal: `https://github.com/username/praktikum-git-d4-rpl.git`).
- **Screenshot Hasil:**
  > *(Sisipkan screenshot halaman repositori GitHub yang baru dibuat beserta URL-nya)*
  
  ![Screenshot Praktikum 15 - Remote Repo GitHub](assets/praktikum-15-github-create-repo.png)
  
- **Penjelasan & Analisis:**
  Remote repository berfungsi sebagai server pusat sinkronisasi kode. Dibuat dalam keadaan kosong (*bare*) agar dapat menerima riwayat commit yang sudah kita buat sebelumnya di repositori lokal.

---

#### Praktikum 16. Menghubungkan Repository Lokal dengan Remote
- **Deskripsi:** Mendaftarkan URL repositori GitHub sebagai remote alias bernama `origin` pada repositori lokal.
- **Perintah:**
  ```bash
  git remote add origin https://github.com/USERNAME/praktikum-git-d4-rpl.git
  git remote -v
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot penambahan remote dan verifikasi URL fetch/push)*
  
  ![Screenshot Praktikum 16 - Remote Add Origin](assets/praktikum-16-git-remote-v.png)
  
- **Penjelasan & Analisis:**
  Perintah `git remote add origin <URL>` memetakan nama alias `origin` ke alamat remote server. Perintah `git remote -v` menampilkan rincian alamat URL yang digunakan untuk operasi `fetch` (mengambil data) dan `push` (mengunggah data).

---

#### Praktikum 17. Mengunggah Proyek ke Remote Repository (`git push`)
- **Deskripsi:** Mengunggah seluruh commit lokal ke remote repository pada branch master/main dan mengatur upstream tracking.
- **Perintah:**
  ```bash
  git push -u origin master
  ```
  *(Jika branch lokal bernama main, gunakan: `git push -u origin main` atau lakukan `git branch -M main` terlebih dahulu)*
- **Screenshot Hasil:**
  > *(Sisipkan screenshot proses upload push di terminal dan tampilan halaman GitHub setelah di-refresh)*
  
  ![Screenshot Praktikum 17 - Git Push](assets/praktikum-17-git-push.png)
  
- **Penjelasan & Analisis:**
  Opsi `-u` (*set upstream*) mengaitkan cabang lokal dengan cabang remote pada `origin`. Git mengunggah seluruh objek commit, tree, dan blob ke GitHub. Halaman GitHub kini menampilkan seluruh file (`README.md`, `profil.html`) beserta riwayat commit-nya.

---

#### Praktikum 18. Simulasi Developer Kedua: Melakukan Clone Proyek
- **Deskripsi:** Mensimulasikan skenario anggota tim kedua yang mengunduh salinan repositori ke folder atau direktori terpisah.
- **Perintah:**
  ```bash
  cd ..
  git clone https://github.com/USERNAME/praktikum-git-d4-rpl.git praktikum-git-dev2
  cd praktikum-git-dev2
  ls
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot proses clone proyek ke folder dev2)*
  
  ![Screenshot Praktikum 18 - Git Clone](assets/praktikum-18-git-clone.png)
  
- **Penjelasan & Analisis:**
  Perintah `git clone` menduplikasi repositori remote secara lengkap ke direktori `praktikum-git-dev2`. Seluruh riwayat commit, struktur file, dan konfigurasi remote origin otomatis tersedia di komputer developer kedua.

---

#### Praktikum 19. Developer Kedua Membuat Perubahan dan Push
- **Deskripsi:** Developer kedua menambahkan berkas baru `jadwal.html`, melakukan commit, dan mengunggahnya ke repositori remote di GitHub.
- **Perintah / Isi File:**
  Buat berkas `jadwal.html`:
  ```html
  <!DOCTYPE html>
  <html lang="id">
  <head>
      <meta charset="UTF-8">
      <title>Jadwal Kuliah</title>
  </head>
  <body>
      <h1>Jadwal Perkuliahan</h1>
      <p>Sistem Terdistribusi - Ruang Lab RPL</p>
  </body>
  </html>
  ```
  Lakukan commit dan push:
  ```bash
  git add .
  git commit -m "Developer 2: Menambahkan jadwal perkuliahan"
  git push origin master
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot commit developer 2 dan proses push ke GitHub)*
  
  ![Screenshot Praktikum 19 - Dev 2 Push](assets/praktikum-19-dev2-push.png)
  
- **Penjelasan & Analisis:**
  Developer kedua berhasil menambahkan fitur baru dan mengirimkannya ke repositori pusat (GitHub). Pada titik ini, repositori remote sudah selangkah lebih maju daripada repositori lokal milik developer pertama.

---

#### Praktikum 20. Developer Pertama Mengambil Perubahan (`git pull`)
- **Deskripsi:** Developer pertama kembali ke repositori awalnya dan menarik pembaruan yang dibuat oleh developer kedua dari GitHub.
- **Perintah:**
  ```bash
  cd ../praktikum-git
  git pull origin master
  ls
  git log --oneline
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot eksekusi `git pull` yang menampilkan download berkas `jadwal.html`)*
  
  ![Screenshot Praktikum 20 - Git Pull](assets/praktikum-20-git-pull.png)
  
- **Penjelasan & Analisis:**
  Perintah `git pull` menjalankan kombinasi `git fetch` (mengambil objek commit baru dari remote) dan `git merge` (menggabungkannya ke cabang lokal aktif). Berkas `jadwal.html` kini otomatis masuk ke repositori developer pertama, menyinkronkan kedua lingkungan kerja secara terdistribusi.

---

### BAGIAN 2: LATIHAN MANDIRI (PROYEK `profil-mahasiswa`)

Proyek latihan ini bertujuan menguji pemahaman mahasiswa secara menyeluruh dalam menyusun sebuah proyek web kolaboratif yang terstruktur, yang pada akhirnya memiliki 4 berkas utama:
1. `README.md`
2. `index.html`
3. `profil.html`
4. `jadwal.html`

---

#### Tahap 1: Inisialisasi Repository Baru
- **Langkah:** Membuat folder `profil-mahasiswa` dan menginisialisasi repositori Git.
- **Perintah:**
  ```bash
  mkdir profil-mahasiswa
  cd profil-mahasiswa
  git init
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot perintah inisialisasi folder dan repositori `profil-mahasiswa`)*
  
  ![Screenshot Latihan Tahap 1 - Git Init](assets/latihan-tahap-01-init.png)
- **Penjelasan:** Repositori lokal baru dibentuk untuk menampung proyek `profil-mahasiswa`.

---

#### Tahap 2: Membuat File `README.md`
- **Langkah:** Membuat berkas `README.md` berisi judul proyek, deskripsi singkat, nama, dan NIM mahasiswa.
- **Perintah / Isi Berkas:**
  Buat file `README.md`:
  ```markdown
  # Proyek Web Profil Mahasiswa
  Repositori ini memuat informasi profil dan jadwal perkuliahan mahasiswa untuk praktikum Sistem Terdistribusi.

  - **Nama**  : [Nama Lengkap Mahasiswa]
  - **NIM**   : [NIM Mahasiswa]
  - **Prodi** : D4 Rekayasa Perangkat Lunak
  - **Kelas** : [Kelas Anda]
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot berkas `README.md` yang telah dibuat pada editor teks atau via terminal)*
  
  ![Screenshot Latihan Tahap 2 - Create README](assets/latihan-tahap-02-readme.png)
- **Penjelasan:** Dokumentasi pengenalan proyek dipersiapkan sebelum berkas web dibangun.

---

#### Tahap 3: Commit Pertama (Membuat README)
- **Langkah:** Memindahkan `README.md` ke staging area dan melakukan commit pertama.
- **Perintah:**
  ```bash
  git add README.md
  git commit -m "Tahap 3: Membuat README"
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot eksekusi commit README)*
  
  ![Screenshot Latihan Tahap 3 - Commit README](assets/latihan-tahap-03-commit-readme.png)
- **Penjelasan:** Versi awal proyek tersimpan dalam riwayat commit.

---

#### Tahap 4: Membuat `index.html` dan Commit
- **Langkah:** Membuat halaman beranda `index.html` dan menyimpannya ke dalam commit.
- **Perintah / Isi Berkas:**
  Buat file `index.html`:
  ```html
  <!DOCTYPE html>
  <html lang="id">
  <head>
      <meta charset="UTF-8">
      <title>Beranda Mahasiswa</title>
  </head>
  <body>
      <h1>Selamat Datang di Portal Profil Mahasiswa</h1>
      <p>Praktikum Sistem Terdistribusi - VCS Git</p>
      <nav>
          <a href="profil.html">Profil Mahasiswa</a> |
          <a href="jadwal.html">Jadwal Kuliah</a>
      </nav>
  </body>
  </html>
  ```
  ```bash
  git add index.html
  git commit -m "Tahap 4: Membuat halaman utama"
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan `index.html` dan eksekusi commit)*
  
  ![Screenshot Latihan Tahap 4 - Commit Index](assets/latihan-tahap-04-commit-index.png)
- **Penjelasan:** Komponen halaman utama proyek berhasil disimpan ke cabang utama.

---

#### Tahap 5: Membuat Branch `fitur-profil`
- **Langkah:** Membuat cabang kerja baru bernama `fitur-profil` dan berpindah ke cabang tersebut.
- **Perintah:**
  ```bash
  git switch -c fitur-profil
  git branch
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan dan perpindahan ke branch `fitur-profil`)*
  
  ![Screenshot Latihan Tahap 5 - Branch Fitur Profil](assets/latihan-tahap-05-branch-profil.png)
- **Penjelasan:** Isolasi pengembangan dilakukan agar penambahan halaman profil tidak mengganggu cabang utama.

---

#### Tahap 6: Membuat `profil.html` dan Commit
- **Langkah:** Menulis berkas `profil.html` dan menyimpannya pada branch `fitur-profil`.
- **Perintah / Isi Berkas:**
  Buat file `profil.html`:
  ```html
  <!DOCTYPE html>
  <html lang="id">
  <head>
      <meta charset="UTF-8">
      <title>Profil Mahasiswa</title>
  </head>
  <body>
      <h1>Profil Lengkap Mahasiswa</h1>
      <ul>
          <li><strong>Nama:</strong> [Nama Anda]</li>
          <li><strong>NIM:</strong> [NIM Anda]</li>
          <li><strong>Program Studi:</strong> D4 Rekayasa Perangkat Lunak</li>
          <li><strong>Minat:</strong> Distributed Systems & Cloud Computing</li>
      </ul>
      <p><a href="index.html">Kembali ke Beranda</a></p>
  </body>
  </html>
  ```
  ```bash
  git add profil.html
  git commit -m "Tahap 6: Menambahkan profil mahasiswa"
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot penambahan `profil.html` dan commit pada branch)*
  
  ![Screenshot Latihan Tahap 6 - Commit Profil](assets/latihan-tahap-06-commit-profil.png)
- **Penjelasan:** Fitur profil mahasiswa selesai dikerjakan secara terpisah pada cabangnya sendiri.

---

#### Tahap 7: Merge Branch `fitur-profil` ke Branch Utama
- **Langkah:** Berpindah kembali ke cabang utama (`master`/`main`) dan menggabungkan cabang `fitur-profil`.
- **Perintah:**
  ```bash
  git switch master
  git merge fitur-profil
  ls
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot proses merge branch `fitur-profil` ke master)*
  
  ![Screenshot Latihan Tahap 7 - Merge ke Master](assets/latihan-tahap-07-merge-master.png)
- **Penjelasan:** Kode fitur profil kini telah diintegrasikan secara permanen ke cabang utama proyek.

---

#### Tahap 8: Membuat Remote Repository di GitHub
- **Langkah:** Membuat repositori kosong bernama `profil-mahasiswa` pada akun GitHub dan menghubungkannya dengan repositori lokal.
- **Perintah:**
  ```bash
  git remote add origin https://github.com/USERNAME/profil-mahasiswa.git
  git remote -v
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan repository di GitHub dan konfigurasi remote origin)*
  
  ![Screenshot Latihan Tahap 8 - Remote GitHub](assets/latihan-tahap-08-remote-repo.png)
- **Penjelasan:** Jalur komunikasi antara repositori lokal dan cloud GitHub telah terjalin.

---

#### Tahap 9: Mengunggah Proyek ke GitHub (`Push`)
- **Langkah:** Mengirimkan seluruh riwayat commit lokal ke GitHub.
- **Perintah:**
  ```bash
  git push -u origin master
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot proses push dan halaman GitHub yang terisi)*
  
  ![Screenshot Latihan Tahap 9 - Push Project](assets/latihan-tahap-09-push-project.png)
- **Penjelasan:** Repositori remote kini memuat `README.md`, `index.html`, dan `profil.html`.

---

#### Tahap 10: Kloning Proyek untuk Kolaborator (Dev 2)
- **Langkah:** Mensimulasikan developer rekanan dengan mengkloning repositori ke folder baru `profil-mahasiswa-collab`.
- **Perintah:**
  ```bash
  cd ..
  git clone https://github.com/USERNAME/profil-mahasiswa.git profil-mahasiswa-collab
  cd profil-mahasiswa-collab
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot eksekusi `git clone` pada folder kedua)*
  
  ![Screenshot Latihan Tahap 10 - Clone Proyek](assets/latihan-tahap-10-clone-collab.png)
- **Penjelasan:** Rekan kerja memperoleh salinan identik dari proyek untuk melanjutkan pengembangan secara terdistribusi.

---

#### Tahap 11: Menambahkan File `jadwal.html` oleh Kolaborator
- **Langkah:** Kolaborator membuat berkas `jadwal.html` yang memuat informasi jadwal perkuliahan.
- **Perintah / Isi Berkas:**
  Buat file `jadwal.html`:
  ```html
  <!DOCTYPE html>
  <html lang="id">
  <head>
      <meta charset="UTF-8">
      <title>Jadwal Kuliah</title>
  </head>
  <body>
      <h1>Jadwal Perkuliahan Mahasiswa</h1>
      <table border="1" cellpadding="8" cellspacing="0">
          <thead>
              <tr>
                  <th>Hari</th>
                  <th>Mata Kuliah</th>
                  <th>Waktu</th>
                  <th>Ruang</th>
              </tr>
          </thead>
          <tbody>
              <tr>
                  <td>Senin</td>
                  <td>Sistem Terdistribusi</td>
                  <td>08.00 - 10.30</td>
                  <td>Lab RPL</td>
              </tr>
              <tr>
                  <td>Rabu</td>
                  <td>Rekayasa Perangkat Lunak</td>
                  <td>10.30 - 13.00</td>
                  <td>Lab Database</td>
              </tr>
          </tbody>
      </table>
      <p><a href="index.html">Kembali ke Beranda</a></p>
  </body>
  </html>
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot pembuatan berkas `jadwal.html` pada editor)*
  
  ![Screenshot Latihan Tahap 11 - Tambah Jadwal](assets/latihan-tahap-11-create-jadwal.png)
- **Penjelasan:** Penambahan fitur jadwal perkuliahan dilakukan di lingkungan lokal developer kedua.

---

#### Tahap 12: Commit dan Push Perubahan oleh Kolaborator
- **Langkah:** Kolaborator menyimpan perubahan berkas `jadwal.html` dan mengunggahnya ke GitHub.
- **Perintah:**
  ```bash
  git add jadwal.html
  git commit -m "Tahap 12: Menambahkan jadwal kuliah"
  git push origin master
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot commit dan push dari lingkungan kolaborator)*
  
  ![Screenshot Latihan Tahap 12 - Dev 2 Commit Push](assets/latihan-tahap-12-dev2-push.png)
- **Penjelasan:** Perubahan jadwal kuliah berhasil diterbitkan ke repositori remote GitHub.

---

#### Tahap 13: Developer Pertama Mengambil Pembaruan Terakhir (`Pull`)
- **Langkah:** Developer pertama kembali ke repositori aslinya dan menarik pembaruan berkas `jadwal.html` dari remote server.
- **Perintah:**
  ```bash
  cd ../profil-mahasiswa
  git pull origin master
  ls
  git log --oneline
  ```
- **Screenshot Hasil:**
  > *(Sisipkan screenshot hasil `git pull` pada developer 1 yang membuktikan berkas `jadwal.html` sudah masuk)*
  
  ![Screenshot Latihan Tahap 13 - Pull Pembaruan](assets/latihan-tahap-13-dev1-pull.png)
- **Penjelasan:** Seluruh 4 berkas (`README.md`, `index.html`, `profil.html`, `jadwal.html`) kini lengkap tersinkronisasi di lingkungan developer pertama.

---

## V. KESIMPULAN

Berdasarkan praktikum yang telah dilaksanakan, dapat ditarik beberapa kesimpulan penting:

1. **Efektivitas Version Control System (VCS):** Git memungkinkan pencatatan riwayat kode secara terperinci, non-destruktif, dan memfasilitasi pengembalian kondisi (*rollback*) jika terjadi kesalahan selama proses pengembangan.
2. **Keunggulan Sistem Terdistribusi:** Dengan arsitektur terdistribusi, setiap pengembang memiliki repositori lokal yang lengkap, sehingga operasi seperti commit, branching, dan log dapat dilakukan dengan sangat cepat tanpa bergantung pada konektivitas jaringan secara konstan.
3. **Pentingnya Branching & Merging:** Fitur *branch* memberikan isolasi lingkungan kerja yang aman saat mengembangkan fitur baru tanpa merusak stabilitas kode produksi utama hingga fitur tersebut siap dan diuji (*merge*).
4. **Kolaborasi Tim Terdistribusi:** Kombinasi perintah `remote`, `clone`, `push`, dan `pull` melalui platform daring seperti GitHub menjadi fondasi utama kolaborasi perangkat lunak skala besar di era komputasi modern.
