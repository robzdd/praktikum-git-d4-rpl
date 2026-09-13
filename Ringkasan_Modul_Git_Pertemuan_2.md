# Ringkasan Praktikum Git - Pertemuan 2
**Sumber:** Modul "Pertemuan 2 - Praktikum.pdf"

## Bagian 1: 20 Langkah Praktikum Git
1. **Praktikum 1. Mengecek Git:** Memastikan Git telah terpasang melalui Command Prompt atau Git Bash dengan mengeksekusi perintah `git --version`.
2. **Praktikum 2. Konfigurasi Identitas Git:** Mengatur nama dan *email* secara global (`git config --global user.name` & `user.email`), serta memverifikasinya melalui `git config --list`.
3. **Praktikum 3. Membuat Repository Pertama:** Membuat *folder* `praktikum-git`, masuk ke *folder* (`cd`), dan menjalankan `git init`.
4. **Praktikum 4. Membuat File Pertama:** Membuat *file* `README.md` (memuat judul, nama, NIM, dan Prodi).
5. **Praktikum 5. Melihat Status:** Menjalankan `git status` untuk mengamati status *file* (belum di-commit).
6. **Praktikum 6. Melakukan Git Add:** Memindahkan *file* ke area *staging* dengan `git add README.md`.
7. **Praktikum 7. Melakukan Commit:** Menyimpan perubahan ke sistem Git permanen dengan `git commit -m "Membuat README"`.
8. **Praktikum 8. Melihat History:** Menampilkan riwayat *commit* dengan `git log --oneline`.
9. **Praktikum 9. Membuat Perubahan Kedua:** Menambahkan baris info mata kuliah pada `README.md` lalu mengecek dengan `git status`.
10. **Praktikum 10. Commit Kedua:** Menjalankan `git add .` dan `git commit -m "Menambahkan informasi mata kuliah"`.
11. **Praktikum 11. Membuat Branch:** Melihat *branch* (`git branch`), membuat dan berpindah ke `fitur-profil` (`git switch -c fitur-profil`).
12. **Praktikum 12. Bekerja pada Branch:** Membuat `profil.html`, menyimpan dengan `git add .` dan `git commit`.
13. **Praktikum 13. Kembali ke Main:** Berpindah ke *branch* `master` (`git switch master`), `profil.html` disembunyikan karena belum di-merge.
14. **Praktikum 14. Melakukan Merge:** Menggabungkan `fitur-profil` ke `master` dengan `git merge fitur-profil`.
15. **Praktikum 15. Membuat Repository Online:** Membuat *repository online* `praktikum-git-d4-rpl` dan menyalin URL-nya.
16. **Praktikum 16. Menghubungkan Repository Lokal dengan Remote:** Mengeksekusi `git remote add origin URL_REPOSITORY` dan memastikannya dengan `git remote -v`.
17. **Praktikum 17. Push Project:** Mengunggah proyek ke *remote repository* dengan `git push -u origin master`.
18. **Praktikum 18. Simulasi Developer Kedua:** Menyalin proyek dari *remote* menggunakan `git clone URL_REPOSITORY` di *folder*/komputer lain.
19. **Praktikum 19. Developer Kedua Membuat Perubahan:** Membuat `jadwal.html`, melakukan `add`, `commit`, dan `push`.
20. **Praktikum 20. Developer Pertama Mengambil Perubahan:** Menarik pembaruan `jadwal.html` dari server menggunakan `git pull`.

---

## Bagian 2: Latihan (Proyek `profil-mahasiswa`)
Tugas akhir dengan 13 tahapan pembuatan proyek kolaborasi dengan struktur akhir: `README.md`, `index.html`, `profil.html`, dan `jadwal.html`.

- **Tahap 1:** Buat repository Git.
- **Tahap 2:** Buat `README.md`.
- **Tahap 3:** Commit: Membuat README.
- **Tahap 4:** Buat `index.html` dan Commit: Membuat halaman utama.
- **Tahap 5:** Buat branch: `fitur-profil`.
- **Tahap 6:** Buat `profil.html` dan Commit: Menambahkan profil mahasiswa.
- **Tahap 7:** Merge ke main.
- **Tahap 8:** Buat remote repository.
- **Tahap 9:** Push project.
- **Tahap 10:** Clone project pada folder/komputer lain.
- **Tahap 11:** Tambahkan `jadwal.html`.
- **Tahap 12:** Commit dan push.
- **Tahap 13:** Pada komputer pertama lakukan: `git pull`.
