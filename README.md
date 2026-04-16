# 🚗 Ekstraksi Fitur Bentuk Kendaraan — Computer Vision

> Tugas Mata Kuliah **Visi Komputer** | Teknik Informatika  
> Topik: **Feature Extraction** menggunakan Shape Features pada Objek Kendaraan

---

## 📋 Deskripsi

Notebook ini mengimplementasikan **ekstraksi fitur bentuk (shape feature extraction)** pada gambar kendaraan di jalan tol. Terdapat dua pendekatan yang digunakan:

1. **Deep Learning (YOLOv8-seg)** — segmentasi instance berbasis model neural network untuk mendeteksi dan mengsegmentasi kendaraan secara akurat.
2. **Computer Vision Klasik (Canny + Kontur OpenCV)** — deteksi tepi dan analisis kontur untuk mengekstrak fitur geometri seperti area, perimeter, aspect ratio, dan circularity.

---

## ✨ Fitur Utama

| Fitur | Deskripsi |
|---|---|
| Deteksi Kendaraan | YOLOv8n-seg mendeteksi objek kendaraan dengan confidence threshold |
| Segmentasi Mask | Instance segmentation per kendaraan dengan warna berbeda |
| Canny Edge Detection | Deteksi tepi menggunakan Gaussian Blur + Canny |
| Bounding Box | Visualisasi kotak pembatas per objek terdeteksi |
| Kontur + Fill | Overlay kontur semi-transparan dan solid fill |
| Shape Features | Ekstraksi area, perimeter, aspect ratio, dan circularity |

---

## 🗂️ Struktur Notebook

```
notebook.ipynb
│
├── Cell 1 — Instalasi & Import Library
├── Cell 2 — Load Gambar
├── Cell 3 — Deteksi dengan YOLOv8
├── Cell 4 — Pemrosesan Visual (Canny, BBox, Mask, Kontur)
├── Cell 5 — Visualisasi 6-Panel (YOLOv8 Pipeline)
└── Cell 6 — Ekstraksi Fitur Bentuk Klasik + Visualisasi 3-Panel
```

---

## 🔬 Penjelasan Tahapan

### Pipeline 1 — YOLOv8 Segmentation (Visualisasi 6-Panel)

| Panel | Keterangan |
|---|---|
| 1. Gambar Asli | Input gambar kendaraan di jalan tol |
| 2. Canny Edge | Hasil deteksi tepi dengan threshold 50–150 |
| 3. Segmentasi + Fitur Bentuk | Overlay kontur Canny di atas gambar asli |
| 4. Bounding Box | Kotak pembatas per objek dari YOLOv8 |
| 5. Kontur + Fill | Mask segmentasi semi-transparan (alpha blending) |
| 6. Full Fill | Mask segmentasi solid tanpa transparansi |

### Pipeline 2 — Classical CV Shape Features (Visualisasi 3-Panel)

| Panel | Keterangan |
|---|---|
| 1. Gambar Asli | Input gambar original |
| 2. Canny Edge | Hasil Canny setelah dilasi kernel 3×3 |
| 3. Segmentasi + Fitur Bentuk | Bounding box + label area & aspect ratio per kontur kendaraan |

**Kriteria filter kontur kendaraan:**
- Area > 8.000 piksel²
- Aspect Ratio: `1.2 < w/h < 4.5` (proporsional kendaraan)

**Fitur yang diekstrak:**
- **Area** — luas region kontur (piksel²)
- **Perimeter** — keliling kontur
- **Aspect Ratio** — rasio lebar terhadap tinggi (`w / h`)
- **Circularity** — seberapa bulat suatu bentuk (`4π × Area / Perimeter²`)

---

## ⚙️ Cara Menjalankan

### 1. Buka di Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

### 2. Upload Gambar

Pastikan file gambar tersedia di path:
```
/content/kendaraan di jalan tol.jpg
```

Upload melalui panel file di Colab atau gunakan:
```python
from google.colab import files
files.upload()
```

### 3. Jalankan Semua Cell

Klik **Runtime → Run all** atau jalankan setiap cell secara berurutan.

---

## 📦 Dependencies

| Library | Fungsi |
|---|---|
| `ultralytics` | YOLOv8 untuk deteksi & segmentasi |
| `opencv-python` | Pemrosesan gambar (Canny, kontur, bounding box) |
| `numpy` | Operasi array dan masking |
| `matplotlib` | Visualisasi hasil |

Instalasi otomatis via:
```bash
pip install ultralytics -q
```

> Library lainnya (`cv2`, `numpy`, `matplotlib`) sudah tersedia secara default di Google Colab.

---

## 📊 Output yang Dihasilkan

- **6-panel figure** dari pipeline YOLOv8: gambar asli → edge → segmentasi → bounding box → kontur fill → solid fill
- **3-panel figure** dari pipeline klasik: gambar asli → canny edge → bounding box dengan label fitur bentuk
- Teks output jumlah dan label kelas kendaraan yang terdeteksi beserta confidence score

---

## 🧠 Konsep yang Dipelajari

- **Instance Segmentation** — membedakan setiap objek secara individual
- **Edge Detection** — menemukan batas/tepi objek menggunakan Canny
- **Shape Features** — representasi numerik bentuk suatu objek
- **Contour Analysis** — analisis geometri kontur untuk klasifikasi bentuk
- **Alpha Blending** — teknik overlay transparan untuk visualisasi mask

---

## 👤 Informasi

> Dibuat sebagai bagian dari tugas praktikum mata kuliah **Visi Komputer**, Program Studi Informatika.
