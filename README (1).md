
# Import Library
```bash
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
1. import cv2: Baris ini mengimpor library OpenCV (cv2). OpenCV (Open Source Computer Vision Library) adalah library Python yang kuat untuk tugas computer vision secara real-time. OpenCV menyediakan sekumpulan fungsi dan class yang lengkap untuk pemrosesan gambar dan video, deteksi objek, kalibrasi kamera, pengenalan wajah, dan masih banyak lagi.

2. import matplotlib.pyplot as plt: Baris ini mengimpor modul pyplot dari library Matplotlib dan memberinya alias plt. Matplotlib adalah library Python penting lainnya untuk membuat visualisasi statis, animasi, dan interaktif. Dengan menggunakan alias plt, kita dapat memanggil fungsi plotting Matplotlib dengan lebih mudah tanpa harus mengetikkan seluruh nama modul setiap saat. Berikut beberapa fungsi Matplotlib yang sering digunakan:
    - plt.imshow(): Menampilkan gambar.
    - plt.plot(): Membuat plot garis.
    - plt.scatter(): Membuat plot sebaran.
    - plt.bar(): Membuat diagram batang.
    - plt.hist(): Membuat histogram.
    - plt.title(): Menetapkan judul plot.
    - plt.xlabel(): Menetapkan label untuk   sumbu x.
    - plt.ylabel(): Menetapkan label untuk sumbu y.
    - plt.show(): Menampilkan plot.

3. import numpy as np: Baris ini mengimpor library NumPy dan memberinya alias np. NumPy adalah library fundamental untuk komputasi ilmiah di Python. NumPy menyediakan operasi array dan matriks yang efisien, fungsi aljabar linear, pembuatan angka acak, dan alat matematika lainnya. OpenCV dan Matplotlib sangat bergantung pada array NumPy untuk mewakili gambar dan struktur data lainnya. 

# Membaca gambar
```bash
img = cv2.imread("rayyan.jpg")
```
img = cv2.imread("putri4.jpg") merupakan perintah Python yang menggunakan OpenCV untuk membaca gambar dari file "putri4.jpg" ke dalam variabel img. 
- Fungsi cv2.imread milik OpenCV digunakan untuk membaca gambar dari sebuah file. Dalam kasus ini secara spesifik, fungsi tersebut mencoba memuat gambar bernama "putri4.jpg" dari direktori kerja (tempat script Python dijalankan).
- img adalah Variabel yang akan menyimpan data gambar setelah gambar dimuat.

# Menampilkan Gambar
```bash 
plt.imshow(img)
```
plt.imshow(img) merupakan modul pyplot pustaka matplotlib digunakan untuk menampilkan data sebagai gambar; yaitu pada raster reguler 2D. sedangkan img adalah variabel yang berisi data gambar yang telah dibaca menggunakan OpenCV atau diperoleh dari sumber lain

# Mengonversi BGR ke RGB
``` bash 
img2 = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) 
```
Menggunakan kode img2 = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) untuk mengonversi gambar yang telah dibaca dalam format BGR (Blue, Green, Red) oleh OpenCV menjadi format RGB (Red, Green, Blue). 
- cv2.cvtColor(): Ini adalah fungsi dari pustaka OpenCV yang digunakan untuk mengonversi ruang warna gambar. 
- img2 untuk menetapkan hasil dari fungsi cv2.cvtColor ke variabel baru bernama img2. Variabel img2 akan menyimpan data gambar setelah konversi warna dilakukan.
- img adalah variabel yang berisi data gambar yang ingin Anda konversi dari BGR ke RGB. Variabel img kemungkinan besar menyimpan data gambar yang dimuat menggunakan fungsi cv2.imread dari OpenCV pada langkah sebelumnya.
- cv2.COLOR_BGR2RGB adalah konstanta yang ditetapkan di dalam OpenCV yang menentukan konversi ruang warna yang diinginkan. Ini menunjukkan bahwa Anda ingin mengonversi gambar dari ruang warna BGR (Biru-Hijau-Merah) ke ruang warna RGB (Merah-Hijau-Biru).

Alasan perlu mengonversi BGR ke RGB : 
- Python, secara default, menggunakan ruang warna BGR (Biru-Hijau-Merah) untuk merepresentasikan gambar. Ini berarti bahwa ketika kita memasukkan gambar, Python menafsirkan urutan warna setiap piksel sebagai BGR. Masalahnya, beberapa format gambar, seperti JPEG dan PNG, menggunakan ruang warna RGB (Merah-Hijau-Biru) sebagai standar. Di sinilah letak perbedaannya. Ketika kita memasukkan gambar dengan urutan warna RGB ke dalam Python, terjadi ketidakcocokan antara interpretasi Python (BGR) dan format gambar (RGB). Akibatnya, urutan warna terbalik, menghasilkan perubahan warna yang Anda lihat: hijau menjadi biru, merah menjadi hijau, dan biru menjadi merah. 
- Solusinya adalah dengan mengonversi gambar dari ruang warna BGR ke RGB sebelum memasukkannya ke Python. Konversi ini memastikan bahwa Python menafsirkan informasi warna dengan benar, menghasilkan representasi warna yang akurat.

# Menampilkan gambar setelah di konversi ke RGB
menampilkan gambar pastinya menggunakan baris kode yang sama dengan sebelumnya yaitu plt.imshow(img2). img2 merupakan variabel yang sudah menyimpan perubahan gambar yang di konversi dari BGR ke RGB. 

# Membuat baris dan kolom 
```bash 
(baris, kolom) = img.shape[:2]
```
Baris kode (baris, kolom) = img.shape[:2] digunakan untuk mengambil dimensi dari gambar yang telah dibaca menggunakan OpenCV dan menyimpannya dalam variabel baris dan kolom
- img.shape adalah atribut dari array Numpy img, yang memberikan dimensi dari array. Dalam konteks gambar, img.shape akan mengembalikan tuple yang berisi informasi tentang dimensi gambar, yaitu (tinggi, lebar, jumlah saluran warna).
- [:2]: Ini adalah slicing yang digunakan untuk membatasi tuple img.shape hanya pada dua elemen pertama, yaitu tinggi (baris) dan lebar (kolom) gambar. Jadi, hasil slicing ini adalah tuple (tinggi, lebar)
- (baris, kolom) = ...: Hasil dari slicing disimpan dalam dua variabel, yaitu baris dan kolom. Variabel ini akan berisi dimensi gambar, dengan baris menyimpan tinggi gambar dan kolom menyimpan lebarnya.
Baris kode(baris, kolom) = img.shape[:2] digunakan untuk menyediakan informasi dimensi gambar yang berguna dalam segmentasi warna.

# Menemukan warna dominan 
```bash
for x in range(baris):
    for y in range(kolom):
        max1=0
        max2=0
        for z in range(3):
            if(max1==0):
                max1=img2[x,y,z]
                imax1=z
            elif(max1<img2[x,y,z]):
                max1=img2[x,y,z]
                imax1=z
            elif(max2<img2[x,y,z]):
                max2=img2[x,y,z]
                imax2=z
        if((img2[x,y,imax1]-img2[x,y,imax2])>10):
            img2[x,y,imax1]=img2[x,y,imax1]-img2[x,y,imax2]/2
            for z in range(3):
                if(z!=imax1):
                    img2[x,y,z]=0
```
- Kode ini menggunakan dua loop for yang bersarang untuk iterasi melalui setiap pixel dalam gambar yang diwakili oleh variabel img2. Loop luar (for x in range(baris)) iterasi melalui setiap baris (koordinat y) pada gambar, dimana baris menyimpan jumlah baris (tinggi gambar). Loop dalam (for y in range(kolom)) iterasi melalui setiap kolom (koordinat x) di dalam baris saat ini, dimana kolom menyimpan jumlah kolom (lebar gambar).
Di dalam loop dalam, tiga variabel diinisialisasi untuk setiap pixel:
- max1: Awalnya diatur ke 0, variabel ini akan menyimpan nilai intensitas warna dominan (intensitas tertinggi) pada pixel saat ini.
- max2: Awalnya diatur ke 0, variabel ini akan menyimpan nilai intensitas warna sekunder (intensitas tertinggi kedua) pada pixel saat ini.
- imax1: Variabel ini akan melacak indeks channel warna (0, 1, atau 2) yang sesuai dengan warna dominan.
- Loop (for z in range(3)) iterasi tiga kali, sekali untuk setiap channel warna (dengan asumsi format RGB dengan channel 0, 1, dan 2 mewakili Merah, Hijau, dan Biru).
- Di dalam loop ini, rangkaian if-else menentukan warna dominan dan sekunder:Jika max1 masih 0 (berarti belum ditemukan warna dominan), intensitas channel warna saat ini ditetapkan ke max1, dan indeksnya disimpan di imax1.Jika intensitas channel warna saat ini lebih besar dari max1 (tetapi bukan yang tertinggi), maka itu menjadi max1 baru dengan indeksnya diperbarui di imax1. Jika intensitas channel warna saat ini lebih besar dari max2 (tetapi bukan yang pertama atau kedua tertinggi), maka itu menjadi max2 baru dengan indeksnya disimpan di imax2.
- Setelah iterasi melalui semua channel warna, pernyataan if memeriksa apakah perbedaan antara intensitas warna dominan dan sekunder (img2[x, y, imax1] dan img2[x, y, imax2]) lebih besar dari nilai ambang batas 10.
- Intensitas warna dominan (img2[x, y, imax1]) dikurangi setengah dari intensitas warna sekunder (img2[x, y, imax2] // 2).

Jadi fungsi kode ini adalah untuk melakukan iterasi melalui setiap pixel dalam gambar.
Selain itu juga mengidentifikasi warna dominan dan sekunder dan jika perbedaan intensitas antara keduanya cukup besar (lebih dari 10), kode ini mengurangi intensitas warna dominan setengah dari intensitas warna sekunder. Maka dapat dilhat hasil gambarnya lebih terang 

Teori pendukung : 
- Teori pendukung untuk implementasi ini berdasarkan pada asumsi bahwa dalam sebuah gambar, warna dominan biasanya memiliki perbedaan nilai yang signifikan dengan warna lainnya. Dengan memeriksa perbedaan antara nilai maksimum pertama dan kedua untuk setiap piksel, kode tersebut mencoba untuk mengidentifikasi piksel-piksel yang mewakili warna dominan dalam gambar. Kemudian, nilai warna yang tidak dominan diatur menjadi 0 untuk meningkatkan kontras dan membuat warna dominan lebih menonjol.

# Segmentasi warna RGB
1. Warna merah 
```Bash 
merah=img2[:,:,0] #Merah
plt.imshow(merah, cmap='gray')
plt.colorbar()
plt.show()
```
- Ekstraksi Komponen Warna Merah: Baris merah=img2[:,:,0] digunakan untuk mengekstraksi komponen warna merah dari gambar yang telah diubah menjadi format RGB sebelumnya (img2). Pada gambar dalam format RGB, sumbu pertama (indeks 0) mewakili warna merah, sumbu kedua (indeks 1) mewakili warna hijau, dan sumbu ketiga (indeks 2) mewakili warna biru. Dengan menggunakan slicing [:,:,0], kita mengambil semua baris dan kolom dari sumbu pertama, yang mewakili warna merah.
- Kemudian, gambar yang telah diekstraksi menjadi komponen warna merah ditampilkan menggunakan plt.imshow() dengan argumen cmap='gray', yang menunjukkan bahwa gambar tersebut akan ditampilkan dalam skala abu-abu. plt.colorbar() digunakan untuk menambahkan skala warna pada sisi untuk menunjukkan nilai intensitas dalam gambar. plt.show() digunakan untuk menampilkan gambar.

Jadi saat kode ini dijalankan gambar akan memudarkan komponen yang bewarna merah

2. Warna hijau
```Bash 
hijau=img2[:,:,1] #Hijau
plt.imshow(hijau, cmap='gray')
plt.colorbar()
plt.show()
```
- Ekstraksi Komponen Warna Hijau: Baris hijau=img2[:,:,1] digunakan untuk mengekstraksi komponen warna hijau dari gambar img2. Dalam format RGB, sumbu pertama (indeks 0) mewakili warna merah, sumbu kedua (indeks 1) mewakili warna hijau, dan sumbu ketiga (indeks 2) mewakili warna biru. Dengan menggunakan slicing [:,:,1], kita mengambil semua baris dan kolom dari sumbu kedua, yang mewakili warna hijau.

- Gambar yang telah diekstraksi menjadi komponen warna hijau ditampilkan menggunakan plt.imshow() dengan argumen cmap='gray', menunjukkan bahwa gambar tersebut akan ditampilkan dalam skala abu-abu. plt.colorbar() ditambahkan untuk menunjukkan skala warna pada sisi untuk menunjukkan nilai intensitas dalam gambar. plt.show() digunakan untuk menampilkan gambar.

Jadi saat kode ini dijalankan gambar akan memudarkan komponen yang bewarna hijau 

3. Warna biru 
``` Bash
biru=img2[:,:,2] #Biru
plt.imshow(biru, cmap='gray')
plt.colorbar()
plt.show()
```
- Ekstraksi Komponen Warna Biru: Baris biru=img2[:,:,2] digunakan untuk mengekstraksi komponen warna biru dari gambar img2. Dalam format RGB, sumbu pertama (indeks 0) mewakili warna merah, sumbu kedua (indeks 1) mewakili warna hijau, dan sumbu ketiga (indeks 2) mewakili warna biru. Dengan menggunakan slicing [:,:,2], kita mengambil semua baris dan kolom dari sumbu ketiga, yang mewakili warna biru.

- Gambar yang telah diekstraksi menjadi komponen warna biru ditampilkan menggunakan plt.imshow() dengan argumen cmap='gray', menunjukkan bahwa gambar tersebut akan ditampilkan dalam skala abu-abu. plt.colorbar() ditambahkan untuk menunjukkan skala warna pada sisi untuk menunjukkan nilai intensitas dalam gambar. plt.show() digunakan untuk menampilkan gambar.

Jadi saat kode ini dijalankan gambar akan memudarkan komponen yang bewarna Biru

Teori pendukung : 
- Teori pendukung untuk langkah-langkah tersebut adalah bahwa dengan mengekstraksi dan menampilkan setiap komponen warna secara terpisah, kita dapat melihat distribusi intensitas warna untuk masing-masing warna (merah, hijau, biru) secara terpisah. Hal ini memungkinkan kita untuk menganalisis kontribusi masing-masing warna terhadap gambar secara individu, yang berguna dalam pemrosesan gambar seperti segmentasi warna, analisis warna, dan lain sebagainya.

# Membuat histogram 
``` bash 
r = img2[:, :, 0]
g = img2[:, :, 1]
b = img2[:, :, 2]
```
``` bash 
color_image = cv2.imread('putri4.jpg')

histogram_biru = cv2.calcHist([b], [0], None, [256], [0, 256])
histogram_hijau = cv2.calcHist([g], [0], None, [256], [0, 256])
histogram_merah = cv2.calcHist([r], [0], None, [256], [0, 256])
histogram_warna = cv2.calcHist([color_image], [0], None, [256], [0, 256])

plt.figure(figsize=(12, 8))
plt.subplot(2, 2, 1)  # Subplot 1 (atas kiri)
plt.plot(histogram_biru, color='b')
plt.title('Histogram Biru')
plt.xlim([0, 256])

plt.subplot(2, 2, 2)  # Subplot 2 (atas kanan)
plt.plot(histogram_hijau, color='g')
plt.title('Histogram Hijau')
plt.xlim([0, 256])

plt.subplot(2, 2, 3)  # Subplot 3 (bawah kiri)
plt.plot(histogram_merah, color='r')
plt.title('Histogram Merah')
plt.xlim([0, 256])


plt.subplot(2, 2, 4)  # Subplot 4 (bawah kanan)
plt.plot(histogram_warna.flatten(), color='gray')  # Flatten histogram multi-dimensi
plt.title('Histogram Warna')
plt.xlim([0, 256])
```
- Membaca Gambar: color_image = cv2.imread('putri4.jpg') digunakan untuk membaca gambar.

- Perhitungan Histogram: cv2.calcHist() digunakan untuk menghitung histogram untuk setiap saluran warna (biru, hijau, merah) serta untuk gambar warna keseluruhan. Namun, dalam kode Anda, b, g, dan r tampaknya tidak didefinisikan sebelumnya. Seharusnya digunakan untuk menghitung histogram dari saluran warna biru, hijau, dan merah terlebih dahulu.

- Menampilkan Histogram: Kode menggunakan plt.subplot() untuk membuat subplot dan menampilkan histogram dari setiap saluran warna serta histogram warna keseluruhan. Namun, Anda dapat menghitung histogram secara terpisah untuk setiap saluran warna, lalu menampilkannya secara terpisah.

Penjelasan hasil histogram 
1. Subplot 1: Histogram Biru
- Histogram Biru menunjukkan distribusi intensitas piksel dalam kanal Biru.
- Sumbu x menunjukkan nilai intensitas piksel Biru (dari 0 hingga 255).
- Sumbu y menunjukkan jumlah piksel dengan masing-masing intensitas.
- Puncak yang dominan di sekitar nilai 100 menunjukkan bahwa terdapat banyak piksel Biru dengan intensitas sedang (sekitar 100 pada skala 0-255).
- Penurunan frekuensi di kedua sisi puncak menunjukkan bahwa terdapat lebih sedikit piksel Biru dengan intensitas yang sangat rendah (dekati 0) atau sangat tinggi (dekati 255).

2. Subplot 2: Histogram Hijau 
- Histogram Hijau menunjukkan distribusi intensitas piksel dalam kanal Hijau.
- Interpretasinya mirip dengan Histogram Biru:
- Sumbu x menunjukkan nilai intensitas piksel Hijau (0-255).
- Sumbu y menunjukkan jumlah piksel dengan tiap intensitas.
- Puncak yang dominan di sekitar nilai 120 menunjukkan bahwa terdapat banyak piksel Hijau dengan intensitas sedang (sekitar 120 pada skala 0-255).
- Penurunan frekuensi di kedua sisi puncak menunjukkan bahwa terdapat lebih sedikit piksel Hijau dengan intensitas yang sangat rendah (dekati 0) atau sangat tinggi (dekati 255).

3. Subplot 3: Histogram Merah 
- Histogram Merah menunjukkan distribusi intensitas piksel dalam kanal Merah.
- Sumbu x menunjukkan nilai intensitas piksel Merah (0-255).
- Sumbu y menunjukkan jumlah piksel dengan tiap intensitas.
- Puncak yang dominan di sekitar nilai 100 menunjukkan bahwa terdapat banyak piksel Merah dengan intensitas sedang (sekitar 100 pada skala 0-255).
- Penurunan frekuensi di kedua sisi puncak menunjukkan bahwa terdapat lebih sedikit piksel Merah dengan intensitas yang sangat rendah (dekati 0) atau sangat tinggi (dekati 255).

4. Histogram Warna merepresentasikan Histogram - Warna merepresentasikan distribusi keseluruhan intensitas piksel di seluruh tiga kanal warna (RGB).
- Sumbu x menunjukkan nilai intensitas piksel (0-255).
- Sumbu y menunjukkan jumlah total piksel dengan tiap intensitas.
- Bentuk kurva yang relatif datar menunjukkan bahwa terdapat distribusi intensitas piksel yang cukup merata di seluruh kanal warna (Biru, Hijau, dan Merah).
- Hal ini menunjukkan bahwa gambar tidak didominasi oleh satu warna tertentu, melainkan memiliki keseimbangan warna yang cukup baik.

Teori pendukung : 
- Histogram Warna: Histogram warna adalah representasi distribusi intensitas warna dalam sebuah gambar. Ini mengukur jumlah piksel dalam gambar yang memiliki nilai intensitas tertentu dalam rentang 0 hingga 255 untuk setiap saluran warna (biru, hijau, merah) atau kombinasi dari ketiganya. Histogram warna berguna untuk menganalisis karakteristik warna dalam gambar, seperti tingkat kecerahan, kontras, dan distribusi warna.

- Ekstraksi Saluran Warna: Setiap gambar digital terdiri dari saluran warna yang merepresentasikan warna pada tingkat piksel. Saluran warna utama dalam gambar RGB adalah biru (Blue), hijau (Green), dan merah (Red). Dalam kode yang diberikan, kita mengambil histogram untuk setiap saluran warna terpisah untuk menganalisis distribusi intensitas warna secara individu.

- Penggunaan cv2.calcHist(): Fungsi cv2.calcHist() dari OpenCV digunakan untuk menghitung histogram dari saluran warna atau gambar keseluruhan. Ini membutuhkan argumen seperti array gambar, saluran warna yang ingin dihitung histogramnya, jumlah bin histogram, dan rentang nilai intensitas yang ingin diperhitungkan. Hasilnya adalah histogram yang merepresentasikan distribusi intensitas warna dalam gambar.

- Visualisasi Histogram: Setelah histogram dihitung, kita menggunakan pustaka matplotlib untuk memvisualisasikannya. Subplot dibuat untuk menampilkan histogram untuk setiap saluran warna terpisah (biru, hijau, merah), serta histogram untuk gambar warna keseluruhan. Grafik plot ditampilkan menggunakan plt.plot(), sedangkan batas sumbu x diatur menggunakan plt.xlim() untuk memastikan histogram ditampilkan dengan benar.

#  Mencari nilai ambang batas citra untuk dapat menampilan kategori warna pada citra
``` Bash
gray = cv2.cvtColor(img2, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

(thresh, binary2) = cv2.threshold(gray, 20, 255, cv2.THRESH_BINARY)
axs[0,1].imshow(binary2, cmap = 'binary')
axs[0,1].set_title('BLUE')

(thresh, binary3) = cv2.threshold(gray, 50, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

(thresh, binary4) = cv2.threshold(gray, 90, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')
``` 
- Konversi ke Citra Skala Abu-abu: gray = cv2.cvtColor(img2, cv2.COLOR_RGB2GRAY) mengonversi gambar RGB menjadi citra skala abu-abu.

- Penerapan Thresholding: cv2.threshold() digunakan untuk menerapkan metode thresholding pada citra skala abu-abu. Hasilnya adalah gambar biner yang menyoroti area tertentu dalam gambar.

- Menampilkan Gambar: plt.imshow() digunakan untuk menampilkan gambar biner dalam subplot. Parameter cmap digunakan untuk menentukan skema warna yang digunakan untuk menampilkan gambar.

- thresh adalah nilai ambang yang digunakan untuk mengklasifikasikan piksel. binary1 menunjukkan hasil thresholding tanpa mengatur ambang. binary2, binary3, dan binary4 menunjukkan hasil thresholding dengan nilai ambang yang berbeda, menyoroti area yang lebih terang dalam gambar.

Dengan menggunakan metode ini, Kita dapat dengan mudah menyoroti area tertentu dalam gambar berdasarkan ambang piksel yang ditentukan.

Teori pendukung : 
- Teori pendukung dari langkah-langkah ini adalah bahwa dengan menerapkan thresholding pada citra skala abu-abu, kita dapat memisahkan objek dari latar belakang berdasarkan tingkat kecerahan piksel. Dengan menggunakan beberapa nilai ambang, kita dapat memperoleh segmentasi yang lebih baik tergantung pada karakteristik gambar. Segmentasi seperti ini sering digunakan sebagai langkah awal dalam analisis gambar lanjutan, seperti deteksi tepi, ekstraksi fitur, atau pengenalan objek.