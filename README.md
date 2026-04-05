# 🔬 EduKit AR — Media Pembelajaran Interaktif Berbasis Augmented Reality

![Unity](https://img.shields.io/badge/Unity-2022.3-black?logo=unity)
![Vuforia](https://img.shields.io/badge/Vuforia-Engine-blue)
![Python](https://img.shields.io/badge/Python-Flask-green?logo=python)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen?logo=mongodb)
![Platform](https://img.shields.io/badge/Platform-Android-orange?logo=android)

> **EduKit AR** adalah aplikasi pembelajaran interaktif berbasis Augmented Reality yang dirancang untuk membantu pengguna memahami komponen elektronika secara visual dan menarik — didukung oleh data real-time dari MongoDB Atlas.

---

## 📱 Tentang Aplikasi

EduKit AR memungkinkan pengguna untuk **menscan objek elektronik fisik** — seperti **Arduino Uno** dan **Sensor Ultrasonik HC-SR04** — menggunakan kamera smartphone. Setelah terdeteksi, aplikasi menampilkan label 3D interaktif dengan panah yang mengarah langsung ke setiap komponen, dan menampilkan deskripsi real-time yang diambil dari database cloud.

Seluruh deskripsi dapat diperbarui secara **langsung** melalui dashboard berbasis web yang dibangun dengan Python Flask, tanpa perlu melakukan rebuild aplikasi.

---

## ✨ Fitur Utama

- 🎯 **AR Model Target Tracking** — Scan objek Arduino & Sensor Ultrasonik secara langsung menggunakan Vuforia Engine
- 🏷️ **Label Komponen Interaktif** — Panah yang mengarah langsung ke setiap pin/komponen
- 📖 **Deskripsi Real-time** — Tap label untuk melihat detail komponen yang diambil langsung dari MongoDB Atlas
- 🌐 **Web Dashboard** — Perbarui deskripsi komponen kapan saja melalui antarmuka web berbasis Python Flask
- 🔄 **Multi-object Support** — Beralih antara Arduino dan Sensor Ultrasonik menggunakan dropdown selector
- ☁️ **Cloud Database** — MongoDB Atlas memastikan data selalu terkini di semua perangkat

---

## 🛠️ Teknologi yang Digunakan

| Layer | Teknologi |
|---|---|
| AR Engine | Unity 2022.3 + Vuforia Engine |
| Aplikasi Mobile | C# (Unity) |
| Backend API | Python (Flask) |
| Database | MongoDB Atlas |
| AR Tracking | Vuforia Model Target |
| UI | Unity UI + TextMeshPro |

---

## 🏗️ Arsitektur Sistem
```
📱 Aplikasi Android (Unity + Vuforia)
        ↕ HTTP Request (C# UnityWebRequest)
🐍 Python Flask API
        ↕ MongoDB Driver (PyMongo)
☁️ MongoDB Atlas (Cloud Database)
        ↕
🌐 Web Dashboard (Python Flask + HTML)
```

---

## 📂 Struktur Project
```
EduKitAR/
├── 📁 Unity Project (utstim1_2)
│   ├── Assets/
│   │   ├── Scripts/
│   │   │   ├── APIManager.cs           # Mengambil data dari Flask API
│   │   │   ├── DescriptionManager.cs   # Menampilkan/menyembunyikan panel deskripsi
│   │   │   ├── LabelClick.cs           # Menangani event tap pada label
│   │   │   ├── ARSelector.cs           # Beralih antar AR target
│   │   │   ├── LineConnector.cs        # Menggambar garis ke komponen
│   │   │   └── ButtonScale.cs          # Animasi tombol saat ditekan
│   │   └── Resources/
│   │       ├── VuforiaModels/
│   │       │   ├── Arduino/            # Database Model Target Arduino
│   │       │   └── Ultrasonic/         # Database Model Target HC-SR04
│
├── 📁 Backend (Python Flask)
│   ├── app.py                          # Aplikasi Flask utama
│   ├── .env                            # MongoDB URI (tidak di-commit)
│   ├── requirements.txt
│   └── templates/
│       ├── index.html
│       ├── arduino.html
│       └── ultrasonic.html
```

---

## 🚀 Cara Menjalankan

### Prasyarat
- Unity 2022.3 LTS
- Vuforia Engine SDK
- Python 3.x
- Akun MongoDB Atlas
- Perangkat Android dengan kamera

### Setup Backend
```bash
# Clone repository
git clone https://github.com/yourusername/edukit-ar.git
cd edukit-ar/backend

# Install dependensi
pip install -r requirements.txt

# Buat file .env
echo "MONGO_URI=uri_mongodb_atlas_kamu" > .env

# Jalankan server Flask
python app.py
```

### Setup Unity

1. Buka project di **Unity 2022.3**
2. Import package **Vuforia Engine**
3. Import database **Model Target** Arduino & Ultrasonik
4. Perbarui URL API di **APIManager.cs**:
```csharp
string url = "http://IP_SERVER_KAMU:5000/api/get-detail/" + jenis + "/" + komponen;
```
5. Build & Run ke perangkat Android

---

## 🗄️ Struktur Database

### Collection: `arduino`
```json
{
  "komponen": "Pin Digital",
  "deskripsi": "Pin 0-13 berfungsi sebagai input/output digital",
  "key": "digital"
}
```

### Collection: `ultrasonic`
```json
{
  "komponen": "Pin Trigger",
  "deskripsi": "Mengirim sinyal ultrasonik selama 10 mikro detik",
  "key": "trigger"
}
```

---

## 🌐 Endpoint API

| Method | Endpoint | Keterangan |
|---|---|---|
| GET | `/api/get-detail/<jenis>/<key>` | Ambil deskripsi komponen |
| GET | `/api/get-data/<jenis>` | Ambil semua komponen berdasarkan jenis |
| POST | `/api/submit-deskripsi` | Perbarui deskripsi komponen |
| GET | `/api/history` | Lihat riwayat perubahan |

---

## 📸 Cara Penggunaan

1. **Buka aplikasi** → Pilih jenis komponen (Arduino / Ultrasonik) dari dropdown
2. **Arahkan kamera** ke objek fisik → Vuforia mendeteksi dan melacak objek
3. **Label AR muncul** dengan panah yang mengarah ke setiap komponen
4. **Tap label manapun** → Aplikasi mengambil deskripsi real-time dari MongoDB Atlas melalui Flask API
5. **Panel deskripsi** menampilkan nama dan penjelasan komponen
6. **Perbarui kapan saja** melalui web dashboard tanpa perlu rebuild aplikasi

---

## 👨‍💻 Pembuat

Dibuat dengan ❤️ untuk keperluan edukasi.

> *"Menjadikan pembelajaran elektronika lebih interaktif, visual, dan menyenangkan melalui Augmented Reality."*

---

## 📄 Lisensi

Project ini dilisensikan di bawah MIT License.
