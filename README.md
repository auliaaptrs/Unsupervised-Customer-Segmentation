-----

# **Analisis Segmentasi Pelanggan (Unsupervised Customer Segmentation)**
**Aulia Putri Salsabila - 5025221281**


## **Deskripsi Proyek**

Proyek ini bertujuan untuk melakukan segmentasi pelanggan grosir berdasarkan data pengeluaran tahunan mereka pada berbagai kategori produk. Dengan menggunakan teknik *unsupervised machine learning*, proyek ini mengidentifikasi kelompok-kelompok (cluster) pelanggan yang berbeda secara alami tanpa menggunakan label yang sudah ada sebelumnya. Tujuannya adalah untuk mendapatkan wawasan mendalam tentang perilaku pelanggan yang dapat digunakan untuk strategi pemasaran dan bisnis yang lebih tertarget.

## **Dataset**

Dataset yang digunakan berisi data dari 440 pelanggan grosir dengan 8 fitur sebagai berikut:

  - **Fresh**: Pengeluaran tahunan untuk produk segar.
  - **Milk**: Pengeluaran tahunan untuk produk susu.
  - **Grocery**: Pengeluaran tahunan untuk produk grosir.
  - **Frozen**: Pengeluaran tahunan untuk produk beku.
  - **Detergents\_Paper**: Pengeluaran tahunan untuk deterjen dan produk kertas.
  - **Delicassen**: Pengeluaran tahunan untuk produk deli.
  - **Channel**: Kanal penjualan pelanggan (Horeca: Hotel/Restoran/Kafe atau Retail).
  - **Region**: Wilayah asal pelanggan (Jakarta, Surabaya, atau Lainnya).

## **Alur Analisis**

Analisis dilakukan melalui beberapa tahapan yang sistematis, yaitu:

1.  **Pembersihan dan Eksplorasi Data (EDA)**

      * Memeriksa data untuk nilai yang hilang (*missing values*) dan memastikan tipe data sesuai.
      * Melakukan analisis outlier menggunakan visualisasi (boxplot dan histogram), yang menunjukkan bahwa data sangat condong ke kanan (*right-skewed*).
      * Menganalisis korelasi antar fitur, di mana ditemukan korelasi kuat antara pengeluaran `Grocery`, `Milk`, dan `Detergents_Paper`.

2.  **Pra-pemrosesan Data**

      * **Transformasi Logaritmik**: Menerapkan transformasi log pada fitur numerik untuk menormalkan distribusi data yang condong dan mengurangi dampak outlier.
      * **Standarisasi**: Menggunakan `StandardScaler` untuk menskalakan data agar setiap fitur memiliki rata-rata 0 dan standar deviasi 1, sebuah langkah penting untuk banyak algoritma clustering.
      * **Reduksi Dimensi**: Menerapkan *Principal Component Analysis* (PCA) untuk mereduksi data menjadi 2 dimensi utama guna mempermudah visualisasi dan evaluasi awal model.

3.  **Pemodelan Clustering**
    Empat algoritma clustering yang berbeda diimplementasikan dan dievaluasi untuk menemukan model segmentasi terbaik:

      * **K-Means Clustering**: Menggunakan *Elbow Method* dan *Silhouette Score* untuk menentukan jumlah cluster yang optimal.
      * **Hierarchical Clustering**: Mengevaluasi berbagai metode *linkage* (Ward, Complete, Average, Single) berdasarkan *Silhouette Score*.
      * **DBSCAN**: Melakukan pencarian parameter (`eps` dan `min_samples`) untuk menemukan kepadatan cluster yang paling sesuai.
      * **Gaussian Mixture Model (GMM)**: Menggunakan *BIC Score* dan *Silhouette Score* untuk menentukan jumlah komponen yang optimal.

## **Hasil dan Kesimpulan**

Setelah mengevaluasi semua model, perbandingan akhir dilakukan menggunakan **Silhouette Score** pada data yang telah distandardisasi untuk menentukan performa terbaik.

| Metode Clustering | Silhouette Score |
| :--- | :-- |
| **Hierarchical** | **0.4799** |
| K-Means | 0.2871 |
| GMM | 0.2847 |
| DBSCAN | 0.2247 |

**Kesimpulan:**

  * **Model Terbaik**: **Hierarchical Clustering** dengan 2 cluster dan metode `single` linkage memberikan hasil terbaik dengan *Silhouette Score* tertinggi (0.480). Ini menunjukkan bahwa data secara alami paling baik dibagi menjadi dua segmen utama.
  * **Interpretasi Segmen**: Dua cluster yang terbentuk kemungkinan besar merepresentasikan:
    1.  **Segmen Horeca (Hotel/Restoran/Kafe)**: Pelanggan dengan pengeluaran dominan pada kategori `Fresh` dan `Frozen`.
    2.  **Segmen Retail**: Pelanggan dengan pengeluaran dominan pada kategori `Grocery`, `Milk`, dan `Detergents_Paper`.

Analisis ini berhasil mengelompokkan pelanggan ke dalam segmen-segmen yang jelas dan dapat ditindaklanjuti, memberikan dasar yang kuat untuk pengambilan keputusan bisnis.

## **Cara Menjalankan Notebook**

1.  Pastikan Sudah memiliki Python dan Jupyter Notebook/JupyterLab terinstal.
2.  Instal pustaka yang diperlukan:
    ```bash
    pip install pandas numpy matplotlib seaborn plotly scikit-learn
    ```
3.  Jalankan sel-sel di dalam file `unsupervised_customer segmentation (2).ipynb` secara berurutan.
