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
- Model yang diuji: Logistic Regression, Random Forest, Decision Tree, Voting Classifier
- Benchmarking awal: Voting Classifier unggul di ROC AUC/akurasi, Random Forest unggul di recall
- Setelah oversampling (SMOTE): Random Forest kombinasi terbaik akurasi dan recall, Voting Classifier recall tinggi tapi akurasi turun
- Hyperparameter tuning hanya untuk Logistic Regression & Random Forest (model lain performa rendah/overfitting)
- **Model final: Logistic Regression**
  - Recall: 0.65 (tertinggi, penting untuk bisnis)
  - Akurasi: 0.70
  - ROC AUC: 0.766
  - Model lebih sederhana dan mudah diinterpretasikan

---

## 5. Feature Importance
- Fitur terpenting: saldo, usia, histori kontak, hasil campaign sebelumnya, campaign, housing, bulan promosi (Mei, Juni, Maret)
- Segmentasi pekerjaan dan waktu campaign sangat berpengaruh

---

## 6. Business Recommendation
1. **Fokuskan campaign pada nasabah dengan saldo tinggi dan usia 30–50 tahun**
2. **Prioritaskan segmen pekerjaan management & retired**
3. **Lakukan campaign intensif di bulan Mei**
4. **Manfaatkan histori kontak dan hasil campaign sebelumnya untuk penargetan**
5. **Kurangi kontak ke nasabah dengan peluang rendah**
6. **Lakukan A/B testing strategi baru vs lama**
7. **Monitoring & evaluasi model secara berkala**

---

## 7. Model Deployment
- Model Logistic Regression final disimpan sebagai `final_logistic_regression_model.pkl` dan siap digunakan untuk prediksi batch atau real-time.

---

## 8. File
- `Capstone3.ipynb`: Notebook pipeline analisis & modeling
- `data_bank_marketing_campaign.csv`: Dataset
- `final_random_forest_model.pkl`: Model Random Forest siap deploy

---

## 9. How to Use
1. Jalankan notebook `Capstone3.ipynb` untuk melihat seluruh proses analisis dan modeling.
2. Untuk prediksi baru, load model dari `final_random_forest_model.pkl` dan lakukan preprocessing data sesuai pipeline di notebook.

---

## 10. Author
Nama: Muhammad Jundullah

---

## 11. References
- UCI Machine Learning Repository: Bank Marketing Dataset
- Scikit-learn, Pandas, Seaborn, Matplotlib 
