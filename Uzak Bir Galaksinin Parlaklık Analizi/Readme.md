# YZM212 Makine Öğrenmesi - 4. Laboratuvar Ödevi
## Uzak Bir Galaksinin Parlaklık Analizi (Bayesyen Çıkarım)

### 1. Problem Tanımı
Bu proje, astronomi gözlemlerinde karşılaşılan gürültülü veriler üzerinden bir gök cisminin gerçek parlaklığını ve ölçüm belirsizliğini tahmin etmeyi amaçlar. 
Gözlem verileri; teleskop gürültüsü ve atmosferik etkiler gibi nedenlerle her zaman "kirli" gelmektedir.

### 2. Veri Seti
Simülasyonda kullanılan veri seti, doğa tarafından bilinen ancak bizim tahmin etmeye çalıştığımız parametreler ışığında üretilmiştir:
 **Gerçek Parlaklık ($\mu$):** 150.0 
**Gözlem Hatası ($\sigma$):** 10.0 
**Gözlem Sayısı (n):** 50 

### 3. Yöntem
[cite_start]Analiz, **Bayesyen Çıkarım (Bayesian Inference)** yöntemi ve **Markov Chain Monte Carlo (MCMC)** örnekleme algoritması kullanılarak gerçekleştirilmiştir. 
**Likelihood:** Normal dağılım modeli kullanılmıştır.
**Prior:** 0-300 parlaklık ve 0-50 hata payı aralığında "informatif olmayan" geniş bir prior tanımlanmıştır.
**Örnekleyici:** `emcee` kütüphanesi ile 32 paralel gezgin kullanılarak 2000 adım simülasyon yapılmıştır.

### 4. Sonuçlar ve Tartışma
Elde edilen sonuçlar, modelin gürültülü veriden gerçek fiziksel değerleri yüksek doğrulukla geri alabildiğini göstermiştir.Corner_Plot analizi, parametreler arasındaki belirsizliği ve korelasyonu görselleştirmektedir.