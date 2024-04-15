# Laporab Proyek Machine Learning - Destriana Ramadani

## Project Overview 
Seiring dengan kemajuan teknologi terkini dengan maraknya layanan online telah menawarkan kemampuan dan kemudahan untuk mengakses sejumlah besar informasi online dengan lebih cepat. Pengguna dapat memberikan ulasan, komentar, dan penilain untuk berbagai jenis layanan dan produk yang tersedia secara online. Namun, kemajuan terkini dalam proses komputasi telah mengakibatkan kelebihan data secara online. Kelebihan data ini membuat lebih sulit dalam menemukan konten yang relevan dan bermanfaat melalui internet.

Baru-baru ini, pengembangan beberapa metode yang membutuhkan daya komputasi lebih rendah telah membuat pengguna lebih mudah dan cepat menemukan konten yang relevan. Oleh karena itu, pengembangan sistem rekomendasi baru-baru ini telah menarik perhatian yang besar. Secara umum, sistem rekomendasi berperan sebagai alat bantu informasi yang menyediakan konten atau informasi yang sesuai dan disesuaikan dengan kebutuhan pengguna. Sistem ini terutama bertujuan untuk mengurangi usaha dan waktu yang diperlukan pengguna untuk mencari informasi yang relevan di internet.

## Business Understanding
Sistem rekomendasi merupakan metode filtering yang memahami preferensi suatu kelompok dan kemudian merekomendasikan barang atau produk yang paling relevan kepada pengguna. Dalam konteks bisnis, hal ini juga dapat didefinisikan sebagai kemungkinan seorang pengguna membeli suatu produk tertentu yang menggambarkan preferensi pengguna terhadap produk yang berbeda. Konsep ini digambarkan sebagai fungsi pengguna dan produk, yang menghasilkan skor yang mengukur minat pengguna terhadap produk.

Selama bertahun-tahun, sistem rekomendasi telah digunakan untuk memecahkan masalah menghubungkan pengguna saat ini ke produk yang paling relevan pada jutaan item dalam inventaris. Misalnya, rekomendasi buku, produk, dan berbagai item dari Amazon, film dari Netflix, aplikasi surat kabar yang dipersonalisasi, atau musik di Spotify adalah beberapa contoh sukses sistem rekomendasi yang digunakan dalam aplikasi e-commerce saat ini.

### 1. Problem Statemant
Berdasarkan penjelasan sebelumnya masalah yang umumnya terjadi pada perusahaan e-commerce dalam menjual produknya adalah bagaimana memberikan rekomendasi produk atau barang yang sesuai dengan preferensi pelanggan dengan efektif dan cepat.

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
- Pada kolom `Publisher`, penerbit dengan terbitan terbanyak diterbitkan oleh `Harlequin` dengan total buku yang diterbitkan hampir 8000 buku dimana jumlah ini hampir dua kali lipat dari jumlah buku yang diterbitkan oleh `Publisher` lain.

- Pada kolom `Book-Author`, penulis dengan buku ciptaan terbanyak ditulis oleh `Agatha Christie` dengan total buku ciptaannya sebanyak 650 yang kemudian diikuti oleh `William Shakespeare`, `Stephen King`, `Ann M. Martin` dan `Carolyn Keene`. 

- Pada perhitungan total buku per `Book-Rating` terlihat bahwa mayoritas buku terdapat pada rating 0 atau mayoritas buku belum memiliki rating

## Data Preparation

### 1. Menggabungkan Dataset
Pada projek ini digunakan 2 dataset yakni *Book* dan *Rating*. Untuk memudahkan pengambilan data berdasarkan gabungan informasi buku dan ratingnya, akan dilakukan pembuatas dataframe baru yang merupakan gabungan kedua dataset tersebut.

### 2. Menghapus Missing Value
Dilakukan pengecekan missing value dan diketahui bahwa terdapat 3 missing value yang selanjutnya baris-baris tersebut akan dihapuskan.

### 3. Menghapus Rating = 0
Dari hasil EDA diketahui bahwa mayoritas buku belum memiliki rating sehingga akan dilakukan penghapusan baris buku yang belum memiliki rating agar sistem rekomendasi yang dibangun hanya merekomendasikan buku-buku yang telah diberikan rating.

## Content Based Filtering

### 1. Data Preparation: Content Based Filtering
Pada pembuatan model sistem rekomendasi berbasis konten akan dibuat berdasarkan kesamaan kata yang dimasukan dengan judul buku yang ada sehingga kolom yang digunakan hanya kolom `Book-Title`. Namun karena jumlah dataset yang cukup banyak sehingga data buku yang akan digunakan pada sistem rekomendasi ini dibatasi hanya pada buku yang memiliki rata-rata rating = 10.0. Dari total 135565 data, setelah dipilih berdasarkan nilai ratingnya didapatkan 18257 data yang akan digunakan pada sistem rekomendasi ini.

### 2. Model Develepment Content Based Filtering
Sistem rekomendasi berbasis konten merupakan model yang bekerja dengan melihat kemiripan dari suatu konten/produk/barang. Model ini akan menghitung kemiripan antar kata yang dimasukan user dengan judul buku yang kemudian model ini akan memberikan rekomendasi buku dengan kemiripan tertinggi. Model dengan pendekatan berbasis konten ini merupakan salah satu metode yang bisa digunakan jika pada dataset hanya terdapat atribut dari konten dan tidak terdapat riwayat transaksi oleh user.

#### 1. TF-IDF
TF-IDF telah banyak digunakan dalam bidang pengambilan informasi dan penambangan teks untuk mengevaluasi hubungan setiap kata dalam kumpulan dokumen. Secara khusus, metode ini digunakan untuk mengekstraksi kata-kata inti (kata kunci) dari dokumen, menghitung derajat yang sama antar dokumen, menentukan peringkat pencarian, dan sebagainya. TF (Term Frequency) dalam TF-IDF merujuk pada kemunculan kata-kata tertentu dalam dokumen. Kata-kata dengan nilai TF yang tinggi menandakan kepentingan yang lebih besar dalam dokumen tersebut. Di sisi lain, DF (Document Frequency) mengindikasikan seberapa sering kata tertentu muncul dalam seluruh kumpulan dokumen. Ini menghitung kemunculan kata tersebut di banyak dokumen, bukan hanya di satu dokumen saja. Kata-kata dengan nilai DF yang tinggi umumnya tidak menjadi fokus karena kecenderungannya adalah muncul di hampir semua dokumen. Sedangkan IDF (Inverse Document Frequency) yang merupakan kebalikan dari DF digunakan untuk menilai pentingnya kata-kata dalam seluruh dokumen. Nilai IDF yang tinggi menandakan bahwa kata-kata tersebut jarang ditemukan di seluruh kumpulan dokumen, sehingga memiliki kepentingan yang lebih besar. Dengan demikian, TF-IDF membantu mengukur relatifnya pentingnya sebuah kata dalam konteks seluruh kumpulan dokumen.

#### 2. Cosine Similarity
Kemiripan dua vektor diukur dengan menggunakan teknik Cosine Similarity. Teknik ini bekerjanya dengan mengukur kosinus sudut antara dua dokumen yang dinyatakan dalam vektor. Sudut antar vektor, menentukan apakah vektor-vektor tersebut menunjuk ke arah yang sama atau berbeda. Jika vektor-vektor menunjuk ke arah yang sama, berarti dokumen-dokumen tersebut serupa, semakin dekat letaknya pada sumbu, semakin mirip pula dokumen-dokumen tersebut. Begitu pula sebaliknya, semakin jauh keduanya dinyatakan pada sumbu, semakin kecil kemiripannya. Setiap dokumen yang digunakan untuk perbandingan, disajikan dalam ruang sebagai plot, dan kesamaan kosinus menangkap orientasi plot tersebut. Pada tahap ini digunakan fungsi `cosine_similarity()` untuk menghitung kemiripan dari matriks hasil TF-IDF.

#### 3. Menampilkan Rekomendasi Buku berdasarkan Kata Pada Judul Buku
Untuk menampilkan rekomendasi buku berdasarkan kata pada judul buku, akan dibuat sebuah fungsi. Fungsi ini memiliki 1 parameter sebagai input kata dan kemudian fungsi ini akan memberikan output berupa 10 rekomendasi buku berdasarkan nilai cosine similarity antara kata input dengan judul buku.

**Berikut hasil rekomendasi dari buku dengan kata `Harry Potter`** :
- `Harry Potter and the Prisoner of Azkaban Color and Activity Book (Harry Potter)`
- `Harry Potter, tome 3 : Harry Potter et le Prisonnier d'Azkaban`
- `The Potter`
- `Harry Potter and the Goblet of Fire (Harry Potter)`
- `The Magical Worlds of Harry Potter`

Dari hasil rekomendasi yang diberikan terlihat bahwa model rekomendasi sistem yang dibangun berhasil memberikan rekomendasi judul buku yang relevan dengan input kata yang dimasukan.

## Collaborative Filtering

### 1. Data Preparation: Collaborative Filtering
Pada pembuatan model sistem rekomendasi berbasis kolaboratif akan dibuat berdasarkan kesamaan dari seorang pengguna dengan suatu kelompok. Hal ini didasarkan pada kesamaan rating yang pernah diberikan terhadap buku yang sama. Data yang digunakan untuk membangun rekomendasi sistem ini adalah `User-ID`, `Book-Title`, dan `Book-Rating`. Agar rekomendasi yang diberikan cukup baik dan dataset yang digunakan cukup banyak sehingga akan dilakukan pemilihan buku yang memiliki jumlah minimal rating sebanyak 50. Dari total 383839 data, setelah dipilih berdasarkan jumlah ratingnya didapatkan 65081 data yang akan digunakan pada sistem rekomendasi ini.

Kemudian dilakukan proses encoding pada data `User-ID` dan `ISBN` menjadi bertipe data integer. Lalu dilakukan pembagian data train dan data validation untuk proses training model dengan data train adalah kolom `User-ID` dan `ISBN` hasil encoding dan data validation adalah kolom `Book-Rating`.

### 2. Model Develepment Collaborative Filtering

#### 1. Proses Training Model
Pada tahap ini dilakukan implementasi model neural network untuk sistem rekomendasi menggunakan TensorFlow. Model ini menggunakan embeddings untuk merepresentasikan pengguna (users) dan item (books) dalam ruang laten yang lebih rendah. Dalam inisialisasi model, Embedding layers digunakan untuk menyandikan pengguna dan item ke dalam vektor numerik, dengan pembatasan L2 regularization. Kemudian, dalam fungsi call, vektor pengguna dan item dipanggil berdasarkan input, dan kemudian dihitung dot product-nya. Setelah itu, bias dari pengguna dan item ditambahkan ke hasil dot product tersebut. Akhirnya, hasil akhir diteruskan melalui fungsi aktivasi sigmoid untuk memperoleh nilai probabilitas. Model ini kemudian dikompilasi dengan binary cross-entropy loss function, optimizer Adam dengan learning rate 0.001, dan metric Root Mean Squared Error (RMSE). Selama proses pelatihan, dua callback digunakan: ReduceLROnPlateau untuk mengurangi learning rate jika 'val_loss' tidak membaik dalam beberapa epochs, dan EarlyStopping untuk menghentikan pelatihan jika tidak ada perbaikan dalam 'val_loss' dalam beberapa epochs berturut-turut. Proses pelatihan kemudian dilakukan dengan data pelatihan dan validasi, menggunakan batch size 8 dan berhenti setelah maksimum 30 epochs atau jika early stopping terpenuhi.

#### 2. Mendapatkan Rekomendasi Buku
Berikut ini adalah langkah-langkah untuk mendapatkan rekomendasi buku. Pertama, sebuah ID pengguna dipilih secara acak dari dataset collaborative_filtering_df. Kemudian, buku-buku yang telah dibeli oleh pengguna tersebut diidentifikasi. Selanjutnya, buku-buku yang belum dibeli oleh pengguna dicari berdasarkan daftar buku yang tersedia dalam dataset. Daftar buku yang belum dibeli tersebut diubah menjadi representasi terenkripsi yang sesuai dengan format yang dimengerti oleh model. Selanjutnya, representasi terenkripsi dari pengguna tersebut diambil, dan digabungkan dengan representasi terenkripsi dari buku-buku yang belum dibeli. Model digunakan untuk memprediksi rating untuk buku-buku tersebut. Sepuluh buku dengan rating tertinggi kemudian dipilih sebagai rekomendasi. ISBN dari buku-buku rekomendasi tersebut kemudian diubah kembali menjadi judul-judul buku yang sesuai, dan ditampilkan bersama dengan lima buku teratas yang telah dibeli oleh pengguna untuk membandingkan rekomendasi dengan preferensi sebelumnya.



Berikut hasil prediksi dari user dengan `User-ID` = `638` :

- **Books with High Ratings from User**
- `The Catcher in the Rye by J.D. Salinger`
- `The Lovely Bones: A Novel by Alice Sebold`
- `The Da Vinci Code by Dan Brown`
- `The Pilot's Wife : A Novel Tag: Author of the Weight of Water (Oprah's Book Club (Hardcover)) by Anita Shreve`
- `The Beach HouseMe Talk Pretty One Day by David Sedaris`

- **Top 10 Books Recommendation**
- `Message in a BottleTo Kill a Mockingbird by Harper Lee`
- `The Little Prince by Antoine de Saint-ExupÃ©ry`
- `The Giver (21st Century Reference) by LOIS LOWRY`
- `1984 by George Orwell`
- `East of Eden (Oprah's Book Club) by John Steinbeck`
- `Charlotte's Web (Trophy Newbery) by E. B. White`
- `The Beach HouseThe Return of the King (The Lord of the Rings, Part 3) by J.R.R. TOLKIEN`
- `Harry Potter and the Goblet of Fire (Book 4) by J. K. Rowling`
- `Harry Potter and the Prisoner of Azkaban (Book 3) by J. K. Rowling`
- `Harry Potter and the Sorcerer's Stone (Book 1) by J. K. Rowling`

Dari hasil sistem rekomendasi yang dibuat, model berhasil memberikan 10 rekomendasi buku berdasarkan buku yang telah diberikan rating oleh user.

## Evaluation 

### Evaluation: Content Based Filtering
Salah satu metode untuk mengukur akurasi dari hasil sistem rekomendasi adalah RSP. Formula metrik Recomender System Precision (RSP) ini adalah sebagai berikut :

$$RSP = R_R/R_A$$

Ket : 

$R_R$ = Jumlah rekomendasi yang relevan

$R_A$ = Jumlah keseluruhan rekomendasi yang prediksi model

Metode ini bekerja dengan membandingkan jumlah keseluruhan rekomendasi yang diberikan model dengan jumlah rekomendasi yang relevan dengan rentang 0 sampai 1.
Jika melihat hasil rekomendasi buku yang telah diberikan terlihat bahwa kelima judul buku yang direkomendasikan mengandung kata "Harry" atau "Potter" sehingga hasil perhitungan RSP nya adalah 5/5 = 1

### Evaluation: Collaborative Filtering
Untuk mengukur akurasi dari model sistem rekomendasi ini adalah dengan menggunakan RMSE
Formula metrik Root Mean Squared Error (RMSE) adalah sebagai berikut :

$$RMSE = \sqrt{\sum{(Y_t - Y_p)^2} \over n}$$

Ket :

$Y_t$ = Y true (Aktual)

$Y_p$ = Y predict (Prediksi)

n = jumlah data

Cara kerja metrik ini adalah dengan menyelisihkan nilai aktual dengan nilai prediksi lalu dikuadratkan kemudian ditotalkan dengan seluruh data dan selanjutnya dibagi dengan jumlah data, terakhir diakarkan. 

![RMSE](https://github.com/DestrianaR/Book-Recommendation-System/blob/33c97a5c966f3490880a92ab9f45bb48d51bc99d/image.png?raw=true)

## Conclusion
Pada projek ini telah dibangun sistem rekomendasi dengan 2 pendekatan yakni **Content Based Filtering** dan **Collaborative Filtering**. Dimana kedua pendekatan ini telah berhasil memberikan rekomendasi buku yang harapannya model ini dapat ditingkatkan menjadi lebih baik dikemudian hari.

## Reference

[1] D. Roy, M. Dutta. "A Systematic Review and Research Perspective on Recommender System". Journal of Big Data,2022. Tersedia: [tautan](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-022-00592-5). Diakses pada 05 Maret 2024.

[2] M. Loukili, F. Messaoudi, M. E. Ghazi. "Machine Learning Based Recommender System For E-Commerce". IAES International Journal of Artificial Intelligence. 2023. Tersedia: [tautan](https://ijai.iaescore.com/index.php/IJAI/article/view/22723). Diakses pada 15 Maret 2024