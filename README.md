# Laporan Proyek Machine Learning - Ades Tikaningsih

## Project Overview 

**Latar Belakang**:

Membaca merupakan salah satu kegiatan yang lekat dengan kehidupan sehari-hari seseorang. Konsep utama dari membaca adalah memahami makna yang terkandung dalam sebuah teks. Terbukti bahwa orang yang memiliki kebiasaan membaca yang tinggi pasti memiliki wawasan yang luas, membaca dapat juga membuat seseorang mengenal, mengetahui serta memahami apa yang belum dikenal, diketahui dan dipahami. Oleh karena itu pemahaman seseorang terhadap pentingnya pemahaman membaca (reading comprehension) merupakan hal yang penting untuk dipelajari. Namun perlu digaris bawahi bahwa membaca juga bisa menimbulkan bahaya, karena apa yang dibaca seseorang akan mempengaruhi karakter yang terbentuk dari pengetahuan yang ia dapat dari buku tersebut. Salah satu langkah yang ditempuh dalam menyediakan bahan bacaan adalah dengan memilah dan memilih jenis bacaan atau buku apa yang seharusnya dibaca, baik dengan mengenali Penulisnya, Kenali sinopsisnya,  Memakai style bahasa yang gampang dipahami dan lain sebagainya. Berdasarkan hal itu dengan kemajuan bidang ilmu pengetahuan danteknologi dibuatlah sebuah sistem rekomendasi yang berguna bagi pengguna internet yang mungkin merasa sulit untuk memilih dari banyak produk dan layanan yang tersedia. Sistem Rekomendasi dapat memprediksi seberapa besar kemungkinan pengguna target akan tertarik dengan item yang mungkin tidak diketahui olehnya. [[1]](https://aclanthology.org/C18-1033.pdf). 

Melihat pentingnya dampak buku bagi kehidupan kita, kita perlu banyak membaca buku. Ketika kita membaca buku, kita pasti memiliki ketertarikan kepada satu atau beberapa bidang. Dikarenakan banyaknya buku yang telah dan akan terbit, kita membutuhkan sistem rekomendasi yang akan menyaring buku - buku sesuai dengan selera dan ketertarikan kita. Dengan adanya sistem rekomendasi ini, kita tidak perlu lama - lama dalam mencari buku sesuai ketertarikan kita. Sistem rekomendasi sangat penting di beberapa industri karena dapat menghasilkan pendapatan dalam jumlah besar ketika efisien atau juga menjadi cara untuk menonjol secara signifikan dari pesaing. Sebagai bukti pentingnya sistem pemberi rekomendasi, kami dapat menyebutkan bahwa, beberapa tahun yang lalu, Netflix mengadakan tantangan ("hadiah Netflix") di mana tujuannya adalah untuk menghasilkan sistem pemberi rekomendasi yang berkinerja lebih baik daripada algoritmanya sendiri dengan hadiah dari 1 juta dolar untuk menang.

## Business Understanding

Sistem rekomendasi buku adalah jenis sistem rekomendasi di mana kita harus merekomendasikan buku sejenis kepada pembaca berdasarkan minatnya. Sistem rekomendasi buku digunakan oleh situs online yang menyediakan ebook seperti google play books, open library, good Read's, dll.

### Problem Statements
Kembangkan sebuah sistem rekomendasi Buku untuk menjawab permasalahan berikut:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Dengan data rating yang Anda miliki, bagaimana merekomendasikan buku lain yang mungkin disukai dan belum pernah dikunjungi oleh pengguna? 

### Goals
Untuk  menjawab pertanyaan tersebut, buatlah sistem rekomendasi dengan tujuan atau goals sebagai berikut:
- Menghasilkan sejumlah rekomendasi Buku yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi Buku yang sesuai dengan preferensi pengguna dan belum pernah dikunjungi sebelumnya dengan teknik collaborative filtering.

**Solution statements**:

Pada latihan kali ini kita akan menggunakan kedua metode yaitu content dan collaborative based filter yaitu :
- Pada Content Based Flter, kita akan menggunakan penulis buku menjadi pusat sebagai pusat dari sistem rekomendasi. 
Dalam algoritma ini, kami mencoba menemukan item pencarian yang mirip. Misalnya, seseorang suka menonton bidikan Sachin Tendulkar, maka dia mungkin juga suka menonton bidikan Ricky Ponting karena kedua video tersebut memiliki tag dan kategori yang mirip.
- Pada Collaborative Based Flter, kita akan menggunakan penilaian dari berbagai pengguna sebagai pusat dari sistem rekomendasi. Sistem pemberi rekomendasi penyaringan berbasis kolaboratif didasarkan pada interaksi pengguna dan item target sebelumnya. Dengan kata sederhana di sini, kami mencoba mencari pelanggan yang mirip dan menawarkan produk berdasarkan apa yang mereka pilih.

## Data Understanding

Kali ini pada pembuatan sistem rekomendasi, saya menggunakan Book Recommendation Dataset dari Kaggle. Dataset bisa diunduh [disini](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Variabel-variabel pada Book Recommendation Dataset adalah sebagai berikut:

- Buku

Buku diidentifikasi dengan ISBN masing-masing. ISBN yang tidak valid telah dihapus dari set data. Selain itu, beberapa informasi berbasis konten diberikan ( Book-Title, Book-Author, Year-Of-Publication, Publisher), diperoleh dari Amazon Web Services. Perhatikan bahwa dalam kasus beberapa penulis, hanya yang pertama disediakan. URL yang menautkan ke gambar sampul juga diberikan, muncul dalam tiga rasa berbeda ( Image-URL-S, Image-URL-M, Image-URL-L), yaitu, kecil, sedang, besar. URL ini mengarah ke situs web Amazon.
- Rating

Berisi informasi rating buku. Peringkat ( Book-Rating) baik eksplisit, dinyatakan dalam skala 1-10 (nilai yang lebih tinggi menunjukkan apresiasi yang lebih tinggi), atau implisit, dinyatakan dengan 0.

**1. Exploratory Data Analysis**

Pada step ini, lakukanlah analisa sederhana, seperti describe(), info(), dan juga visualisasi agar kita dapatkan suatu insight dari dataset.
Jumlah dataset buku 271360 baris 8 kolom, dan jumlah dataset rating 1149780 baris 3 kolom. Berdasarkan jumlah data rating dan books terbilang banyak, di sini saya hanya mengambil 10000 baris book dataset dan 5000 baris untuk rating dataset. 

Data Buku

![image](https://user-images.githubusercontent.com/110407053/192125666-a2ab4ddd-2228-4a79-8c1c-88ce35eef5b3.png)
Data Rating

![image](https://user-images.githubusercontent.com/110407053/192125641-d1c1bd8b-7153-4eb0-bb81-6c5d3b971cf2.png)

Pada dataset buku, ada beberapa kolom yang di hapus karena tidak diperlukan untuk proyek ini seperti URL gambar. 

Mengecek informasi pada dataset dengan fungsi info() berikut.

![image](https://user-images.githubusercontent.com/110407053/192125760-b76667e1-32e5-4821-9614-6b1620ae928d.png)

Berdasarkan informasi buku dataset memiliki 5 kolom dengan tipe ogject.

![image](https://user-images.githubusercontent.com/110407053/192125751-9d8f3903-394b-4be4-b502-0455e1958e0f.png)

Berdasarkan informasi rating dataset memiliki 2 kolom dengan tipe int64 yaitu user_id, rating dan 1 bertipe object yaitu ISBN

Dan kita akan menamai ulang kolom-kolom dari setiap file karena nama kolom tersebut berisi spasi, dan huruf kapital sehingga perlu diperbaiki agar mudah digunakan.

#### 2. Visualisasi data buku dan rating

![image](https://user-images.githubusercontent.com/110407053/192126113-b68c29d5-a43b-4ebf-8955-fbd4c07fe058.png)

Pada gambar diatas menunjukan bahwa kategori penulis (top 50) terbanyak adalah stephen king dengan total 70 buku 

![image](https://user-images.githubusercontent.com/110407053/192127390-b82f6f39-0f43-4502-8da7-6ca5a84a8dd9.png)

Pada gambar diatas menunjukan bahwa buku teratas (top 20) dengan judul The golden compass dengan jumlah 4 buku 

![image](https://user-images.githubusercontent.com/110407053/192127095-1cf41a45-670c-45f8-8522-7e3346f83a62.png)



## Data Preparation
Pada bagian akan menerapkan beberapa proses antara lain sebagai berikut :

**1. Cek missing value**

![image](https://user-images.githubusercontent.com/110407053/192125779-5fc21f42-fb35-4c25-b230-6073a0e7f376.png)
![image](https://user-images.githubusercontent.com/110407053/192125783-9d2f91d7-1a63-478e-ab9f-99f9a2de779e.png)

Data buku dan rating tidak memiliki missing value sehingga bisa diteruskan untuk proses selanjutnya.

**2. Membuang data duplikat**

Selanjutnya, proyek ini hanya akan menggunakan data unik untuk dimasukkan ke dalam proses pemodelan. Oleh karena itu, perlu menghapus data yang duplikat dengan fungsi drop_duplicates(). Proses ini dilakukan supaya dataset tetap memiliki integritas dan tidak berulang.

**3. konversi data series menjadi list**

Selanjutnya, kita perlu melakukan konversi data series menjadi list. Dalam hal ini, kita menggunakan fungsi tolist() dari library numpy. Implementasikan kode berikut.

GAMBAR PRINT LEN LIST...............

**4. Membuat dictionary**

Tahap berikutnya, kita akan membuat dictionary untuk menentukan pasangan key-value pada data book_ISBN, book_author, book_title dan book_year_of_publication yang telah kita siapkan sebelumnya.

## Modeling

Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Kini, saatnya mengembangkan sistem rekomendasi dengan pendekatan content based filtering dan collaborative filtering.

#### 1. Model Development dengan Content Based Filtering 

###### TF-IDF Vectorizer

TF-IDF adalah singkatan dari Term Frequency Inverse Document Frequency. Ini adalah algoritma yang sangat umum untuk mengubah teks menjadi representasi angka yang bermakna yang digunakan untuk menyesuaikan algoritma mesin untuk prediksi![[2]](TF-IDF Vectorizer scikit-learn
TF-IDF Vectorizer scikit-learn. (2021). Retrieved 25 September 2022, from https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a)
Pada tahap ini, kita akan membangun sistem rekomendasi judul buku berdasarkan penulisnya. TfidfVectorizer dapat menangani nama-nama penulis seberapa sering mereka muncul dalam dokumen. 

gambar tfid................

Selanjutnya, lakukan fit dan transformasi ke dalam bentuk matriks. Perhatikanlah, matriks yang kita miliki berukuran (10000, 5575). Nilai 10000 merupakan ukuran data dan 5575 merupakan nama penulis. Selanjutnya ubah tfid menjadi matriks dengan fungsi todense()

gambar todense...........

Selanjutnya, mari kita lihat matriks tf-idf untuk beberapa judul buku dengan penulis buku. Sampai di sini, telah berhasil mengidentifikasi representasi fitur penting dari setiap judul buku dengan fungsi tfidfvectorizer. Kita juga telah menghasilkan matriks yang menunjukkan korelasi antara judul buku dengan penulis. Selanjutnya, kita akan menghitung derajat kesamaan antara satu buku dengan penulis lainnya untuk menghasilkan kandidat penulis yang akan direkomendasikan.

###### Cosine Similarity

Cosine Similarity mengukur kesamaan antara dua vektor ruang hasil kali dalam. Ini diukur dengan kosinus sudut antara dua vektor dan menentukan apakah dua vektor menunjuk ke arah yang kira-kira sama. ![[3]](https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8) kita akan menghitung derajat kesamaan (similarity degree) antar restoran dengan teknik cosine similarity. Di sini, kita menggunakan fungsi cosine_similarity dari library sklearn. Pada tahapan ini, kita menghitung cosine similarity dataframe tfidf_matrix yang kita peroleh pada tahapan sebelumnya. Dengan satu baris kode untuk memanggil fungsi cosine similarity dari library sklearn, kita telah berhasil menghitung kesamaan (similarity) antar restoran. Kode di atas menghasilkan keluaran berupa matriks kesamaan dalam bentuk array. 

gambar similarity...........

Selanjutnya, mari kita lihat matriks kesamaan setiap resto dengan menampilkan nama restoran dalam 5 sampel kolom (axis = 1) dan 10 sampel baris (axis=0). Jalankan kode berikut.

###### Mendapatkan Rekomendasi


## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
