# M3_Churn_Capstone
M3_E-commerce Customer Churn_Capstone

**Latar Belakang**  
  
Churn rate adalah tingkat atau persentase pelanggan memutus hubungan dengan sebuah bisnis atau perusahaan pada periode tertentu. Alasan utama mengapa customer churn rate penting adalah persentase pelanggan yang hilang tersebut sangat memengaruhi growth rate perusahaan
[Glints](https://glints.com/id/lowongan/churn-rate-adalah/).

Dalam konteks retensi pelanggan, customer churn adalah isu kritis yang harus diatasi oleh perusahaan. Hal ini dikarenakan peningkatan retensi pelanggan dapat memberikan dampak signifikan terhadap profitabilitas. Misalnya, sebuah riset menunjukkan bahwa peningkatan retensi pelanggan sebesar 5% dapat meningkatkan laba hingga 25% [Bain](https://media.bain.com/Images/BB_Prescription_cutting_costs.pdf).

Dengan memahami dan menerapkan strategi untuk mengurangi churn, perusahaan tidak hanya dapat meningkatkan retensi tetapi juga menciptakan hubungan yang lebih kuat dengan pelanggan, yang pada gilirannya mendukung keberlanjutan dan pertumbuhan bisnis.

Dataset yang akan dibahas hari ini merupakan milik sebuah perusahaan e-commerce online terkemuka. Perusahaan ini ingin mengetahui pelanggan seperti apa yang akan berhenti/churn, sehingga mereka dapat untuk menawarkan promo kepada pelanggan yang lebih tepat dan menjaga retensi pelanggan.

**Problem Statement and Goals**  
  
Sebelum menawarkan promo, perusahaan perlu merancang strategi agar promo tepat sasaran. Promo tentunya tidak diberikan kepada semua pelanggan, namun diprioritaskan untuk mereka yang diperkirakan akan churn. Langkah ini bertujuan untuk efisiensi dalam pengeluaran promo. Jika perusahaan keliru dalam memberikan promo atau memberikan promo secara sembarangan kepada pelanggan yang tidak diprediksi akan churn, hal ini dapat menyebabkan kerugian operasional akibat pengeluaran biaya untuk promo yang sebenarnya tidak perlu.

Goals dari perusahaan ialah memprediksi pelanggan seperti apa yang sangat mungkin akan churn, agar dapat memfokuskan penawaran promo kepada mereka. Perusahaan juga ingin mengidentifikasi faktor-faktor atau variabel yang mempengaruhi keputusan pelanggan untuk churn agar dapat merancang rencana yang lebih efektif untuk meningkatkan loyalitas pelanggan.

**Analytic Approach**  
  
Bangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi probabilitas pelanggan akan churn atau tidak, tentunya berdasarkan analisis data untuk menemukan pola yang membedakan pelanggan yang akan churn atau tidak.

Selain itu, dengan mengetahui faktor apa saja yang mempengaruhi pelanggan *churn* dapat menjadi pendukung pengambilan keputusan strategi pemasaran.

**Evaluation Metrics**  
  
Dalam melakukan prediksi, kesalahan yang dapat terjadi yaitu:

**Type 1 error** : False Positive  
Konsekuensi: kerugian perusahaan karena mengeluarkan biaya promo untuk pelanggan yang tidak tepat.

**Type 2 error** : False Negative  
Konsekuensi: kerugian perusahaan karena customer berhenti/*churn*.

**Target**:   
0 : Pelanggan tidak *churn*  
1 : Pelanggan *churn*

**Evaluation**:
Evaluation yang digunakan ialah Sensitivity, Accuracy, F2 Score.

[Confussion Matrix](https://dearpandemic.org/wp-content/uploads/2022/05/Sarah-1.png)

- **True Positive (TP)**: Customer diprediksi *churn* dan TERJADI *churn*
- **False Positive (FP)**: Customer diprediksi *churn*, namun ternyata TIDAK *churn*
- **False Negative (FN)**: Customer diprediksi tidak *churn*, namun ternyata TERJADI *churn*
- **True Negative (TN)**: Customer diprediksi tidak *churn* dan kenyataannya TIDAK *churn*
- **Sensitivity or Recall**: TP / (TP + FN)
- **Accuracy**: (TP + TN) / (TP + TN + FP + FN)
- **F2 Score**: (1 + 2^2) * (Specificity * Sensitivity) / (2^2 * Specificity + Sensitivity)

Menurut [Singh et al. (2024)](https://www.sciencedirect.com/science/article/pii/S2666764923000401), kombinasi antara sensitivity dan accuracy adalah matriks evaluasi yang paling cocok untuk konteks custome churn.

Mempertahankan Pelanggan akan sangat diperhatikan dalam kasus ini (*False Negative*) karena dapat berakibat buruk terhadap keberlangsungan perusahaan. Namun, jika kita tetap ingin melihat evaluasi dari (*False Positive*), sehingga digunakan juga F2 Score.

**Final Model**
Benchmarking Model dilakukan untuk mendapatkan hasil yang terbaik, diantaranya Logistic Regression, Decision Tree, Random Forest, KNN, AdaBoost, XGBoost, GradientBoost, LightGBM, dan SVC dengan metode Cross-Validation dan Prediction F2 Score. **LightGBM** dengan hyperparameter tuning menjadi model terbaik dengan parameter 
 - `learning_rate`    : 0.04
 - `max_depth`        : 20
 - `n_estimators`     : 250
 - `random_state`     : 0
 - `subsample`        : 0.8
 
Fitur-fitur yang berpengaruh signifikan terhadap Customer Churn yaitu `Tenure` dan `Complain`, serta honorable mention fitur `NumberOfAddress`.
 - `Tenure`    : semakin kecil nilainya berarti customer masih baru dalam memakai e-commerce, sehingga semakin besar peluang  Customer akan churn karena belum ada brand loyalty.
 - `Complain`  : jika flag = 1 maka peluang churn meningkat, dan
 - `NumberOfAddress`: semakin banyak maka peluang untuk Churn meningkat.
