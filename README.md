# Laporan Proyek Machine Learning: System Recomendation Movie - Muhammad Husain
---
## Project Overview

Sistem rekomendasi yang merupakan bagian dari sistem penyaringan informasi yang memprediksi preferensi atau penilaian atas suatu item yang diberikan oleh pengguna dapat menjadi sebuah solusi atas overloadnya jumlah informasi yang sering didapat oleh pengguna. Pembuatan sistem rekomendasi ini sendiri bertujuan untuk mengurangi informasi yang berlebih yang diterima oleh suatu individu dengan hanya menampilkan informasi yang paling relevan dari banyaknya data sehingga informasi yang diberikan hanya infromasi yang sesuai dengan individu tersebut. Teknik yang paling umum digunakan dalam sistem rekomendasi ada 3, diantaranya content- based filtering, collaborative filtering, dan hybrid filtering. Sistem rekomendasi sudah banyak diimplementasikan di berbagai macam area, area yang paling terkenal menggunakan konsep sistem rekomendasi salah satunya digunakan pada sistem rekomendasi film [(Evan et al., 2020_)](https://lintar.untar.ac.id/repository/penelitian/buktipenelitian_10390001_7A281222103549.pdf?utm_source).
Film merupakan salah satu dunia hiburan yang digemari oleh masyarakat. Semakin ramainya penggemar film perlu diberikan informasi terkait film-film supaya penonton tertarik dn berminat menonton film yang ditawarkan. Genre film merupakan bentuk atau kategori dari beberapa film tertentu yang mempunyai kesamaan bentuk, tema, suasana dan lain sebagainya. Ada beberapa genre film, diantaranya: action, adventure, comedy, horror, romance, drama dan lainnya. Banyaknya genre dan judul film yang telah rilis serta keberadaan informasi film yang tersedia seharusnya bermanfaat dalam memberikan kemudahan masyarakat, tetapi kenyataannya banyak pilihan membuat masyarakat bingung dalam menentukan pilihan film mana yang akan ditonton. Dalam mengatasi hal tersebut diperlukan sebuah sistem rekomendasi untuk penentuan pemilihan film yang akan ditonton.[(Ibadurrohman et al., 2023_)](https://ejurnal.itats.ac.id/semtik/article/download/4153/3059).
Proyek yang dirancang kali ini merupakan proyek membuat sistem rekomendasi judul film berdasarkan genre menggunakan data dari metadata movies yang didownload dari kaggle. Oleh sebab itu, dibuatlah sistem rekomendasi yang dapat menyelasaikan permasalahan pelanggan, dan dapat dengan mudah mendapatkan rekomendasi film berdasarkan genre dari judul film yang dicari atau yang telah diinput sebelumnya. Metode untuk sistem rekomendasi judul film berdasarkan genre ini menggunakan teknik content-based filtering.
___
# Business Understanding
---
#### Problem Statements
berdasarkan latar belakang diatas, berikut ini rumusan masalah yang dapat diselesaikan pada proyek ini:

- Bagaimana cara melakukan pra-pemrosesan pada data movie recomendation yang akan digunakan agar dapat membuat model yang baik menggunakan teknik content-base filtering?
- Bagaimana memberikan rekomendasi judul film berdasarkan genre pada setiap judul film yang pelanggan input sehingga dapat memberikan preferensi yang sesuai pelanggan inginkan?
 
#### Goals
- Melakukan pra-pemrosesan dengan baik agar dapat digunakan dalam pembuatan model.
- Membuat pelanggan lebih mudah menemukan judul film yang tepat dengan bantuan sistem rekomendasi judul film berdasarkan genre yang dibuat.

#### Solution Statements
### Solusi untuk Mencapai Tujuan Proyek

Berikut adalah langkah-langkah yang diambil untuk mencapai tujuan dari proyek ini:

1. **Pra-pemrosesan Data**  
   Beberapa teknik yang dilakukan pada tahap ini meliputi:  
   - Memeriksa apakah terdapat data kosong atau nilai yang hilang pada dataset.  
   - Menganalisis jumlah data yang tersedia, kemudian mendetailkan fitur-fitur pada kolom genre.  
   - Mengurutkan data berdasarkan `movieId` untuk memastikan konsistensi, lalu menghapus data yang duplikat.  
   - Menghapus entri film dengan judul yang sama untuk menghindari duplikasi hasil rekomendasi.  

2. **Penggunaan Metode Content-Based Filtering**  
   - Definisi: Content-Based Filtering adalah pendekatan yang merekomendasikan item berdasarkan kesamaan dengan item yang telah disukai atau dicari oleh pengguna sebelumnya.  
   - Cara Kerja: Sistem ini menganalisis profil minat pengguna berdasarkan karakteristik item, seperti genre atau fitur lainnya, yang pernah dinilai. Kemudian, sistem menyarankan item dengan karakteristik serupa.  
 



# Data Understanding
---
Data pada project ini menggunakan data yang bersumber pada sebuah situs kaggle, dimana fokus pada data tersebut menyajikan data-data daftar film dari yg terlama hingga ke yg terbaru serta memberikan korelasi dengan data rating yg disediakan pada dataset (tidak terlalu banyak digunakan pada studi kasus projek ini).
Informasi dataset dapat dilihat pada tabel dibawah ini :

| Jenis    | Keterangan                                                |
|----------|-----------------------------------------------------------|
| Title    | Movie recomendation pjct                                   |
| Source   |[Kaggle](https://www.kaggle.com/datasets/sayan0211/movie-recomendation-pjct)                                                  |
| Maintainer | [sayan0211](https://www.kaggle.com/datasets/sayan0211/movie-recomendation-pjct)                                                   |
| License  | Database: Open Database, Contents: Database Contents      |
| Visibility | Publik                                                  |
| Tags     | Movies and TV Shows |
| Usability | 2.94 |

Pada berkas yang diunduh yakni movies.csv berisi 9742 rows × 3 columns dan ratings.csv berisi 100k++ baris dan 4 columns. Kolom-kolom tersebut terdiri dari 2 buah kolom bertipe objek dan 1 buah kolom bertipe numerik (tipe data int64) pada file movies.csv. Untuk penjelasan mengenai variabel-variable pada dataset movies recomendation ini dapat dilihat sebagai berikut:
- **movieId** merupakan parameter bernilai unique. Parameter ini digunakan utk mengindetifikasi daftar tiap-tiap film.
- **userId** merupakan parameter bernilai unique. Parameter ini digunakan utk mengindetifikasi daftar tiap-tiap pengguna.
- **rating** merupakan parameter berisi nilai rating film yg diberikan pengguna
- **genre** merupakan parameter yg menyimpan tiap-tiap kategori film
- **title** merupakan parameter yg menyimpan judul masing-masing film

Berikut beberapa tahapan Data Understanding diantaranya sebagai berikut:
- Meload Dataset ke dalam sebuah Dataframe menggunakan pandas
- ``` df.info()``` digunakan untuk mengecek tipe kolom pada dataset
- ```df.isna().sum()``` digunakan untuk mengecek apakah ada kolom yg kosong, pada dataset ini nilai kosong tidak ditemukan
- ```df.describe()``` digunakan utk mendapatkan info mengenai dataset terhadap nilai rata-rata, median, banyaknya data, nilai Q1 hingga Q3 dan lain-lain.
- ``` len(nama_variable.unique()) ```menghitung panjang data unique dari variable tertentu
- Mengurutkan dataset dan menghapus data movieId yg sama

- Menampilkan rata-rata genre yg paling banyak muncul pada dataset
![Screenshot 2025-04-21 121314](https://github.com/user-attachments/assets/a12accde-b5e6-461c-9274-3bdc3a7e68d4)


# Data Preparation
---
Berikut adalah tahapan-tahapan dalam melakukan Persiapan data:
1. Menghitung jumlah data pada genre
![Image](https://github.com/user-attachments/assets/c0a0d49a-0d06-4d46-a097-0f9f5b8f776a)

2. Men-drop judul yg duplikat (membersihkan data)

![Screenshot 2025-04-21 122843](https://github.com/user-attachments/assets/1c406626-ab2c-41b7-b672-fbe7e87a6f92)

3. Mereset ulang penomoran index data (tranformasi data)

![Screenshot 2025-04-21 122938](https://github.com/user-attachments/assets/023f5864-e865-4c0f-adfe-730343c3e921)

Teknik yang digunakan pada tahapan Proses Data adalah vektorisasi fungsi CountVectorizer dari library scikit-learn. CountVectorizer digunakan untuk mengubah teks yang diberikan menjadi vektor berdasarkan frekuensi (jumlah) setiap kata yang muncul di seluruh teks. 
CountVectorizer membuat matriks di mana setiap kata unik diwakili oleh kolom matriks, dan setiap sampel teks dari dokumen adalah baris dalam matriks. Nilai setiap sel tidak lain adalah jumlah kata dalam sampel teks tertentu.

Pada proses vektorisasi ini, digunakan metode sebagai berikut. 
1. ```fit``` metode berfungsi untuk melakukan perhitungan idf pada data
![Screenshot 2025-04-21 123220](https://github.com/user-attachments/assets/6d0dc900-a9d3-4d4f-877f-ccca498228d2)
2. ```get_feature_names_out()``` berfungsi untuk melakukan mapping array dari fitur index integer ke fitur nama
3. ```fit_transform()``` berfungsi untuk mempelajari kosa kata dan Inverse Document Frequency (IDF) dengan memberikan nilai return berupa *document-term matrix*


![Screenshot 2025-04-21 123242](https://github.com/user-attachments/assets/8ad2c4c4-6af1-4a6a-b75d-3e84b7a2663e)

5. ```todense()``` berfungsi untuk mengubah vektor tf-idf dalam bentuk matriks

![Screenshot 2025-04-21 124225](https://github.com/user-attachments/assets/3fe13a67-f04a-4c07-9df4-86cd1b682c9b)


# Modeling
---
Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah *modeling* terhadap data. Pada tahap ini Model machine learning yang digunakan pada sistem rekomendasi ini adalah model _content-based filtering_ dengan _simlarty measure_ yang digunakan adalah _Cosine Similarity_.. 
Model _content-based filtering_ ini bekerja dengan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna dengan menggunakan _similarity_ tertentu.

Sedangkan _cosine similarity_ adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai _cosine similarity_.
cara kerja dari fungsi *cosine similiraty* yaitu dengan melakukan perhitungan yang sering digunakan untuk menghitung kemiripan diantara item-item [[7]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748). Secara umum, fungsi similarity adalah fungsi yang menerima dua buah obyek berupa bilangan riil (0 dan 1) dan mengembalikan nilai kemiripan (similarity) antara kedua obyek tersebut berupa bilangan riil. Cosine similarity merupakan salah satu metode pengukuran kemiripan yang populer. Metode ini digunakan untuk menghitung nilai kosinus sudut antara dua vektor dan biasanya digunakan untuk mengukur kemiripan antara dua teks/dokumen. Fungsi cosine similarity antara item A dan item B ditunjukkan sebagai berikut [[8]](https://jurnal.uns.ac.id/itsmart/article/download/35008/27748).

![Screenshot 2025-04-21 124009](https://github.com/user-attachments/assets/6086dec6-0fa9-4301-8d89-ca164e4d4fd9)

Keterangan:
```
𝑠𝑖𝑚(𝐴, 𝐵) = nilai similaritas dari item A dan item B
𝑛(𝐴) = banyaknya fitur konten item A 
𝑛(𝐵) = banyaknya fitur konten item B 
𝑛(𝐴 ∩ 𝐵)  = banyaknya fitur konten yang terdapat pada item A dan juga terdapat pada item B
```
Jika kedua objek memiliki nilai similaritas 1, maka kedua objek dikatakan identik dan sebaliknya. Semakin besar hasil dari fungsi similarity, maka kedua objek yang dievaluasi dianggap semakin mirip dan sebaliknya. 

* Berikut cara melatih model dengan menggunakan *consine similarity* yg dapat dilihat pada gambar dibawah brikut ini:
![Screenshot 2025-04-21 124244](https://github.com/user-attachments/assets/ec2ed481-3a59-4948-b98b-86a02f17e5ec)

* Pada tahapan ini menampilkan matriks kesamaan setiap judul dengan menampilkan judul film dalam 10 sampel kolom (axis = 1) dan 10 sampel baris (axis=0).
![Screenshot 2025-04-21 124316](https://github.com/user-attachments/assets/f6c55ae0-eb19-479d-b682-3f18a047aea3)


Dalam pemanggilan rekomendasi judul film menggunakan function yang dibuat dengan code seperti yg terlihat pada dibawah berikut ini:
![Screenshot 2025-04-21 124412](https://github.com/user-attachments/assets/adf218a0-0cea-4b94-a008-2dee4310372c)

Tahapan yang dilakukan pada fungsi tersebut ialah sebagai berikut.
1. Mengambil indeks dari judul film yang telah didefinisikan sebelumnnya
2. Mengambil skor kemiripan dengan semua film
3. Mengurutkan film berdasarkan skor kemiripan
4. Mengambil 19 judul berdasarkan kemiripan dari 1-20 karena urutan 0 memberikan indeks yang sama dengan judul film yang diinput
5. Mengambil judul film dari skor kemiripan
6. Mengembalikan 19 rekomendasi judul film dari kemiripan skor yang telah diurutkan dan menampilkan genre dari 19 rekomendasi film tersebut

Berikut _top_-20 _recommemdation_ berdasarkan genre dari judul film "*Toy Story (1995)*"
judul | genre
---|---
Toy Story (1995) | Adventure|Animation|Children|Comedy|Fantasy
![Screenshot 2025-04-21 124450](https://github.com/user-attachments/assets/fda662f0-d1af-4c1b-b37b-c866a23c023c)

Dengan hasil yang diberikan di atas berdasarkan judul film "Toy Story (1995)" dengan genre Adventure, Animatioan, Childrren, Comedy, Fantasi maka didapatkan 19 rekomendasi judul film dengan genre yang serupa ataupun mirip.

# Evaluation
---
Pada proyek ini, Metric yang digunakan pada sistem rekomendasi judul film berdasarkan genre adalah accuracy precision. Precision adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus

$$\ Precission=TP/(TP+FP)$$
~~~
keterangan:
TP = True Positif (prediksi positif dan hal tersebut benar)
FP = False Positif (prediksi positif dan hal tersebut salah)
~~~
Alasan accuracy Precision dipilih adalah karena metrik ini dapat membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif. Dalam hal ini adalah rasio item yang direkomendasikan memiliki genre yang mirip atau serupa dibandingkan dengan genre dari judul film yang diinput.

Code yang digunakan untuk melihat jumlah genre yang mirip atau serupa adalah sebagai berikut.
~~~
# menghitung banyaknya data genre pada hasil rekomendasi yg dilakukan 
value = pd.DataFrame(recomendation['genre'].value_counts().reset_index().values, columns = ['genre', 'count'])
value.head()
~~~
Output:
~~~

        genre   	                                                 count
0	    Adventure|Animation|Children|Comedy|Fantasy                  12
1	    Adventure|Animation|Children|Comedy|Fantasy|IMAX              3	                                 
2	    Action|Adventure|Animation|Children|Comedy|Fantasy            2
3	    Adventure|Animation|Children|Comedy|Fantasy|Romance           1
4	    Adventure|Animation|Children|Comedy|Fantasy|War               1
~~~
Dari output tersebut dihitung accuracy precision nya adalah
```
TP = 19 #jumlah prediksi benar untuk genre yang mirip atau serupa
FP = 0 #jumlah prediksi salah untuk genre yang mirip atau serupa

Precision = TP/(TP+FP)
print("{0:.0%}".format(Precision))
```
Dipilih nya nilai True Positif 19 karna ia merupakan nilai atau jumlah yg diduga memiliki kemiripan/identik dengan genre yg dipilih yaitu 19 (12+3+2+1+1). hasil rekomendasi yg dihasilkan model menunjukan kemiripan dengan genre film yg dinput yaitu Adventure, Animatioan, Childrren, Comedy dan Fantasi
sedangkan utk nilai False Positif tidak teridentifikasi pada hasil output dari genre yg diinput maka nilai nya 0 
Output:
```
100%
```
Kesimpulan dari output yang dihasilkan bahwa prediksi rekomendasi yang diberikan 100% presisi sesuai genre yang mirip atau serupa dengan genre dari judul yang diinput.
