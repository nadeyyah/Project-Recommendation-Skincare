# Laporan Proyek Machine Learning - Nadia Alzena Zahrani
# Domain Proyek
<h2>Latar Belakang</h2>
<p>
Sephora adalah salah satu platform e-commerce terbesar yang menyediakan berbagai produk kecantikan, mulai dari skincare, makeup, perawatan rambut, hingga parfum dari berbagai merek ternama. Dengan banyaknya produk yang tersedia, pelanggan sering mengalami kesulitan dalam menemukan produk yang paling sesuai dengan kebutuhan dan preferensi mereka. Kompleksitas produk, kurangnya informasi yang memadai, serta proses pencarian yang memakan waktu menjadi tantangan utama dalam pengalaman berbelanja di platform ini.
</p>
<p>
Untuk mengatasi kendala tersebut, pengembangan sistem rekomendasi berbasis konten dianggap sebagai solusi yang tepat. Sistem ini menggunakan teknik <em>content-based filtering</em> dengan mengekstraksi fitur produk melalui TF-IDF, kemudian mengukur tingkat kemiripan antar produk menggunakan metode <strong>cosine similarity</strong>. Pendekatan ini memungkinkan sistem memberikan rekomendasi produk yang relevan dan disesuaikan dengan preferensi pengguna berdasarkan kesamaan karakteristik produk yang sebelumnya diminati (Yusuf, 2021; Sari, 2020).
</p>
<p>
Beberapa penelitian sebelumnya mengindikasikan bahwa cosine similarity merupakan metode yang efektif untuk mengukur kemiripan produk berbasis atribut teks, sehingga dapat meningkatkan akurasi sistem rekomendasi pada platform e-commerce dengan skala kecil hingga menengah. Dengan fokus pada metode ini, proyek ini bertujuan mengembangkan sistem rekomendasi yang dapat memperbaiki pengalaman berbelanja pelanggan Sephora sekaligus meningkatkan penjualan (Yusuf, 2021; Sari, 2020).
</p>
<h2>Business Understanding</h2>
<p>
Proyek ini bertujuan menciptakan sistem rekomendasi produk untuk toko online Sephora. Karena banyaknya produk yang tersedia, pelanggan sering mengalami kesulitan menemukan produk yang cocok dengan preferensi dan kebutuhan mereka. Proses pencarian yang lama dapat menurunkan tingkat kepuasan pelanggan serta efisiensi berbelanja. Oleh sebab itu, sistem rekomendasi yang mampu memberikan saran produk secara personal dan relevan sangat diperlukan untuk meningkatkan pengalaman dan loyalitas pelanggan.
</p>
<h3>Problem Statements</h3>
<ul>
  <li>Pelanggan mengalami kesulitan dalam menemukan produk yang sesuai dengan preferensi dan karakteristik mereka di tengah banyaknya pilihan produk.</li>
  <li>Proses pencarian produk yang lambat menyebabkan berkurangnya kepuasan pelanggan dan menurunkan efisiensi berbelanja.</li>
</ul>
<h3>Goals</h3>
<ul>
  <li>Mengembangkan sistem rekomendasi produk yang mampu memberikan rekomendasi yang relevan dan personal berdasarkan preferensi pelanggan.</li>
  <li>Meningkatkan pengalaman berbelanja, kepuasan pelanggan, dan penjualan melalui rekomendasi yang akurat serta proses pencarian yang lebih cepat dan efisien.</li>
</ul>
<h3>Solution Statement</h3>
<ul>
  <li>Mengimplementasikan metode <em>content-based filtering</em> dengan menggunakan TF-IDF untuk mengekstraksi fitur produk seperti bahan, kategori utama, dan kategori tersier.</li>
  <li>Menghitung kemiripan antar produk menggunakan <strong>cosine similarity</strong> untuk merekomendasikan produk yang memiliki karakteristik serupa dengan produk yang diminati oleh pengguna.</li>
</ul>
<p>
Dengan pendekatan ini, sistem diharapkan dapat memberikan rekomendasi yang lebih tepat dan sesuai dengan kebutuhan pelanggan, sehingga dapat meningkatkan kepuasan mereka dan mendorong peningkatan penjualan produk di platform Sephora.
</p>
<!-- Referensi -->
<p><strong>Referensi:</strong></p>
<ul>
  <li>Yusuf, M. (2021). Penerapan Sistem Rekomendasi Content Based Filtering pada Mobile E-Commerce. <em>Repository Darmajaya</em>.</li>
  <li>Sari, R. (2020). Sistem Rekomendasi Produk Berbasis Content-Based Filtering Menggunakan Cosine Similarity. <em>Jurnal Teknologi Informasi</em>.</li>
</ul>

# Data Understanding
<h2>Data yang Digunakan</h2>
<p>
Dataset ini diambil dari <a href="https://www.kaggle.com/datasets/nadyinky/sephora-products-and-skincare-reviews" target="_blank">Kaggle - Sephora Products and Skincare Reviews</a>. Dua file utama yang digunakan adalah <code>product_info.csv</code> dan <code>reviews_1250-end.csv</code> dengan dimensi masing-masing (8494, 27) dan (49977, 19).
</p>

<h3>Dataset Produk (<code>product_info.csv</code>)</h3>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Description</th>
      <th>Data Type</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>product_id</td><td>Identitas unik produk dari situs</td><td>object</td></tr>
    <tr><td>product_name</td><td>Nama lengkap produk</td><td>object</td></tr>
    <tr><td>brand_id</td><td>Identitas unik merek produk</td><td>int64</td></tr>
    <tr><td>brand_name</td><td>Nama lengkap merek produk</td><td>object</td></tr>
    <tr><td>loves_count</td><td>Jumlah pengguna yang menandai produk sebagai favorit</td><td>int64</td></tr>
    <tr><td>rating</td><td>Rata-rata rating produk berdasarkan ulasan pengguna</td><td>float64</td></tr>
    <tr><td>reviews</td><td>Jumlah ulasan pengguna untuk produk</td><td>float64</td></tr>
    <tr><td>size</td><td>Ukuran produk (misal: oz, ml, g, pack, dll.)</td><td>object</td></tr>
    <tr><td>variation_type</td><td>Jenis variasi produk (misal: ukuran, warna)</td><td>object</td></tr>
    <tr><td>variation_value</td><td>Nilai spesifik dari variasi produk (misal: 100 mL, Golden Sand)</td><td>object</td></tr>
    <tr><td>variation_desc</td><td>Deskripsi variasi produk (misal: warna kulit terang)</td><td>object</td></tr>
    <tr><td>ingredients</td><td>Daftar bahan yang terkandung dalam produk</td><td>object</td></tr>
    <tr><td>price_usd</td><td>Harga produk dalam dolar AS</td><td>float64</td></tr>
    <tr><td>value_price_usd</td><td>Potensi penghematan harga produk</td><td>float64</td></tr>
    <tr><td>sale_price_usd</td><td>Harga diskon produk dalam dolar AS</td><td>float64</td></tr>
    <tr><td>limited_edition</td><td>Apakah produk edisi terbatas (1-ya, 0-tidak)</td><td>int64</td></tr>
    <tr><td>new</td><td>Apakah produk baru (1-ya, 0-tidak)</td><td>int64</td></tr>
    <tr><td>online_only</td><td>Apakah hanya dijual online (1-ya, 0-tidak)</td><td>int64</td></tr>
    <tr><td>out_of_stock</td><td>Apakah produk sedang habis stok (1-ya, 0-tidak)</td><td>int64</td></tr>
    <tr><td>sephora_exclusive</td><td>Apakah produk eksklusif di Sephora (1-ya, 0-tidak)</td><td>int64</td></tr>
    <tr><td>highlights</td><td>Daftar tag/fitur utama produk (misal: Vegan, Matte Finish)</td><td>object</td></tr>
    <tr><td>primary_category</td><td>Kategori utama produk</td><td>object</td></tr>
    <tr><td>secondary_category</td><td>Kategori kedua produk</td><td>object</td></tr>
    <tr><td>tertiary_category</td><td>Kategori ketiga produk</td><td>object</td></tr>
    <tr><td>child_count</td><td>Jumlah variasi produk yang tersedia</td><td>int64</td></tr>
    <tr><td>child_max_price</td><td>Harga tertinggi dari variasi produk</td><td>float64</td></tr>
    <tr><td>child_min_price</td><td>Harga terendah dari variasi produk</td><td>float64</td></tr>
  </tbody>
</table>

<h3>Dataset Ulasan (<code>reviews_1250-end.csv</code>)</h3>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Description</th>
      <th>Data Type</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>author_id</td><td>Identitas unik penulis ulasan</td><td>object</td></tr>
    <tr><td>rating</td><td>Rating yang diberikan penulis (1-5)</td><td>int64</td></tr>
    <tr><td>is_recommended</td><td>Apakah penulis merekomendasikan produk (1-ya, 0-tidak)</td><td>float64</td></tr>
    <tr><td>helpfulness</td><td>Rasio rating positif terhadap total rating ulasan</td><td>float64</td></tr>
    <tr><td>total_feedback_count</td><td>Total jumlah feedback (positif dan negatif) pada ulasan</td><td>int64</td></tr>
    <tr><td>total_neg_feedback_count</td><td>Jumlah feedback negatif pada ulasan</td><td>int64</td></tr>
    <tr><td>total_pos_feedback_count</td><td>Jumlah feedback positif pada ulasan</td><td>int64</td></tr>
    <tr><td>submission_time</td><td>Tanggal ulasan diposting (yyyy-mm-dd)</td><td>object</td></tr>
    <tr><td>review_text</td><td>Isi utama ulasan yang ditulis penulis</td><td>object</td></tr>
    <tr><td>review_title</td><td>Judul ulasan</td><td>object</td></tr>
    <tr><td>skin_tone</td><td>Warna kulit penulis (misal: fair, tan, dll.)</td><td>object</td></tr>
    <tr><td>eye_color</td><td>Warna mata penulis</td><td>object</td></tr>
    <tr><td>skin_type</td><td>Jenis kulit penulis</td><td>object</td></tr>
    <tr><td>hair_color</td><td>Warna rambut penulis</td><td>object</td></tr>
    <tr><td>product_id</td><td>Identitas unik produk yang diulas</td><td>object</td></tr>
    <tr><td>product_name</td><td>Nama produk yang diulas</td><td>object</td></tr>
    <tr><td>brand_name</td><td>Nama merek produk yang diulas</td><td>object</td></tr>
    <tr><td>price_usd</td><td>Harga produk pada saat ulasan ditulis</td><td>float64</td></tr>
  </tbody>
</table>

<h3>Ringkasan Missing Value</h3>
<h4>Dataset Produk (product_info.csv)</h4>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Jumlah Missing Value</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>product_id</td><td>0</td></tr>
    <tr><td>product_name</td><td>0</td></tr>
    <tr><td>brand_id</td><td>0</td></tr>
    <tr><td>brand_name</td><td>0</td></tr>
    <tr><td>loves_count</td><td>0</td></tr>
    <tr><td>rating</td><td>278</td></tr>
    <tr><td>reviews</td><td>278</td></tr>
    <tr><td>size</td><td>1631</td></tr>
    <tr><td>variation_type</td><td>1444</td></tr>
    <tr><td>variation_value</td><td>1598</td></tr>
    <tr><td>variation_desc</td><td>7244</td></tr>
    <tr><td>ingredients</td><td>945</td></tr>
    <tr><td>price_usd</td><td>0</td></tr>
    <tr><td>value_price_usd</td><td>8043</td></tr>
    <tr><td>sale_price_usd</td><td>8224</td></tr>
    <tr><td>limited_edition</td><td>0</td></tr>
    <tr><td>new</td><td>0</td></tr>
    <tr><td>online_only</td><td>0</td></tr>
    <tr><td>out_of_stock</td><td>0</td></tr>
    <tr><td>sephora_exclusive</td><td>0</td></tr>
    <tr><td>highlights</td><td>2207</td></tr>
    <tr><td>primary_category</td><td>0</td></tr>
    <tr><td>secondary_category</td><td>8</td></tr>
    <tr><td>tertiary_category</td><td>990</td></tr>
    <tr><td>child_count</td><td>0</td></tr>
    <tr><td>child_max_price</td><td>5740</td></tr>
    <tr><td>child_min_price</td><td>5740</td></tr>
  </tbody>
</table>

<h4>Dataset Ulasan (reviews_1250-end.csv)</h4>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Jumlah Missing Value</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Unnamed: 0</td><td>0</td></tr>
    <tr><td>author_id</td><td>0</td></tr>
    <tr><td>rating</td><td>0</td></tr>
    <tr><td>is_recommended</td><td>3817</td></tr>
    <tr><td>helpfulness</td><td>13455</td></tr>
    <tr><td>total_feedback_count</td><td>0</td></tr>
    <tr><td>total_neg_feedback_count</td><td>0</td></tr>
    <tr><td>total_pos_feedback_count</td><td>0</td></tr>
    <tr><td>submission_time</td><td>0</td></tr>
    <tr><td>review_text</td><td>59</td></tr>
    <tr><td>review_title</td><td>14378</td></tr>
    <tr><td>skin_tone</td><td>7201</td></tr>
    <tr><td>eye_color</td><td>6260</td></tr>
    <tr><td>skin_type</td><td>3631</td></tr>
    <tr><td>hair_color</td><td>8851</td></tr>
    <tr><td>product_id</td><td>0</td></tr>
    <tr><td>product_name</td><td>0</td></tr>
    <tr><td>brand_name</td><td>0</td></tr>
    <tr><td>price_usd</td><td>0</td></tr>
  </tbody>
</table>
<ul>
  <li>
    <strong>product_info.csv</strong> memiliki 8.494 data produk unik dengan 27 fitur. Beberapa fitur seperti <code>rating</code>, <code>reviews</code>, <code>size</code>, <code>variation_type</code>, <code>variation_value</code>, <code>variation_desc</code>, <code>ingredients</code>, <code>value_price_usd</code>, <code>sale_price_usd</code>, <code>highlights</code>, <code>secondary_category</code>, <code>tertiary_category</code>, <code>child_max_price</code>, dan <code>child_min_price</code> memiliki missing value dengan jumlah bervariasi. Tidak ditemukan data duplikat pada fitur utama.</li>
  <li>
    <strong>reviews_1250-end.csv</strong> terdiri dari 49.977 data ulasan dengan 19 fitur. Beberapa fitur seperti <code>is_recommended</code>, <code>helpfulness</code>, <code>review_text</code>, <code>review_title</code>, <code>skin_tone</code>, <code>eye_color</code>, <code>skin_type</code>, dan <code>hair_color</code> memiliki missing value. Tidak ditemukan data duplikat pada fitur utama.</li>
</ul>
<ul>
  <li>
    Pada data produk, fitur <code>product_id</code> memiliki 8.494 nilai unik, <code>brand_id</code> sebanyak 304, dan <code>primary_category</code> sebanyak 9 kategori. Fitur lain seperti <code>size</code>, <code>variation_value</code>, dan <code>ingredients</code> juga memiliki keragaman nilai yang tinggi.
  </li>
  <li>
    Pada data ulasan, <code>author_id</code> memiliki 41.457 nilai unik, <code>product_id</code> sebanyak 1.104, dan <code>skin_tone</code> sebanyak 14 kategori berbeda. Fitur lain seperti <code>eye_color</code>, <code>skin_type</code>, dan <code>hair_color</code> juga menunjukkan variasi data yang cukup besar.
  </li>
</ul>
<h3>Exploratory Data Analysis (EDA)</h3>
<ol>
  <li>
    <strong>Top 5 Most Dominating Product Types by Primary Category</strong><br>
    Visualisasi ini menunjukkan lima kategori utama produk dengan jumlah terbanyak pada dataset. Jenis produk primer yang paling banyak dijual pada situs Sephora adalah <strong>Skincare, Makeup, Fragrance, Hair,</strong> dan <strong>Bath & Body Mist</strong>. Hal ini menandakan bahwa kebutuhan utama pelanggan Sephora memang berpusat pada perawatan kulit dan kecantikan.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_1.png" alt="Top 5 Most Dominating Product Types by Primary Category" width="500"><br>
  </li>
  <li>
    <strong>Top 5 Brand Dominations</strong><br>
    Grafik berikut menampilkan lima merek dengan jumlah produk terbanyak di katalog Sephora. Brand yang paling banyak dijual adalah <strong>Sephora Collection, Clinique, Dior, Kérastase,</strong> dan <strong>Tarte</strong>. Dominasi brand-brand ini menunjukkan kepercayaan pelanggan dan kekuatan brand di pasar kecantikan.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_2.png" alt="Top 5 Brand Dominations" width="500"><br>
  </li>
  <li>
    <strong>Top 5 Ingredient Dominations</strong><br>
    Visualisasi ini memperlihatkan lima bahan yang paling sering digunakan dalam produk-produk kecantikan di dataset. Ingredients yang paling banyak dikandung oleh produk yang dijual pada toko ini adalah <strong>Glycerin, Phenoxyethanol, Caprylyl Glycol, Limonene,</strong> dan <strong>Tocopherol</strong>. Bahan-bahan ini umum ditemukan dalam produk skincare karena manfaatnya yang baik untuk kulit.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_3.png" alt="Top 5 Ingredient Dominations" width="500"><br>
  </li>
  <li>
    <strong>Rating Distributions</strong><br>
    Grafik distribusi rating memberikan gambaran bagaimana persebaran penilaian produk oleh pengguna. <strong>Rating 5 adalah rating yang paling sering diberikan oleh author pada saat memberikan penilaian produk</strong>, sementara rating rendah seperti 2 sangat jarang diberikan. Hal ini menunjukkan tingkat kepuasan pelanggan yang tinggi terhadap produk-produk di Sephora.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_4.png" alt="Rating Distributions" width="500"><br>
  </li>
  <li>
    <strong>Distribution of Average Ratings by Authors</strong><br>
    Visualisasi ini menampilkan distribusi rata-rata rating yang diberikan oleh para penulis ulasan. Sebagian besar author cenderung memberikan rating tinggi, memperkuat temuan bahwa kepuasan pelanggan terhadap produk Sephora memang sangat baik.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_5.png" alt="Distribution of Average Ratings by Authors" width="500"><br>
  </li>
  <li>
    <strong>Average Rating for Top 5 Most Reviewed Product</strong><br>
    Grafik berikut menunjukkan rata-rata rating untuk lima produk dengan jumlah ulasan terbanyak. <strong>Lima produk dengan jumlah ulasan terbanyak semuanya memiliki rata-rata penilaian yang tinggi, yaitu di atas 4,5</strong>. Hal ini menandakan bahwa produk-produk populer di Sephora tidak hanya banyak diminati, tetapi juga memiliki kualitas yang sangat baik menurut pelanggan.<br>
    <img src="https://raw.githubusercontent.com/nadeyyah/Project-Recommendation-Skincare/main/recommendation_asset/asset_6.png" alt="Average rating for Top 5 Most Reviewed product" width="500"><br>
  </li>
</ol>

# DATA PREPARATION

## Product Dataset (Content-Based Filtering)
Dataset produk awal memiliki dimensi **(8494, 27)**, artinya terdapat 8494 baris data produk dengan 27 fitur. Dataset ini berisi informasi produk yang dijual di situs Sephora, termasuk kandungan produk, jenis produk, dan atribut lainnya.

### Pemilihan Fitur
Dari 27 fitur, dipilih 6 fitur yang dianggap paling relevan untuk analisis produk skincare secara komprehensif, yaitu:

- `product_id`: Identitas unik untuk membedakan setiap produk.
- `product_name`: Nama produk.
- `brand_name`: Nama brand yang memproduksi produk.
- `ingredients`: Kandungan bahan dalam produk, penting untuk menyesuaikan dengan kebutuhan kulit pengguna.
- `primary_category`: Kategori utama produk, seperti pewangi atau lotion.
- `tertiary_category`: Kategori tambahan yang lebih spesifik untuk memperjelas karakteristik produk.

### Pemeriksaan Data
- **Duplikasi data**: Tidak ditemukan data duplikat.

- **Missing value**: Terdapat missing value pada fitur `ingredients` (945) dan `tertiary_category` (990).

Setelah pembersihan, dataset tersisa **6642 baris** dengan fitur-fitur unik sebagai berikut:
<code>
product_id 6642
product_name 6592
brand_name 278
ingredients 5962
primary_category 7
tertiary_category 106
</code>

- ### Vektorisasi Fitur
Menggunakan TF-IDF Vectorizer untuk mengubah fitur teks menjadi representasi numerik, 
<p> Bobot TF-IDF untuk term <code>t</code> dalam dokumen <code>d</code> dihitung dengan mengalikan nilai TF dan IDF: </p>

<p style="text-align: center;">
  <strong>TF-IDF(t, d) = TF(t, d) × IDF(t)</strong>
</p>

<p>Dengan demikian, kata-kata yang sering muncul dalam sebuah dokumen tetapi jarang muncul di dokumen lain akan memiliki bobot TF-IDF yang tinggi, sehingga lebih representatif untuk dokumen tersebut.</p>
Langkah ini menghasilkan matriks fitur gabungan yang siap digunakan dalam sistem rekomendasi berbasis konten.

## Reviews Dataset (Collaborative-filtering)

Dataset ulasan awal berdimensi **(49977, 19)**, berisi data rating dan ulasan pengguna terhadap produk.

### Pemilihan Fitur
Dari 19 fitur, dipilih 3 fitur utama:

- `author_id`: Identitas unik pengguna yang memberikan ulasan.
- `product_id`: Identitas produk yang diulas.
- `rating`: Penilaian yang diberikan pengguna.

### Pemeriksaan Data
- **Missing value**: Tidak ditemukan missing value pada ketiga fitur ini.
- **Duplikasi data**: Ditemukan 33 data duplikat yang kemudian dihapus.
Setelah pembersihan, dataset tersisa **49944 baris** dengan karakter unik:
<code>
author_id 41457
product_id 1104
rating 5
</code>

### Split Data dan Encoding
Data dibagi menjadi data latih dan uji dengan proporsi 80:20. Selanjutnya, `author_id` dan `product_id` diencoding menjadi indeks numerik berdasarkan data latih agar dapat digunakan dalam model.
<code>
train_df, test_df = train_test_split(reviews_df, test_size=0.2, random_state=42)
</code>

<h3>Encoding User dan Product dari Data Train</h3>
<p>
Pada tahap ini, <code>author_id</code> dan <code>product_id</code> dari data training diubah menjadi format numerik menggunakan <code>pandas.Categorical</code>. Proses ini penting agar data dapat digunakan dalam model machine learning yang memerlukan input numerik.
</p>
<p>
Label Encoding adalah metode yang mengonversi setiap nilai kategori menjadi angka integer yang berbeda, tanpa membuat kolom dummy atau one-hot encoding. Ini sangat cocok untuk data seperti user ID dan product ID yang bersifat nominal dan memiliki banyak kategori unik. Dengan encoding ini, setiap user dan produk memiliki indeks numerik yang dapat digunakan untuk membangun matriks user-item pada model collaborative filtering.
</p>
<pre><code>user_cat = pd.Categorical(train_df['author_id'])
product_cat = pd.Categorical(train_df['product_id'])

train_user_ids = user_cat.codes
train_product_ids = product_cat.codes
train_ratings = train_df['rating'].values
</code></pre>
<p>
Selanjutnya, dibuat mapping dari <code>author_id</code> dan <code>product_id</code> ke indeks numerik yang unik. Mapping ini berguna untuk mengkonversi data test nanti agar sesuai dengan encoding data train.
</p>

<pre><code>user_id_to_idx = dict(zip(user_cat.categories, range(len(user_cat.categories))))
product_id_to_idx = dict(zip(product_cat.categories, range(len(product_cat.categories))))
</code></pre>

<h3>Membuat Matriks Rating User-Item untuk Data Train</h3>
<p>
Jumlah pengguna dan produk dihitung berdasarkan kategori unik. Kemudian dibuat matriks nol dengan ukuran <code>(num_users, num_products)</code> untuk menampung rating yang diberikan oleh pengguna ke produk.
</p>

<pre><code>num_users = len(user_cat.categories)
num_products = len(product_cat.categories)
rating_matrix = np.zeros((num_users, num_products))

for u, p, r in zip(train_user_ids, train_product_ids, train_ratings):
    rating_matrix[u, p] = r
</code></pre>

<p>
Matriks ini berisi rating yang diberikan oleh setiap pengguna pada produk tertentu dan digunakan sebagai input untuk model collaborative filtering.
</p>

<h3>Fungsi Encoding untuk Data Test</h3>
<p>
Secara teknis, <code>pandas.Categorical</code> mengelompokkan data ke dalam kategori dan memberikan kode integer untuk setiap kategori berdasarkan urutan kemunculannya. Contohnya, jika terdapat user dengan ID 'U1', 'U2', dan 'U3', maka mereka bisa diberi kode 0, 1, dan 2 secara berurutan.
</p>
<p>
Untuk data test, <code>author_id</code> dan <code>product_id</code> juga harus diencoding menggunakan mapping yang dibuat dari data train agar konsisten. Fungsi berikut melakukan pemetaan tersebut dan menghilangkan baris yang mengandung user atau produk yang tidak dikenal (cold start problem).
</p>

<pre><code>def encode_user_product_ids(df, user_mapping, product_mapping):
    encoded_users = df['author_id'].map(user_mapping)
    encoded_products = df['product_id'].map(product_mapping)
    mask = encoded_users.notna() & encoded_products.notna()
    return encoded_users[mask].astype(int), encoded_products[mask].astype(int), df.loc[mask, 'rating']

test_user_ids, test_product_ids, test_ratings = encode_user_product_ids(test_df, user_id_to_idx, product_id_to_idx)
</code></pre>

<p>
Dengan cara ini, data test siap digunakan untuk evaluasi model dengan format yang sama seperti data train.
</p>

# Model Development
<h3>Model yang Digunakan</h3>

<h4>1. Content-Based Filtering</h4>
<p>
Content-Based Filtering adalah metode rekomendasi yang menggunakan informasi fitur produk untuk memberikan rekomendasi produk serupa berdasarkan preferensi pengguna sebelumnya. Sistem ini membandingkan fitur produk yang sudah disukai pengguna dengan produk lain menggunakan ukuran kesamaan, dalam hal ini <strong>cosine similarity</strong>.
</p>

<h5>Kelebihan:</h5>
<ul>
  <li>Dapat memberikan rekomendasi personal tanpa perlu data pengguna lain.</li>
  <li>Bekerja baik untuk produk baru yang memiliki deskripsi fitur lengkap.</li>
  <li>Mudah diinterpretasikan karena berdasarkan kesamaan fitur produk.</li>
</ul>

<h5>Kekurangan:</h5>
<ul>
  <li>Terbatas pada fitur yang tersedia, sehingga kurang efektif jika fitur kurang informatif.</li>
  <li>Rentan terhadap masalah "serendipity" dan kurang variasi rekomendasi.</li>
  <li>Memerlukan data fitur produk yang lengkap dan berkualitas.</li>
</ul>

<h5>Rumus Cosine Similarity</h5>

![Cosine Similarity](https://pplx-res.cloudinary.com/image/private/user_uploads/71119209/16062b23-fea4-4776-802c-fa909663875a/image.jpg)

<h5>Langkah Pemodelan Content-Based Filtering</h5>

<pre><code>
## Menghitung matriks cosine similarity antar produk
cosine_sim_matrix = cosine_similarity(combined_features)

## Menyimpan matriks similarity dalam DataFrame dengan index product_id
similarity_df = pd.DataFrame(cosine_sim_matrix, index=product_df['product_id'], columns=product_df['product_id'])

## Fungsi untuk menghasilkan rekomendasi berdasarkan product_id
def generate_recommendations(item_id, num_recommendations=5):
    idx = product_df.index[product_df['product_id'] == item_id].tolist()[0]
    similarity_scores = cosine_sim_matrix[idx]
    sorted_indices = similarity_scores.argsort()[::-1]
    filtered_indices = [i for i in sorted_indices if i != idx][:num_recommendations]
    recommended_items = product_df.loc[filtered_indices, ['product_name', 'brand_name', 'primary_category', 'tertiary_category']].copy()
    recommended_items.insert(0, 'ranking', range(1, num_recommendations + 1))
    product_name = product_df.loc[product_df['product_id'] == item_id, 'product_name'].values[0]

    print(f"Recommendations for: {product_name}\n")
    print(tabulate(recommended_items, headers='keys', tablefmt='psql', showindex=False))

    return {
        'product_name': product_name,
        'recommendations': recommended_items
    }
</code></pre>
<p><strong>Parameter fungsi <code>generate_recommendations</code>:</strong></p>
<ul>
  <li><code>item_id</code>: ID produk yang menjadi acuan rekomendasi.</li>
  <li><code>num_recommendations</code>: Jumlah produk yang ingin direkomendasikan (default 5).</li>
</ul>
---

<h4>2. Collaborative Filtering</h4>
<p>
Collaborative Filtering merekomendasikan produk berdasarkan interaksi pengguna lain yang memiliki preferensi serupa. Model ini menggunakan data rating pengguna terhadap produk dan menghitung kesamaan baik antar produk (item-based) maupun antar pengguna (user-based) menggunakan <strong>cosine similarity</strong>.
</p>

<h5>Kelebihan:</h5>
<ul>
  <li>Dapat menemukan pola preferensi yang kompleks tanpa memerlukan fitur produk.</li>
  <li>Mampu memberikan rekomendasi yang bervariasi dan serendipity lebih tinggi.</li>
  <li>Bekerja dengan baik pada data rating yang cukup besar.</li>
</ul>

<h5>Kekurangan:</h5>
<ul>
  <li>Memerlukan data rating pengguna yang cukup lengkap (cold start problem).</li>
  <li>Rentan terhadap sparsity (data sangat jarang) dan skalabilitas jika data sangat besar.</li>
</ul>

<h5>Langkah Pemodelan Collaborative Filtering</h5>
<pre><code># Transpose matriks rating untuk mendapatkan vektor item
item_matrix = rating_matrix.T

# Hitung cosine similarity antar item
item_similarity = cosine_similarity(item_matrix)

# Fungsi rekomendasi gabungan item-based dan user-based
def recommend_products_with_cosine_and_similar_users(user_id, review_data, product_data, n=5, m=5):
    if user_id not in review_data['author_id'].values:
        print(f"User {user_id} not found in the review data.")
        return

    # Buat matriks user-product rating
    user_product_matrix = review_data.pivot_table(index='author_id', columns='product_id', values='rating').fillna(0)

    # Hitung matriks similarity item dan user
    item_similarity_matrix = cosine_similarity(user_product_matrix.T)
    item_similarity_df = pd.DataFrame(item_similarity_matrix, index=user_product_matrix.columns, columns=user_product_matrix.columns)

    user_similarity_matrix = cosine_similarity(user_product_matrix)
    user_similarity_df = pd.DataFrame(user_similarity_matrix, index=user_product_matrix.index, columns=user_product_matrix.index)

    # Produk yang sudah dirating user
    user_ratings = review_data[review_data['author_id'] == user_id]
    rated_products = user_ratings['product_id'].tolist()

    all_products = user_product_matrix.columns.tolist()
    unrated_products = [p for p in all_products if p not in rated_products]

    # Hitung skor rekomendasi berbasis item
    scores = {}
    for rated_product in rated_products:
        if rated_product not in item_similarity_df.index:
            continue
        rated_product_rating = user_ratings[user_ratings['product_id'] == rated_product]['rating'].values[0]
        for unrated_product in unrated_products:
            if unrated_product not in item_similarity_df.columns:
                continue
            similarity_score = item_similarity_df.loc[rated_product, unrated_product]
            scores[unrated_product] = scores.get(unrated_product, 0) + similarity_score * rated_product_rating

    recommended_products = sorted(scores.items(), key=lambda x: x[1], reverse=True)[:n]

    # Hitung rekomendasi berbasis user dari user serupa
    if user_id not in user_similarity_df.index:
        print(f"User {user_id} not found in the user similarity matrix.")
        similar_user_recommendations = []
    else:
        similar_users = user_similarity_df.loc[user_id].sort_values(ascending=False).drop(user_id).head(m).index.tolist()
        similar_user_scores = {}
        for sim_user in similar_users:
            sim_user_ratings = review_data[review_data['author_id'] == sim_user]
            for _, row in sim_user_ratings.iterrows():
                product = row['product_id']
                rating = row['rating']
                if product not in rated_products and rating >= 4:
                    similar_user_scores[product] = max(similar_user_scores.get(product, 0), rating)
        similar_user_recommendations = sorted(similar_user_scores.items(), key=lambda x: x[1], reverse=True)[:m]

    # Tampilkan rekomendasi item-based
    print(f"\nTop-{n} Item-based Recommendations for User {user_id}:\n")
    recommendations = []
    for rank, (product_id, score) in enumerate(recommended_products, start=1):
        product_info = product_data[product_data['product_id'] == product_id]
        if product_info.empty:
            continue
        product_name = product_info.iloc[0]['product_name']
        category = product_info.iloc[0]['primary_category']
        recommendations.append([rank, product_id, product_name, category, score])
    print(tabulate(recommendations, headers=["Rank", "Product ID", "Product Name", "Category", "Score"], tablefmt="psql"))

    # Tampilkan rekomendasi user-based
    print(f"\nTop-{m} User-based Recommendations from Similar Users for User {user_id}:\n")
    user_based_recs = []
    for rank, (product_id, rating) in enumerate(similar_user_recommendations, start=1):
        product_info = product_data[product_data['product_id'] == product_id]
        if product_info.empty:
            continue
        product_name = product_info.iloc[0]['product_name']
        category = product_info.iloc[0]['primary_category']
        user_based_recs.append([rank, product_id, product_name, category, rating])
    print(tabulate(user_based_recs, headers=["Rank", "Product ID", "Product Name", "Category", "Rating"], tablefmt="psql"))
</code></pre>

<p><strong>Parameter fungsi <code>recommend_products_with_cosine_and_similar_users</code>:</strong></p>
<ul>
  <li><code>user_id</code>: ID pengguna yang ingin diberikan rekomendasi.</li>
  <li><code>review_data</code>: DataFrame berisi data ulasan dan rating pengguna.</li>
  <li><code>product_data</code>: DataFrame berisi data produk.</li>
  <li><code>n</code>: Jumlah rekomendasi berbasis item yang ingin ditampilkan (default 5).</li>
  <li><code>m</code>: Jumlah rekomendasi berbasis user dari pengguna serupa (default 5).</li>
</ul>

---

# Evaluation

# Kesimpulan
