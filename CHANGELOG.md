# Catatan Rilis Exavera CBT Enterprise Edition (Release Notes & Changelog)

Seluruh pembaruan versi resmi aplikasi klien Computer-Based Testing (CBT) Exavera Enterprise Edition dicatat secara terperinci di sini.

---

## [v1.0.0-rc.2+2] — 15 November 2026

> **Status Rilis:** Stabil / Release Candidate 2 (Patch 2) — Enterprise Assessment Client  
> **Berkas Master Enterprise:** `Exavera-CBT-Enterprise-v1.0.0-rc.2-b2-Android-Universal-Release.apk`  
> **Berkas Alias Unduh Langsung:** `exavera-cbt.apk`  
> **Target Biner:** Android 8.0+ & Chromebook (ARCVM)  
> **SHA-256 Checksum:** `d60f9d2cb73ae20c3c0aa20ec636c4e4490c4f213639f60ac3a31468a4e727a4`  
> **Ukuran Berkas:** 80,105,448 byte (~76.4 MB)

---

### 📦 Taksonomi Berkas Rilis Enterprise (Canonical Artifacts)

| Klasifikasi | Nama Berkas Artefak | Deskripsi Penggunaan |
| :--- | :--- | :--- |
| **Tier 1 (Master Enterprise)** | `Exavera-CBT-Enterprise-v1.0.0-rc.2-b2-Android-Universal-Release.apk` | Biner rilis resmi berstandar Enterprise untuk arsip dinas & GitHub Releases |
| **Tier 2 (Public Enterprise)** | `Exavera-CBT-Enterprise-v1.0.0-rc.2-Android-Universal.apk` | Distribusi publik portal sekolah tanpa tag build number |
| **Tier 3 (MDM Provisioning)** | `Exavera-CBT-Enterprise-Client.apk` | Pemasangan massal via MDM, Google Workspace Admin (Chromebook) & ADB push |
| **Tier 4 (CDN Mirror)** | `exavera-cbt.apk` | Tautan unduh permanen otomatis (*In-App Update Engine*) |

---

### 🚀 Sorotan Pembaruan Terkini

#### 1. Perbaikan Kritis Resolusi Kunci Nuke TOTP (Factory Reset)
- **Resolusi Kunci Bertingkat Dinamis:** Memperbaiki validasi kode darurat Nuke (Factory Reset gawai) dengan membaca rahasia pengawas (`PROCTOR_TOTP_SECRET`) langsung dari Android Keystore terenkripsi secara asinkron.
- **Dukungan Multi-Candidate Secrets:** Sistem memvalidasi kunci dinamis sesi pengawas, kunci Keystore perangkat, serta identitas sekolah tanpa bergantung pada hardcode.
- **Validasi Input Fleksibel:** Mendukung pemindaian QR Code kamera, pengunggahan gambar kode QR dari galeri, dan dialog entri manual 6-digit PIN pengawas.

#### 2. Sistem Pemeriksaan Pembaruan Otomatis (In-App Update Checker)
- **Deteksi Versi Mandiri Sideloading:** Aplikasi secara otomatis memverifikasi manifest `version.json` saat diluncurkan tanpa ketergantungan pada Google Play Store.
- **Pembaruan Fleksibel (Soft vs Hard Update):**
  - **Pembaruan Opsional (*Soft Update*):** Dialog informatif dengan opsi *"Nanti Saja"* dan *"Perbarui Sekarang"*.
  - **Pembaruan Wajib (*Force Update*):** Proteksi antarmuka terkunci jika versi terpasang berada di bawah ambang batas kompatibilitas protokol ujian sekolah.
- **Fail-Safe Offline 3 Detik:** Pengecekan versi dibatasi timeout 3.0 detik secara senyap sehingga tidak memblokir siswa saat berada di jaringan intranet lokal/offline.
- **Pengecekan Manual:** Tombol interaktif *"Periksa Pembaruan"* ditambahkan pada lembar menu profil siswa dan pengawas.

#### 3. Dukungan Sesi Gladi Bersih & Instant Submit Unlock
- **Deteksi Kanonikal Paket Simulasi:** Mengenali otomatis kode mapel `MULTI`, tag judul `[GLADI BERSIH]`, ID `SIM-`, atau akun guru `GURU-`.
- **Bypass Gembok 90% Durasi:** Tombol submit langsung aktif hijau sejak menit awal pengerjaan untuk keperluan uji coba jaringan dan pengumpulan lembar jawaban tanpa menunggu 90% waktu.
- **Proteksi Ujian Resmi:** Ujian resmi (PAS/PAT/Asesmen) tetap 100% terkunci dengan aturan pengerjaan minimal 90%.

#### 4. Proteksi Anti-Curang Alarm Suara Jalur Keras (Hardware STREAM_ALARM)
- **Sirene Darurat Dwinaada (880 Hz / 1760 Hz):** Berbunyi otomatis saat siswa membuka menu Recent Apps atau berpindah aplikasi.
- **Kebal Mute & Tombol Volume:** Dialirkan melalui kanal hardware alarm sistem Android/Chromebook.
- **Anti-False Alarm (300 ms Debounce):** Penundaan cerdas 300 ms untuk membedakan perpindahan aplikasi nyata dengan pemunculan keyboard virtual.
- **Pemadaman Instan (< 10 ms):** Suara langsung padam begitu siswa kembali ke layar ujian.

#### 5. Orkestrasi Mandiri BLE Telemetri Real-Time & Live Radar Pengawas
- **Wire Protocol V2:** Paket siaran radio 20-byte terstandarisasi dengan 10 kode pelanggaran dan 5-state status pengerjaan.
- **Transmisi Radio Kontinu:** Tetap memancarkan denyut telemetri bahkan saat masa hitung mundur pelanggaran (*cooldown*).
- **Android Foreground Service:** Mencegah sistem operasi mematikan radio Bluetooth di latar belakang.

#### 6. Penyempurnaan Tipografi & Ergonomi UI
- **Tipografi Ragged-Right Presisi:** Mengeliminasi celah kata renggang (*typographic rivers*) dengan perataan rata kiri alami (*TextAlign.left*) dan *Golden Ratio Line-Height* 1.45.
- **Fixed Viewport Modal:** Wacana tabel dan teks panjang dapat di-zoom dan digeser dengan lancar di dalam batas viewport yang kokoh.
- **Micro-Chip Kognitif Sebaris:** Label indikator `[ TOPIK ] [ C2 • MEMAHAMI ]` terpadu rapi di atas kartu soal.
- **Anti-Glitch Render Engine:** Peredaman *blurRadius* aman untuk Impeller (Vulkan) dan Skia (OpenGL ES).

---

### 📦 Panduan Instalasi & Pembaruan

1. Unduh berkas resmi `Exavera-CBT-Enterprise-v1.0.0-rc.2-b2-Android-Universal-Release.apk` atau `exavera-cbt.apk`.
2. Pasang di perangkat Android (versi 8.0 ke atas) atau Chromebook yang mendukung aplikasi Android (ARCVM).
3. Jika muncul dialog *"Pasang dari sumber tidak dikenal"*, berikan izin untuk melanjutkan instalasi.
4. Buka aplikasi dan pastikan versi yang tertera pada pojok layar masuk adalah `v1.0.0-rc.2+2`.
