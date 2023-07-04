
# word segmentation

Word segmentation pada gambar adalah proses untuk memisahkan teks yang ada dalam sebuah gambar menjadi unit-unit kata yang terpisah. Ini merupakan langkah penting dalam pengolahan bahasa alami dan pemrosesan gambar, karena memungkinkan komputer untuk memahami dan memproses teks yang ada dalam gambar.

Berikut ini adalah beberapa metode yang umum digunakan dalam word segmentation pada gambar:

1. Optical Character Recognition (OCR): OCR adalah teknologi yang digunakan untuk mengenali dan mengubah teks yang ada dalam gambar menjadi teks yang dapat diedit. Dalam konteks word segmentation, OCR dapat digunakan untuk mengenali karakter individu dalam gambar, dan kemudian karakter-karakter tersebut dapat digabungkan menjadi unit-unit kata.

2. Connected Component Analysis: Metode ini melibatkan analisis struktur dan bentuk karakter dalam gambar. Pertama, gambar diubah menjadi gambar biner, di mana hanya ada dua tingkat kecerahan (hitam dan putih). Kemudian, komponen-komponen terhubung yang mewakili karakter dalam gambar diidentifikasi dan dipisahkan berdasarkan jarak dan orientasi relatif mereka.

3. Metode berbasis kontur: Metode ini melibatkan deteksi kontur pada gambar untuk mengidentifikasi batas karakter. Kontur adalah garis yang membentuk batas objek dalam gambar. Dalam kasus word segmentation, kontur dapat digunakan untuk mengenali batas-batas karakter dan memisahkan mereka menjadi kata-kata.

4. Deep Learning: Pendekatan yang lebih mutakhir dalam word segmentation pada gambar menggunakan algoritma deep learning, seperti Convolutional Neural Networks (CNN) atau Recurrent Neural Networks (RNN). Model-model ini dilatih pada dataset gambar dengan anotasi teks untuk mempelajari pola-pola dan fitur-fitur yang berkaitan dengan kata-kata dalam gambar. Setelah dilatih, model dapat mengidentifikasi dan memisahkan kata-kata dalam gambar yang belum pernah dilihat sebelumnya.

Word segmentation pada gambar dapat memiliki tantangan tertentu, terutama jika gambar memiliki teks yang terdistorsi, ukuran font yang beragam, atau latar belakang yang kompleks. Namun, dengan penggunaan metode-metode yang tepat dan kemajuan dalam algoritma deep learning, kemampuan word segmentation pada gambar telah meningkat secara signifikan dalam beberapa tahun terakhir.

pada tugas pengolaan citra pada kali ini adalah word segmentation dengan menggunakan metode berbasis kontur berikut penjelasan codingan yang saya buat 

Kode yang Anda berikan mengimpor modul `matplotlib.pyplot`, `skimage.io`, `skimage.color`, dan `skimage.measure`. Modul `matplotlib.pyplot` digunakan untuk membuat plot dan visualisasi data. Modul `skimage.io` digunakan untuk membaca dan menulis gambar. Modul `skimage.color` digunakan untuk mengubah ruang warna gambar. Modul `skimage.measure` digunakan untuk melakukan analisis terhadap gambar.

Berikut ini adalah beberapa contoh penggunaan modul yang Anda impor:

1. Membaca gambar:
```python
image = io.imread('gambar.jpg')
```
Pada contoh di atas, gambar dengan nama file 'gambar.jpg' dibaca dan dimuat ke dalam variabel `image`.

2. Mengubah ruang warna gambar:
```python
image_gray = color.rgb2gray(image)
```
Pada contoh di atas, gambar yang ada dalam variabel `image` diubah menjadi skala abu-abu menggunakan fungsi `rgb2gray()` dari modul `skimage.color`. Hasilnya disimpan dalam variabel `image_gray`.

3. Menampilkan gambar:
```python
plt.imshow(image)
plt.show()
```
Pada contoh di atas, gambar yang ada dalam variabel `image` ditampilkan menggunakan `imshow()` dari modul `matplotlib.pyplot`. Kemudian, `show()` digunakan untuk menampilkan plot gambar.

4. Menghitung properti gambar:
```python
regions = measure.regionprops(image_gray)
```
Pada contoh di atas, properti-properti dari gambar yang ada dalam variabel `image_gray` dihitung menggunakan fungsi `regionprops()` dari modul `skimage.measure`. Hasilnya disimpan dalam variabel `regions`.

Fungsi `detect_letters(image_path)` di atas menerima parameter `image_path`, yang merupakan path (lokasi) file gambar yang akan diolah. Fungsi ini melakukan deteksi huruf dalam gambar menggunakan beberapa langkah pemrosesan. Berikut adalah penjelasan langkah-langkahnya:

1. Membaca gambar:
```python
image = io.imread(image_path)
```
Fungsi `io.imread()` dari modul `skimage.io` digunakan untuk membaca gambar dari `image_path` dan memuatnya ke dalam variabel `image`.

2. Mengubah gambar ke skala keabuan:
```python
gray = color.rgb2gray(image)
```
Fungsi `color.rgb2gray()` dari modul `skimage.color` digunakan untuk mengubah gambar ke dalam skala keabuan. Hasilnya disimpan dalam variabel `gray`.

3. Melakukan thresholding:
```python
threshold = gray < 0.5
```
Thresholding dilakukan dengan membandingkan setiap piksel dalam gambar keabuan (`gray`) dengan nilai threshold 0.5. Hal ini menghasilkan gambar biner di mana piksel-piksel dengan nilai di bawah 0.5 dianggap hitam, sedangkan piksel-piksel dengan nilai di atas 0.5 dianggap putih. Hasilnya disimpan dalam variabel `threshold`.

4. Membersihkan gambar dengan operasi morfologi:
```python
clean_image = measure.label(threshold)
```
Fungsi `measure.label()` dari modul `skimage.measure` digunakan untuk melakukan operasi label pada gambar biner (`threshold`). Hasilnya adalah gambar yang telah dibersihkan dari noise dan objek-objek terhubung diidentifikasi sebagai komponen terpisah. Hasilnya disimpan dalam variabel `clean_image`.

5. Temukan kontur huruf:
```python
contours = measure.find_contours(clean_image, 0.5)
```
Fungsi `measure.find_contours()` dari modul `skimage.measure` digunakan untuk mencari kontur pada gambar (`clean_image`) dengan nilai ambang 0.5. Kontur yang ditemukan akan merepresentasikan batas-batas objek dalam gambar. Hasilnya disimpan dalam variabel `contours`.

6. Deteksi huruf berdasarkan area dan aspek rasio:
```python
detected_letters = []
for contour in contours:
    y, x = contour[:, 0], contour[:, 1]
    ymin, ymax = int(min(x)), int(max(x))
    xmin, xmax = int(min(y)), int(max(y))
    width = xmax - xmin
    height = ymax - ymin
    area = width * height
    aspect_ratio = width / height
    if area > 50 and aspect_ratio > 0.2:
        detected_letters.append((xmin, ymin, width, height))
```
Pada langkah ini, setiap kontur yang ditemukan diperiksa untuk menentukan apakah merupakan huruf berdasarkan ukuran area dan aspek rasio (rasio lebar dan tinggi). Kontur yang memenuhi kriteria tersebut akan ditambahkan ke dalam daftar `detected_letters` dalam bentuk koordinat dan ukuran bounding box.

7. Mengembalikan hasil deteksi huruf:
```python
return detected_letters
```
Hasil deteksi huruf dalam bentuk daftar koordinat dan ukuran bounding box

Dengan menggunakan gambar "lauren.jpg", Anda dapat memanggil fungsi `detect_letters()` untuk mendeteksi huruf dalam gambar tersebut. Berikut adalah contoh penggunaannya:

```python
detected_letters = detect_letters('lauren.jpg')
print(detected_letters)
```

Outputnya akan berupa daftar koordinat dan ukuran bounding box untuk setiap huruf yang terdeteksi dalam gambar "lauren.jpg". Anda dapat memodifikasi fungsi tersebut sesuai dengan kebutuhan atau menggunakan outputnya untuk langkah-langkah selanjutnya dalam pemrosesan teks atau pengenalan karakter.

Dengan menggunakan gambar "lauren.jpg", Anda dapat memanggil fungsi `detect_letters()` untuk mendeteksi huruf dalam gambar tersebut. Berikut adalah contoh penggunaannya:

```python
detected_letters = detect_letters('lauren.jpg')
print(detected_letters)
```

Outputnya akan berupa daftar koordinat dan ukuran bounding box untuk setiap huruf yang terdeteksi dalam gambar "lauren.jpg". Anda dapat memodifikasi fungsi tersebut sesuai dengan kebutuhan atau menggunakan outputnya untuk langkah-langkah selanjutnya dalam pemrosesan teks atau pengenalan karakter.

Dengan menggunakan gambar "lauren.jpg", Anda dapat memanggil fungsi `detect_letters()` untuk mendeteksi huruf dalam gambar tersebut. Berikut adalah contoh penggunaannya:

```python
detected_letters = detect_letters('lauren.jpg')
print(detected_letters)
```

Outputnya akan berupa daftar koordinat dan ukuran bounding box untuk setiap huruf yang terdeteksi dalam gambar "lauren.jpg". Anda dapat memodifikasi fungsi tersebut sesuai dengan kebutuhan atau menggunakan outputnya untuk langkah-langkah selanjutnya dalam pemrosesan teks atau pengenalan karakter.

```python
from skimage import io

image_path = 'path/to/your/image.jpg'
image = io.imread(image_path)
```
Fungsi membaca file gambar dan mengembalikannya sebagai array NumPy, yang kemudian dapat Anda manipulasi atau proses lebih lanjut dalam kode Anda.

Kode yang Anda berikan menggunakan perpustakaan untuk membuat gambar dan menampilkan gambar dengan hasil deteksi huruf. Berikut rincian kodenya:matplotlib.pyplot:

1. Atur ukuran gambar ke dimensi yang lebih besar 30x20:
   ```python
   plt.figure(figsize=(30, 20))
   ```

2. Memplot gambar asli:
   ```python
   plt.subplot(1, 2, 1)
   plt.imshow(image)
   plt.axis('off')
   plt.title('Gambar Awal')
   ```

3. Panggil fungsi untuk mendapatkan huruf yang 'terdeteksi:detect_letters'
   ```python
   detected_letters = detect_letters(image_path)
   ```

4. Plot gambar dengan persegi panjang di sekitar huruf yang terdeteksi:
   ```python
   plt.subplot(1, 2, 2)
   plt.imshow(image)
   plt.axis('off')
   plt.title('Deteksi Huruf')
   ```

5. Iterasi di atas huruf yang terdeteksi dan tambahkan persegi panjang di sekitarnya:
   ```python
   for (x, y, width, height) in detected_letters:
       rect = plt.Rectangle((y, x), height, width, edgecolor='b', linewidth=3, fill=False)
       plt.gca().add_patch(rect)
   ```

6. Tampilkan gambar akhir dengan hasil deteksi huruf:
   ```python
   plt.show()
   ```



