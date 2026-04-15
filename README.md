# 🎬 ESP32 OLED Video Player (Pro Edition)

Sebuah *web-based tool* komprehensif untuk mengonversi video apapun menjadi animasi 1-bit (Monochrome) yang dapat dijalankan dengan mulus di layar OLED 128x64 (SSD1306 / SH1106) menggunakan mikrokontroler ESP32.

Project ini tidak hanya mengekstrak *frame*, tetapi juga dilengkapi dengan algoritma *Image Processing* tingkat lanjut yang biasa digunakan oleh *tools* profesional (seperti Image2cpp), memastikan video dan teks kamu tetap tajam, memiliki gradasi halus, dan tidak menjadi siluet hitam pekat.

## ✨ Fitur Utama (Pro Edition)
* 🧮 **Advanced Dithering Algorithms:** Mendukung **Bayer 8x8** (Super halus untuk video), **Atkinson** (Mencegah bayangan *nge-blok* hitam), dan **Floyd-Steinberg**.
* 📏 **Smart Scaling & Panning:** Pilihan skala mulai dari *Best Fit*, *Stretch*, *Fill / Cover* (penuhi layar tanpa merusak rasio), hingga *Custom* (atur W, H, X, Y secara manual).
* 🖋️ **Sub-Pixel Thickness (Morphology):** Fitur penipis/penebal teks dan garis secara halus menggunakan hitungan desimal, menyelamatkan detail kecil agar tidak hilang di layar OLED.
* 👁️ **NTSC Luminance Conversion:** Menggunakan rumus persepsi mata manusia untuk mendeteksi warna abu-abu/coklat dengan sangat akurat sebelum dijadikan hitam-putih.
* ⚡ **High-Performance ESP32 Code:** Kode hasil *generate* menggunakan metode `millis()` (Non-blocking) untuk FPS konstan dan fitur *I2C Overclock* (800 kHz) agar video berjalan tanpa *lag*.
* 💾 **Auto-Save Settings:** Semua pengaturan *slider* dan *dropdown* di web akan tersimpan otomatis secara lokal di *browser* kamu.

## 🛠️ Perangkat Keras yang Dibutuhkan
1. **ESP32** (NodeMCU/WROOM)
2. **Display OLED 128x64** (Chip SSD1306 atau SH110X, Komunikasi I2C)
3. Kabel Jumper

### Konfigurasi Pin (Wiring Standar)
| OLED Pin | ESP32 Pin |
| :---: | :---: |
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

## 📦 Kebutuhan Software (Library)
Pastikan kamu sudah menginstal library berikut di Arduino IDE (via Library Manager):
* `Adafruit GFX Library`
* `Adafruit SSD1306` (Jika menggunakan OLED SSD1306)
* `Adafruit SH110X` (Jika menggunakan OLED SH1106)

## 🚀 Cara Penggunaan

### 1. Ekstrak Video di Web Converter
1. Buka halaman Web Converter (Buka file `index.html` di browser atau kunjungi link GitHub Pages project ini).
2. Masukkan video yang ingin kamu tampilkan. *(Tips: Kamu bisa menekan tombol "Putar 90°" jika menggunakan video vertikal / Reels).*
3. Atur metode *Dithering*, *Skala*, dan *Ketebalan Garis* hingga *preview* di layar terlihat memuaskan.
4. Klik **Mulai Extract Frame-by-Frame** dan tunggu hingga selesai.

### 2. Upload ke ESP32
1. Klik **Copy Data Array**, lalu *paste* hasilnya ke sebuah file / tab baru di Arduino IDE dengan nama `VideoFrame.h`.
2. Klik **Copy Kode Main.ino**, lalu *paste* ke file utama *sketch* Arduino kamu.
3. Di dalam file `Main.ino`, pilih tipe OLED yang kamu gunakan dengan menghapus tanda komentar (`//`) pada bagian `#define PAKAI_SSD1306` atau `#define PAKAI_SH1106`.
4. **⚠️ PENTING:** Karena array video memakan memori Flash yang besar, masuk ke menu **Tools > Partition Scheme** di Arduino IDE dan ubah menjadi **"Huge APP (3MB No OTA/1MB SPIFFS)"**.
5. Klik **Upload** ke ESP32.

## 💡 Pro-Tips Pengaturan Gambar
* **Untuk Video Manusia / Pemandangan:** Gunakan metode **Bayer 8x8 Dithering**. Ini akan menghasilkan gradasi bintik yang stabil dan tidak bergetar saat video berjalan.
* **Untuk Animasi Teks / Kartun Kartun Simple:** Gunakan **Solid Threshold**. Jika teks terlihat terputus-putus, tambahkan *Ketebalan Garis* ke arah **Putih +** (Misal: 0.5 atau 1.0).
* **Untuk Mencegah Objek Gelap Menyatu (Siluet):** Gunakan metode **Atkinson Dithering** dikombinasikan dengan menaikkan *Brightness* sedikit.

## 👨‍💻 Kreator
Dikembangkan dan dioprek dengan 💻 oleh **Tri Wahyu**.
* 📸 Instagram: [@Triwahyu45](https://instagram.com/Triwahyu45)
* 🎥 YouTube: [Tri Wahyu](https://youtube.com/@Triwahyu45)

Jika *tool* ini bermanfaat buat *project* robotika, *skripsi*, atau sekadar iseng-iseng kamu, jangan lupa kasih ⭐ (Star) di repository ini ya!
