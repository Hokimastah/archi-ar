# 🏗️ Archi-AR  
### *Bring Your Blueprints to Life.*  
Web-based Augmented Reality untuk Visualisasi Arsitektur Imersif.

---

## 📑 Daftar Isi
- [Latar Belakang](#-latar-belakang)
- [Solusi Kami](#-solusi-kami)
- [Fitur Utama](#-fitur-utama)
- [Analisis Teknis](#-analisis-teknis)
- [Struktur Proyek](#-struktur-proyek)

---

## 🧐 Latar Belakang

Dalam industri arsitektur dan properti, komunikasi visual adalah hal yang krusial. Namun sering terjadi gap antara ide arsitek dan pemahaman klien:

- **Keterbatasan Visualisasi 2D** – Klien sulit membayangkan ruang dari gambar statis.
- **Inefisiensi Maket Fisik** – Biaya tinggi, waktu lama, dan sulit dibawa.
- **App Friction** – Klien enggan menginstal aplikasi AR khusus yang berat.

**Archi-AR** hadir untuk mengatasi semua masalah tersebut.

---

## 💡 Solusi Kami

Archi-AR adalah platform **WebAR** yang berjalan langsung di browser Android **tanpa instalasi**.

- **Real-Scale Visualization** (skala 1:1) di lingkungan nyata.
- Mode **tabletop** (maket digital) di atas meja.
- **Interaktif & Imersif** — pengguna dapat masuk ke dalam bangunan.

---

## 🌟 Fitur Utama

### 1️⃣ Dynamic 3D Asset Library  
Pengguna dapat mengganti model 3D secara real-time melalui UI drawer, tanpa reload halaman.  
✔ Cocok untuk A/B testing desain (klasik vs modern).

### 2️⃣ First Person View (FPV) Walkthrough  
Fitur unggulan yang jarang ada di WebAR:  
- Mode kamera orang pertama  
- Virtual joystick (Nipple.js)  
- Kontrol elevasi untuk mensimulasikan naik lantai atau melihat atap

### 3️⃣ Smart Gesture Control  
Gestur sentuh berbasis Touch Event API:  
- **One-finger rotate**  
- **Two-finger pinch-to-scale**  
- Tanpa library eksternal → performa lebih stabil

### 4️⃣ Surface Detection (WebXR Hit-Test)  
Sistem mendeteksi bidang datar dan menampilkan **reticle** agar objek tidak melayang.

---

## 🔬 Analisis Teknis

### **A. Core Architecture (Three.js + WebXR)**
- Rendering oleh **Three.js**  
- AR session oleh **WebXR Device API**  
- Model format **.glb** melalui GLTFLoader  
- Lighting: Ambient + Directional Light  
- Struktur Scene Graph yang dioptimalkan untuk mobile

### **B. Touch Interaction Logic**
Ditulis manual tanpa library gestur untuk kontrol penuh.

**Pinch Scaling**  
Menghitung jarak Euclidean antara dua titik sentuh:  


**Rotation**  
Pergerakan horizontal jari → rotasi mesh pada sumbu Y.

### **C. FPV Movement (Virtual Joystick)**
Joystick menghasilkan vektor `(x, y)`. Sistem kemudian:

1. Menghitung arah **Forward** dan **Right** dari kamera.  
2. Menggerakkan seluruh dunia 3D ke arah sebaliknya.  

→ Menimbulkan ilusi bahwa pengguna yang bergerak, bukan objeknya.  
→ Teknik **World Movement** sangat stabil untuk WebAR.

### **D. Memory Management**
- Semua object, texture, dan material dihapus menggunakan `dispose()`  
- Mengurangi risiko crash pada perangkat Android dengan memori terbatas

---