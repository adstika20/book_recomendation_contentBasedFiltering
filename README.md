# Laporan Proyek Machine Learning - Ades Tikaningsih

## Project Overview 

**Latar Belakang**:

Membaca merupakan salah satu kegiatan yang lekat dengan kehidupan sehari-hari seseorang. Konsep utama dari membaca adalah memahami makna yang terkandung dalam sebuah teks. Terbukti bahwa orang yang memiliki kebiasaan membaca yang tinggi pasti memiliki wawasan yang luas, membaca dapat juga membuat seseorang mengenal, mengetahui serta memahami apa yang belum dikenal, diketahui dan dipahami. Oleh karena itu pemahaman seseorang terhadap pentingnya pemahaman membaca (reading comprehension) merupakan hal yang penting untuk dipelajari. Namun perlu digaris bawahi bahwa membaca juga bisa menimbulkan bahaya, karena apa yang dibaca seseorang akan mempengaruhi karakter yang terbentuk dari pengetahuan yang ia dapat dari buku tersebut. Salah satu langkah yang ditempuh dalam menyediakan bahan bacaan adalah dengan memilah dan memilih jenis bacaan atau buku apa yang seharusnya dibaca, baik dengan mengenali Penulisnya, Kenali sinopsisnya,  Memakai style bahasa yang gampang dipahami dan lain sebagainya. Berdasarkan hal itu dengan kemajuan bidang ilmu pengetahuan danteknologi dibuatlah sebuah sistem rekomendasi yang berguna bagi pengguna internet yang mungkin merasa sulit untuk memilih dari banyak produk dan layanan yang tersedia. Sistem Rekomendasi dapat memprediksi seberapa besar kemungkinan pengguna target akan tertarik dengan item yang mungkin tidak diketahui olehnya. Dalam karya ini, saya mempertimbangkan sistem rekomendasi buku, yang dapat berguna di perpustakaan, sekolah, dan portal e-learning [[1]](https://aclanthology.org/C18-1033.pdf). Saat ini, dengan perkenalan e-book, pembaca dapat mengakses sumber daya murah dengan sedikit usaha. Diharapkan bahwa tindakan membaca untuk kesenangan akan tersebar luas.

## Business Understanding

Melihat pentingnya dampak buku bagi kehidupan kita, kita perlu banyak membaca buku. Ketika kita membaca buku, kita pasti memiliki ketertarikan kepada satu atau beberapa bidang. Dikarenakan banyaknya buku yang telah dan akan terbit, kita membutuhkan sistem rekomendasi yang akan menyaring buku - buku sesuai dengan selera dan ketertarikan kita. Dengan adanya sistem rekomendasi ini, kita tidak perlu lama - lama dalam mencari buku sesuai ketertarikan kita.

Pada latihan kali ini kita akan menggunakan kedua metode yaitu content dan collaborative based filter.

Pada Content Based Flter, kita akan menggunakan penulis buku menjadi pusat sebagai pusat dari sistem rekomendasi
Pada Collaborative Based Flter, kita akan menggunakan penilaian dari berbagai pengguna sebagai pusat dari sistem rekomendasi

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

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
