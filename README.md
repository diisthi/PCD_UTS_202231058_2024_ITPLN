# PCD_UTS_202231058_2024_ITPLN

## UTS Pengolahan Citra

### Laporan Praktikum

#### Tahapan menyelesaikan projek:
  Pertama-tama saya menuliskan nama menggunakan tiga macam warna yang telah ditentukan. kemudian saya foto dan saya masukkan kedalam folder yang sama dengan notebook yang akan saya buat. kemudian saya mengolah citra tersebut dan berikut adalah langkah-langkahnya:

#### Import Library
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
  Pada codingan diatas saya mengimport library yaitu cv2, numpy, dan matplotlib.
Library cv2 digunakan untuk memanipulasi citra seperti membaca, menulis, menampilkan, menganalisis gambar. 
Library numpy digunakan untuk numerik seperti mengubah warna pada gambar menjadi sebuah matrix angka yang akan merepresentasikan warna tersebut.
Library matplotlib digunakan untuk  membuat plot seperti memvisualisasikan gambar, data, dan animasi.

#### Mengimport gambar
```bash
img = cv2.imread("nama7.jpg")
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
  Codingan diatas adalah code untuk membaca gambar. Gambar yang ingin dibaca harus berada do folder yang sama dengan notebook agar dapat dimaba. code 'img' merupakan inisialisasi untuk gambar sedangkan 'imsread' digunakan untuk membaca gambar. untuk code 'cv2.cvtColor(img, cv2.COLOR_BGR2RGB)' adalah code untuk mengubah warna pada gambar agar berubah menjadi berwarna atau RGB. 

#### Mendeteksi warna gambar
```bash
red,green,blue = cv2.split(img)
```
  Codingan diatas adalah code untuk memfilter gambar menjadi merah, hijau, dan biru. gambar dibagi menjadi bagian merah, hijau, dan biru.

#### Menampilkan gambar setelah dideteksi
```bash
fig, axs = plt.subplots(4,2,figsize=(15,15))
axs[0,0].imshow(img)
axs[0,0].set_title("ASLI")

axs[1,0].imshow(blue, cmap="gray")
axs[1,0].set_title("BLUE")

axs[2,0].imshow(red, cmap="gray")
axs[2,0].set_title("RED")

axs[3,0].imshow(green, cmap="gray")
axs[3,0].set_title("GREEN")
```
  Pada syntax pertama, 'fig' adalah sebuah objek untuk mewakili seluruh gambar dan 'axs' adalah array dua dimensi dari sumbu objek. 
pada syntax kedua yaitu untuk menampilkan gambar asli. syntax 'imshow' digunakan untuk menampilkan gambar. selanjutnya untuk 'cmap="gray"' adalah syntax untuk mengatur warna ke skala abu-abu. dan untuk warna biru masih bisa terbaca begitu juga untuk warna merah dan hijau.

#### Histogram
```bash
histimg = cv2.calcHist([img],[0],None,[256],[0,256])
histRed = cv2.calcHist([red],[0],None,[256],[0,256])
histGreen = cv2.calcHist([green],[0],None,[256],[0,256])
histBlue = cv2.calcHist([blue],[0],None,[256],[0,256])

fig, axs = plt.subplots(2, 2, figsize=(15, 15))
axs[1,1].plot(histimg, color='black')
axs[1,1].set_title('Histogram Gambar Asli')

axs[0,0].plot(histRed, color='red')
axs[0,0].set_title('Histogram Komponen Merah')

axs[0,1].plot(histGreen, color='green')
axs[0,1].set_title('Histogram Komponen Hijau')

axs[1,0].plot(histBlue, color='blue')
axs[1,0].set_title('Histogram Komponen Biru')

plt.show()
```
  'cv2.calcHist()' adalah syntax untuk menghitung histogram dari gambar. untuk parameter pertama merupakan gambar, parameter kedua adalah warna yang ingin dihitung. parameter ketiga adalah maska. maska biasanya digunakan untuk menghitung histogram pada area tertentu dari gambar yang telah diinput. 'axs[1,1].plot(histimg, color='black')
axs[1,1].set_title('Histogram Gambar Asli')' code berikut adalah untuk menampilkan histogram gambar asli begitu juga untuk codingan pada warna biru, merah, dan hijau.

#### Mengurutkan Ambang batas
```bash
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(15,15))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

(thresh, binary2) = cv2.threshold(gray, 30, 255, cv2.THRESH_BINARY)
axs[0,1].imshow(binary2, cmap = 'binary')
axs[0,1].set_title('BLUE')

(thresh, binary3) = cv2.threshold(gray, 50, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')
```
  Kode yang diberikan melakukan beberapa operasi pemrosesan gambar menggunakan library OpenCV dan matplotlib di Python.
Pertama, gambar dimuat dan dikonversi ke skala abu-abu dengan fungsi 'cv2.cvtColor'.
Kemudian fungsi 'cv2.threshold' digunakan untuk mengelompokkan gambar untuk nilai ambang batas yang berbeda. Segmentasi ini dilakukan dengan membuat piksel yang nilainya lebih besar dari ambang batas tertentu berwarna putih, sedangkan piksel yang nilainya kurang dari ambang batas berwarna hitam, sesuai dengan parameter yang diberikan. Kemudian, hasil segmentasi tersebut ditampilkan dalam subplot 2x2 dengan menggunakan plt.subplots.
Setiap gambar hasil segmentasi disertai dengan judul yang menggambarkan ambang nilai yang digunakan dalam proses segmentasi. Dalam contoh ini, digunakan empat ambang nilai yang berbeda untuk mendemonstrasikan efek dari variasi ambang pada hasil segmentasi. Pada gambar pertama, tidak ada segmentasi yang dilakukan, sehingga tidak ada perubahan dalam gambar dari skala abu-abu asli.Pada gambar kedua, segmentasi dilakukan dengan ambang nilai 50, menghasilkan gambar biner dengan daerah-daerah yang lebih terang mewakili objek-objek yang lebih terang dalam gambar asli. Pada gambar ketiga, ambang nilai ditingkatkan menjadi 80, sehingga hanya daerah-daerah yang lebih cerah lagi yang dianggap sebagai objek dalam gambar biner. Terakhir, pada gambar keempat, ambang nilai dinaikkan lagi menjadi 100, menyebabkan hanya daerah-daerah paling cerah yang tersisa sebagai objek dalam gambar biner.

#### Teori yang terkait dengan projek
  Deteksi warna adalah proses penting dalam pemrosesan gambar digital untuk mengidentifikasi dan mengekstrak warna dari gambar. Teknik ini digunakan dalam berbagai aplikasi, seperti segmentasi gambar, analisis tekstur, dan pengenalan objek. Salah satu teknik umum untuk deteksi warna adalah ambang batas warna, di mana nilai intensitas warna pada setiap kanal warna dibandingkan dengan ambang batas yang telah ditentukan. Piksel dengan nilai yang melebihi ambang batas dianggap sebagai bagian dari objek yang ingin diidentifikasi. Teknik deteksi warna lainnya termasuk pencocokan warna langsung, segmentasi berbasis wilayah, dan pembelajaran mesin. Pemilihan teknik yang tepat tergantung pada kompleksitas gambar, akurasi yang diinginkan, dan sumber daya komputasi yang tersedia. Deteksi warna dan ambang batas warna merupakan dasar penting dalam pengolahan citra digital dan memiliki banyak aplikasi dalam berbagai bidang, seperti industri, medis, dan ilmiah.

