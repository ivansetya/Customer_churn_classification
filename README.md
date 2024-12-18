# Customer_churn_classification

## Domain proyek
Loyalitas pelanggan merupakan salah satu aspek penting yang menentukan keberhasilan sebuah perusahaan, terutama dalam industri perbankan yang sangat kompetitif. Pemahaman terhadap faktor-faktor yang memengaruhi keputusan pelanggan untuk tetap menggunakan layanan atau meninggalkan bank menjadi hal yang krusial.

Dataset ini menyajikan informasi rinci tentang pelanggan sebuah bank, termasuk data demografi, perilaku keuangan, dan hubungan mereka dengan bank. Variabel target dalam dataset ini berupa variabel biner yang mencerminkan status pelanggan, yaitu apakah mereka masih aktif menggunakan layanan bank atau telah memutuskan untuk menutup akun mereka.

Dengan menganalisis data ini, diharapkan dapat diperoleh wawasan mendalam mengenai pola dan faktor yang berkontribusi terhadap keputusan pelanggan untuk meninggalkan bank. Informasi ini dapat membantu bank mengembangkan strategi yang lebih efektif untuk meningkatkan retensi pelanggan dan mengurangi tingkat pengabaian (customer churn), sehingga mendukung pertumbuhan bisnis secara berkelanjutan.

Target :

0 : Customer tidak churn

1 : Customer churn
## Business Understanding
### Problem Statements
- Perusahaan ingin mengurangi loss akibat hilangnya pelanggan parameter apa yang penting dengan melakukan prediksi terhadap kemungkinan pelanggan churn.
- Fitur utama manakah yang penting dalam memprediksi pelanggan melakukan churn? CreditScore, Age, Gender, Balance data-data demografi mana yang dapat mempengaruhi seseorang churn.
### Goals
- Memprediksi kemungkinan seorang pelanggan akan churn/tidak
- Mencari tahu variabel apa saja yang mempengaruhi pelanggan churn
## Data Understanding
- Surname: Surname
- CreditScore: Credit score
- Geography: Country (Germany/ France/ Spain)
- Gender: Gender (Female/ Male)
- Age: Age
- Tenure: How many years of customer
- Balance: Balance
- NumOfProducts: The number of bank product used
- HasCrCard: Credit card status (0 = No, 1 = Yes)
- IsActiveMember: Active membership status (0 = No, 1 = Yes)
- EstimatedSalary: Estimated salary
- Exited: Churn or not? (0 = No, 1 = Yes)
1. **Jumlah nasabah untuk tiap categorical variables, dibagi berdasarkan asal negaranya**

![image](https://github.com/user-attachments/assets/3e213665-f3b0-4a0b-8065-8f90236324a9)

2. **Perbandingan churn customers pada tiap negara**

![image](https://github.com/user-attachments/assets/caa2092d-1bd0-4d94-89f6-fd92c16ad570)

3. **Perbandingan churn customers pada tiap gender**
 
![image](https://github.com/user-attachments/assets/c81a5a6a-6ac6-4dd9-990b-7d56f51841ea)

4. **Perbandingan churn customers untuk tiap lama tahun Tenure/masa cicilan**
   
![image](https://github.com/user-attachments/assets/072f8c63-dc4b-493d-9843-5d25ad4f877e)

## Data Preparation
1. EDA = untuk data overview mengetahui visualisasi data terhadap target latih
2. Data Cleaning = outlier, missing data, duplicate dan drop fitur yang tidak diperlukan
3. Data Splitting = membagi data kedalam train dan test 80:20
4. Data Normalization = melakukan encoding pada tipe fitur objek menjadi numerikal sebagai penguat fitur latih
5. Imbalancing = melakukan resampling karena data target cenderung tidak berimbang

![image](https://github.com/user-attachments/assets/dc4d801a-ae41-48f3-b89b-923931841935)

6. Data Training = penggunaan model-model klasifikasi (tree based)
7. Cross Validation = melakukan rata-rata pada pelatihan model berulang untuk memastikan bahwa hasil yang diberikan konsisten dan valid
8. Hyperparamater Tuning = melakukan tuning untuk meningkatkan skor metric (f2-score)
9. Evaluation = intepretasi evaluasi metrik dengan confusion metrik dari model terbaik dan benchmarking model sebelum dan sesudah tuning
## Modeling
- Cross Validation menggunakan skfold dengan splits 5 kali
  
![image](https://github.com/user-attachments/assets/29b5546c-c205-4f7a-bf08-a46ccb6251fc)

Model GradientBoost dan XGBoost dipilih menjadi 2 model paling optimal karena memiliki nilai recall rata-rata paling tinggi dan standar deviasi terendah.
- **Gradient Boost(f2-score)**
Train Set:
Before tuning: 0.65
After tuning: 0.67
Test Set:
Before tuning: 0.53
After tuning: 0.66
- **XGBoost(f2-score)**
Train Set:
Before tuning: 0.58
After tuning: 0.68
Test Set:
Before tuning: 0.52
After tuning: 0.67

## Evaluation
- **Gradient Boost**
  
  ![image](https://github.com/user-attachments/assets/0dff7108-2e80-40a8-9e8c-125144338df0)
  
  ![image](https://github.com/user-attachments/assets/e30dd28c-5b6c-4c09-82d6-2bb825140615)
  
- **XG Boost**
  
  ![image](https://github.com/user-attachments/assets/e8f0441c-a183-4339-a1e7-87cbff0bd275)
  
  ![image](https://github.com/user-attachments/assets/66e6097a-0688-447a-b6da-d22aa11adc4a)

Kesimpulan pada hasil training untuk menjawab masalah yang pertama adalah
Hyperparameter tuning berhasil meningkatkan F2 Score pda test set dari model dengan XGBoost sebesar 0.15. Performa model sebesar 0.67 bisa dikatakan belum bagus karena jumlah False Negative masih sekitar 1/4 dari total kelas 1 (churn).

Metric F2 Score digunakan karena cost function dari False Negative dianggap lebih besar dari False Positif, sehingga jumlah False Negative yang dihasilkan oleh model harus diminimalkan. Namun, karena jumlah kelas 1 hanya sekitar 20% dari jumlah data, menggunakan teknik resampling saja belum cukup untuk bisa menghasilkan model dengan performa optimal, harus dicoba dengan melakukan pendekatan lain, misalnya dikombinasikan dengan feature engineering.

Kemudian dilakukan feature importance untuk menjawab permasalahan kedua dengan hasil sebagai berikut
![image](https://github.com/user-attachments/assets/d44015e0-a4bb-480c-a4a9-1d2e095c202b)



