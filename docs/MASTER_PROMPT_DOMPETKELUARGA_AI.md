# MASTER PROMPT — DOMPETKELUARGA AI
## Instruksi Eksekusi untuk Coding Agent

> **Tujuan:** Bangun DompetKeluarga AI sebagai aplikasi keuangan pribadi dan keluarga yang benar-benar berfungsi, aman, teruji, dan dapat dikembangkan.
>
> **Repositori:** https://github.com/gyot/DompetKeluarga.git

## 1. Peran dan misi

Bertindaklah sebagai Senior Full-Stack Engineer, Software Architect, Database Engineer, AI Engineer, UI/UX Designer, QA Engineer, dan Security Engineer.

Baca instruksi ini sampai selesai. Periksa repositori yang tersedia, kemudian implementasikan aplikasi secara nyata. Jangan berhenti pada rencana, mockup, contoh kode, atau dokumentasi saja.

### Aturan wajib

1. Periksa struktur repositori, branch aktif, README, teknologi, dependensi, konfigurasi, database, autentikasi, serta fitur existing sebelum mengubah kode.
2. Pertahankan teknologi dan fitur existing yang masih layak. Jangan melakukan rewrite besar tanpa alasan teknis yang jelas.
3. Jika repositori kosong atau source code tidak tersedia, jangan mengarang seolah-olah kode sudah diperiksa. Jelaskan hambatan dan minta source code yang benar sebelum membuat perubahan yang berisiko.
4. Jangan menimpa branch produksi secara langsung. Gunakan branch kerja terpisah dan buat perubahan yang mudah ditinjau.
5. Implementasikan fitur hingga frontend, backend, dan database benar-benar terhubung.
6. Jangan menggunakan mock data sebagai pengganti backend produksi. Seed data demo harus terpisah dan jelas.
7. Jangan meninggalkan tombol, menu, form, atau halaman yang tidak berfungsi.
8. Jangan menaruh API key, password, token, atau secret di frontend, repository, log, screenshot, atau respons API.
9. Jangan menjalankan migrasi destruktif atau menghapus data existing tanpa backup dan persetujuan yang diperlukan.
10. Jalankan tes yang relevan dan laporkan hasil aktual. Jangan mengklaim tes berhasil jika belum dijalankan.
11. Jika suatu layanan memerlukan kredensial atau layanan eksternal yang belum tersedia, implementasikan integrasinya dengan aman, dokumentasikan konfigurasi yang diperlukan, dan nyatakan bahwa tes eksternal belum dapat dilakukan.
12. Jangan menunggu seluruh aplikasi selesai untuk mulai menguji. Implementasikan secara bertahap.

## 2. Visi produk

DompetKeluarga AI adalah platform keuangan pribadi dan keluarga untuk:

- Mencatat pemasukan, pengeluaran, transfer, refund, dan penyesuaian saldo.
- Mengelola rekening bank, dompet tunai, dan e-wallet.
- Mengendalikan pengeluaran yang tidak terencana.
- Membuat anggaran bulanan dengan metode zero-based budgeting.
- Mengelola tagihan, transaksi berulang, tabungan, utang, dan piutang.
- Memantau arus kas, saldo, tren pengeluaran, dan laporan.
- Mengelola keuangan bersama anggota keluarga secara transparan dan sesuai izin.
- Memasukkan transaksi menggunakan bahasa alami melalui AI.
- Mendapatkan analisis dan rekomendasi berdasarkan data keuangan aktual.
- Diakses melalui web responsif, PWA, dan Android jika wrapper APK diperlukan.

Bahasa utama: Bahasa Indonesia. Mata uang default: IDR (Rupiah). Zona waktu default: `Asia/Jakarta`. Semua perhitungan keuangan harus konsisten dan dapat dijelaskan.

Aplikasi inti harus tetap dapat digunakan ketika provider AI tidak tersedia.

## 3. Audit dan pemilihan teknologi

Pertama, identifikasi teknologi dan arsitektur repositori. Pertahankan stack existing jika memungkinkan.

Jika repositori benar-benar kosong, gunakan pilihan awal berikut, dengan versi yang kompatibel:
- Frontend: React + TypeScript + Vite.
- UI: Tailwind CSS dan komponen UI yang konsisten.
- Backend: Laravel API.
- Database: PostgreSQL atau MySQL/MariaDB sesuai lingkungan.
- Auth: Laravel Sanctum atau mekanisme aman yang cocok dengan arsitektur.
- Grafik: library chart yang kompatibel.
- PWA: manifest, service worker, dan strategi cache aman.
- Android: PWA terlebih dahulu; wrapper Android terpelihara bila diperlukan.
- AI: adapter provider di backend.

Jangan mengganti stack existing hanya untuk mengikuti daftar ini. Dokumentasikan keputusan arsitektur.

Pisahkan presentation, API/controller, business logic/service, data access/model, AI adapter, dan security/authorization.

## 4. Autentikasi dan akun

Implementasikan:
- Registrasi, login, logout.
- Reset password dan verifikasi email bila sesuai.
- Profil pengguna dan penggantian password.
- Pengelolaan sesi/perangkat.
- Preferensi mata uang, tanggal, zona waktu, bahasa, dan tampilan.
- Rate limiting untuk autentikasi.
- Penghapusan akun dengan konfirmasi dan kebijakan retensi data yang jelas.

Gunakan password hashing kuat dan mekanisme sesi/token aman. Jangan pernah menyimpan password teks biasa atau membocorkan keberadaan akun pada alur pemulihan.

## 5. Keluarga, workspace, dan hak akses

Satu pengguna dapat membuat atau bergabung dengan keluarga/workspace. Data keuangan setiap keluarga harus terisolasi.

Role awal:
- **Owner:** mengelola keluarga, anggota, dan pengaturan.
- **Admin:** mengelola operasional sesuai izin.
- **Member:** mencatat transaksi dan mengakses data sesuai izin.
- **Viewer:** hanya melihat data yang diizinkan.

Fitur:
- Undangan anggota dengan token aman, masa berlaku, dan status.
- Terima/tolak undangan.
- Tambah/keluarkan anggota sesuai kebijakan.
- Visibilitas transaksi dan opsi kategori privat bila diperlukan.
- Audit pencatat dan waktu perubahan.

Authorization harus ditegakkan di backend pada setiap request. Lindungi dari IDOR dan akses lintas keluarga. Menyembunyikan tombol di frontend bukan pengganti pemeriksaan izin di backend.

## 6. Dashboard

Tampilkan data aktual:
- Saldo rekening dan ringkasan keuangan.
- Pemasukan, pengeluaran, dan selisih bulan berjalan.
- Penggunaan dan sisa anggaran.
- Grafik arus kas dan pengeluaran per kategori.
- Transaksi terbaru.
- Tagihan mendatang/terlambat.
- Target tabungan.
- Utang dan piutang.
- Peringatan anggaran.
- Ringkasan AI jika tersedia.

Sediakan filter periode, anggota, rekening, kategori, dan workspace sesuai izin. Jangan gunakan angka hardcoded. Definisikan perbedaan saldo rekening, total aset, dan anggaran; hindari perhitungan ganda.

## 7. Rekening dan dompet

Dukung rekening bank, tunai, e-wallet, tabungan, dan jenis lain yang dapat dikonfigurasi.

Data minimal: nama, jenis, saldo awal, tanggal saldo awal, mata uang, pemilik/workspace, status, dan catatan opsional.

Fitur: CRUD, arsip, riwayat mutasi, rekonsiliasi, penyesuaian saldo dengan audit, dan transfer antar rekening.

Transfer internal tidak boleh dihitung sebagai pemasukan atau pengeluaran keluarga. Transfer harus menghubungkan transaksi sumber dan tujuan secara konsisten dan atomik.

## 8. Transaksi

Jenis transaksi:
- Pemasukan.
- Pengeluaran.
- Transfer.
- Refund/pengembalian dana.
- Penyesuaian saldo.
- Jenis lain jika aturan bisnisnya terdokumentasi.

Field minimal: workspace, jenis, nominal, mata uang, tanggal/waktu, rekening, kategori/subkategori, deskripsi, pencatat, pihak terkait opsional, tag, lampiran, status, sumber input, dan timestamps.

Fitur:
- Tambah, edit, detail, hapus/arsip dengan konfirmasi sesuai kebijakan.
- Pencarian, filter, sort, pagination.
- Lampiran bukti transaksi.
- Duplikasi transaksi.
- Transaksi berulang.
- Impor/ekspor.
- Riwayat perubahan dan deteksi duplikasi.

Gunakan tipe uang yang tepat (`DECIMAL` atau integer minor units dengan kebijakan konsisten), bukan floating point untuk perhitungan uang. Validasi server-side. Operasi yang mengubah banyak entitas harus menggunakan database transaction. Terapkan idempotency untuk endpoint yang berisiko menerima request berulang.

Koreksi transaksi harus menjaga konsistensi saldo dan audit trail.

## 9. Kategori

Sediakan kategori/subkategori pemasukan dan pengeluaran, termasuk kategori bawaan seperti makanan, rumah tangga, transportasi, pendidikan, kesehatan, tagihan, cicilan, hiburan, kebutuhan anak, tabungan, dan lainnya.

Pengguna dapat membuat, mengubah, memberi ikon/warna, mengarsipkan, dan mengatur kategori sesuai izin. Jangan menghapus kategori secara destruktif jika sudah digunakan; gunakan arsip atau pemetaan ke kategori pengganti.

## 10. Zero-based budgeting

Implementasikan zero-based budgeting dengan prinsip:

`Pendapatan yang dialokasikan - Total alokasi = 0`

Dukung anggaran bulanan per kategori/subkategori, tabungan, pembayaran utang, pengeluaran wajib, dana darurat, dan pengeluaran fleksibel.

Fitur:
- Buat dan salin anggaran antarbulan.
- Lihat alokasi belum ditentukan.
- Bandingkan anggaran, aktual, dan sisa.
- Persentase pemakaian.
- Peringatan sebelum batas dan saat terlampaui.
- Carry-over saldo kategori jika diaktifkan.
- Anggaran keluarga bersama.

Bedakan pendapatan yang diharapkan dari pendapatan yang diterima, anggaran dari pengeluaran aktual, serta alokasi dari saldo rekening. Jangan memperlakukan anggaran sebagai saldo rekening.

## 11. Tagihan dan transaksi berulang

Dukung tagihan listrik, air, internet, sewa, cicilan, pendidikan, langganan, dan iuran.

Fitur: jatuh tempo, nominal tetap/variabel, frekuensi, pengingat, status belum dibayar/dibayar/terlambat/dibatalkan, riwayat pembayaran, transaksi berulang, retry terkontrol, dan pencegahan transaksi ganda.

Tagihan terjadwal tidak otomatis berarti sudah dibayar. Gunakan scheduler/queue sesuai stack dan buat proses idempotent.

## 12. Tabungan, utang, dan piutang

### Target tabungan
Dukung target dana darurat, pendidikan, kendaraan, rumah, liburan, dan tujuan lain. Simpan nominal target, tenggat, saldo terkumpul, progres, serta riwayat kontribusi.

Transfer ke rekening tabungan sendiri bukan otomatis pengeluaran konsumsi keluarga.

### Utang dan piutang
Dukung pokok, bunga/biaya, pembayaran sebagian, jatuh tempo, jadwal cicilan, saldo tersisa, dan riwayat pembayaran. Dokumentasikan perlakuan akuntansi agar pokok yang sudah dicatat sebagai kewajiban tidak dihitung sebagai pengeluaran baru ketika dibayar.

## 13. Laporan dan analitik

Sediakan laporan:
- Arus kas.
- Pemasukan/pengeluaran per periode.
- Pengeluaran per kategori dan anggota.
- Perbandingan bulanan/tahunan.
- Anggaran versus realisasi.
- Tren saldo rekening.
- Tagihan.
- Utang/piutang.
- Target tabungan.

Sediakan filter tanggal, anggota, rekening, kategori, grafik responsif, dan ekspor CSV/Excel/PDF sesuai stack. Dokumentasikan perlakuan transfer, refund, saldo awal, dan transaksi batal dalam laporan.

## 14. AI Assistant

AI harus dapat:
- Mencatat transaksi dari bahasa alami.
- Meminta klarifikasi bila informasi tidak lengkap.
- Mengusulkan kategori.
- Merangkum pengeluaran.
- Mendeteksi perubahan pola belanja.
- Membantu menyusun anggaran.
- Menjawab pertanyaan tentang data yang boleh diakses.
- Membantu target tabungan dan rekomendasi penghematan berdasarkan data aktual.

Contoh:
- “Bulan ini uang paling banyak habis untuk apa?”
- “Berapa sisa anggaran belanja?”
- “Catat pengeluaran makan siang 35 ribu tunai hari ini.”
- “Saya menerima gaji 8 juta di rekening BCA.”
- “Bandingkan pengeluaran bulan ini dengan bulan lalu.”

### Alur parsing transaksi
1. Terima teks dari pengguna.
2. Ambil konteks yang diperlukan dan diizinkan.
3. Minta AI menghasilkan objek terstruktur.
4. Validasi backend untuk nominal, tanggal, jenis, kategori, rekening, dan izin.
5. Minta klarifikasi jika ada informasi penting yang belum jelas.
6. Tampilkan ringkasan untuk dikonfirmasi.
7. Setelah konfirmasi, simpan melalui service transaksi normal.
8. Tampilkan hasil dan ID transaksi.

AI tidak boleh menulis langsung ke database atau melewati validasi dan authorization. Gunakan structured output jika provider mendukungnya. Jangan mengarang saldo atau transaksi. Bedakan fakta, estimasi, dan rekomendasi. Aplikasi harus tetap berfungsi tanpa AI.

## 15. AI Provider Manager / Configuration Center

Buat halaman admin untuk mengatur provider tanpa mengedit source code.

### Adapter
Definisikan kontrak konsisten, misalnya:
- `chat()`
- `testConnection()`
- `getCapabilities()`
- `validateConfiguration()`

Implementasikan adapter OpenAI-compatible terlebih dahulu. Adapter native atau provider lokal harus terpisah jika protokolnya berbeda. Jangan menganggap semua provider mendukung parameter, model discovery, tools, atau structured output yang sama.

### Wizard konfigurasi
Langkah 1 — Provider:
- Nama konfigurasi.
- Provider/adapter.
- Protokol.
- Status.

Langkah 2 — Endpoint:
- Base URL.
- Validasi skema HTTPS untuk endpoint remote.
- Endpoint path sesuai protokol.

Langkah 3 — Kredensial:
- API key.
- Status key tersimpan.
- Rotasi/ganti key.
- Jangan mengembalikan secret ke browser.

Langkah 4 — Model:
- Model ID manual.
- Model discovery hanya bila provider mendukungnya.
- Kapabilitas model yang sudah diverifikasi.

Langkah 5 — Pengaturan lanjutan:
- Temperature.
- Batas output token.
- Timeout.
- Retry.
- Structured/JSON output.
- Tool calling.
- Parameter khusus adapter yang valid.

Langkah 6 — Pengujian dan aktivasi:
- Tombol uji koneksi yang melakukan request backend nyata.
- Loading state dan durasi.
- Pesan sukses/gagal yang aman.
- Simpan konfigurasi.
- Aktifkan/nonaktifkan provider.
- Catat status tes dan waktu tes.

Jangan menampilkan sukses hanya karena form valid. Jangan mengarang model ID atau endpoint provider.

### Secret management
- Enkripsi API key di backend sebelum disimpan.
- Kelola master encryption key melalui environment atau secret manager.
- Jangan pernah mengembalikan key dalam API response.
- Kembalikan metadata seperti `has_api_key`, bukan secret.
- Jangan menyimpan secret di localStorage/sessionStorage, log, source, fixture, atau dokumentasi.
- Terapkan role admin, audit perubahan tanpa merekam secret, dan rotasi key.
- Jangan menimpa secret lama sampai secret baru tervalidasi dan berhasil disimpan.

### Keamanan Base URL / SSRF
Base URL yang dimasukkan pengguna dapat menimbulkan risiko SSRF. Tolak skema yang tidak didukung; blokir localhost, IP private/internal, link-local, endpoint metadata cloud, port/host yang tidak diizinkan, dan redirect ke host lain. Validasi DNS dan hasil resolusi IP, cegah DNS rebinding, batasi egress melalui firewall/proxy, ukuran request/respons, dan timeout. Pemeriksaan URL sederhana saja tidak cukup.

Aktifkan provider hanya jika konfigurasi wajib valid dan tes koneksi berhasil. Fallback harus eksplisit dan tidak boleh melanggar kebijakan privasi atau biaya.

## 16. Pengaturan dan notifikasi

Configuration Center:
- Profil.
- Keluarga dan izin.
- Mata uang/zona waktu.
- Kategori.
- Rekening.
- Anggaran.
- Notifikasi.
- Preferensi AI/provider.
- Privasi dan keamanan.
- Backup/ekspor.
- Sesi dan audit log.

Notifikasi:
- Anggaran hampir habis/terlampaui.
- Tagihan mendatang/terlambat.
- Target tabungan.
- Undangan keluarga.
- Perubahan anggota.
- Aktivitas keamanan.
- Ringkasan berkala.

Mulai dari notifikasi dalam aplikasi. Email/push dapat ditambahkan sesuai infrastruktur. Cegah notifikasi ganda dengan proses idempotent.

## 17. UI/UX, PWA, dan Android

UI harus modern, profesional, konsisten, aksesibel, dan responsif. Sediakan light/dark mode, navigasi jelas, form validation, loading/error/empty states, konfirmasi tindakan destruktif, format Indonesia, dan dukungan keyboard/screen reader.

Navigasi utama:
1. Dashboard
2. Transaksi
3. Anggaran
4. Rekening
5. Tagihan
6. Tabungan
7. Utang/piutang
8. Laporan
9. AI Assistant
10. Keluarga
11. Pengaturan

Setiap tombol harus benar-benar berfungsi.

Untuk PWA: manifest, ikon, instalasi, service worker, offline fallback, dan penanganan koneksi. Jangan cache data keuangan sensitif secara berlebihan.

Untuk APK wrapper bila dibutuhkan: gunakan solusi terpelihara, validasi TLS tetap aktif, dan jangan mengekspos API key. Uji autentikasi, cookie/session, deep link, back navigation, dan fitur native pada perangkat nyata sebelum menyatakan berhasil.

## 18. Database dan integritas data

Evaluasi entitas berikut dan sesuaikan dengan model existing agar tidak membuat tabel duplikat:

- users
- families/workspaces
- family_members
- family_invitations
- accounts
- transactions
- transaction_transfers
- categories
- budgets
- budget_allocations
- recurring_transactions
- bills
- savings_goals
- savings_contributions
- debts
- debt_payments
- attachments
- notifications
- ai_provider_configs
- ai_usage_logs
- audit_logs
- user_settings

Gunakan migrasi versioned, foreign key, index, constraint, timestamps konsisten, transaksi database, dan soft delete jika tepat. Buat backup sebelum migrasi berisiko. Pisahkan seed data demo dari produksi. Verifikasi skema dan data setelah migrasi.

## 19. Keamanan

Terapkan:
- Validasi server-side.
- Authentication dan authorization.
- Rate limiting.
- CSRF protection sesuai arsitektur.
- CORS terbatas.
- Pencegahan XSS dan SQL injection.
- Validasi upload dan batas ukuran file.
- Penyimpanan lampiran yang aman.
- Cookie/session aman.
- Secret management dan redaksi log.
- Audit trail.
- Isolasi data lintas keluarga.
- Error handling tanpa stack trace di production.
- Dependency/security audit.
- Perlindungan endpoint admin.
- Batas penggunaan dan biaya AI.

Kirim ke provider AI hanya data minimum yang diperlukan. Jangan pernah mengirim seluruh database hanya untuk menjawab pertanyaan sederhana.

## 20. API dan business logic

Buat API konsisten dan terdokumentasi sesuai arsitektur existing. Kelompok endpoint mencakup auth, profil, keluarga, anggota, rekening, transaksi, kategori, anggaran, tagihan, tabungan, utang, laporan, notifikasi, AI chat, parsing transaksi, provider configuration, connection test, activation, dan audit log.

Setiap endpoint harus memiliki validasi, authorization, HTTP status yang benar, error handling, pagination bila diperlukan, dan tes.

Aturan saldo, transfer, anggaran, utang, serta transaksi AI harus berada di service/business logic, bukan hanya frontend.

## 21. Pengujian wajib

Buat dan jalankan tes yang sesuai stack untuk:

**Auth:** registrasi, login, logout, reset password, akses tanpa autentikasi.

**Multiuser:** isolasi keluarga, izin viewer, akses silang, akses admin.

**Transaksi:** pemasukan, pengeluaran, transfer, refund, edit/hapus, saldo konsisten, nominal/tanggal invalid, request ganda.

**Anggaran:** alokasi nol, realisasi, overspending, carry-over, perbandingan bulan.

**AI:** key salah, timeout, rate limit, model tidak ditemukan, respons tidak valid, konfirmasi transaksi, tidak ada kebocoran secret, data tidak cukup, isolasi keluarga.

**Frontend:** validasi form, loading/error/empty state, navigasi, responsif, transaksi, wizard AI.

**Operasional:** migrasi, seeder, build, API integration, dan backup/restore jika tersedia.

Laporkan tes yang lulus, gagal, dilewati, atau belum dijalankan. Jangan mematikan tes untuk membuat build terlihat berhasil.

## 22. Urutan implementasi

### Tahap 0 — Audit
- Baca struktur repositori dan branch.
- Identifikasi stack, fitur existing, dan hambatan.
- Catat risiko dan rencana.

### Tahap 1 — Fondasi
- Struktur aplikasi, database, migrasi, auth, role/permission, isolasi workspace, layout.

### Tahap 2 — Keuangan inti
- Rekening, kategori, transaksi, transfer, saldo, dashboard, audit trail.

### Tahap 3 — Perencanaan
- Zero-based budget, tagihan, transaksi berulang, tabungan, utang/piutang.

### Tahap 4 — Laporan
- Arus kas, analitik kategori, perbandingan periode, ekspor.

### Tahap 5 — AI
- Adapter, provider manager, enkripsi secret, connection test, AI chat, parsing transaksi, konfirmasi, analisis.

### Tahap 6 — Kolaborasi
- Undangan, anggota, izin, notifikasi, audit aktivitas.

### Tahap 7 — PWA/Android
- Instalasi, offline handling, wrapper bila diperlukan, pengujian mobile.

### Tahap 8 — Hardening
- Security review, performa, dependency audit, tes menyeluruh, dokumentasi deployment.

Setelah setiap tahap, jalankan tes, perbaiki masalah, dan catat statusnya. Prioritaskan alur inti yang bisa digunakan dari awal hingga akhir.

## 23. Definition of Done

Fitur tidak selesai hanya karena halaman dibuat. Fitur dianggap selesai jika:
1. UI berfungsi.
2. Backend dan database terhubung.
3. Validasi dan izin bekerja.
4. Error/loading/empty states tersedia.
5. Alur berhasil dan gagal ditangani.
6. Tes relevan dijalankan.
7. Dokumentasi diperbarui.
8. Tidak ada secret atau data contoh sensitif.

Aplikasi siap untuk uji penerimaan ketika alur utama pengguna berfungsi dari awal hingga akhir tanpa mock data. Klaim siap produksi hanya boleh dibuat setelah deployment, backup, keamanan, migrasi, observabilitas, dan pengujian operasional diverifikasi.

## 24. Hasil yang harus diserahkan

- Source code nyata.
- Migrasi/model database.
- Backend API dan frontend.
- Auth dan authorization.
- Integrasi AI dan wizard provider.
- Test suite.
- Dokumentasi setup lokal.
- Contoh environment variables tanpa secret.
- Panduan migrasi dan deployment.
- Panduan backup/restore.
- Panduan konfigurasi AI.
- Daftar file yang dibuat/diubah.
- Daftar fitur selesai dan belum selesai.
- Hasil tes aktual.
- Risiko tersisa.

## 25. Instruksi eksekusi untuk agent

**Mulai sekarang dengan Tahap 0 — Audit repositori.**

1. Periksa apakah repository dan source code benar-benar tersedia serta branch mana yang aktif.
2. Laporkan stack, struktur, fitur existing, dan masalah akses.
3. Buat branch kerja terpisah sebelum mengubah kode.
4. Susun daftar tugas berdasarkan dependensi.
5. Implementasikan tahap demi tahap secara langsung di source code.
6. Jalankan tes setelah setiap tahap dan perbaiki error yang ditemukan.
7. Periksa regresi, keamanan, dan konsistensi database.
8. Perbarui dokumentasi dan laporkan progres yang faktual.
9. Jangan membuat commit atau pull request kecuali benar-benar dilakukan dan diizinkan oleh lingkungan kerja.
10. Jangan mengklaim pekerjaan selesai sebelum kriteria Definition of Done terpenuhi.

Jika akses repositori tidak tersedia, berhenti sebelum melakukan perubahan yang berisiko dan jelaskan tindakan yang dibutuhkan untuk melanjutkan. Jangan mengarang hasil inspeksi.

**Target akhir:** DompetKeluarga AI menjadi aplikasi keuangan pribadi dan keluarga yang benar-benar berfungsi, aman, teruji, mudah dikonfigurasi, dan dapat dikembangkan lebih lanjut tanpa membangun ulang dari nol.