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
<h3>Dataset yang Digunakan</h3>
<p>
Penelitian ini menggunakan data dari situs <a href="https://www.kaggle.com/datasets/nadyinky/sephora-products-and-skincare-reviews" target="_blank">Kaggle</a> dengan nama dataset <strong>Sephora Products and Skincare Reviews</strong>. Dari beberapa file yang tersedia, dua dataset yang digunakan adalah <code>product_info.csv</code> dan <code>reviews_1250-end.csv</code>. 
</p>
<ul>
  <li>
    <strong>product_info.csv</strong> berisi <strong>8.494 baris</strong> dan <strong>27 kolom</strong> yang merepresentasikan informasi detail produk.
  </li>
  <li>
    <strong>reviews_1250-end.csv</strong> berisi <strong>49.977 baris</strong> dan <strong>19 kolom</strong> yang merepresentasikan ulasan pengguna terhadap produk.
  </li>
</ul>

<h3>Fitur dan Deskripsi Dataset Produk (<code>product_info.csv</code>)</h3>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>product_id</td><td>Identitas unik produk dari situs</td></tr>
    <tr><td>product_name</td><td>Nama lengkap produk</td></tr>
    <tr><td>brand_id</td><td>Identitas unik merek produk</td></tr>
    <tr><td>brand_name</td><td>Nama lengkap merek produk</td></tr>
    <tr><td>loves_count</td><td>Jumlah pengguna yang menandai produk sebagai favorit</td></tr>
    <tr><td>rating</td><td>Rata-rata rating produk berdasarkan ulasan pengguna</td></tr>
    <tr><td>reviews</td><td>Jumlah ulasan pengguna untuk produk</td></tr>
    <tr><td>size</td><td>Ukuran produk (misal: oz, ml, g, pack, dll.)</td></tr>
    <tr><td>variation_type</td><td>Jenis variasi produk (misal: ukuran, warna)</td></tr>
    <tr><td>variation_value</td><td>Nilai spesifik dari variasi produk (misal: 100 mL, Golden Sand)</td></tr>
    <tr><td>variation_desc</td><td>Deskripsi variasi produk (misal: warna kulit terang)</td></tr>
    <tr><td>ingredients</td><td>Daftar bahan yang terkandung dalam produk</td></tr>
    <tr><td>price_usd</td><td>Harga produk dalam dolar AS</td></tr>
    <tr><td>value_price_usd</td><td>Potensi penghematan harga produk</td></tr>
    <tr><td>sale_price_usd</td><td>Harga diskon produk dalam dolar AS</td></tr>
    <tr><td>limited_edition</td><td>Apakah produk edisi terbatas (1-ya, 0-tidak)</td></tr>
    <tr><td>new</td><td>Apakah produk baru (1-ya, 0-tidak)</td></tr>
    <tr><td>online_only</td><td>Apakah hanya dijual online (1-ya, 0-tidak)</td></tr>
    <tr><td>out_of_stock</td><td>Apakah produk sedang habis stok (1-ya, 0-tidak)</td></tr>
    <tr><td>sephora_exclusive</td><td>Apakah produk eksklusif di Sephora (1-ya, 0-tidak)</td></tr>
    <tr><td>highlights</td><td>Daftar tag/fitur utama produk (misal: Vegan, Matte Finish)</td></tr>
    <tr><td>primary_category</td><td>Kategori utama produk</td></tr>
    <tr><td>secondary_category</td><td>Kategori kedua produk</td></tr>
    <tr><td>tertiary_category</td><td>Kategori ketiga produk</td></tr>
    <tr><td>child_count</td><td>Jumlah variasi produk yang tersedia</td></tr>
    <tr><td>child_max_price</td><td>Harga tertinggi dari variasi produk</td></tr>
    <tr><td>child_min_price</td><td>Harga terendah dari variasi produk</td></tr>
  </tbody>
</table>

<h3>Fitur dan Deskripsi Dataset Ulasan (<code>reviews_1250-end.csv</code>)</h3>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>author_id</td><td>Identitas unik penulis ulasan</td></tr>
    <tr><td>rating</td><td>Rating yang diberikan penulis (1-5)</td></tr>
    <tr><td>is_recommended</td><td>Apakah penulis merekomendasikan produk (1-ya, 0-tidak)</td></tr>
    <tr><td>helpfulness</td><td>Rasio rating positif terhadap total rating ulasan</td></tr>
    <tr><td>total_feedback_count</td><td>Total jumlah feedback (positif dan negatif) pada ulasan</td></tr>
    <tr><td>total_neg_feedback_count</td><td>Jumlah feedback negatif pada ulasan</td></tr>
    <tr><td>total_pos_feedback_count</td><td>Jumlah feedback positif pada ulasan</td></tr>
    <tr><td>submission_time</td><td>Tanggal ulasan diposting (yyyy-mm-dd)</td></tr>
    <tr><td>review_text</td><td>Isi utama ulasan yang ditulis penulis</td></tr>
    <tr><td>review_title</td><td>Judul ulasan</td></tr>
    <tr><td>skin_tone</td><td>Warna kulit penulis (misal: fair, tan, dll.)</td></tr>
    <tr><td>eye_color</td><td>Warna mata penulis</td></tr>
    <tr><td>skin_type</td><td>Jenis kulit penulis</td></tr>
    <tr><td>hair_color</td><td>Warna rambut penulis</td></tr>
    <tr><td>product_id</td><td>Identitas unik produk yang diulas</td></tr>
    <tr><td>product_name</td><td>Nama produk yang diulas</td></tr>
    <tr><td>brand_name</td><td>Nama merek produk yang diulas</td></tr>
    <tr><td>price_usd</td><td>Harga produk pada saat ulasan ditulis</td></tr>
  </tbody>
</table>

<h3>Ringkasan Tipe Data dan Missing Value</h3>
<ul>
  <li>
    <strong>product_info.csv</strong> memiliki 8.494 data produk unik dengan 27 fitur. Beberapa fitur seperti <code>rating</code>, <code>reviews</code>, <code>size</code>, <code>variation_type</code>, <code>variation_value</code>, <code>variation_desc</code>, <code>ingredients</code>, <code>value_price_usd</code>, <code>sale_price_usd</code>, <code>highlights</code>, <code>secondary_category</code>, <code>tertiary_category</code>, <code>child_max_price</code>, dan <code>child_min_price</code> memiliki missing value dengan jumlah bervariasi. Tidak ditemukan data duplikat pada fitur utama.</li>
  <li>
    <strong>reviews_1250-end.csv</strong> terdiri dari 49.977 data ulasan dengan 19 fitur. Beberapa fitur seperti <code>is_recommended</code>, <code>helpfulness</code>, <code>review_text</code>, <code>review_title</code>, <code>skin_tone</code>, <code>eye_color</code>, <code>skin_type</code>, dan <code>hair_color</code> memiliki missing value. Tidak ditemukan data duplikat pada fitur utama.</li>
</ul>

<h3>Jumlah Nilai Unik pada Fitur Utama</h3>
<ul>
  <li>
    Pada data produk, fitur <code>product_id</code> memiliki 8.494 nilai unik, <code>brand_id</code> sebanyak 304, dan <code>primary_category</code> sebanyak 9 kategori. Fitur lain seperti <code>size</code>, <code>variation_value</code>, dan <code>ingredients</code> juga memiliki keragaman nilai yang tinggi.
  </li>
  <li>
    Pada data ulasan, <code>author_id</code> memiliki 41.457 nilai unik, <code>product_id</code> sebanyak 1.104, dan <code>skin_tone</code> sebanyak 14 kategori berbeda. Fitur lain seperti <code>eye_color</code>, <code>skin_type</code>, dan <code>hair_color</code> juga menunjukkan variasi data yang cukup besar.
  </li>
</ul>

# DATA PREPARATION

# Model Development

# Evaluation

# Kesimpulan
