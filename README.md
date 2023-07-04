
# PENJELASAN TEORI

Cropped Image: Menggunakan cropped image dapat membantu memfokuskan analisis hanya pada region of interest (ROI) yang mengandung plat kendaraan. Dengan menghapus bagian gambar yang tidak relevan, seperti latar belakang atau area lain di sekitar plat, kita dapat meningkatkan akurasi deteksi dan meminimalkan pengaruh gangguan visual.

img.shape: img.shape adalah atribut pada citra yang memberikan informasi tentang dimensi dan ukuran citra. Dengan menggunakan img.shape, kita dapat memperoleh informasi tentang lebar (width), tinggi (height), dan jumlah saluran warna (channels) dalam citra. Informasi ini dapat digunakan untuk mengatur parameter dan menyesuaikan metode deteksi plat, seperti ukuran kernel dalam filter atau menentukan batasan ROI pada citra.

Citra Biner (Binary): Penerapan operasi biner pada citra dapat membantu memisahkan plat kendaraan dari latar belakangnya. Dengan menerapkan teknik segmentasi, seperti thresholding atau metode adaptif seperti Otsu's thresholding, citra dapat dikonversi menjadi citra biner yang hanya berisi dua nilai piksel (misalnya hitam dan putih). Ini memudahkan pemrosesan selanjutnya, seperti deteksi kontur atau pemrosesan morfologi.

# SOURCE CODE
import cv2 as cv

import matplotlib.pyplot as plt

%matplotlib inline

import numpy as np

img = cv.imread("deteksiplat.jpg")

print(img.shape)

cropped_image = img[812:848, 90:185]

fig, axs = plt.subplots(1,2, figsize = (10,10))

ax = axs.ravel()

ax[0].imshow(img)

ax[0].set_title('Gambar Asli')

ax[1].imshow(cropped_image)

ax[1].set_title('Plat Terdeteksi')

(tresh, img_binary) = cv.threshold(cropped_image, 128, 255, cv.THRESH_BINARY)

edges = cv.Canny(img_binary, 100,150)

fig, axs = plt.subplots(1,2, figsize = (10,10))

ax = axs.ravel()

ax[0].imshow(img_binary, cmap='gray')

ax[0].set_title('Binary Image')

ax[1].imshow(edges, cmap='gray')

ax[1].set_title('Edges Image')

# PENJELASAN/ ALUR PROJECT

Mengimpor library:

cv2 adalah library OpenCV yang digunakan untuk pemrosesan citra dan video.

matplotlib.pyplot digunakan untuk membuat plot dan visualisasi citra.

%matplotlib inline digunakan untuk menampilkan plot secara inline di notebook Jupyter.

Membaca gambar:

img = cv.imread("deteksiplat.jpg") membaca gambar dengan nama "deteksiplat.jpg" dan menyimpannya ke dalam variabel img.

print(img.shape) mencetak dimensi gambar, yaitu lebar, tinggi, dan jumlah saluran warna (channels) dari citra.

Cropping image:

cropped_image = img[812:848, 90:185] mengambil bagian tertentu dari gambar dengan memotong (crop) gambar pada rentang piksel (812:848) untuk tinggi dan (90:185) untuk lebar. Hasilnya disimpan dalam variabel cropped_image.

Visualisasi citra:

fig, axs = plt.subplots(1,2, figsize = (10,10)) membuat plot dengan 1 baris dan 2 kolom, dan menentukan ukuran gambar.
axs.ravel() mengubah array dari objek sumbu ke dalam array 1 dimensi.

ax[0].imshow(img) menampilkan gambar asli pada sumbu pertama.

ax[0].set_title('Gambar Asli') menambahkan judul pada sumbu pertama.

ax[1].imshow(cropped_image) menampilkan citra yang sudah dipotong pada sumbu kedua.

ax[1].set_title('Plat Terdeteksi') menambahkan judul pada sumbu kedua.

Konversi menjadi citra biner:

(tresh, img_binary) = cv.threshold(cropped_image, 128, 255, cv.THRESH_BINARY) melakukan thresholding pada citra yang sudah dipotong dengan menggunakan nilai ambang 128. Hasilnya disimpan dalam variabel img_binary, dan ambang yang digunakan disimpan dalam variabel tresh.

Deteksi tepi:

edges = cv.Canny(img_binary, 100,150) melakukan deteksi tepi pada citra biner menggunakan metode Canny. Nilai ambang bawah dan ambang atas yang digunakan untuk deteksi tepi adalah 100 dan 150.




