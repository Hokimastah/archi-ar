🏗️ Archi-AR

"Bring Your Blueprints to Life."
Platform Augmented Reality Berbasis Web untuk Visualisasi Arsitektur Imersif.

📑 Daftar Isi

Latar Belakang & Masalah

Solusi Kami

Fitur Utama

Analisis Teknis (Deep Dive)

Struktur Proyek

Panduan Instalasi & Demo

Tim Pengembang

🧐 Latar Belakang & Masalah

Dalam industri arsitektur dan properti, komunikasi visual adalah kunci. Namun, terdapat kesenjangan besar (gap) antara ide arsitek dan pemahaman klien:

Keterbatasan Visualisasi 2D: Klien sering kesulitan membayangkan skala dan ruang hanya dari denah kertas atau layar monitor.

Inefisiensi Maket Fisik: Pembuatan maket fisik memakan biaya mahal, waktu lama, rapuh, dan sulit dibawa ke lokasi pertemuan.

Hambatan Aplikasi (App Friction): Klien enggan mengunduh aplikasi khusus yang berukuran besar hanya untuk melihat satu desain.

Archi-AR hadir untuk menjawab tantangan ini.

💡 Solusi Kami

Archi-AR adalah aplikasi Web-based Augmented Reality (WebAR). Solusi ini memungkinkan arsitek membawa "maket digital" tak terbatas di dalam saku mereka.

Tanpa Instalasi: Berjalan langsung di browser (Chrome/Edge) pada smartphone Android.

Real-Scale Visualization: Klien dapat melihat bangunan dalam ukuran sebenarnya (1:1) di lahan kosong, atau ukuran maket di atas meja rapat.

Interaktif: Klien bisa "masuk" ke dalam bangunan, bukan hanya melihat dari luar.

🌟 Fitur Utama

Berdasarkan kode yang telah dikembangkan, berikut adalah fitur unggulan sistem:

1. 📂 Dynamic 3D Asset Library

Menggunakan sistem Drawer UI, pengguna dapat mengganti model 3D secara real-time tanpa me-reload halaman.

Benefit: Mempermudah A/B testing desain di depan klien (misal: membandingkan desain klasik vs modern).

2. 🚶 First Person View (FPV) Walkthrough

Fitur andalan (Killer Feature) yang jarang ada di WebAR standar.

Mengubah perspektif kamera menjadi orang pertama.

Dilengkapi Virtual Joystick (Nipple.js) untuk berjalan maju/mundur/samping.

Dilengkapi Elevation Control untuk simulasi naik ke lantai 2 atau melihat atap.

3. 🤏 Smart Gesture Control

Interaksi intuitif berbasis sentuhan layar (Touch Event API):

One-Finger Rotate: Memutar orientasi bangunan.

Two-Finger Pinch: Mengubah skala bangunan (Scaling) secara presisi.

4. 🎯 Surface Detection (Hit-Test)

Sistem secara otomatis memindai lingkungan, mendeteksi bidang datar (lantai/meja), dan menampilkan Reticle (penanda target) untuk memastikan objek tidak melayang di udara.

🔬 Analisis Teknis (Deep Dive)

Bagian ini menjelaskan logika kode di balik layar untuk sesi tanya jawab teknis.

A. Arsitektur Core (Three.js & WebXR)

Aplikasi ini dibangun di atas Three.js sebagai rendering engine dan WebXR Device API sebagai jembatan ke hardware kamera/sensor HP.

Scene Graph: Mengelola pencahayaan (Directional & Ambient Light) dan objek 3D.

GLTFLoader: Mengurai file .glb (format standar industri untuk 3D web) yang ringan namun detail.

B. Algoritma Interaksi Sentuh (Touch Logic)

Kami tidak menggunakan library gestur eksternal, melainkan menulis logika matematika vektor sendiri untuk performa maksimal:

Scaling (Pinch):

Menghitung jarak Euclidean (Hypot) antara dua titik sentuh jari (touches[0] dan touches[1]).

Jika jarak membesar > Scale Up. Jika mengecil > Scale Down.

Code Snippet Logic: scaleFactor = currentDistance / startDistance.

Rotation:

Mendeteksi pergeseran horizontal (deltaX) dari satu jari.

Mengonversi piksel layar ke radian putaran sumbu Y.

C. Logika FPV (Virtual Joystick)

Integrasi Nipple.js dengan Three.js:

Saat joystick digerakkan, ia menghasilkan vektor (x, y).

Sistem menghitung vektor "Forward" dan "Right" dari kamera saat ini.

Posisi objek 3D digeser berlawanan arah dengan input joystick, menciptakan ilusi bahwa "kamera/pengguna" yang berjalan, padahal dunia 3D-nya yang bergeser di sekitar pengguna (teknik World Movement untuk stabilitas AR).

D. Manajemen Memori

Menggunakan dispose() saat mereset scene untuk mencegah memory leak di browser HP yang memorinya terbatas.

📂 Struktur Proyek

Archi-AR/
├── index.html          # Single-File Application (HTML + CSS + JS Logic)
├── 3d_assets/          # Folder penyimpanan model
│   ├── tower_house.glb
│   └── astronaut.glb
└── README.md           # Dokumentasi ini


📱 Panduan Instalasi & Demo

Untuk presentasi, ikuti langkah deployment lokal ini:

Persiapan Aset:
Pastikan file .glb sudah ada di folder 3d_assets/.

Local Server (Wajib HTTPS):
WebXR memerlukan konteks aman (HTTPS).

Buka VS Code.

Jalankan Live Server pada index.html.

Tunneling (Agar bisa dibuka di HP):
Gunakan ngrok untuk membuat link publik:

ngrok http 5500


Akses:
Buka URL https://....ngrok-free.app di Chrome Android.

👥 Tim Pengembang

"Admin Grup Bumi Datar"

Peran

Tanggung Jawab

Project Manager

Konsep, Presentasi, Manajemen Aset

Core Developer

Logika Three.js, WebXR, & Integrasi FPV

UI/UX Designer

Desain Interface Glassmorphism & User Flow

"Architecture is a visual art, and the buildings speak for themselves. We just give them a voice through AR."