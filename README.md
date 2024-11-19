# Laporan Proyek Machine Learning - Destriana Ramadani

## Project Overview 
Seiring dengan kemajuan teknologi terkini dengan maraknya layanan online telah menawarkan kemampuan dan kemudahan untuk mengakses sejumlah besar informasi online dengan lebih cepat. Pengguna dapat memberikan ulasan, komentar, dan penilain untuk berbagai jenis layanan dan produk yang tersedia secara online. Namun, kemajuan terkini dalam proses komputasi telah mengakibatkan kelebihan data secara online. Kelebihan data ini membuat lebih sulit dalam menemukan konten yang relevan dan bermanfaat melalui internet. Oleh karena itu, pengembangan sistem rekomendasi menjadi sangat penting dan bermanfaat untuk memberikan rekomendasi produk sesuai dengan preferensi pengguna.

Dengan jumlah buku yang tersedia di pasaran yang terus bertambah, mencari buku yang sesuai dengan minat dan kebutuhan bisa menjadi tugas yang menantang. Sistem rekomendasi produk buku penting karena membantu pengguna menemukan buku yang sesuai dengan minat dan preferensi mereka dengan lebih mudah. 

## Business Understanding
Sistem rekomendasi merupakan metode filtering yang memahami preferensi suatu kelompok dan kemudian merekomendasikan barang atau produk yang paling relevan kepada pengguna. Dalam konteks bisnis, hal ini juga dapat didefinisikan sebagai kemungkinan seorang pengguna membeli suatu produk tertentu yang menggambarkan preferensi pengguna terhadap produk yang berbeda. Konsep ini digambarkan sebagai fungsi pengguna dan produk, yang menghasilkan skor yang mengukur minat pengguna terhadap produk.

Sistem rekomendasi tidak hanya memberikan rekomendasi berdasarkan preferensi yang sudah ada, tetapi juga dapat memperluas cakupan minat pengguna dengan menyarankan buku-buku yang mungkin belum pernah mereka pertimbangkan sebelumnya. Dengan minat dan preferensi tiap orang yang unik, sistem rekomendasi dapat memberikan rekomendasi yang dipersonalisasi berdasarkan riwayat pembelian, penilaian buku sebelumnya, atau preferensi yang dinyatakan oleh pengguna.

### 1. Problem Statemant
Berdasarkan penjelasan sebelumnya masalah yang umumnya terjadi pada perusahaan e-commerce dalam menjual produknya adalah :

**Bagaimana memberikan rekomendasi produk atau barang yang sesuai dengan preferensi pelanggan dengan efektif dan cepat?**

### 2. Goals
Dengan banyaknya data yang tersedia, maka pada projek ini akan dilakukan pembuatan sistem rekomendasi untuk memberikan rekomendasi yang memudahkan pelanggan dalam melakukan pencarian barang atau produk yang relevan secara efektif.

### 3. Solution Approach
Pada pembuatan sistem rekomendasi ini akan digunakan dua pendekatan yang cukup terkenal yakni **Content Based Filtering** dan **Collaborative Filtering**. **Content Based Filtering** atau filter berbasis konten merupakan metode filter berdasarkan atribut profil pengguna serta produk atau item. Metode merekomendasikan item yang kontennya serupa dengan produk yang pernah dinilai tinggi oleh pengguna atau cocok dengan atribut penanda pengguna. Profil yang dibuat untuk pengguna dan item menjelaskan berbagai karakteristik yang melekat, yang membantu metode ini dalam mengaitkan pengguna ke item yang paling relevant. Sedangkan **Collaborative Filtering** atau filter berbasis kolaboratif merupakan metode filter dengan menganalisis interaksi historis dan data penggunaan di seluruh pengguna untuk mengidentifikasi kelompok pengguna/item yang sangat cocok. Misalnya, jika sekelompok orang diketahui menyukai coklat dan seseorang diketahui sering membeli coklat merek tertentu, maka dapat diasumsikan bahwa orang tersebut mungkin juga menyukai coklat lain yang sering dibeli oleh sekelompok orang tersebut. Metode **Collaborative Filtering** secara garis besar diklasifikasikan menjadi dua jenis, yaitu Pendekatan berbasis memori dan Pendekatan Berbasis Model. Perbedaan antara pendekatan-pendekatan ini terletak pada metode yang digunakan untuk menghitung kesamaan antar kelompok pelanggan yaitu metode statistik dalam hal pendekatan berbasis memori dan mempelajari parameter menggunakan metode penurunan gradien, faktorisasi matriks, atau jaringan saraf berlapis untuk metode berbasis model.

## Data Understanding
Dataset yang digunakan pada projek ini terdiri dari 3 file dataset yaitu Users, Books dan Ratings. Namun berdasarkan 2 metode yang telah dijelaskan sebelumnya hanya akan digunakan 2 file dataset yakni Books dan Rating.
link : [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?select=Ratings.csv). 

### 1. Informasi Data
- Buku (*Books*)
   Pada dataset ini terdapat 271360 baris dan 5 kolom dengan informasi kolom sebagai berikut:
   * `ISBN` : (*International Standard Book Number*) adalah kode pengidentifikasian buku yang bersifat unik (identitas buku).
   * `Book-Title` : Judul buku 
   * `Book-Author` : Penulis buku
   * `Year-Of-Publication` : Tahun publikasi buku
   * `Image-URL-S` : Link untuk melihat gambar kecil dari buku 
   * `Image-URL-M` : Link untuk melihat gambar sedang dari buku
   * `Image-URL-L` : Link untuk melihat gambar besar dari buku
   
   Berdasarkan uraian informasi dataset *Books* sebelumnya, kolom `Image-URL-S`, `Image-URL-M`, dan `Image-URL-L` tidak akan digunakan

- Peringkat (*Ratings*)
   Pada dataset ini terdapat 1149780 baris dan 3 kolom dengan informasi kolom sebagai berikut:
   * `User-ID` : Nomor identitas pemberi rating
   * `ISBN` : kode pengidentifikasian buku yang bersifat unik (identitas buku)
   * `Book-Rating` : Rating yang diberikan konsumen (rentang 0 - 10)


### 2. Exploratory Data Analysis (EDA)
![Plot Top 10 Publisher](https://github.com/DestrianaR/Book-Recommendation-System/blob/main/Top_10_Publisher.png?raw=true)

Gambar 1. Plot Top 10 Publisher

Pada Gambar 1. terlihat visualisasi 10 penerbit dengan buku terbanyak. Penerbit *Harlequin* menerbitkan buku paling banyak dengan hampir dua kali lipat dari penerbit lain yakni sebesar 7500 buku diikuti oleh penerbit *Silhoutte*, *Pocket* dsb.

![Plot Top 10 Author](https://github.com/DestrianaR/Book-Recommendation-System/blob/main/Top_10_Author.png?raw=true)

Gambar 2. Plot Top 10 Author

Pada Gambar 2. terlihat visualisasi 10 penulis dengan buku terbanyak. Penulis  *Agatha Christie* menciptakan buku paling banyak yakni sebesar 650 buku, diikuti oleh *William Shakespeare*, *Stephen King* dsb.

![Plot Total Book in each Rating](https://github.com/DestrianaR/Book-Recommendation-System/blob/main/Book_Rating.png?raw=true)

Gambar 3. Plot Total Book in each Rating

Pada Gambar 3. terlihat jumlah buku pada tiap rating dengan rentang nilai 0-10. Rating dengan buku terbanyak adalah rating 0 dimana jumlah buku yang memiliki rating ini berjumlah 7 kali lipat dari rating dengan buku terbanyak kedua yakni rating 8. Ini menandakan bahwa mayoritas buku pada dataset belum memiliki rating.

## Data Preparation

Pada projek ini digunakan 2 dataset yakni *Book* dan *Rating*. Untuk memudahkan pengambilan data berdasarkan gabungan informasi buku dan ratingnya, akan dilakukan beberapa tahap berikut:

1. Pembuatan dataframe baru 

   Pembuatan dataframe baru dihasilkan dari 2 dataset *Book* dan *Rating* dengan fungsi `.merge()` pada kolom `ISBN`.

2. Menghapus *Missing Value*

   *Missing Value* adalah  adalah keadaan di mana tidak ada nilai yang tersedia atau tidak diisi untuk suatu variabel dalam dataset.
   Tujuan: Nilai *Missing Value* tidak dapat diproses sehingga dilakukan penghapusan baris yang terdapat missing value tersebut.

3. Menghapus Rating = 0

   Dari hasil EDA diketahui bahwa mayoritas buku belum memiliki rating sehingga akan dilakukan penghapusan baris buku yang belum memiliki rating.
   Tujuan: Agar rekomendasi yang diberikan telah memiliki rating yang cukup baik.

## *Content Based Filtering*

### 1. Data Preparation: *Content Based Filtering*
Pada pembuatan model sistem rekomendasi berbasis konten akan dibuat berdasarkan kesamaan kata yang dimasukan dengan judul buku yang ada sehingga kolom yang digunakan hanya kolom `Book-Title`. Namun karena jumlah dataset yang cukup banyak sehingga data buku yang akan digunakan pada sistem rekomendasi ini dibatasi hanya pada buku yang memiliki rata-rata rating = 10.0. Dari total 135565 data, setelah dipilih berdasarkan nilai ratingnya didapatkan 18257 data yang akan digunakan pada sistem rekomendasi ini.

1. Membuat dataframe untuk menghitung rata-rata rating tiap buku

   Pada tahap ini dibuat dataframe untuk menghitung rata-rata tiap buku dengan fungsi `.groupby()` kolom `Book-Title` lalu menghitung rata-rata kolom `Book-Rating` dengan fungsi `.mean()`.

2. Memilih buku dengan nilai rata-rata rating = 10

   Dilakukan pemilihan buku dengan nilai rata-rata rating = 10.
   
   Tujuan = Untuk mengurangi jumlah data buku yang terlalu besar pada pembuatan model dan memberikan rekomendasi buku dengan rating tinggi

3. Pemiliihan kolom yang akan digunakan pada pembuatan model

   karena model sistem rekomendasi berbasis konten akan dibuat berdasarkan kesamaan kata yang dimasukan dengan judul buku yang ada sehingga kolom yang digunakan hanya kolom `Book-Title`

### 2. Modelling: *Content Based Filtering*
Sistem rekomendasi berbasis konten merupakan model yang bekerja dengan melihat kemiripan dari suatu konten/produk/barang. Model ini akan menghitung kemiripan antar kata yang dimasukan user dengan judul buku yang kemudian model ini akan memberikan rekomendasi buku dengan kemiripan tertinggi. Model dengan pendekatan berbasis konten ini merupakan salah satu metode yang bisa digunakan jika pada dataset hanya terdapat atribut dari konten dan tidak terdapat riwayat transaksi oleh user.

#### 1. TF-IDF
TF-IDF telah banyak digunakan dalam bidang pengambilan informasi dan penambangan teks untuk mengevaluasi hubungan setiap kata dalam kumpulan dokumen. Secara khusus, metode ini digunakan untuk mengekstraksi kata-kata inti (kata kunci) dari dokumen, menghitung derajat yang sama antar dokumen, menentukan peringkat pencarian, dan sebagainya. TF (Term Frequency) dalam TF-IDF merujuk pada kemunculan kata-kata tertentu dalam dokumen. Kata-kata dengan nilai TF yang tinggi menandakan kepentingan yang lebih besar dalam dokumen tersebut. Di sisi lain, DF (Document Frequency) mengindikasikan seberapa sering kata tertentu muncul dalam seluruh kumpulan dokumen. Ini menghitung kemunculan kata tersebut di banyak dokumen, bukan hanya di satu dokumen saja. Kata-kata dengan nilai DF yang tinggi umumnya tidak menjadi fokus karena kecenderungannya adalah muncul di hampir semua dokumen. Sedangkan IDF (Inverse Document Frequency) yang merupakan kebalikan dari DF digunakan untuk menilai pentingnya kata-kata dalam seluruh dokumen. Nilai IDF yang tinggi menandakan bahwa kata-kata tersebut jarang ditemukan di seluruh kumpulan dokumen, sehingga memiliki kepentingan yang lebih besar. Dengan demikian, TF-IDF membantu mengukur relatifnya pentingnya sebuah kata dalam konteks seluruh kumpulan dokumen.

#### 2. Cosine Similarity
Kemiripan dua vektor diukur dengan menggunakan teknik *Cosine Similarity*. Teknik ini bekerjanya dengan mengukur kosinus sudut antara dua dokumen yang dinyatakan dalam vektor. Sudut antar vektor, menentukan apakah vektor-vektor tersebut menunjuk ke arah yang sama atau berbeda. Jika vektor-vektor menunjuk ke arah yang sama, berarti dokumen-dokumen tersebut serupa, semakin dekat letaknya pada sumbu, semakin mirip pula dokumen-dokumen tersebut. Begitu pula sebaliknya, semakin jauh keduanya dinyatakan pada sumbu, semakin kecil kemiripannya. Setiap dokumen yang digunakan untuk perbandingan, disajikan dalam ruang sebagai plot, dan kesamaan kosinus menangkap orientasi plot tersebut. Pada tahap ini digunakan fungsi `cosine_similarity()` untuk menghitung kemiripan dari matriks hasil TF-IDF.

#### 3. Menampilkan Rekomendasi Buku berdasarkan Kata Pada Judul Buku
Untuk menampilkan rekomendasi buku berdasarkan kata pada judul buku, akan dibuat sebuah fungsi. Fungsi ini memiliki 1 parameter sebagai input kata dan kemudian fungsi ini akan memberikan output berupa 10 rekomendasi buku berdasarkan nilai *Cosine Similarity* antara kata input dengan judul buku.

**Berikut hasil rekomendasi dari buku dengan kata `Harry Potter`** :

Tabel 1. Hasil rekomendasi buku *Content Based Filtering* dengan kata `Harry Potter`

| No. | Book Title |
|--|---|
| 1. | Harry Potter and the Prisoner of Azkaban Color and Activity Book (Harry Potter) | 
| 2. | Harry Potter, tome 3 : Harry Potter et le Prisonnier d'Azkaban |
| 3. | The Potter | 
| 4. | Harry Potter and the Goblet of Fire (Harry Potter) |
| 5. | The Magical Worlds of Harry Potter |

Dari hasil rekomendasi yang diberikan terlihat bahwa model rekomendasi sistem yang dibangun berhasil memberikan rekomendasi judul buku yang relevan dengan input kata yang dimasukan.

## *Collaborative Filtering*

### 1. Data Preparation: *Collaborative Filtering*
Pada pembuatan model sistem rekomendasi berbasis kolaboratif akan dibuat berdasarkan kesamaan dari seorang pengguna dengan suatu kelompok. Hal ini didasarkan pada kesamaan rating yang pernah diberikan terhadap buku yang sama. Agar rekomendasi yang diberikan cukup baik dan dataset yang digunakan cukup banyak sehingga akan dilakukan pemilihan buku yang memiliki jumlah minimal rating sebanyak 50. Dari total 383839 data, setelah dipilih berdasarkan jumlah ratingnya didapatkan 65081 data yang akan digunakan pada sistem rekomendasi ini.

1. Pemilihan buku berdasarkan jumlah rating

   Dilakukan perhitungan jumlah rating dari masing-masing buku, lalu dipilih buku dengan jumlah rating > 50.
   
   Tujuan: Untuk mengurangi jumlah data buku yang digunakan.

2. *Encoding* `User-ID` dan `ISBN`
   
   Proses *Encoding* merupakan perubahan data object menjadi numerik.
   
   Tujuan: Algoritma untuk membuat model hanya bisa menerima data dalam bentuk numerik.

3. Membagi dataset

   Dilakukan pembagian dataset train dan validation dimana kolom `users` dan `book` yang merupakan hasil encoding akan menjadi variabel fitur dan kolom `Book-Rating` akan menjadi variabel target.

### 2. Modelling: *Collaborative Filtering*

#### 1. Proses Training Model
Pada tahap ini dilakukan implementasi model neural network untuk sistem rekomendasi menggunakan TensorFlow. Model ini menggunakan embeddings untuk merepresentasikan pengguna (users) dan item (books) dalam ruang laten yang lebih rendah. Dalam inisialisasi model, Embedding layers digunakan untuk menyandikan pengguna dan item ke dalam vektor numerik, dengan pembatasan L2 regularization. Kemudian, dalam fungsi call, vektor pengguna dan item dipanggil berdasarkan input, dan kemudian dihitung dot product-nya. Setelah itu, bias dari pengguna dan item ditambahkan ke hasil dot product tersebut. Akhirnya, hasil akhir diteruskan melalui fungsi aktivasi sigmoid untuk memperoleh nilai probabilitas. Model ini kemudian dikompilasi dengan binary cross-entropy loss function, optimizer Adam dengan learning rate 0.001, dan metric *Root Mean Squared Error* (RMSE). Selama proses pelatihan, dua callback digunakan: *ReduceLROnPlateau* untuk mengurangi learning rate jika `val_loss` tidak membaik dalam beberapa epochs, dan *EarlyStopping* untuk menghentikan pelatihan jika tidak ada perbaikan dalam `val_loss` dalam beberapa epochs berturut-turut. Proses pelatihan kemudian dilakukan dengan data pelatihan dan validasi, menggunakan batch size 8 dan berhenti setelah maksimum 30 epochs atau jika early stopping terpenuhi.

#### 2. Mendapatkan Rekomendasi Buku
Berikut ini adalah langkah-langkah untuk mendapatkan rekomendasi buku. Pertama, sebuah ID pengguna dipilih secara acak dari dataset `collaborative_filtering_df`. Kemudian, buku-buku yang telah dibeli oleh pengguna tersebut diidentifikasi. Selanjutnya, buku-buku yang belum dibeli oleh pengguna dicari berdasarkan daftar buku yang tersedia dalam dataset. Daftar buku yang belum dibeli tersebut diubah menjadi representasi terenkripsi yang sesuai dengan format yang dimengerti oleh model. Selanjutnya, representasi terenkripsi dari pengguna tersebut diambil, dan digabungkan dengan representasi terenkripsi dari buku-buku yang belum dibeli. Model digunakan untuk memprediksi rating untuk buku-buku tersebut. Sepuluh buku dengan rating tertinggi kemudian dipilih sebagai rekomendasi. ISBN dari buku-buku rekomendasi tersebut kemudian diubah kembali menjadi judul-judul buku yang sesuai, dan ditampilkan bersama dengan lima buku teratas yang telah dibeli oleh pengguna untuk membandingkan rekomendasi dengan preferensi sebelumnya.

Berikut hasil prediksi dari user dengan `User-ID` = `55490` :

Tabel 2. Buku dengan rating tertinggi oleh user 55490

| No. | Book Title | Book Author |
|--|---|---|
| 1. | Roses Are Red (Alex Cross Novels) | James Patterson |
| 2. | The Vampire Lestat (Vampire Chronicles, Book II) | ANNE RICE |
| 3. | Hannibal | Thomas Harris |
| 4. | Kiss the Girls | James Patterson |
| 5. | The Gunslinger (The Dark Tower, Book 1) | Stephen King |

Tabel 3. Rekomendasi buku sistem rekomendasi *Collaborative Filtering*

| No. | Book Title | Book Author |
|--|---|---|
| 1. | The Little Prince | Antoine de Saint-ExupÃ©ry |
| 2. | Anne of Green Gables (Anne of Green Gables Novels (Paperback)) | L.M. MONTGOMERY |
| 3. | Anne Frank: The Diary of a Young Girl | ANNE FRANK |
| 4. | The Stand: Complete and Uncut | Stephen King |
| 5. | Fahrenheit 451 | RAY BRADBURY |
| 6. | High Five (A Stephanie Plum Novel) | Janet Evanovich |
| 7. | Charlotte's Web (Trophy Newbery) | B. White |
| 8. | Harry Potter and the Prisoner of Azkaban (Book 3) | J. K. Rowling |
| 9. | Outlander  | DIANA GABALDON |
| 10. | A Wrinkle In Time | MADELEINE L'ENGLE |

Dari hasil sistem rekomendasi yang dibuat, model berhasil memberikan 10 rekomendasi buku berdasarkan buku yang telah diberikan rating oleh user.

## Evaluation 

### Evaluation: *Content Based Filtering*
Salah satu metode untuk mengukur akurasi dari hasil sistem rekomendasi adalah RSP. Formula metrik *Recomender System Precision* (RSP) ini adalah sebagai berikut :

$$RSP = R_R/R_A$$

Ket : 

$R_R$ = Jumlah rekomendasi yang relevan

$R_A$ = Jumlah keseluruhan rekomendasi yang prediksi model

Metode ini bekerja dengan membandingkan jumlah keseluruhan rekomendasi yang diberikan model dengan jumlah rekomendasi yang relevan dengan rentang 0 sampai 1.
Jika melihat hasil rekomendasi buku yang telah diberikan terlihat bahwa kelima judul buku yang direkomendasikan mengandung kata "Harry" atau "Potter" sehingga hasil perhitungan RSP nya adalah 5/5 = 1. 

Sehingga dari hasil perhitungan metrics RSP dapat disimpulkan bahwa model sistem rekomendasi berbasis konten ini **berhasil memberikan rekomendasi buku yang relevan dengan kata kunci yang dimasukan.**

### Evaluation: *Collaborative Filtering*
Untuk mengukur akurasi dari model sistem rekomendasi ini adalah dengan menggunakan RMSE
Formula metrik Root Mean Squared Error (RMSE) adalah sebagai berikut :

$$RMSE = \sqrt{\sum{(Y_t - Y_p)^2} \over n}$$

Ket :

$Y_t$ = Y true (Aktual)

$Y_p$ = Y predict (Prediksi)

n = jumlah data

Cara kerja metrik ini adalah dengan menyelisihkan nilai aktual dengan nilai prediksi lalu dikuadratkan kemudian ditotalkan dengan seluruh data dan selanjutnya dibagi dengan jumlah data, terakhir diakarkan. 

![RMSE](https://github.com/DestrianaR/Book-Recommendation-System/blob/main/RMSE.png?raw=true)

Gambar. 4 Plot RMSE Model Sistem Rekomendasi *Collaborative Filtering*.

Dari Gambar 4. Terlihat bahwa model sudah cukup baik. Hal ini terlihat dari adanya penurunan nilai RMSE seiring dengan bertambahnya epoch. Selisih antara nilai RMSE data train dan data test juga tidak terlalu besar yakni sekitar 6%.

Sehingga dari hasil perhitungan metrics RMSE dapat disimpulkan bahwa model sistem rekomendasi kolaboratif ini **berhasil memberikan rekomendasi buku dengan tingkat kesalahan yang cukup kecil.**

## Conclusion
Pada projek ini telah dibangun sistem rekomendasi dengan 2 pendekatan yakni **Content Based Filtering** berdasarkan data judul buku dan **Collaborative Filtering** berdasarkan riwayat pemberian rating pada buku sebelumnya dimana kedua pendekatan ini telah berhasil memberikan rekomendasi buku yang relevan.


## Reference

[1] D. Roy, M. Dutta. "A Systematic Review and Research Perspective on Recommender System". Journal of Big Data,2022. Tersedia: [tautan](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-022-00592-5). Diakses pada 05 Maret 2024.

[2] M. Loukili, F. Messaoudi, M. E. Ghazi. "Machine Learning Based Recommender System For E-Commerce". IAES International Journal of Artificial Intelligence. 2023. Tersedia: [tautan](https://ijai.iaescore.com/index.php/IJAI/article/view/22723). Diakses pada 15 Maret 2024
