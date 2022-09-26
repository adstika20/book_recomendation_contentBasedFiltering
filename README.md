# Laporan Proyek Machine Learning - Ades Tikaningsih

## Project Overview 

**Latar Belakang**:

Membaca merupakan salah satu kegiatan yang lekat dengan kehidupan sehari-hari seseorang. Konsep utama dari membaca adalah memahami makna yang terkandung dalam sebuah teks. Terbukti bahwa orang yang memiliki kebiasaan membaca yang tinggi pasti memiliki wawasan yang luas, membaca dapat juga membuat seseorang mengenal, mengetahui serta memahami apa yang belum dikenal, diketahui dan dipahami. 

Oleh karena itu pemahaman seseorang terhadap pentingnya membaca merupakan hal yang penting untuk dipelajari. Namun perlu digaris bawahi bahwa membaca juga bisa menimbulkan bahaya, karena apa yang dibaca seseorang akan mempengaruhi karakter yang terbentuk dari pengetahuan yang ia dapat dari buku tersebut. Salah satu langkah yang ditempuh dalam menyediakan bahan bacaan adalah dengan memilah dan memilih jenis bacaan atau buku apa yang seharusnya dibaca, baik dengan mengenali Penulisnya, Kenali sinopsisnya dan lain sebagainya. Berdasarkan hal itu dengan kemajuan bidang ilmu pengetahuan dan  teknologi dibuatlah sebuah sistem rekomendasi yang berguna bagi pengguna internet yang mungkin merasa sulit untuk memilih dari banyak produk dan layanan yang tersedia. Sistem Rekomendasi dapat memprediksi seberapa besar kemungkinan pengguna target akan tertarik dengan item yang mungkin tidak diketahui olehnya. [[1]](https://aclanthology.org/C18-1033.pdf). 

Melihat pentingnya dampak buku bagi kehidupan kita serta banyaknya buku yang telah dan akan terbit, kita membutuhkan sistem rekomendasi yang akan menyaring buku - buku sesuai dengan selera dan ketertarikan kita. Dengan adanya sistem rekomendasi ini, kita tidak perlu lama - lama dalam mencari buku sesuai ketertarikan kita. Sistem rekomendasi sangat penting di beberapa industri karena dapat menghasilkan pendapatan dalam jumlah besar. Sebagai bukti pentingnya sistem pemberi rekomendasi, kami dapat menyebutkan bahwa, beberapa tahun yang lalu, Netflix mengadakan tantangan ("hadiah Netflix") di mana tujuannya adalah untuk menghasilkan sistem pemberi rekomendasi yang berkinerja lebih baik daripada algoritmanya sendiri dengan hadiah dari 1 juta dolar untuk menang.

## Business Understanding

Sistem rekomendasi buku adalah jenis sistem rekomendasi di mana kita harus merekomendasikan buku sejenis kepada pembaca berdasarkan minatnya. Sistem rekomendasi buku digunakan oleh situs online yang menyediakan ebook seperti google play books, open library, good Read's dan lain-lain.

### Problem Statements
Kembangkan sebuah sistem rekomendasi Buku untuk menjawab permasalahan berikut:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Dengan data rating yang Anda miliki, bagaimana merekomendasikan buku lain yang mungkin disukai dan belum pernah dibaca oleh pengguna? 

### Goals
Untuk  menjawab pertanyaan tersebut, buatlah sistem rekomendasi dengan tujuan atau goals sebagai berikut:
- Menghasilkan sejumlah rekomendasi Buku yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi Buku yang sesuai dengan preferensi pengguna dan belum pernah dibaca sebelumnya dengan teknik collaborative filtering.

**Solution statements**:

Pada latihan kali ini kita akan menggunakan dua metode yaitu content dan collaborative based filter yaitu :
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

Jumlah dataset buku 271360 baris 8 kolom, dan jumlah dataset rating 1149780 baris 3 kolom. Berdasarkan jumlah data rating dan books yang terbilang banyak, di sini saya hanya mengambil 10000 baris book dataset dan 5000 baris untuk rating dataset. 

Data Buku

![image](https://user-images.githubusercontent.com/110407053/192125666-a2ab4ddd-2228-4a79-8c1c-88ce35eef5b3.png)
Data Rating

![image](https://user-images.githubusercontent.com/110407053/192125641-d1c1bd8b-7153-4eb0-bb81-6c5d3b971cf2.png)

Pada dataset buku, ada beberapa kolom yang di hapus karena tidak diperlukan untuk proyek ini seperti URL gambar. 

Mengecek informasi pada dataset dengan fungsi info() berikut.

![image](https://user-images.githubusercontent.com/110407053/192125760-b76667e1-32e5-4821-9614-6b1620ae928d.png)

Berdasarkan informasi buku dataset memiliki 5 kolom dengan tipe object.

![image](https://user-images.githubusercontent.com/110407053/192125751-9d8f3903-394b-4be4-b502-0455e1958e0f.png)

Berdasarkan informasi rating dataset memiliki 2 kolom dengan tipe int64 yaitu user_id, rating dan 1 bertipe object yaitu ISBN

Dan kita akan menamai ulang kolom-kolom dari setiap file karena nama kolom tersebut berisi spasi, dan huruf kapital sehingga perlu diperbaiki agar mudah digunakan.

#### 2. Visualisasi data buku dan rating

![image](https://user-images.githubusercontent.com/110407053/192126113-b68c29d5-a43b-4ebf-8955-fbd4c07fe058.png)

Pada gambar diatas menunjukan bahwa kategori penulis (top 50) terbanyak adalah stephen king dengan total 70 buku 

![image](https://user-images.githubusercontent.com/110407053/192127390-b82f6f39-0f43-4502-8da7-6ca5a84a8dd9.png)

Pada gambar diatas menunjukan bahwa buku teratas (top 20) dengan judul The golden compass dengan jumlah 4 buku 

![image](https://user-images.githubusercontent.com/110407053/192127095-1cf41a45-670c-45f8-8522-7e3346f83a62.png)

Output diatas menunjukkan informasi sebagai berikut :
- Menghitung jumlah total rating 1116, jumlah rating explisit 485 dan jumlah rating implisit 631
- Feedback Implisit (rating implisit) adalah Suka dan tidak suka pengguna dicatat dan dicatat berdasarkan tindakannya seperti klik, pencarian, dan pembelian. Mereka ditemukan dalam jumlah besar tetapi umpan balik negatif tidak ditemukan.
- Feedback Eksplisit (rating implisit) adalah Pengguna menentukan suka atau tidak sukanya dengan tindakan seperti bereaksi terhadap item atau memberi peringkat. Ini memiliki umpan balik positif dan negatif tetapi jumlahnya lebih sedikit

## Data Preparation
Pada bagian akan menerapkan beberapa proses antara lain sebagai berikut :

**1. Cek missing value**

![image](https://user-images.githubusercontent.com/110407053/192125779-5fc21f42-fb35-4c25-b230-6073a0e7f376.png)
![image](https://user-images.githubusercontent.com/110407053/192125783-9d2f91d7-1a63-478e-ab9f-99f9a2de779e.png)

Data buku dan rating tidak memiliki missing value sehingga bisa diteruskan untuk proses selanjutnya.

**2. Membuang data duplikat**

Selanjutnya, proyek ini hanya akan menggunakan data unik untuk dimasukkan ke dalam proses pemodelan. Oleh karena itu, perlu menghapus data yang duplikat dengan fungsi drop_duplicates(). Proses ini dilakukan supaya dataset tetap memiliki integritas dan tidak berulang.

**3. konversi data series menjadi list**

Selanjutnya, kita perlu melakukan konversi data series menjadi list. Dalam hal ini, kita menggunakan fungsi tolist() dari library numpy. 

![image](https://user-images.githubusercontent.com/110407053/192132320-1f3f074b-9606-42b5-9352-387e4347fb87.png)

**4. Membuat dictionary**

Tahap berikutnya, kita akan membuat dictionary untuk menentukan pasangan key-value pada data book_ISBN, book_author, book_title dan book_year_of_publication yang telah kita siapkan sebelumnya.

![image](https://user-images.githubusercontent.com/110407053/192132323-15dc1450-f3c1-44ba-b227-cb44ce653692.png)


## Modeling

Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan dengan mengembangkan sistem rekomendasi dengan pendekatan content based filtering dan collaborative filtering.

#### 1. Model Development dengan Content Based Filtering

Ide dari sistem rekomendasi berbasis konten (content-based filtering) adalah merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi. Pada proyek ini model content based filtering hanya menggunakan data buku sedangkan data rating tidak diperlukan.

###### TF-IDF Vectorizer

TF-IDF adalah singkatan dari Term Frequency Inverse Document Frequency. Ini adalah algoritma yang sangat umum untuk mengubah teks menjadi representasi angka yang bermakna yang digunakan untuk menyesuaikan algoritma mesin untuk prediksi[[2](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a)].
Pada tahap ini, kita akan membangun sistem rekomendasi judul buku berdasarkan penulisnya. TfidfVectorizer dapat menangani nama-nama penulis seberapa sering mereka muncul dalam dokumen. 

![image](https://user-images.githubusercontent.com/110407053/192132335-1b2a50b4-b28f-4dca-83b0-f106a2a81e2b.png)


Selanjutnya, lakukan fit dan transformasi ke dalam bentuk matriks. 

Perhatikanlah, matriks yang kita miliki berukuran (10000, 5575). Nilai 10000 merupakan ukuran data dan 5575 merupakan nama penulis. Selanjutnya ubah tfid menjadi matriks dengan fungsi todense()

![image](https://user-images.githubusercontent.com/110407053/192132359-2f7e5f79-f3e9-45df-bb22-aa1eefe6e252.png)

Selanjutnya, mari kita lihat matriks tf-idf untuk beberapa judul buku dengan penulis buku. Sampai di sini, telah berhasil mengidentifikasi representasi fitur penting dari setiap judul buku dengan fungsi tfidfvectorizer. Kita juga telah menghasilkan matriks yang menunjukkan korelasi antara judul buku dengan penulis. Selanjutnya, kita akan menghitung derajat kesamaan antara satu buku dengan penulis lainnya untuk menghasilkan kandidat penulis yang akan direkomendasikan.

###### Cosine Similarity

Cosine Similarity mengukur kesamaan antara dua vektor ruang hasil kali dalam. Ini diukur dengan kosinus sudut antara dua vektor dan menentukan apakah dua vektor menunjuk ke arah yang kira-kira sama. [[3](https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8)] kita akan menghitung derajat kesamaan (similarity degree) antar judul buku dengan teknik cosine similarity. Di sini, kita akan menghitung cosine similarity dataframe tfidf_matrix yang kita peroleh pada tahapan sebelumnya. Dengan satu baris kode untuk memanggil fungsi cosine similarity dari library sklearn, kita telah berhasil menghitung kesamaan (similarity) antar judul buku. Menghasilkan keluaran berupa matriks kesamaan dalam bentuk array. 

![image](https://user-images.githubusercontent.com/110407053/192132374-272e6936-5c5a-477f-98ca-e6ced898481a.png)

Dengan cosine similarity, kita berhasil mengidentifikasi kesamaan antara satu buku dengan buku lainnya. Shape (10000, 10000) merupakan ukuran matriks similarity dari data yang kita miliki. Berdasarkan data yang ada, matriks di atas sebenarnya berukuran 10000 judul buku  x 10000 judul buku (masing-masing dalam sumbu X dan Y). Artinya, kita mengidentifikasi tingkat kesamaan pada 10000 judul buku. Tapi tentu kita tidak bisa menampilkan semuanya. Oleh karena itu, kita hanya memilih 10 judul buku pada baris vertikal dan 5 restoran pada sumbu horizontal seperti pada contoh di atas. 

![image](https://user-images.githubusercontent.com/110407053/192132384-776c057d-9c8c-41b1-b941-8ffee9776c20.png)


###### Mendapatkan Rekomendasi

Untuk mendaptkan rekomendasi, kita membuat fungsi author_recommendations dengan beberapa parameter sebagai berikut: 
*  i : sebagai judul buku (index kemiripan dataframe)
*  M : Dataframe mengenai similarity yang telah kita definisikan sebelumnya.
*  items : nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'book_title'  dan 'book_author'
*  k : banyak rekomendasi yang ingin diberikan

Dengan menggunakan argpartition, kita mengambil sejumlah nilai k tertinggi dari similarity data (dalam kasus ini: dataframe cosine_sim_df). Kemudian, kita mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam variabel closest. Berikutnya, kita perlu menghapus book_title' yang dicari agar tidak muncul dalam daftar rekomendasi. Dalam kasus ini, nanti kita akan mencari nama penulis dari judul buku "The Diaries of Adam and Eve" yang telah di baca, selain nama nanti akan keluar informasi ISBN, judul buku lain yang mirip , dan  tahun publikasi. Oleh karena itu, perlu drop terlebih dahulu 'book_title', 'book_author' agar tidak muncul dalam daftar rekomendasi yang diberikan nanti.  Buku "The Diaries of Adam and Eve" penulisnya adalah Mark Twain. Tentu kita berharap rekomendasi yang diberikan adalah judul buku dengan kategori yang mirip. Nah, sekarang, dapatkan judul buku recommendation dengan memanggil fungsi yang telah kita definisikan sebelumnya:

![image](![image](https://user-images.githubusercontent.com/110407053/192181265-d83d5cd9-f413-443a-b424-9f5d81bb1e66.png))

Berdasarkan output di atas ada 5 buku yaitu yang direkomendasikan sesuai dengan rekomendasi yang di minta sebelumnya.

#### 2. Model Development dengan Collaborative Filtering

Collaborative filtering bergantung pada pendapat komunitas pengguna. Ia tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten. Pada materi ini, kita akan menerapkan teknik collaborative filtering untuk membuat sistem rekomendasi. Teknik ini membutuhkan data rating dari user. 

Goal proyek kita kali ini adalah menghasilkan rekomendasi sejumlah buku yang sesuai dengan preferensi pengguna berdasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna, kita akan mengidentifikasi buku-buku yang mirip dan belum pernah dibaca oleh pengguna untuk direkomendasikan. Kita akan menggunakan teknik collaborative filtering untuk membuat rekomendasi ini. 

###### Data Preparation
Selanjutnya, pahami terlebih dahulu data rating yang kita miliki. Load data di awal dan membaca file ratings.csv. Selanjutnya  melakukan persiapan data untuk menyandikan (encode) fitur ‘user’ dan ‘user_id’ ke dalam indeks integer. Berikut adalah sebagian output-nya:

![image](https://user-images.githubusercontent.com/110407053/192146267-18984e31-c03e-43bf-aac9-de677386e87f.png)


Selanjutnya, lakukan hal yang sama pada fitur ‘ISBN’. Terakhir petakan ISBN dan user_id ke dataframe yang berkaitan. Output jumlah user, jumlah BUKU, dan mengubah nilai rating menjadi float.

![image](https://user-images.githubusercontent.com/110407053/192146479-cf897f6b-6c1a-4235-96e3-0cfbff2692e2.png)

Tahap persiapan telah selesai. Berikut adalah hal-hal yang telah kita lakukan pada tahap ini:

- Memahami data rating yang kita miliki.
- Menyandikan (encode) fitur ‘user_id’ dan ‘ISBN’ ke dalam indeks integer. 
- Memetakan ‘user_id’ dan ‘ISBN’ ke dataframe yang berkaitan.
- Mengecek beberapa hal dalam data seperti jumlah user, jumlah resto, kemudian mengubah nilai rating menjadi float.
- Terakhir menghitung min rating dan max rating
Tahap persiapan ini penting dilakukan agar data siap digunakan untuk pemodelan. 

###### Membagi Data untuk Training dan Validasi

Sebelum membagi data training dan validasi, perlu mengacak dataset terlebih dahulu agar distribusinya menjadi random.

![image](https://user-images.githubusercontent.com/110407053/192146756-53958519-98ad-470c-bad8-7eac523014d7.png)

Selanjutnya, kita bagi data train dan validasi dengan komposisi 70:30. Namun sebelumnya, kita perlu memetakan (mapping) data user dan buku menjadi satu value terlebih dahulu. Lalu, buatlah rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training. 

![image](https://user-images.githubusercontent.com/110407053/192146813-2567a043-87bc-4697-8020-8a699c8de48d.png)

Data telah siap untuk dimasukkan ke dalam model.

###### Proses Training
Pada tahap ini, model menghitung skor kecocokan antara pengguna dan buku dengan teknik embedding. Pertama, kita melakukan proses embedding terhadap data user dan buku. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan buku. Selain itu, kita juga dapat menambahkan bias untuk setiap user dan buku. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.

Di sini, kita membuat class RecommenderNet dengan keras Model class. Kode class RecommenderNet ini terinspirasi dari tutorial dalam situs [Keras](https://keras.io/examples/structured_data/collaborative_filtering_movielens/) dengan beberapa adaptasi sesuai kasus yang sedang kita selesaikan. 

## Evaluation

#### 1. Evaluation Model Development dengan Collaborative Filtering

Evaluasi dilakukan untuk mengetahui peforma akurasi dan error yang terjadi. RMSE Melihat perbedaan antara peringkat yang diprediksi oleh sistem pemberi rekomendasi dan peringkat aktual yang diberikan oleh pengguna. RMSE yang rendah menunjukkan bahwa sistem pemberi rekomendasi mampu memprediksi peringkat pengguna secara akurat[[4](https://medium.com/analytics-vidhya/loss-functions-to-evaluate-regression-models-8dac47e327e2)]. Saya menggunakan metode evaluasi RMSE untuk mencari jumlah dari kesalahan kuadrat atau selisih antara nilai sebenarnya dengan nilai prediksi yang telah ditentukan.  Rumus formula RMSE adalah sebagai berikut : 

![image](https://user-images.githubusercontent.com/110407053/192153091-af28de1e-434f-4c23-be7d-c33068bc7dfd.png)

Y ' = Nilai Prediksi 
Y   = Nilai Sejati
n    = Jumlah Data

Dengan mengggunakan matriks RMSE output dari modelnya adalah sebagai berikut.

![image](https://user-images.githubusercontent.com/110407053/192147072-634a2a0d-c611-4c26-8861-93efa8539707.png)


![image](https://user-images.githubusercontent.com/110407053/192147032-639ffb2a-3f83-4a2d-a8c9-8adde0cc539a.png)

Perhatikanlah, proses training model cukup baik dan model konvergen pada epochs sekitar 20. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.22 dan error pada data validasi sebesar 0.34. Nilai RMSE rendah menunjukkan bahwa variasi nilai yang dihasilkan oleh suatu model prakiraan mendekati variasi nilai obeservasinya. RMSE menghitung seberapa berbedanya seperangkat nilai. Semakin kecil nilai RMSE, semakin dekat nilai yang diprediksi dan diamati. Nilai tersebut cukup bagus untuk sistem rekomendasi. Mari kita cek, apakah model ini bisa membuat rekomendasi dengan baik.

![image](https://user-images.githubusercontent.com/110407053/192157169-db62c88a-feb2-41f5-a1a6-ed6d033b1228.png)

Selamat! Anda telah berhasil memberikan rekomendasi kepada user 277235 . dari output  kita dapat membandingkan antara  books_have_been_read_by_user (buku yang sudah pernah dibaca pengguna) dan Top 10 Book Recommendation for user.   

Perhatikanlah, beberapa buku rekomendasi menyediakan White Teeth: A Novel : Zadie Smith
Girl in Hyacinth Blue : Susan Vreeland yang sesuai dengan rating user / sudah pernah di baca pengguna.

Kita memperoleh rekomendasi judul buku beserta penulisnya yaitu buku White Teeth: A Novel : Zadie Smith
Girl in Hyacinth Blue : Susan Vreeland

Prediksi yang dihasilkan cukup sesuai. Sampai di tahap ini, Anda telah berhasil membuat sistem rekomendasi dengan dua teknik, yaitu Content based Filtering dan Collaborative Filtering. Sistem rekomendasi yang Anda buat telah berhasil memberikan sejumlah rekomendasi buku yang sesuai dengan preferensi pengguna. 

#### 2. Evaluation Model Development dengan Content Based Filtering

Matik evaluasi untuk model berbasis konten dengan menghitung jumlah buku yang di rekomendasikan sesuai dengan penulis/jumlah buku yang ditulis oleh penulis yang sama. 

![image](https://user-images.githubusercontent.com/110407053/192157742-71e61641-92b3-4037-b584-3f10ccb81bf2.png)


- Variabel books_that_have_been_read_row di bawah ini akan mengambil satu row dari buku yang pernah dibaca sebelumnya, dan 
- variabel books_that_have_been_read_author adalah penulis buku dari buku yang pernah dibaca sebelumnya
- Variabel books_with_the_same_author menunjukkan jumlah buku yang sudah ditulis oleh penulis buku yang berasal dari buku yang pernah dibaca sebelumnya
- Ternyata buku yang telah ditulis oleh Mark Twain berjumlah 16 buku. Jadi jumlah akurasi dari model adalah 31, 25 %

Sampai di tahap ini, proyek ini telah berhasil membuat sistem rekomendasi dengan dua teknik, yaitu Content based Filtering dan Collaborative Filtering. Sistem rekomendasi yang telah dibuat berhasil memberikan sejumlah rekomendasi buku yang sesuai dengan preferensi pengguna. 

## REFERENCES

[[1](https://aclanthology.org/C18-1033.pdf)] Haifa , . I. Diana and S. Stan , "Authorship Identification for Literary Book Recommendations," Proceedings of the 27th International Conference on Computational Linguistics, p. 390–400, 2018.

[[2](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a)] Chaudhary, "TF-IDF Vectorizer scikit-learn," 2020. [Online]. Available: https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a.

[[3](https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8.)] Mantur, "Book Recommender System," Juny 2021. [Online]. Available: https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8.

[[4](https://medium.com/analytics-vidhya/loss-functions-to-evaluate-regression-models-8dac47e327e2)]P. Muniraj, "Loss functions to evaluate Regression Models," 18 December 2021. [Online]. Available: Loss functions to evaluate Regression Models.

