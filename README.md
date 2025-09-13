Kebijakan Visibilitas & Akses Repositori — GitHub Organization

1) Tujuan

Memastikan repositori hanya terlihat oleh pengguna yang memiliki akses langsung, menerapkan prinsip least-privilege, serta menjaga auditabilitas dan keamanan kode.

2) Cakupan

Berlaku untuk seluruh repositori, tim, anggota organisasi, dan kolaborator eksternal (outside collaborators) di Organization GitHub ini.

3) Prinsip Umum
	•	Least privilege: akses diberikan seminimal mungkin, sesuai kebutuhan tugas.
	•	Need-to-know: repo tidak tampak/terlihat jika tidak ada akses eksplisit.
	•	By-team, not by-person (jika memungkinkan): kelola akses via Teams agar mudah diaudit.
	•	Time-bounded: akses sementara harus ada tanggal kadaluarsa dan direview berkala.
	•	Auditable: setiap pemberian akses jejaknya harus terdokumentasi.

⸻

4) Standar Konfigurasi di Level Organisasi (Org-Level)

4.1. Base permissions
	•	Set Base permissions = None (Members tidak dapat melihat repo apa pun tanpa undangan).

4.2. Default repository visibility
	•	Set Default repository visibility = Private.

4.3. Kontrol pembuatan & perubahan repo
	•	Nonaktifkan izin anggota untuk mengubah repository visibility.
	•	Batasi siapa yang boleh membuat repo baru (hanya Owner/Platform Team).

4.4. Forking
	•	Nonaktifkan forking untuk repositori private/internal di level organisasi.

4.5. Keamanan akun
	•	Wajibkan 2FA/SSO untuk semua anggota Org (jika tersedia).
	•	Aktifkan Audit Log & notifikasi keamanan org.

Catatan: Setting ini memastikan tidak ada “akses default”, sehingga daftar repo setiap anggota hanya berisi repo yang mereka miliki akses langsung.

⸻

5) Standar Konfigurasi di Level Repositori (Repo-Level)

5.1. Visibility
	•	Semua repo berstatus Private.
	•	Dilarang menggunakan Internal kecuali ada persetujuan keamanan (karena Internal terlihat oleh seluruh member Org).

5.2. Pemberian akses
	•	Tambahkan akses hanya via Teams (disarankan) atau Add people untuk pengecualian.
	•	Role minimal: Read jika hanya butuh cloning; Write untuk kontributor; Maintain/Admin terbatas pada maintainer inti.

5.3. Outside collaborators
	•	Diperbolehkan hanya by-exception dengan justifikasi & tanggal berakhir akses.
	•	Scope akses hanya ke repo yang diperlukan.

5.4. Branch & proteksi
	•	Wajib Branch protection untuk main/release (review wajib, status checks, no force-push).
	•	Aktifkan secret scanning, Dependabot alerts, & security updates.

5.5. Forking (per repo)
	•	Pastikan Allow forking dimatikan pada Settings repo private.

⸻

6) Proses Permintaan & Persetujuan Akses

6.1. Kanal permintaan
	•	Semua permintaan akses dilakukan via Issue Template “Access Request” di repo org-governance (atau sistem tiket internal).

6.2. Informasi wajib
	•	Nama pengguna GitHub / email
	•	Repo yang diminta
	•	Role (Read/Write/Maintain/Admin)
	•	Alasan bisnis (justifikasi)
	•	Durasi/expiry (tanggal review)

6.3. Persetujuan
	•	Minimal 2 pihak: Repo Admin/Maintainer + Owner/Platform/Security.
	•	Akses diberikan setelah persetujuan terdokumentasi.

6.4. Implementasi
	•	Tambahkan user ke Team yang relevan atau Add people pada repo tersebut.

⸻

7) Onboarding & Offboarding

7.1. Onboarding
	•	Tambahkan anggota ke Team fungsi (mis. frontend-dev, backend-api) — jangan beri akses org-wide.
	•	Team tersebut punya akses hanya ke repo yang dibutuhkan.

7.2. Offboarding
	•	Hapus dari semua Teams & outside collaborations pada hari terakhir kerja.
	•	Transfer kepemilikan repo pribadi terkait pekerjaan (bila ada) ke Org/Team.

⸻

8) Review & Audit Berkala

8.1. Frekuensi
	•	Bulanan: review outside collaborators & Admin access.
	•	Kuartalan (Jan/Apr/Jul/Okt): audit keseluruhan akses repo & kepatuhan kebijakan.

8.2. Cakupan audit
	•	Daftar repo yang bukan private.
	•	Repo dengan Allow forking aktif (harus off untuk private).
	•	Member dengan role Admin di repo (minimalkan).
	•	Akses tanpa tim (individual) yang tidak lagi relevan.
	•	Akses yang melewati tanggal kadaluarsa.

8.3. Tindakan
	•	Cabut akses kedaluwarsa.
	•	Normalkan akses individual menjadi by-Team jika memungkinkan.

⸻

9) Pengecualian
	•	Semua pengecualian (mis. repo Internal, akses darurat, demo publik) harus:
	•	Memiliki justifikasi,
	•	Disetujui Owner/Security,
	•	Memiliki tanggal review,
	•	Didokumentasikan di org-governance.

⸻

10) Penanganan Pelanggaran
	•	Pelanggaran ringan: peringatan & koreksi akses dalam 1×24 jam.
	•	Pelanggaran berat/berulang: pencabutan akses hingga investigasi selesai; laporan insiden dicatat.

⸻

11) Lampiran A — Pemetaan Menu (Ringkas)
	•	Base permissions: Org → Settings → Member privileges → Base permissions: None.
	•	Default repo visibility: Org → Settings → Repository defaults → Private.
	•	Disable forking: Org → Settings → Member privileges/Repository forking → Off (dan per-repo: Settings → uncheck “Allow forking”).
	•	Restrict change visibility: Org → Settings → Member privileges → nonaktifkan “Allow members to change repository visibilities”.
	•	2FA/SSO enforcement: Org → Settings → Security → enforce 2FA/SSO.
	•	Repo collaborators/teams: Repo → Settings → Collaborators & teams.
	•	Branch protection: Repo → Settings → Branches → Add rule.
	•	Security features: Repo → Settings → Code security & analysis → aktifkan yang relevan.

⸻

12) Lampiran B — Checklist Cepat

Org (sekali set awal)
	•	Base permissions = None
	•	Default repo visibility = Private
	•	Nonaktifkan change visibility oleh member
	•	Nonaktifkan forking private/internal
	•	Enforce 2FA/SSO

Repo baru (setiap kali)
	•	Visibility = Private
	•	Access via Team (bukan perorangan) bila memungkinkan
	•	“Allow forking” = Off
	•	Branch protection untuk main
	•	Secret scanning, Dependabot alerts aktif

Audit bulanan/kuartalan
	•	Review outside collaborators
	•	Review Admin access
	•	Cabut akses kedaluwarsa
	•	Pastikan semua repo yang sensitif tetap Private
