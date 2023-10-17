# Sistem_rekomendasi_film

# Domain Proyek
## Latar Belakang
Pada era digital, kita memiliki akses tak terbatas ke berbagai konten film, yang dapat membuat konsumen bingung dan merasa overwhelmed saat harus memutuskan film apa yang akan mereka tonton. Karena itu, pengembangan sistem rekomendasi menjadi sangat relevan dalam konteks ini.

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
   Untuk mengatasi masalah berlimpahnya informasi film di internet dan meningkatkan pengalaman pengguna dalam mencari film yang ingin ditonton, kita dapat mengimplementasikan sistem rekomendasi berbasis Collaborative Filtering. Collaborative Filtering akan menggunakan data seperti peringkat dan ulasan pengguna, serta genre film, untuk menghasilkan rekomendasi yang sesuai dengan preferensi pengguna. Sistem ini akan mengidentifikasi pola kesukaan pengguna dan membandingkannya dengan pola kesukaan pengguna lain, sehingga dapat merekomendasikan film yang mungkin disukai oleh pengguna berdasarkan kesamaan preferensi dengan pengguna lain. Dengan demikian, pengguna akan dapat menemukan film yang sesuai dengan selera mereka dengan lebih mudah dan menyenangkan. Selain itu, dengan mengumpulkan data interaksi pengguna, sistem ini juga dapat membantu industri perfilman dalam mengidentifikasi tren dan preferensi pengguna, yang dapat digunakan untuk pengembangan lebih lanjut dalam industri perfilman.

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

# Data Preparartion
Dalam persiapan data, saya menggunakan beberapa teknik pada tiga data frame, yaitu movie_df, rating_df, dan tags_df. Berikut adalah penjelasan singkat tentang teknik yang saya terapkan:

1. **Normalisasi:** Normalisasi dilakukan untuk mengubah nilai kolom numerik dalam dataset ke skala umum, sehingga perbedaan rentang nilai tidak memengaruhi analisis kita. Saya menggunakan metode normalisasi Min-Max, yang akan mengubah nilai-nilai dalam rentang tertentu. Dengan ini, data menjadi lebih mudah dibandingkan dan diinterpretasikan. Proses normalisasi dilakukan dengan kode yang sesuai.

Dengan menerapkan teknik-teknik ini, data yang akan digunakan untuk analisis dan pengembangan model akan menjadi lebih bersih, lengkap, dan siap digunakan. Ini akan membantu meningkatkan kualitas model rekomendasi film yang akan kita bangun nantinya.

