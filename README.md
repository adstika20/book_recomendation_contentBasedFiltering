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

Kali ini pada pembuatan sistem rekomendasi, saya menggunakan Book Recommendation Dataset dari Kaggle. Dataset bisa diunduh [disini](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). 
 
**Read Data**
Variabel-variabel pada Book Recommendation Dataset adalah sebagai berikut:
- Buku
Buku diidentifikasi dengan ISBN masing-masing. ISBN yang tidak valid telah dihapus dari set data. Selain itu, beberapa informasi berbasis konten diberikan ( Book-Title, Book-Author, Year-Of-Publication, Publisher), diperoleh dari Amazon Web Services. Perhatikan bahwa dalam kasus beberapa penulis, hanya yang pertama disediakan. URL yang menautkan ke gambar sampul juga diberikan, muncul dalam tiga rasa berbeda ( Image-URL-S, Image-URL-M, Image-URL-L), yaitu, kecil, sedang, besar. URL ini mengarah ke situs web Amazon.
- Rating
Berisi informasi rating buku. Peringkat ( Book-Rating) baik eksplisit, dinyatakan dalam skala 1-10 (nilai yang lebih tinggi menunjukkan apresiasi yang lebih tinggi), atau implisit, dinyatakan dengan 0.

**Visualisasi Data**


Sekarang di file buku, kami memiliki beberapa kolom tambahan yang tidak diperlukan untuk tugas kami seperti URL gambar. Dan kita akan menamai ulang kolom-kolom dari setiap file karena nama kolom tersebut berisi spasi, dan huruf kapital sehingga kita akan perbaiki agar mudah digunakan.

**Exploratory Data Analysis**


## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
