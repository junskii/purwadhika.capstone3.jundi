# purwadhika.capstone3.jundi

# Capstone 3: Bank Marketing Campaign Prediction

## 1. Business Understanding
### 1.1 Background
Sebuah bank di Indonesia ingin meningkatkan efisiensi telemarketing produk term deposit. Selama ini, seluruh nasabah dihubungi tanpa mempertimbangkan kemungkinan mereka akan membuka deposito, sehingga menyebabkan pemborosan biaya dan waktu.

### 1.2 Problem Statement
Bagaimana memprediksi apakah seorang nasabah akan membuka term deposit setelah dihubungi oleh marketing?

### 1.3 Objective
- Membangun model klasifikasi untuk memprediksi peluang nasabah membuka deposito.
- Meningkatkan efisiensi marketing dengan menargetkan nasabah yang lebih akurat.
- Memberikan rekomendasi kepada tim marketing mengenai nasabah yang lebih potensial.

### 1.4 Business Impact
- Mengurangi cost marketing
- Meningkatkan konversi campaign
- Mempermudah tim marketing memilih target yang potensial

---

## 2. Data Understanding
### 2.1 Data Overview
- **Jumlah data:** 7813 entri
- **Fitur:** 11 kolom (4 numerik: age, balance, campaign, pdays; 7 kategorikal: job, housing, loan, contact, month, poutcome, deposit)
- **Target:** `deposit` (yes/no)
- **Tidak ada missing value**

### 2.2 Distribusi Target
- Kelas target hampir seimbang: 4081 (no), 3732 (yes)

### 2.3 Cohort Analysis
- Analisis distribusi nasabah membuka deposito per bulan. Bulan Mei memiliki lonjakan konversi tertinggi.

### 2.4 Univariate & Bivariate Analysis
- Banyak fitur numerik memiliki outliers (age, balance, campaign, pdays)
- Fitur penting: balance, age, histori kontak, hasil campaign sebelumnya, bulan promosi
- Pekerjaan management & retired lebih banyak membuka deposito

### 2.5 Correlation Analysis
- Korelasi antar fitur numerik divisualisasikan dengan heatmap

---

## 3. Data Preparation
### 3.1 Handling Outliers
- Menggunakan Winsorizing pada balance & pdays untuk mengurangi pengaruh nilai ekstrem

### 3.2 Feature Scaling
- Menggunakan RobustScaler untuk menormalkan fitur numerik

### 3.3 Encoding Categorical Features
- One-hot encoding pada fitur kategorikal
- Target diubah menjadi 1 (yes) dan 0 (no)

### 3.4 Data Splitting
- Data dibagi menjadi training (80%) dan testing (20%)

---

## 4. Modeling & Evaluation
### 4.1 Model Benchmarking
- Model yang diuji: Logistic Regression, Decision Tree, Random Forest, Voting Classifier
- Evaluasi dengan Stratified K-Fold Cross Validation (K=5)
- Metrik: ROC AUC, Accuracy, Recall

### 4.2 Handling Imbalance
- Oversampling dengan SMOTE untuk meningkatkan recall pada kelas minoritas

### 4.3 Hyperparameter Tuning
- RandomizedSearchCV untuk Random Forest & Logistic Regression
- Parameter terbaik:
  - Random Forest: n_estimators=200, min_samples_split=2, min_samples_leaf=4, max_depth=20, bootstrap=True
  - Logistic Regression: solver=liblinear, penalty=l2, C=0.1

### 4.4 Feature Importance & Selection
- Fitur terpenting: balance, age, contact_unknown, poutcome_success, pdays, campaign, housing_yes, month_may, loan_yes, month_jun, month_mar
- Model akhir dibangun dengan fitur-fitur terpilih

### 4.5 Final Model Evaluation
- **Random Forest**: Precision 73%, Recall 62%, Accuracy 71%, ROC AUC 0.765
- **Logistic Regression**: Precision 71%, Recall 65%, Accuracy 70%, ROC AUC 0.766

---

## 5. Insight & Business Recommendation
- **Faktor utama:** Saldo, usia, histori kontak, hasil campaign sebelumnya, dan waktu promosi
- **Segmentasi:** Management & retired lebih potensial untuk deposito
- **Rekomendasi:**
  - Gunakan Random Forest untuk memprioritaskan leads
  - Fokuskan campaign pada nasabah dengan probabilitas tinggi membuka deposito
  - Lakukan pendekatan berbeda untuk segmen dengan minat rendah
  - Evaluasi campaign bulanan untuk mengidentifikasi waktu terbaik promosi

---

## 6. Model Deployment
- Model Random Forest hasil tuning dan feature selection disimpan dalam file `final_random_forest_model.pkl` untuk prediksi di masa depan.

---

## 7. File
- `Capstone3.ipynb`: Notebook pipeline analisis & modeling
- `data_bank_marketing_campaign.csv`: Dataset
- `final_random_forest_model.pkl`: Model Random Forest siap deploy

---

## 8. How to Use
1. Jalankan notebook `Capstone3.ipynb` untuk melihat seluruh proses analisis dan modeling.
2. Untuk prediksi baru, load model dari `final_random_forest_model.pkl` dan lakukan preprocessing data sesuai pipeline di notebook.

---

## 9. Author
Nama: Muhammad Jundullah

---

## 10. References
- UCI Machine Learning Repository: Bank Marketing Dataset
- Scikit-learn, Pandas, Seaborn, Matplotlib 
