# 📋 Catatan Fase Pengembangan Web Quiz Game (Hacker Edition)

Proyek ini telah diperbarui dari versi dasar (basic template) menjadi game kuis bertema **Cyberpunk / Hacker Terminal** modern yang lengkap, imersif, dan kaya fitur edukatif.

---

## 📌 Ringkasan Fase Pengerjaan

### 🔹 Fase 1: Analisis Kebutuhan & Perbaikan Bug Kritis
- **Masalah Teridentifikasi:**
  1. *Hardcoded Index Bug*: Seluruh soal pada versi awal memiliki `answer: 0` dan opsi tidak pernah diacak, sehingga opsi pertama selalu benar.
  2. *Kurangnya Variasi Soal*: Hanya 10 soal statis.
  3. *UI Alert Bawaan*: Penggunaan `alert()` untuk instruksi dan game over merusak estetika antarmuka hacker.
  4. *Tanpa Feedback Visual*: Jawaban langsung berpindah tanpa menunjukkan opsi mana yang benar/salah.
  5. *Tidak Ada Audio*: Tidak ada efek suara futuristik.
- **Tindakan Fase 1:**
  - Mengganti logika pemilihan dan pengacakan dengan algoritma **Fisher-Yates Shuffle**.
  - Merancang arsitektur standalone file tanpa dependensi berat agar tetap portabel dan cepat dibuka di browser manapun.

---

### 🔹 Fase 2: Peningkatan Data & Mekanik Kuis
- **Bank Soal Diperluas:** 42 soal komprehensif mencakup:
  - *HTML & CSS* (Semantic elements, Box Model, Flexbox/Grid, Animasi, Selector)
  - *JavaScript Core* (Event Loop, Promises, DOM, Tipe Data, Scope, BigInt, Object.freeze)
  - *Web Security & Protokol* (HTTPS, CORS, XSS, CSRF, LocalStorage vs Cookies, HSTS, JWT, DDoS, MIME-sniffing)
- **Mode Permainan:**
  - **Standard Hack:** 10 Soal acak dengan waktu 20 detik per soal.
  - **Speedrun Blitz:** 15 Detik per soal untuk uji ketangkasan cepat.
  - **Survival Mode:** 3 Nyawa (Lives), game over jika nyawa habis, berjalan tanpa batas melintasi node server.
- **Filter Kategori:** Semua (Mixed), HTML & CSS, JavaScript, Web Security.
- **Penilaian Modern & Streak Combo:**
  - Skor dasar + bonus sisa waktu + multiplier combo (x1.2, x1.5, x2.0).
  - Tampilan visual combo glow api terminal.

---

### 🔹 Fase 3: Sistem Audio Cyberpunk (Web Audio API Synthesizer)
- Implementasi engine suara sintesis murni menggunakan Web Audio API browser (100% offline, tanpa file .mp3 eksternal):
  - *Click / Select*: Beep laser sci-fi
  - *Correct Answer*: Arpeggio akor harmonik futuristik
  - *Wrong Answer / Glitch*: Low frequency buzzer error
  - *Timer Warning Pulse*: Detak sonar frekuensi tinggi
  - *Mission Victory / Defeat*: Audio fanfare & power-down
  - Tombol toggle Mute/Unmute audio (Hotkeys: `M`).

---

### 🔹 Fase 4: Desain Visual Futuristik & UI/UX Imersif
- **Matrix Digital Rain Canvas:** Kanvas hujan kode Matrix yang dinamis dengan karakter kepala yang bersinar terang (*glowing lead characters*).
- **Efek CRT Scanlines:** Overlay retro terminal monitor dengan tombol toggle (Hotkeys: `V`).
- **Cyberpunk Terminal HUD:**
  - Border neon, aksen sudut sci-fi, dan tipografi `Orbitron` & `Roboto Mono`.
  - Timer bar dinamis dengan transisi warna (Hijau -> Kuning -> Merah berdenyut).
  - Feedback visual seketika: Opsi terpilih menyala Hijau jika benar, Merah jika salah, serta menyorot jawaban yang benar disertai ringkasan penjelasan edukatif.
- **Modal Dialog Terminal Kustom:**
  - Briefing Misi (menggantikan `alert()`).
  - Hall of Fame (Papan Skor Lokal tersimpan di `localStorage`).
- **Mission Debriefing (Layar Hasil):**
  - Rincian Akurasi (%), Waktu Tempuh, Rekor Streak, dan Gelar Hacker (*Script Kiddie*, *Cyber Phantom*, *The One / Neo*).
  - Fitur **"Review Answers"** untuk melihat kembali catatan soal dan penjelasan jawaban.
  - Navigasi Keyboard: Tombol `[A]`, `[B]`, `[C]`, `[D]` atau `[1]`, `[2]`, `[3]`, `[4]` untuk menjawab, `[Space]` untuk lanjut, `[Enter]` untuk mulai/ulang.

---

### 🔹 Fase 5: Audit Bug, Edge-Case Handling & Penyempurnaan (Bug Fix Phase)
- **Resolusi Konflik Hotkey C vs V:** Memperbaiki konflik tombol `C` (yang sebelumnya memicu CRT toggle saat pemain ingin memilih opsi jawaban C) dipindahkan ke tombol `V`, dan disinkronkan di seluruh teks petunjuk UI.
- **Perbaikan Mode Survival Node Counter:** Memperbaiki bug di mana penomoran node ter-reset ke `NODE: 01/∞` saat seluruh bank soal selesai di putaran pertama. Sekarang node counter terus meningkat secara konsisten (`NODE: 01/∞`, `NODE: 02/∞`, ..., `NODE: 35/∞`).
- **Dynamic Re-shuffling pada Survival Cycle:** Setiap siklus baru pada mode Survival mengacak ulang posisi opsi jawaban secara dinamis, sehingga pemain tidak bisa sekadar menghafal posisi huruf jawaban di putaran berikutnya.
- **Safe Text Node Rendering:** Mengganti injeksi `innerHTML` pada opsi soal, judul, dan intel penjelasan dengan `textContent` / `append` aman, mencegah tag HTML teknis (seperti `<article>`, `<link>`, `<div>`) terinterpretasi sebagai elemen browser dan menghilang dari layar.
- **Backdrop Click Modal Dismissal:** Pengguna sekarang dapat menutup modal briefing, leaderboard, atau review dengan mengklik area gelap di luar modal box secara intuitif.
- **Pintasan Keyboard Layar Utama:** Menambahkan dukungan tombol `Enter` pada Home Screen untuk langsung memulai hack sequence, dan pada Result Screen untuk mengulang ronde tanpa perlu menggunakan mouse.
- **Optimasi Performa Canvas Matrix:** Mencegah kebocoran context state dan CPU overload dengan mengisolasi efek `shadowBlur` hanya pada karakter kepala.
