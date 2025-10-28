# Project-UTS-Muhamad-Putra-Al-ikhsan
# README

## Penjelasan Program Segmentasi Citra Digital

Program ini dibuat untuk mempelajari konsep **segmentasi citra digital** menggunakan berbagai metode seperti thresholding global (Otsu), thresholding adaptif, deteksi tepi (Canny), dan segmentasi watershed. Tujuan dari program ini adalah untuk memisahkan objek pada citra dari latar belakangnya menggunakan teknik-teknik pengolahan citra berbasis piksel.

### 1. Import Library

Program ini menggunakan beberapa library utama yaitu:

* `skimage.data` untuk mengambil citra contoh bawaan dari pustaka scikit-image.
* `cv2` (OpenCV) untuk melakukan berbagai operasi pengolahan citra seperti thresholding, deteksi tepi, dan segmentasi watershed.
* `numpy` untuk operasi numerik dan manipulasi array citra.
* `matplotlib.pyplot` untuk menampilkan hasil citra pada setiap tahap pemrosesan.

### 2. Membaca dan Menampilkan Gambar

Citra yang digunakan adalah citra koin dari `skimage.data.coins()`.
Citra tersebut dikonversi menjadi format BGR agar kompatibel dengan fungsi OpenCV. Selain itu, citra grayscale juga disiapkan karena sebagian besar metode segmentasi bekerja pada citra hitam putih.
Hasil ditampilkan menggunakan dua subplot: citra asli dan versi grayscale.

### 3. Global Thresholding (Otsu Method)

Metode **Otsu** digunakan untuk menentukan nilai ambang (threshold) optimal secara otomatis dengan cara meminimalkan variansi antar kelas piksel.
Teknik ini membagi citra menjadi dua bagian: objek (foreground) dan latar belakang (background).
Citra hasil threshold ditampilkan dalam bentuk biner, di mana piksel objek berwarna putih dan latar belakang berwarna hitam.

### 4. Adaptive Thresholding

Berbeda dari Otsu yang menggunakan satu nilai ambang global, **adaptive thresholding** menghitung ambang secara lokal pada setiap area kecil citra.
Program menggunakan metode **Gaussian Adaptive**, yang cocok untuk citra dengan pencahayaan tidak merata.
Hasilnya adalah citra biner dengan segmentasi yang lebih halus dan responsif terhadap perubahan intensitas lokal.

### 5. Edge-based Segmentation (Canny Edge Detection)

Tahap ini menggunakan algoritma **Canny** untuk mendeteksi tepi objek berdasarkan perubahan intensitas piksel.
Canny bekerja melalui beberapa langkah, termasuk perataan citra (smoothing), perhitungan gradien, dan penentuan batas tepi dengan ambang bawah dan atas.
Hasilnya menampilkan kontur objek utama pada citra dengan jelas.

### 6. Watershed Segmentation

Metode **Watershed** digunakan untuk segmentasi yang lebih kompleks dengan memandang citra sebagai permukaan topografi. Titik minimum lokal dianggap sebagai lembah (catchment basins), dan batas antar objek terbentuk menyerupai garis air yang memisahkan lembah tersebut.

Tahapan dalam implementasi watershed pada program ini meliputi:
a. **Threshold biner:** Membalik citra agar objek menjadi latar belakang.
b. **Noise removal:** Menghapus noise menggunakan operasi morfologi (opening).
c. **Penentuan area background dan foreground:** Menggunakan dilasi dan transformasi jarak (distance transform).
d. **Menentukan area tidak diketahui:** Dengan mengurangkan area background dan foreground.
e. **Labeling marker:** Memberi label pada setiap area objek menggunakan `connectedComponents`.
f. **Penerapan algoritma watershed:** OpenCV mengubah batas antar objek menjadi piksel dengan nilai -1, yang kemudian ditandai dengan warna merah pada citra hasil.

### 7. Visualisasi Hasil

Program menampilkan hasil setiap tahap pemrosesan citra menggunakan beberapa jendela figure:

* Citra asli dan grayscale.
* Hasil Otsu Thresholding.
* Hasil Adaptive Thresholding.
* Hasil Canny Edge Detection.
* Hasil akhir segmentasi Watershed beserta batas objek yang ditandai merah.

### 8. Kesimpulan

Program ini menunjukkan bahwa segmentasi citra digital dapat dilakukan dengan berbagai pendekatan tergantung pada karakteristik citra.
Metode thresholding cocok untuk citra dengan kontras tinggi antara objek dan latar belakang, sedangkan metode watershed lebih efektif untuk citra dengan objek yang saling berdekatan.
Dengan memahami setiap metode ini, kita dapat memilih teknik segmentasi yang paling sesuai untuk aplikasi pengolahan citra tertentu.
