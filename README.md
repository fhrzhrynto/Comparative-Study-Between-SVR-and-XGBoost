# Prediksi Engagement Video TikTok: SVR vs XGBoost

Proyek ini membandingkan kinerja algoritma **Support Vector Regression (SVR)** dan **XGBoost Regressor** dalam memprediksi *Adjusted Engagement Index* (AEI) pada konten video TikTok berdasarkan variabel interaksi pengguna dan kepadatan informasi konten.

## 📌 Ringkasan Metodologi

- **Dataset:** Data sekunder TikTok dari Kaggle dengan total 19.382 baris data.
- **Prapemrosesan Data:** Penanganan nilai yang hilang melalui imputasi teks (`"No Transcription"`), imputasi numerik menggunakan median, serta imputasi kategori status klaim menggunakan `"unknown"`.
- **Pembagian Data:** 80% data latih (15.505 baris) dan 20% data uji (3.877 baris).
- **Standarisasi Fitur:** Menggunakan `StandardScaler` dengan metode standardisasi Z-score.

## 📐 Feature Engineering

Penelitian ini menggunakan dua variabel prediktor (*independent variables*) dan satu variabel target (*dependent variable*).

- **Active Engagement Ratio (\(X_1\)):** Merepresentasikan rasio interaksi aktif, yang mencakup komentar, berbagi, dan unduhan video, terhadap jumlah penayangan.
- **Content Density (\(X_2\)):** Merepresentasikan kepadatan informasi konten berdasarkan jumlah kata dalam transkrip dan durasi video.
- **Adjusted Engagement Index (AEI atau \(Y\)):** Variabel target yang merepresentasikan tingkat engagement video berdasarkan jumlah penayangan serta pembobotan interaksi berupa likes, komentar, dan unduhan.
## ⚙️ Konfigurasi Model

### Support Vector Regression (SVR)

Model SVR menggunakan kernel Radial Basis Function (RBF) dengan konfigurasi hyperparameter berikut:

| Hyperparameter | Nilai |
|---|---:|
| `kernel` | `rbf` |
| `C` | 50 |
| `gamma` | 0.1 |
| `epsilon` | 0.05 |

### XGBoost Regressor

Model XGBoost menggunakan konfigurasi berikut:

| Hyperparameter | Nilai |
|---|---:|
| `n_estimators` | 100 |
| `max_depth` | 3 |
| `learning_rate` | 0.05 |
| `subsample` | 0.8 |

## 📊 Hasil Evaluasi Model

Evaluasi dilakukan menggunakan 3.877 data uji. Kinerja kedua model dibandingkan berdasarkan tiga metrik: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), dan koefisien determinasi (\(R^2\)).

| Algoritma | MAE | RMSE | \(R^2\) |
|---|---:|---:|---:|
| **Support Vector Regression (SVR)** | **0.0762** | 0.0988 | 0.5051 (50.51%) |
| **XGBoost Regressor** | 0.0767 | **0.0969** | **0.5245 (52.45%)** |

**Interpretasi hasil:**

- **MAE:** SVR menghasilkan nilai MAE lebih rendah, yaitu 0.0762, sehingga memiliki rata-rata kesalahan absolut yang sedikit lebih kecil.
- **RMSE:** XGBoost menghasilkan RMSE lebih rendah, yaitu 0.0969, yang menunjukkan kesalahan kuadrat rata-rata yang lebih kecil setelah memperhitungkan akar kuadratnya.
- **R²:** XGBoost memperoleh nilai R² sebesar 0.5245, lebih tinggi dibandingkan SVR sebesar 0.5051.

## 💡 Kesimpulan

1. **XGBoost Regressor menunjukkan kinerja keseluruhan yang lebih baik** berdasarkan nilai R² yang lebih tinggi dan RMSE yang lebih rendah.
2. **SVR unggul dalam metrik MAE**, dengan nilai 0.0762 dibandingkan 0.0767 pada XGBoost.
3. Kedua model menunjukkan kemampuan prediksi yang cukup konsisten pada video dengan tingkat engagement rendah. Namun, kesalahan prediksi cenderung lebih bervariasi pada video dengan engagement tinggi, baik dalam bentuk *overestimation* maupun *underestimation*.

Berdasarkan hasil tersebut, XGBoost Regressor dipilih sebagai model dengan kinerja keseluruhan terbaik berdasarkan dua dari tiga metrik evaluasi yang digunakan.

## 🛠️ Teknologi dan Library

- **Bahasa Pemrograman:** Python 3
- **Pengolahan Data:** `pandas`, `numpy`
- **Machine Learning:** `scikit-learn`
- **Gradient Boosting:** `xgboost`
- **Lingkungan Pengembangan:** Google Colab

## 📂 Dataset

Dataset yang digunakan berasal dari Kaggle dan memiliki lisensi **CC0: Public Domain**.
https://www.kaggle.com/datasets/yakhyojon/tiktok

## 🚀 Menjalankan Notebook

1. Buka file notebook `.ipynb` yang tersedia di repository ini.
2. Pilih **Open in Colab** atau unggah notebook ke [Google Colab](https://colab.research.google.com/).
3. Pastikan dataset tersedia dan jalur pemuatannya sudah sesuai.
4. Instal library yang diperlukan jika belum tersedia.
5. Jalankan cell secara berurutan untuk mereproduksi proses prapemrosesan, pelatihan model, dan evaluasi.

---

*Proyek ini merupakan bagian dari penelitian akademik mengenai prediksi engagement video TikTok menggunakan pendekatan machine learning.*


# TikTok Video Engagement Prediction: SVR vs. XGBoost

This project compares the performance of **Support Vector Regression (SVR)** and **XGBoost Regressor** in predicting the *Adjusted Engagement Index* (AEI) of TikTok video content based on user interaction variables and content density.

## 📌 Methodology Overview

- **Dataset:** Secondary TikTok data obtained from Kaggle, consisting of 19,382 rows.
- **Data Preprocessing:** Handling missing values through text imputation (`"No Transcription"`), median imputation for numerical variables, and categorical imputation for claim status using `"unknown"`.
- **Train-Test Split:** 80% for training (15,505 rows) and 20% for testing (3,877 rows).
- **Feature Scaling:** Using `StandardScaler` with Z-score standardization.

## 📐 Feature Engineering

This study uses two predictor variables (*independent variables*) and one target variable (*dependent variable*).

- **Active Engagement Ratio (\(X_1\)):** Represents the ratio of active interactions, including comments, shares, and downloads, to the number of video views.
- **Content Density (\(X_2\)):** Represents content information density based on the number of words in the video transcript relative to its duration.
- **Adjusted Engagement Index (AEI or \(Y\)):** The target variable representing video engagement based on view counts and weighted interactions, including likes, comments, and downloads.

## ⚙️ Model Configuration

### Support Vector Regression (SVR)

The SVR model uses the Radial Basis Function (RBF) kernel with the following hyperparameter configuration:

| Hyperparameter | Value |
|---|---:|
| `kernel` | `rbf` |
| `C` | 50 |
| `gamma` | 0.1 |
| `epsilon` | 0.05 |

### XGBoost Regressor

The XGBoost model uses the following configuration:

| Hyperparameter | Value |
|---|---:|
| `n_estimators` | 100 |
| `max_depth` | 3 |
| `learning_rate` | 0.05 |
| `subsample` | 0.8 |

## 📊 Model Evaluation Results

Evaluation was performed using 3,877 test samples. The performance of both models was compared using three metrics: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and the coefficient of determination (\(R^2\)).

| Algorithm | MAE | RMSE | \(R^2\) |
|---|---:|---:|---:|
| **Support Vector Regression (SVR)** | **0.0762** | 0.0988 | 0.5051 (50.51%) |
| **XGBoost Regressor** | 0.0767 | **0.0969** | **0.5245 (52.45%)** |

**Results Interpretation:**

- **MAE:** SVR achieves a lower MAE of 0.0762, indicating a slightly smaller average absolute prediction error.
- **RMSE:** XGBoost achieves a lower RMSE of 0.0969, indicating better performance in terms of errors that penalize larger deviations more heavily.
- **R²:** XGBoost achieves an R² of 0.5245, outperforming SVR, which obtains 0.5051.

## 💡 Conclusion

1. **XGBoost Regressor demonstrates better overall performance**, achieving a higher R² and a lower RMSE.
2. **SVR performs better in terms of MAE**, with a value of 0.0762 compared to 0.0767 for XGBoost.
3. Both models demonstrate relatively consistent predictive performance for videos with low engagement levels. However, prediction errors tend to vary more for videos with high engagement, resulting in both *overestimation* and *underestimation*.

Based on these results, XGBoost Regressor is selected as the best overall-performing model according to two of the three evaluation metrics used.

## 🛠️ Technologies and Libraries

- **Programming Language:** Python 3
- **Data Processing:** `pandas`, `numpy`
- **Machine Learning:** `scikit-learn`
- **Gradient Boosting:** `xgboost`
- **Development Environment:** Google Colab

## 📂 Dataset

The dataset was obtained from Kaggle and is licensed under **CC0: Public Domain**.
https://www.kaggle.com/datasets/yakhyojon/tiktok

## 🚀 How to Run the Notebook

1. Open the `.ipynb` notebook available in this repository.
2. Select **Open in Colab** or upload the notebook to [Google Colab](https://colab.research.google.com/).
3. Ensure the dataset is available and the file path is configured correctly.
4. Install the required libraries if they are not already available.
5. Run the cells sequentially to reproduce the data preprocessing, model training, and evaluation processes.

---

*This project is part of an academic research study on TikTok video engagement prediction using machine learning approaches.*
