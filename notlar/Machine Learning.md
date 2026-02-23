# Makine Öğrenmesi

Amaç, bilgisayarın geçmiş veriler üzerinden öğrendiği örüntü ile yeni örneklere bakarak tahmin yapabilmesi ve karar verebilmesidir.

1. Supervised (Gözetimli)
2. Unsupervised (Gözetimsiz)
3. Reinforcement (Pekiştirmeli)

# 1️ Supervised Learning

Etiketli veriler kullanılarak modelin giriş (X) ile hedef değişken (Y) arasındaki ilişkiyi öğrenmesi.

### Classification

- Logistic Regression
- Decision Tree
- Random Forest
- SVM
- KNN
- Naive Bayes
- Gradient Boosting

### Regression

- Linear Regression
- Ridge / Lasso
- Decision Tree Regressor
- Random Forest Regressor
- Gradient Boosting Regressor

# 2️ Unsupervised Learning

Veriler etiketsizdir. Algoritma verideki yapıları ve örüntüleri keşfeder.

### Clustering

- K-Means
- Hierarchical Clustering
- DBSCAN

### Dimensionality Reduction

- PCA
- t-SNE
- UMAP

### Association Rule Learning

- Apriori
- FP-Growth

# 3️ Reinforcement Learning

Bir agent’ın environment içinde ödül-ceza sistemiyle öğrenmesi.

# Simple Linear Regression

Tek bir girdi (X) ve çıktı (Y) arasındaki doğrusal ilişkiyi modelleyen algoritmadır.

Y = A + BX

Error = y - ŷ

## Cost Function

Cost function, modelin tahmin hatasını ölçen ve minimize edilmesi gereken matematiksel fonksiyondur.
MSE = (1/n) Σ(y - ŷ)²

## Gradient Descent

Gradient Descent hata fonksiyonunun (cost function) minimumunu bulmak için kullanılan optimizasyon algoritmasıdır.
Amaç MSE(Mean Square Error)nin minimize edilmesidir.
Burada A (intercept) ve B (slope) değerlerini en iyi şekilde bulmamız gerekir.
Parametreler güncellenir:

A = A - α ∂MSE/∂A  
B = B - α ∂MSE/∂B

A: Sabit d.
B: Slope
∂MSE/∂A: Cost functionun A parametresine göre türevi

α bizim öğrenme oranımız (minimum globali bulurken attığımız adımın büyüklüğü de denebilir)
eğer α çok büyük olursa model optimal noktayı kaçırabilir fakat α nın çok küçük olduğu durumda öğrenme çok yavaş gerçekleşebilir. Bu yüzden mikro adımlar da atmadan açıyı yavaş yavaş artırarak minimum globali bulmaya çalışırız.

Cost function (MSE), linear regression probleminde parametrelere göre bakıldığında bir paraboldür.
Parabolün en alt noktası global minimumdur.
Bir fonksiyonun minimum veya maksimum olduğu noktada türev sıfırdır.
MSE’nin A (intercept) ve B (slope) parametrelerine göre türevini alma sebebimizbu parametreleri değiştirerek hatanın en küçük olduğu noktayı matematiksel olarak bulabilmektir.

Gradient Descent algoritmasında parametreler eşzamanlı olarak güncellenir. 
Her iterasyonda A ve B birlikte güncellenir ve hata kademeli azaltılır. 
Bu süreç türevlerin sıfıra yaklaşmasına kadar devam eder.

<p align="center">
  <img src="../images/gd-image.png" width="500">
</p>

# Multiple Linear Regression (Çoklu Doğrusal Regresyon)

Multiple Linear Regression, birden fazla bağımsız değişken (X₁, X₂, ..., Xₙ) ile bir bağımlı değişken (Y) arasındaki doğrusal ilişkiyi modelleyen regresyon yöntemidir.

Basit linear regression’da tek bir X varken, burada birden fazla X değişkeni kullanılır.

## Matematiksel Model

Ŷ = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ

Ŷ: Tahmin edilen değer  
β₀: Sabit terim (intercept)  
βᵢ: Katsayılar  
Xᵢ: Bağımsız değişkenler  

βᵢ katsayısı, Xᵢ bir birim arttığında (diğer değişkenler sabitken) Y'nin ne kadar değiştiğini gösterir.

Genellikle Mean Squared Error (MSE) kullanılır:

MSE = (1/n) Σ(y - ŷ)²

Amaç:

min J(β₀, β₁, ..., βₙ)

Cost function tüm parametrelere bağlıdır.

## Gradient Descent ile Güncelleme

Her parametre için kısmi türev alınır:

βⱼ = βⱼ - α ∂MSE/∂βⱼ

Tüm parametreler her iterasyonda eşzamanlı olarak güncellenir.

1 değişken → Doğru
2 değişken → Düzlem
n değişken → Hiper düzlem

<p align="center">
  <img src="../images/cYAx7.png" width="500">
</p>

yüzeyin çukur noktası global minimumdur.

Simple lineer reg ile model ve öğrenme mantığı aynıdır. Sadece katsayı artar, hesap karmaşıklığı artar.






## Model Performans Ölçümü (Regression)

### R-Square
R kare modelin veriye ne kadar iyi uyduğunu ölçer.

R² = 1 - (SS_res / SS_tot)

Burada:
SS_res (Residual Sum of Squares):
Σ (y - ŷ)² yani gerçek değer ile tahmin arasındaki farkların karelerinin toplamı(hata)

SS_tot (Total Sum of Squares):
Σ (y - ȳ)² yani gerçek değerlerin ortalamadan farklarının kare toplamı(total varyans)

y: Gerçek değer  
ŷ: Tahmin edilen değer  
ȳ: Gerçek değerlerin ortalaması  

R² = 1 Model veriyi mükemmel açıklar  
R² = 0 Model ortalamadan daha iyi değildir  
R² < 0 Model ortalamadan daha kötüdür

### Adjusted R-Square

Modele feature eklendiğinde R² artma eğilimindedir fakat bu yanıltıcı olabilir. Eklenen değişken çıktı ile alakasızsa R² gereksiz şişebilir fakat adjusted R², R² nin aksine modelle alakasız olan değişkenleri cezalandırır böylece R² değerinin gereksiz şişmesini önler.
Her zaman hem R² hem de adjusted R² değerlendirilmelidir.

R²_adj = 1 - [ (1 - R²)(n - 1) / (n - p - 1) ]

Burada:
R²: Determinasyon katsayısı  
n: Gözlem (örnek) sayısı  
p: Bağımsız değişken sayısı  

p arttıkça payda küçülür ve bu durum modele karmaşıklık cezası (Eğer yeni feature gerçekten katkı sağlamıyorsa seni cezalandırırım mantığı) uygulanmasına neden olur.




