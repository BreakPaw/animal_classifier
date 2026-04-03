# animal_classifier
Berdasarkan visualisasi kurva Loss dan Accuracy awal, model mengalami overfitting. Untuk mengoptimalkan kode dan mendapatkan hasil good fit (selisih antara metrik testing/validation dengan training menjadi rendah dan stabil), kita melakukan langkah-langkah penyelesaian berikut:

Mengatur Porsi Data (Data Split): Mengubah proporsi pembagian dataset menjadi 80% untuk Training, 10% untuk Validation, dan 10% untuk Testing. Memperbanyak data latih membantu model mengenali pola secara lebih umum.

Menerapkan Data Augmentation: Menambahkan RandomHorizontalFlip() dan RandomRotation(10) khusus pada transformasi data training. Hal ini mencegah model sekadar menghafal gambar dengan memberikan variasi sudut dan posisi.

Menyesuaikan Hyperparameter: Menaikkan jumlah Batch Size dari 16 menjadi 32 agar pembaruan bobot (weight update) berjalan lebih stabil. Selain itu, Epoch diturunkan dari 10 menjadi 8 untuk mencegah model memaksakan pembelajaran di akhir fase (early stopping manual).

Menambahkan Regularisasi pada Arsitektur Model: Menyisipkan BatchNorm2d setelah setiap layer konvolusi untuk mempercepat dan menstabilkan pembelajaran. Selain itu, menambahkan Dropout(0.5) sebelum layer Linear untuk secara acak menonaktifkan 50% neuron selama pelatihan agar model tidak bergantung pada satu fitur saja.

Menambahkan Weight Decay (L2 Regularization): Memberikan parameter weight_decay=1e-4 pada optimizer Adam. Hal ini berfungsi untuk memberikan penalti pada bobot model yang terlalu besar, sehingga menjaga model tetap sederhana dan tidak overfit.
