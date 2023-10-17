# Sistem_rekomendasi_film

# Domain Proyek
## Latar Belakang
Pada era digital, semua orang memiliki akses tak terbatas ke berbagai konten film, yang dapat membuat konsumen bingung dan merasa overwhelmed saat harus memutuskan film apa yang akan mereka tonton. Karena itu, pengembangan sistem rekomendasi menjadi sangat relevan dalam konteks ini.

Sistem rekomendasi adalah solusi yang populer untuk membantu pengguna dalam menavigasi melalui berbagai pilihan film yang ada. Salah satu metode yang digunakan dalam pengembangan sistem rekomendasi adalah Collaborative Filtering (CF), yang memungkinkan rekomendasi berdasarkan interaksi pengguna dengan item serta pola kesukaan yang mereka tunjukkan dalam sejarah interaksi mereka.

Dengan pendekatan CF, sistem rekomendasi akan menganalisis data seperti ulasan pengguna, peringkat, atau perilaku penonton lainnya untuk mencari pola yang menghubungkan pengguna yang memiliki kesukaan serupa. Kemudian, sistem ini akan merekomendasikan film berdasarkan preferensi pengguna tersebut. Ini dapat membantu pengguna menemukan film baru yang mungkin mereka sukai, bahkan jika film-film tersebut tidak mendapatkan perhatian luas dalam industri perfilman.

Oleh karena itu, penelitian ini akan mengulas pembangunan sistem rekomendasi menggunakan metode Collaborative Filtering sebagai solusi untuk mengatasi masalah penentuan pilihan film dalam era digital ini. Dengan pendekatan ini, diharapkan penggemar film dapat dengan lebih mudah menemukan film-film yang sesuai dengan selera mereka, meningkatkan pengalaman menonton mereka, dan pada akhirnya mendukung industri perfilman dalam menghadapi persaingan dari hiburan digital lainnya.

# Business Understanding
## Problem Statement
   Bagaimana cara mengatasi masalah informasi film yang berlimpah di internet, sehingga para penikmat film dapat dengan mudah menemukan film yang sesuai dengan preferensi mereka?

## Goals:
  1. Mengurangi kebingungan para penikmat film saat mencari film yang ingin ditonton.
  2. Meningkatkan efisiensi dalam menemukan film berdasarkan preferensi pengguna.
  3. Menyediakan solusi yang membantu industri perfilman dalam menghadapi persaingan hiburan digital.

## Solution Statement:
   Untuk mengatasi masalah berlimpahnya informasi film di internet dan meningkatkan pengalaman pengguna dalam mencari film yang ingin ditonton, sehingga dapat mengimplementasikan sistem rekomendasi berbasis Collaborative Filtering. Collaborative Filtering akan menggunakan data seperti peringkat dan ulasan pengguna, serta genre film, untuk menghasilkan rekomendasi yang sesuai dengan preferensi pengguna. Sistem ini akan mengidentifikasi pola kesukaan pengguna dan membandingkannya dengan pola kesukaan pengguna lain, sehingga dapat merekomendasikan film yang mungkin disukai oleh pengguna berdasarkan kesamaan preferensi dengan pengguna lain. Dengan demikian, pengguna akan dapat menemukan film yang sesuai dengan selera mereka dengan lebih mudah dan menyenangkan. Selain itu, dengan mengumpulkan data interaksi pengguna, sistem ini juga dapat membantu industri perfilman dalam mengidentifikasi tren dan preferensi pengguna, yang dapat digunakan untuk pengembangan lebih lanjut dalam industri perfilman.

# Data Understanding
Dataset yang digunakan diundung melalui laman kaggle, berikut link unduhnya: https://www.kaggle.com/datasets/aigamer/movie-lens-dataset
- Penjelasan Fitur yang ada dalam Dataset:
  - movies.csv
      - movieId : Unique Id disediakan untuk setiap Film
      - title : Nama film dengan Tahun dalam tanda kurung
      - genres : Genre pada film tersebut
  - ratings.csv
      - userId : Unique Id disediakan untuk setiap Pengguna
      - movieId : Unique Id disediakan untuk setiap Film
      - rating : Penilaian pengguna terhadap film terkait
      - timestamp : Kode waktu film
  - tags.csv
      - userId : Unique Id disediakan untuk setiap Pengguna
      - movieId : Unique Id disediakan untuk setiap Film
      - tag : Metadata yang dibuat pengguna tentang film.
      - timestamp : Kode waktu film

- Dalam Data Movies terdapat 3 fitur yakni movieId bertipe data int64, title bertipe data object, dan genres bertipe data object
- Terdapat 4 Fitur dalam dataset Rating, fitur userID bertipe data int64, fitur movieId bertipe data int64, fitur rating bertipe data float64, dan fitur timestam bertipe data int64
- Terdapat 4 fitur dalam dataset tags yaitu userId bertipe data int64, movieId bertipe data int64, tag bertipe data object, dan timestamp bertipe data int64
- Semua dataset tidak memiliki missing Value

# Data Preparation
Dalam persiapan data, menggunakan beberapa teknik pada tiga data frame, yaitu movie_df, rating_df, dan tags_df. Berikut adalah penjelasan singkat tentang teknik yang diterapkan:

1. **Normalisasi:** Normalisasi dilakukan untuk mengubah nilai kolom numerik dalam dataset ke skala umum, sehingga perbedaan rentang nilai tidak memengaruhi analisis yang dilakukan. Normalisasi dapat menggunakan metode normalisasi Min-Max, yang akan mengubah nilai-nilai dalam rentang tertentu. Dengan ini, data menjadi lebih mudah dibandingkan dan diinterpretasikan. Proses normalisasi dilakukan dengan kode yang sesuai.

Dengan menerapkan teknik-teknik ini, data yang akan digunakan untuk analisis dan pengembangan model akan menjadi lebih bersih, lengkap, dan siap digunakan. Ini akan membantu meningkatkan kualitas model rekomendasi film yang akan dibangun nantinya.

# Modeling
Proses pemodelan yang digunakan di sini melibatkan teknik embedding, khususnya menggunakan Model Neural Collaborative Filtering (NCF). Model NCF adalah jaringan saraf yang digunakan untuk menyusun rekomendasi berdasarkan umpan balik implisit dari pengguna terhadap item. Data pelatihan untuk model ini harus berisi pasangan urutan (ID pengguna, ID film) yang menunjukkan interaksi pengguna dengan item, seperti memberi peringkat atau mengklik. Model NCF pertama kali diperkenalkan dalam makalah oleh Xiangnan He, Lizi Liao, Hanwang Zhang, Liqiang Nie, Xia Hu, dan Tat-Seng Chua yang berjudul "Neural Collaborative Filtering."

Langkah-langkah untuk menghasilkan daftar rekomendasi film berdasarkan aktivitas pengguna berdasarkan peringkat yang diberikan oleh pengguna adalah sebagai berikut:

1. Mengidentifikasi film-film yang telah ditonton oleh pengguna dan menggabungkannya dalam sebuah dataframe baru.
2. Mencari peringkat terendah dari film-film yang telah ditonton oleh pengguna.
3. Membuat daftar film terbaik (top_movie_refference) dengan mengurutkannya berdasarkan peringkat film.
4. Membuat dataframe baru (user_pref_df) berdasarkan dataframe utama (movie_df) dan memilih hanya film-film yang termasuk dalam daftar film terbaik.
5. Menghitung rata-rata peringkat yang diberikan oleh pengguna untuk film-film tersebut.

# Evaluation
Dalam evaluasi model ini, kami menggunakan beberapa metrik, yaitu Mean Squared Error (MSE), precision, dan recall. Mean Squared Error adalah salah satu metrik yang paling umum digunakan untuk mengukur seberapa baik model dalam melakukan prediksi. MSE digunakan untuk mengestimasi sejauh mana prediksi model mendekati nilai aktual. Semakin rendah nilai MSE, semakin baik model dalam memprediksi data aktual, dan ini berarti model ini dapat digunakan untuk peramalan di masa depan.

- **MSE**: dihitung dengan mengurangkan nilai prediksi dari nilai aktual, kemudian hasilnya dikuadratkan dan dijumlahkan untuk semua data yang dievaluasi, kemudian hasilnya dibagi oleh jumlah data tersebut. Dalam proyek ini, nilai MSE yang diperoleh adalah 0.0083. Nilai yang mendekati nol menunjukkan bahwa prediksi model sangat sesuai dengan data aktual, sehingga model ini dapat diandalkan dalam peramalan di masa depan.
  
   ![image](https://github.com/wayanadi26/Sistem_rekomendasi_film/assets/88713651/c67f9d50-28f6-4fb2-99a0-8850b7462f95)

- **Precision**: Precision adalah tingkat sejauh mana sistem memberikan jawaban yang sesuai dengan apa yang pengguna minta. Sementara recall adalah sejauh mana sistem berhasil menemukan kembali informasi yang relevan. Dalam proyek ini, nilai Precision yang diperoleh adalah sempurna, yaitu 1.0000.

   ![image](https://github.com/wayanadi26/Sistem_rekomendasi_film/assets/88713651/b9889e6a-1ec3-4340-b4e1-d9f578157643)

- **Recal**: Recall merupakan metrik yang mengukur sejauh mana sistem berhasil dalam mengidentifikasi kembali informasi yang relevan. Dalam proyek ini, sistem berhasil mencapai nilai Recall sebesar 0.6907.

   ![image](https://github.com/wayanadi26/Sistem_rekomendasi_film/assets/88713651/357903b1-85e2-4d7e-8fbe-ba60b6995ac8)

