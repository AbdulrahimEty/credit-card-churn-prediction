Credit Card Customer Churn Prediction
Bir banka müşterilerinin ne zaman ayrılacağını tahmin etmek için model kurdum. Verideki davranışsal sinyallerle churn (müşteri kaybı) tahmini yapıyorum.
Dataset
Kaggle'dan aldım: BankChurners veriseti.
10.127 müşteri, 23 sütun. Hedef değişken: Attrition_Flag (mevcut vs ayrılmış müşteri).
Ne Yaptım
Veri dengesizdi — %85 mevcut, %15 ayrılmış müşteri. Bu projede recall kritikti çünkü ayrılacak müşteriyi kaçırmak bankanın gelir kaybı demek.
Gender'ı map ile, Education_Level ve Card_Category'yi ordinal mantıkla encode ettim. Income_Category için manuel sayısal değer atadım — "$40K - $60K" yerine 50000 gibi. Unknown değerlere median atadım. Marital_Status için one-hot kullandım.
class_weight='balanced' ile dengesizliği yönettim. LightGBM, XGBoost, Random Forest ve Gradient Boosting denedim.
Sonuçlar
ModelAccuracyChurn RecallLightGBM0.970.91XGBoost0.970.90Random Forest0.950.76
LightGBM kazandı. 407 churn müşterinin 369'unu yakaladı, sadece 38'ini kaçırdı.
Önemli Bulgular
EDA aşamasında işlem miktarı düşük müşterilerin ayrılma eğiliminde olduğunu gözlemledim. Feature importance bunu doğruladı — Total_Trans_Amt modelin en güçlü sinyali çıktı.
Banka için pratik çıkarım: İşlem miktarı düşen müşteriler kampanya/tutundurma hedefi olmalı.
Kullanılanlar
Python, Pandas, Scikit-learn, LightGBM, XGBoost, Matplotlib, Seaborn
