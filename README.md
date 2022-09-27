# Laporan Proyek Machine Learning - Ades Tikaningsih

## Project Overview 

**Latar Belakang**:

Membaca merupakan salah satu kegiatan yang lekat dengan kehidupan sehari-hari seseorang. Konsep utama dari membaca adalah memahami makna yang terkandung dalam sebuah teks. Terbukti bahwa orang yang memiliki kebiasaan membaca yang tinggi pasti memiliki wawasan yang luas, membaca dapat juga membuat seseorang mengenal, mengetahui serta memahami apa yang belum dikenal, diketahui dan dipahami. 

Oleh karena itu pemahaman seseorang terhadap pentingnya membaca merupakan hal yang penting untuk dipelajari. Namun perlu digaris bawahi bahwa membaca juga bisa menimbulkan bahaya, karena apa yang dibaca seseorang akan mempengaruhi karakter yang terbentuk dari pengetahuan yang ia dapat dari buku tersebut. Salah satu langkah yang ditempuh dalam menyediakan bahan bacaan adalah dengan memilah dan memilih jenis bacaan atau buku apa yang seharusnya dibaca, baik dengan mengenali Penulisnya, Kenali sinopsisnya dan lain sebagainya. Berdasarkan hal itu dengan kemajuan bidang ilmu pengetahuan dan  teknologi dibuatlah sebuah sistem rekomendasi yang berguna bagi pengguna internet yang mungkin merasa sulit untuk memilih dari banyak produk dan layanan yang tersedia. Sistem Rekomendasi dapat memprediksi seberapa besar kemungkinan pengguna target akan tertarik dengan item yang mungkin tidak diketahui olehnya. [[1]](https://aclanthology.org/C18-1033.pdf). 

Melihat pentingnya dampak buku bagi kehidupan kita serta banyaknya buku yang telah dan akan terbit, kita membutuhkan sistem rekomendasi yang akan menyaring buku - buku sesuai dengan selera dan ketertarikan kita. Dengan adanya sistem rekomendasi ini, kita tidak perlu lama - lama dalam mencari buku sesuai ketertarikan kita. Sistem rekomendasi sangat penting di beberapa industri karena dapat menghasilkan pendapatan dalam jumlah besar. Sebagai bukti pentingnya sistem pemberi rekomendasi, kami dapat menyebutkan bahwa, beberapa tahun yang lalu, _Netflix_ mengadakan tantangan ("hadiah _Netflix_") di mana tujuannya adalah untuk menghasilkan sistem pemberi rekomendasi yang berkinerja lebih baik daripada algoritmanya sendiri dengan hadiah dari 1 juta dolar untuk menang.

## Business Understanding

Sistem rekomendasi buku adalah jenis sistem rekomendasi di mana kita harus merekomendasikan buku sejenis kepada pembaca berdasarkan minatnya. Sistem rekomendasi buku digunakan oleh situs online yang menyediakan ebook seperti _google play books_, _open library_, _good Read's_ dan lain-lain.

### Problem Statements
Kembangkan sebuah sistem rekomendasi Buku untuk menjawab permasalahan berikut:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik _content-based filtering_?
- Dengan data rating yang Anda miliki, bagaimana merekomendasikan buku lain yang mungkin disukai dan belum pernah dibaca oleh pengguna? 

### Goals
Untuk  menjawab pertanyaan tersebut, buatlah sistem rekomendasi dengan tujuan atau goals sebagai berikut:
- Menghasilkan sejumlah rekomendasi Buku yang dipersonalisasi untuk pengguna dengan teknik _content-based filtering_.
- Menghasilkan rekomendasi sejumlah buku yang sesuai dengan preferensi pengguna berdasarkan rating dan belum pernah dibaca sebelumnya dengan teknik _collaborative filtering_.

**Solution statements**:

Pada latihan kali ini kita akan menggunakan dua metode yaitu _content_ dan _collaborative based filter_ yaitu :
- Pada _Content Based Flter_, kita akan menggunakan penulis buku menjadi pusat sebagai pusat dari sistem rekomendasi. 
Dalam algoritma ini, kami mencoba menemukan item pencarian yang mirip. Misalnya, seseorang suka menonton bidikan Sachin Tendulkar, maka dia mungkin juga suka menonton bidikan _Ricky Ponting_ karena kedua video tersebut memiliki tag dan kategori yang mirip.
- Pada _Collaborative Based Flter_, kita akan menggunakan penilaian dari berbagai pengguna sebagai pusat dari sistem rekomendasi. Sistem pemberi rekomendasi penyaringan berbasis kolaboratif didasarkan pada interaksi pengguna dan item target sebelumnya. Dengan kata sederhana di sini, kami mencoba mencari pelanggan yang mirip dan menawarkan produk berdasarkan apa yang mereka pilih.

## Data Understanding

Kali ini pada pembuatan sistem rekomendasi, saya menggunakan Book Recommendation Dataset dari Kaggle. Dataset bisa diunduh [disini](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset).   
Dataset _Book Recommendation_ memiliki 2 file antara lain :

- Buku

Pada file buku terdapat beberapa variabel-variabel yaitu :
1. ISBN untuk mengidentifikasi jenis-jenis buku
2. Book-Title : Judul buku yang menerima ulasan pembaca,
3. Book-Author : Penulis buku yang menerima ulasan pembaca
4. Year-Of-Publication : Tahun publikasi buku
5. Publisher : Nama penerbit buku
6. Image-URL-S: URL menautkan gambar sampul buku yang mengarah ke situs web Amazon dengan ukuran kecil(S)
8. Image-URL-M: URL menautkan gambar sampul buku yang mengarah ke situs web Amazon dengan ukuran sedang(M)
9. Image-URL-L: URL menautkan gambar sampul buku yang mengarah ke situs web Amazon dengan ukuran besar(L)

Gambar di bawah ialah salah satu contoh sampul buku yang di akses menggunakan URL di atas, Image-URL-S  

![image](https://user-images.githubusercontent.com/110407053/192336996-f54dcccf-7055-44eb-9320-36630988389f.png)

- Rating

Pada file rating terdapat beberapa variabel-variabel yaitu :
1. user_id : Id pengguna yang telah membaca dan memberi rating
2. ISBN : untuk mengidentifikasi jenis-jenis buku
3. rating: Peringkat ( Book-Rating) baik eksplisit, dinyatakan dalam skala 1-10 (nilai yang lebih tinggi menunjukkan apresiasi yang lebih tinggi), atau implisit, dinyatakan dengan 0.

Kemudian jumlah dataset buku ada 271360 baris 8 kolom, dan jumlah dataset rating ada 1149780 baris 3 kolom. Berdasarkan jumlah data rating dan books yang terbilang banyak, di sini saya hanya mengambil 10000 baris book dataset dan 5000 baris untuk rating dataset. Setelah memahami variabel setiap data kemudian ada beberapa proses lain yaitu :

#### 1. Melihat dataset

Melihat book dataset dan rating dataset menggunakan fungsi head().

Data Buku

|ISBN|book_title|book_author|book_year_of_publication|Publisher|Image-URL-S|Image-URL-M|Image-URL-L|			
|----|----------|-----------|------------------------|---------|-----------|-----------|-----------|
|0195153448|Classical Mythology|Mark P. O.|Morford|2002|Oxford University Press|http://images.amazon.com/images/P/0195153448.0|http://images.amazon.com/images/P/0195153448.0|http://images.amazon.com/images/P/0195153448.0|
|0002005018|Clara Callan|Richard Bruce Wright|2001|HarperFlamingo Canada|http://images.amazon.com/images/P/0002005018.0|http://images.amazon.com/images/P/0002005018.0|http://images.amazon.com/images/P/0002005018.0|
|0060973129|Decision in Normandy|Carlo D'Este|1991|HarperPerennial|http://images.amazon.com/images/P/0060973129.0|http://images.amazon.com/images/P/0060973129.0|http://images.amazon.com/images/P/0060973129.0|
|0374157065|Flu: The Story of the Great Influenza Pandemic|Gina Bari Kolata|1999|Farrar Straus Giroux|http://images.amazon.com/images/P/0374157065.0|	http://images.amazon.com/images/P/0374157065.0|http://images.amazon.com/images/P/0374157065.0|
|0393045218|The Mummies of Urumchi|E. J. W. Barber|1999|W. W. Norton &amp; Company|http://images.amazon.com/images/P/0393045218.0|http://images.amazon.com/images/P/0393045218.0|http://images.amazon.com/images/P/0393045218.0|

Output diatas menampilkan data-data yang terdapat pada dataset buku.

Data Rating

|User-ID|ISBN	|Book-Rating|
|-------|-----|-----------|
|276725|034545104X|0|
|276726|0155061224|5|
|276727|0446520802|0|
|276729|052165615X|3|
|276729	|0521795028|6|
	
Menampilkan user_id, ISBN buku dan jumlah rating pada buku.

Mengecek informasi pada dataset dengan fungsi info() berikut.



<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10000 entries, 0 to 9999
Data columns (total 8 columns):
 |#| Column | Non-Null Count | Dtype |
 |-| ------ | -------------- | ----- |
 |0| ISBN |                10000 non-null | object |
 |1| Book-Title |          10000 non-null | object |
 |2|   Book-Author |         10000 non-null | object |
 |3|   Year-Of-Publication|  10000 non-null | object |
 |4|   Publisher |           10000 non-null | object |
 |5|   Image-URL-S |         10000 non-null | object |
 |6|   Image-URL-M |        10000 non-null | object |
 |7|   Image-URL-L |          10000 non-null | object |
dtypes: object(8)
memory usage: 625.1+ KB


# melihat info dataset buku
rating_dataset.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5000 entries, 0 to 4999
Data columns (total 3 columns):
 #   Column       Non-Null Count  Dtype 
---  ------       --------------  ----- 
 0   User-ID      5000 non-null   int64 
 1   ISBN         5000 non-null   object
 2   Book-Rating  5000 non-null   int64 
dtypes: int64(2), object(1)
memory usage: 117.3+ KB





Berdasarkan informasi buku dataset memiliki 5 kolom dengan tipe object yaitu ISBN, title, author, year_of_publication dan publisher.

![image](https://user-images.githubusercontent.com/110407053/192125751-9d8f3903-394b-4be4-b502-0455e1958e0f.png)

Berdasarkan informasi rating dataset memiliki 2 kolom dengan tipe int64 yaitu user_id, rating dan 1 bertipe object yaitu ISBN

Selanjutnya kita perlu menamai ulang kolom-kolom dari setiap file karena nama kolom tersebut berisi spasi, dan huruf kapital sehingga perlu diperbaiki agar mudah digunakan. Semua nama kolom pada dataset buku dan dataset rating di ubah menggunakan fungsi rename(). Selain itu, pada dataset buku ada beberapa kolom yang di hapus dengan fungsi drop() karena tidak diperlukan untuk proyek ini seperti kolom Image-URL-S,Image-URL-M,Image-URL-L. 

#### 2. Visualisasi data buku dan rating

![image](https://user-images.githubusercontent.com/110407053/192126113-b68c29d5-a43b-4ebf-8955-fbd4c07fe058.png)

Gambar 1. Top Author

Top 50 author menggunakan px.bar, setiap baris DataFrame direpresentasikan sebagai tanda persegi panjang dapat dilihat pada Gambar 1. Gambar 1 menunjukan bahwa kategori penulis (top 50) terbanyak adalah stephen king dengan jumlah 70 buku 

![image](https://user-images.githubusercontent.com/110407053/192127390-b82f6f39-0f43-4502-8da7-6ca5a84a8dd9.png)

Gambar 2. Top Book

Top 20 book menggunakan px.bar, setiap baris DataFrame direpresentasikan sebagai tanda persegi panjang dapat dilihat pada Gambar 2. Gambar 2 menunjukan bahwa buku teratas (top 20) diraih dengan judul The golden compass dengan jumlah 4 buku. 

![image](https://user-images.githubusercontent.com/110407053/192127095-1cf41a45-670c-45f8-8522-7e3346f83a62.png)

Gambar 3. Rating distribution

Distribusi rating menggunakan Bart chart dapat dilihat pada Gambar 3. Pada Gambar 3, sebagian besar pengguna memberi rating 8 sejumlah lebih dari 120, ada beberapa informasi lain seperti :
- Menghitung jumlah total rating 1116, jumlah rating explisit 485 dan jumlah rating implisit 631
- _Feedback Implisit_ (rating implisit) adalah Suka dan tidak suka pengguna dicatat dan dicatat berdasarkan tindakannya seperti klik, pencarian, dan pembelian. Mereka ditemukan dalam jumlah besar tetapi umpan balik negatif tidak ditemukan.
- _Feedback Eksplisit_ (rating implisit) adalah Pengguna menentukan suka atau tidak sukanya dengan tindakan seperti bereaksi terhadap item atau memberi peringkat. Ini memiliki umpan balik positif dan negatif tetapi jumlahnya lebih sedikit

## Data Preparation
Pada bagian akan menerapkan beberapa proses antara lain sebagai berikut :

**1. Cek missing value**

Selanjutnya, mari kita cek lagi datanya apakah ada missing value atau tidak. Karena datanya terdiri dari ratusan bahkan ribuan baris tentu akan susah dalam menemukan nilai field yang kosong. Oleh karena itu, Pandas memungkinkan kita dapat menemukan missing value secara cepat dengan fungsi isna() dan sum(). Fungsi isna() untuk mengidentifikasi nilai yang hilang, dan fungsi sum() untuk menghitungnya.

![image](https://user-images.githubusercontent.com/110407053/192125779-5fc21f42-fb35-4c25-b230-6073a0e7f376.png)

![image](https://user-images.githubusercontent.com/110407053/192125783-9d2f91d7-1a63-478e-ab9f-99f9a2de779e.png)

Data buku dan rating tidak memiliki _missing value_ sehingga bisa diteruskan untuk proses selanjutnya.

**2. Melihat jumlah data buku rate 10**

Meneliti buku-buku yang di rate 10 oleh pengguna menggunakan dataset rating berdasarkan perbandingan ISBN buku dan nilai maksimal rating. Ternyata diperoleh sejumlah 300 buku yang dapat dikatakan best book. Karena proyek ini hanya akan menggunakan data unik untuk dimasukkan ke dalam proses pemodelan. Oleh karena itu, perlu menghapus data yang duplikat dengan fungsi drop_duplicates(). Proses ini dilakukan supaya dataset tetap memiliki integritas dan tidak berulang.

**3. konversi data series menjadi list**

Selanjutnya, kita perlu melakukan konversi data series menjadi list (daftar). Dalam hal ini, kita menggunakan fungsi tolist() dari library numpy. Data yang dikonversi adalah dataset buku
- Mengonversi data series ‘ISBN’ menjadi dalam bentuk list
- Mengonversi data series ‘title’ menjadi dalam bentuk list
- Mengonversi data series ‘author’ menjadi dalam bentuk list
- Mengonversi data series ‘year_of_publication’ menjadi dalam bentuk list
Setelah membuat list selanjutnya, kita akan membuat dictionary untuk menentukan pasangan key-value pada data book_ISBN, book_author, book_title dan book_year_of_publication yang telah kita siapkan sebelumnya. 

**4. Encode user_id**

Proses ini dilakukan pada metode _collaborative filtering_ dengan persiapan data untuk menyandikan (encode) fitur ‘user’ dan ‘user_id’ ke dalam indeks integer. Selanjutnya, lakukan hal yang sama pada fitur ‘ISBN’. Terakhir petakan ISBN dan user_id ke dataframe yang berkaitan. Output jumlah user, jumlah BUKU, dan mengubah nilai rating menjadi float.

![image](https://user-images.githubusercontent.com/110407053/192146479-cf897f6b-6c1a-4235-96e3-0cfbff2692e2.png)

Tahap persiapan telah selesai. Berikut adalah hal-hal yang telah kita lakukan pada tahap ini:

- Memahami data rating yang kita miliki.
- Menyandikan (encode) fitur ‘user_id’ dan ‘ISBN’ ke dalam indeks integer. 
- Memetakan ‘user_id’ dan ‘ISBN’ ke dataframe yang berkaitan.
- Mengecek beberapa hal dalam data seperti jumlah user, jumlah resto, kemudian mengubah nilai rating menjadi float.
- Terakhir menghitung min rating dan max rating
Tahap persiapan ini penting dilakukan agar data siap digunakan untuk pemodelan. 

## Modeling

Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan dengan mengembangkan sistem rekomendasi dengan pendekatan content based filtering dan collaborative filtering.

#### 1. Model Development dengan Content Based Filtering

Ide dari sistem rekomendasi berbasis konten (content-based filtering) adalah merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi. Pada proyek ini model content based filtering hanya menggunakan data buku sedangkan data rating tidak diperlukan. Berikut prosesnya :

###### TF-IDF Vectorizer

TF-IDF adalah singkatan dari Term Frequency Inverse Document Frequency. Ini adalah algoritma yang sangat umum untuk mengubah teks menjadi representasi angka yang bermakna yang digunakan untuk menyesuaikan algoritma mesin untuk prediksi[[2](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a)].
Pada tahap ini, kita akan membangun sistem rekomendasi judul buku berdasarkan penulisnya. TfidfVectorizer dapat menangani nama-nama penulis seberapa sering mereka muncul dalam dokumen. Selanjutnya, lakukan fit dan transformasi ke dalam bentuk matriks. hasil yang diperoleh adalah matriks yang berukuran (10000, 5575). Nilai 10000 merupakan ukuran data dan 5575 merupakan nama penulis. Selanjutnya ubah tfid menjadi matriks dengan fungsi todense(). Sampai di sini, telah berhasil mengidentifikasi representasi fitur penting dari setiap judul buku dengan fungsi tfidfvectorizer. Kita juga telah menghasilkan matriks yang menunjukkan korelasi antara judul buku dengan penulis. Selanjutnya, kita akan menghitung derajat kesamaan antara satu buku dengan penulis lainnya untuk menghasilkan kandidat penulis yang akan direkomendasikan.

###### Cosine Similarity

Cosine Similarity mengukur kesamaan antara dua vektor ruang hasil kali dalam. Ini diukur dengan kosinus sudut antara dua vektor dan menentukan apakah dua vektor menunjuk ke arah yang kira-kira sama. [[3](https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8)] kita akan menghitung derajat kesamaan (similarity degree) antar judul buku dengan teknik cosine similarity. Di sini, kita akan menghitung cosine similarity dataframe tfidf_matrix yang kita peroleh pada tahapan sebelumnya. Dengan satu baris kode untuk memanggil fungsi cosine similarity dari library sklearn, kita telah berhasil menghitung kesamaan (similarity) antar judul buku. Menghasilkan keluaran berupa matriks kesamaan dalam bentuk array. 

Dengan cosine similarity, kita berhasil mengidentifikasi kesamaan antara satu buku dengan buku lainnya. Shape (10000, 10000) merupakan ukuran matriks similarity dari data yang kita miliki. Berdasarkan data yang ada, matriks di atas sebenarnya berukuran 10000 judul buku  x 10000 judul buku (masing-masing dalam sumbu X dan Y). Artinya, kita mengidentifikasi tingkat kesamaan pada 10000 judul buku. Tapi tentu kita tidak bisa menampilkan semuanya. Oleh karena itu, kita hanya memilih 10 judul buku pada baris vertikal dan 5 buku pada sumbu horizontal seperti pada contoh di atas. 

###### Mendapatkan Rekomendasi
 
Sebelum melakukan rekomendasi, kita membuat fungsi author_recommendations dengan beberapa parameter sebagai berikut: 
 *  i : sebagai judul buku (index kemiripan dataframe)
*   M : Dataframe mengenai similarity yang telah kita definisikan sebelumnya.
*   items : nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini  adalah 'book_title'  dan 'book_author'
*  k  : banyak rekomendasi yang ingin diberikan
 
Dengan menggunakan argpartition, kita mengambil sejumlah nilai k tertinggi dari si milarity data (dalam kasus ini: dataframe cosine_sim_df). Kemudian, kita mengambil  data dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam  variabel closest. Berikutnya, kita perlu menghapus book_title' yang dicari agar tidak  muncul dalam daftar rekomendasi. Dalam kasus ini, nanti kita akan mencari nama penulis  dari judul buku "The Diaries of Adam and Eve" yang telah di baca _user_. Oleh karena itu, perlu drop terlebih dahulu 'book_title', 'book_author' agar tidak muncul dalam daftar rekomendasi yang diberikan nanti. Berikut ini output rekomendasi judul buku "The Diaries of Adam and Eve".

|book_ISBN|book_title|book_author|book_year_of_publication|
|---------|----------|-----------|------------------------|
|0965881199|The Diaries of Adam and Eve|Mark Twain|1998|

Tabel 1. Rekomendasi Buku metode Content Based Filtering

Tabel 1 menginformasikan rekomendasi Buku "The Diaries of Adam and  Eve" ditulis oleh penulis bernama Mark Twain, ISBN 0965881199 dan dipublikasi tahun 1998.
Tentu kita berharap rekomendasi yang diberikan  adalah judul buku dengan kategori yang mirip. Nah, sekarang, dapatkan judul buku  recommendation dengan memanggil fungsi yang telah kita definisikan sebelumnya:
 
|book_title|book_author|
|----------|-----------|
|ADVENTURES OF HUCKLEBERRY FINN (ENRICHED CLASS|Mark Twain|
|Adventures of Huckleberry Finn|Mark Twain|
|The Complete Short Stories of Mark Twain|Mark Twain|
|Treasury of Illustrated Classics: Adventures|Mark Twain|
|A Connecticut Yankee in King Arthur's Court|Mark Twain|

Tabel 2. Top 5 Recommendation Content Based Filtering

Berdasarkan Tabel 2 di atas sistem merekomendasikan top 5 buku dengan judul buku "The Di aries of Adam and Eve" dengan penulis yang sama yaitu Mark Twain yang direkomendasikan sesuai dengan rekomendasi yang di minta sebelumnya.
 
#### 2. Model Development dengan Collaborative Filtering
 
Setelah sebelumnya dilakukan prosen  Mengubah userID menjadi list, kemudian Mapping us erID ke dataframe user Mapping ISBN ke dataframe BOOK maka saatnya bagian pem odelan. Collaborative filtering bergantung pada pendapat komunitas pengguna. Ia tidak  memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten. Pada  materi ini, kita akan menerapkan teknik collaborative filtering untuk membuat sistem  rekomendasi. Teknik ini membutuhkan data rating dari user. Tahapan pemodelan proyek  ini menggunakan teknik RecommenderNet. 
 
Dari data rating pengguna, kita akan mengidentifikasi buku-buku yang mirip dan belum pernah dibaca oleh pengguna untuk direkomendasikan. Kita akan menggunakan teknik  collaborative filtering untuk membuat rekomendasi ini. 
 
###### Membagi Data untuk Training dan Validasi
 
Sebelum membagi data training dan validasi, perlu mengacak dataset terlebih dahulu ag ar distribusinya menjadi random. Selanjutnya, kita bagi data train dan validasi dengan komposisi 70:30. Namun se belumnya, kita perlu memetakan (mapping) data user dan buku menjadi satu value  terlebih dahulu. Lalu, buatlah rating dalam skala 0 sampai 1 agar mudah dalam  melakukan proses training. 
 
###### Proses Training
Pada tahap ini, model menghitung skor kecocokan antara pengguna dan buku dengan tek nik embedding. Pertama, kita melakukan proses embedding terhadap data user dan buku.  Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan buku.  Selain itu, kita juga dapat menambahkan bias untuk setiap user dan buku. Skor  kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.
 
Di sini, kita membuat class RecommenderNet dengan keras Model class. Kode class RecommenderNet ini terinspirasi dari tutorial dalam situs [keras](https://keras.io/examples/structured_data/collaborative_filtering_movielens/). 
   
 
###### Top-N recommendation
 
Setelah dilakukan proses compile dan train model maka saatnya mendapatkan rekomendasi untuk menghasilkan rekomendasi sejumlah buku yang sesuai dengan preferensi pengguna ber dasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna, kita akan  mengidentifikasi buku-buku yang mirip dan belum pernah dibaca oleh pengguna untuk  direkomendasikan. Berikut outputnya :
 
![image](https://user-images.githubusercontent.com/110407053/192473664-826be691-9764-43cf-8b50-28c74d3a036c.png)

Gambar 4. Rekomendasi buku dengan teknik Collaborative Filtering

Pada output di atas kita telah berhasil memberikan rekomendasi kepada user 277235. dari output  kita dapat membandingkan antara  books_have_been_read_by_user (buku yang  sudah pernah dibaca pengguna) yaitu buku "The Pelican Brief" penulisnya "John Grisham"  dan Kita memperoleh rekomendasi judul buku Top 10 Book Recommendation untuk user yaitu  ada 3 kategori buku yang belum pernah dibaca yaitu  buku "A Time to Kill : JOHN  GRISHAM","The Client : John Grisham" , "The Pelican Brief : John Grisham"


 
## Evaluation
 
#### 1. Evaluation Model Development dengan Collaborative Filtering
 
Evaluasi dilakukan untuk mengetahui peforma akurasi dan error yang terjadi. RMSE Melihat perbedaan antara peringkat yang diprediksi oleh sistem pemberi rekomendasi dan  peringkat aktual yang diberikan oleh pengguna. RMSE yang rendah menunjukkan bahwa  sistem pemberi rekomendasi mampu memprediksi peringkat pengguna secara akurat. Saya menggunakan metode evaluasi RMSE untuk mencari jumlah dari  kesalahan kuadrat atau selisih antara nilai sebenarnya dengan nilai prediksi yang  telah ditentukan.  Rumus formula RMSE adalah sebagai berikut : 

![image](https://user-images.githubusercontent.com/110407053/192476524-3352009a-cc22-4a6b-bb98-817058df7b9f.png)

Y  ' = Nilai Prediksi 
Y    = Nilai Sejati
n     = Jumlah Data
 
Hasil training menggunakan metrik RMSE 
 
![image](https://user-images.githubusercontent.com/110407053/192476254-c691342b-092e-4c1f-8f80-901773c31a68.png)

Gambar 4. Training model
 
![image](https://user-images.githubusercontent.com/110407053/192476092-abf9dc5d-5b3a-4360-b871-dabfe204eab1.png)

Gambar 4. Visualisasi Matrik 

Perhatikanlah hasil training model pada gambar 4, proses training model cukup baik dan model konvergen pada epochs se kitar 20. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.22% dan  error pada data validasi sebesar 0.34%. Nilai RMSE rendah menunjukkan bahwa variasi  nilai yang dihasilkan oleh suatu model prakiraan mendekati variasi nilai  obeservasinya. RMSE menghitung seberapa berbedanya seperangkat nilai. Semakin kecil  nilai RMSE, semakin dekat nilai yang diprediksi dan diamati. Nilai tersebut cukup  bagus untuk sistem rekomendasi. Untuk memudahkan dalam memahami hasil training dapat dilihat pada gambar 5 visualisasi model metric.

Seperti yang telah dijelaskan di tahap pemodelan menggunakan Collaborative Filtering, mari kita mencoba kembali merekomendasi buku yang sesuai dengan preferensi pengguna berdasarkan rating  yang telah diberikan sebelumnya.
 
![image](https://user-images.githubusercontent.com/110407053/192476731-688d534d-00b5-4d37-adfa-3989422dc279.png)
 
Pada output di atas kita telah berhasil memberikan rekomendasi kepada user 277235. dari output  kita dapat membandingkan antara  books_have_been_read_by_user (buku yang  sudah pernah dibaca pengguna) yaitu buku "The Pelican Brief" penulisnya "John Grisham"  dan Kita memperoleh rekomendasi judul buku Top 10 Book Recommendation untuk user yaitu  ada 3 kategori buku yang belum pernah dibaca yaitu  buku "A Time to Kill : JOHN  GRISHAM","The Client : John Grisham" , "The Pelican Brief : John Grisham"
 
Prediksi yang dihasilkan cukup sesuai. Sampai di tahap ini, Anda telah berhasil me mbuat sistem rekomendasi dengan dua teknik, yaitu Content based Filtering dan  Collaborative Filtering. Sistem rekomendasi yang Anda buat telah berhasil memberikan  sejumlah rekomendasi buku yang sesuai dengan preferensi pengguna. 
 
#### 2. Evaluation Model Development dengan Content Based Filtering

Matrik evaluasi dalam sistem rekomendasi metode Content Based Filtering menggunakan precision. Precision adalah jumlah item rekomendasi yang relevan.
Rumus precision

![image](https://user-images.githubusercontent.com/110407053/192476856-f0e90012-bbf9-48fd-ad8e-5ef8bfd4d0b2.png)

Contoh cara kerja precision sistem memberi 5 item untuk direkomendasikan pada pengguna. Kemudian, dari 5 item itu, ada 3 yang relevan. Maka presisinya jadi 60%. 
Pada proyek ini kita akan mencari rekomendai nama penulis dari judul buku "The Diaries of Adam and Eve" yang telah di baca. 

|book_ISBN|book_title|book_author|book_year_of_publication|
|---------|----------|-----------|------------------------|
|0965881199|The Diaries of Adam and Eve|Mark Twain|1998|

Tabel 3. Rekomendasi buku dengan teknik Content Based Filtering

Dari hasil rekomendasi di atas, diketahui buku "The Diaries of Adam and Eve" penulisnya adalah Mark Twain. Tentu kita berharap rekomendasi yang diberikan adalah judul buku dengan kategori yang mirip. Nah, sekarang, dapatkan judul buku recommendation dengan memanggil fungsi yang telah kita definisikan sebelumnya:

|book_title|book_author|
|----------|-----------|
|ADVENTURES OF HUCKLEBERRY FINN (ENRICHED CLASS|Mark Twain|
|Adventures of Huckleberry Finn|Mark Twain|
|The Complete Short Stories of Mark Twain|Mark Twain|
|Treasury of Illustrated Classics: Adventures|Mark Twain|
|A Connecticut Yankee in King Arthur's Court|Mark Twain|

Tabel 5. Rekomendasi buku top 5 dengan teknik Content Based Filtering

Semua item yang direkomendasikan memiliki penulis yang sama yaitu Mark Twain (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.
atau dapat ditulis 
Precission = 5/5.
Jadi presisinya = 100%

Selain itu, ada metode lain untuk evaluasi untuk model berbasis konten dengan menghitung jumlah buku yang di rekomendasikan sesuai dengan penulis/jumlah buku yang ditulis oleh penulis yang sama. 

- Variabel books_that_have_been_read_row di bawah ini akan mengambil satu row dari buku yang pernah dibaca sebelumnya, dan 
- variabel books_that_have_been_read_author adalah penulis buku dari buku yang pernah dibaca sebelumnya
- Variabel books_with_the_same_author menunjukkan jumlah buku yang sudah ditulis oleh penulis buku yang berasal dari buku yang pernah dibaca sebelumnya
- Ternyata buku yang telah ditulis oleh Mark Twain berjumlah 16 buku. Jadi jumlah akurasi dari model adalah 31, 25 %

## KESIMPULAN 
Disimpulkan bahwa penggunaan metode collaborative filtering dan Content based Filtering dapat memberikan suatu saran rekomendasi kepada user secara efektif. Dengan teknik Content based Filtering telah berhasil menghasilkan sejumlah rekomendasi Buku yang dipersonalisasi untuk pengguna. Dan dengan teknik Collaborative Filtering telah berhasil Menghasilkan rekomendasi sejumlah buku yang sesuai dengan preferensi pengguna berdasarkan rating dan belum pernah dibaca sebelumnya.  Selain itu, dengan menggunakan beberapa metrik evaluasi, kita dapat mulai menilai kinerja model lebih dari sekadar relevansi.


## REFERENCES

[[1](https://aclanthology.org/C18-1033.pdf)] Haifa , . I. Diana and S. Stan , "Authorship Identification for Literary Book Recommendations," Proceedings of the 27th International Conference on Computational Linguistics, p. 390–400, 2018.

[[2](https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a)] Chaudhary, "TF-IDF Vectorizer scikit-learn," 2020. [Online]. Available: https://medium.com/@cmukesh8688/tf-idf-vectorizer-scikit-learn-dbc0244a911a.

[[3](https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8)] Mantur, "Book Recommender System," Juny 2021. [Online]. Available: https://medium.com/@manturdipa/book-recommender-system-ec8bbaa983a8.


