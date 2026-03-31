# YZM212 Makine Öğrenmesi - III. Laboratuvar Raporu

**Ders:** Makine Öğrenmesi (YZM212)  
**Konu:** Lineer Cebir Temelleri: Matris Manipülasyonu, Özdeğer ve Özvektör Analizi  
[cite_start]**Rapor Tarihi:** 29.03.2026 

---

## 1. GİRİŞ: MAKİNE ÖĞRENMESİNDE LİNEER CEBİRİN STRATEJİK ÖNEMİ

### 1.1. Veri Temsili ve Matris Yapıları
Makine öğrenmesi algoritmaları için veri, ham bir bilgi yığını değil, matematiksel bir operatördür. Bir veri seti $X \in \mathbb{R}^{m \times n}$ olarak tanımlandığında; [cite_start]$m$ örneklemi (observations), $n$ ise bu örneklemlerin özniteliklerini (features) temsil eder. Görüntü işlemede pikseller, doğal dil işlemede kelime vektörleri (embeddings) tamamen matris formundadır.

### 1.2. Matris Manipülasyonu: Verinin Yeniden Şekillendirilmesi
[cite_start]Matris manipülasyonu; toplama, skaler çarpım ve özellikle matris çarpımı gibi işlemleri içerir[cite: 6]. ML perspektifinden manipülasyonun amacı:
* **Boyut Dönüşümü:** Yüksek boyutlu veriyi daha düşük boyutlu bir alt uzaya projekte etmek.
* [cite_start]**Özellik Çıkarımı:** Matris ayrıştırma (Decomposition) yöntemleriyle verinin içindeki korelasyonları ve gizli yapıları (latent features) çözmek.

---

## 2. ÖZDEĞER VE ÖZVEKTÖR ANALİZİ: TEORİK ÇERÇEVE

### 2.1. Matematiksel Tanım
[cite_start]Bir kare matris $A$ için, bir lineer dönüşüm uygulandığında yönü değişmeyen ancak boyu $\lambda$ kadar ölçeklenen vektörlere **özvektör** ($v$), ölçek katsayısına ise **özdeğer** ($\lambda$) denir[cite: 6, 12]:

$$A \cdot v = \lambda \cdot v$$

### 2.2. Karakteristik Denklem ve Abel-Ruffini Kısıtı
[cite_start]Özdeğerlerin hesabı geleneksel olarak karakteristik polinomun çözülmesine dayanır: $det(A - \lambda I) = 0$. 
* **Önemli Not:** Abel-Ruffini Teoremi uyarınca, 5. derece ve üstü ($n > 4$) polinomlar için genel bir cebirsel çözüm yolu yoktur. Bu durum, bilgisayarların özdeğerleri "doğrudan" değil, "iteratif" algoritmalarla hesaplamasını zorunlu kılar.

### 2.3. Makine Öğrenmesindeki Kritik Uygulamalar
1.  **Temel Bileşen Analizi (PCA):** Verinin kovaryans matrisinin özvektörleri hesaplanır. [cite_start]En büyük özdeğere sahip özvektör, verideki varyansın (bilginin) en yoğun olduğu "Principal Component" (Ana Bileşen) yönüdür.
2.  [cite_start]**Boyut İndirgeme:** Düşük özdeğere sahip yönler "gürültü" olarak kabul edilip atılır, böylece model karmaşıklığı azaltılır.
3.  **Google PageRank:** İnternet grafiğinin komşuluk matrisi üzerinden en büyük özdeğere karşılık gelen özvektör bulunur. Bu vektördeki her bileşen bir web sayfasının "önem skorunu" belirler.
4.  **Spektral Kümeleme:** Veri noktaları arasındaki benzerlik matrisinin özdeğerleri kullanılarak verinin doğal gruplara (clusters) ayrılması sağlanır.

---

## 3. NUMPY LINALG.EIG FONKSİYONUNUN DERİNLİĞİNE İNCELEMESİ

[cite_start]NumPy’ın `eig` fonksiyonu, Python seviyesinde bir arayüz sunsa da asıl ağır iş yükünü Fortran ve C tabanlı **LAPACK** kütüphanesine devreder.

### 3.1. Algoritmik İşleyiş Adımları

1.  [cite_start]**Girdi Validasyonu:** Matrisin karesel yapıda olup olmadığı ve veri tipi (float, complex) kontrol edilir.
2.  [cite_start]**Hessenberg Dönüşümü:** Matris, hesaplama karmaşıklığını $O(n^4)$'ten $O(n^3)$'e indirmek için Hessenberg formuna indirgenir.
3.  **QR Algoritması:** Matris, köşegen forma (Schur formu) yaklaşana kadar iteratif olarak $Q$ (dik/ortogonal) ve $R$ (üst üçgen) matrislerine ayrıştırılır. [cite_start]İterasyon sonunda köşegen üzerindeki değerler özdeğerleri verir.
4.  [cite_start]**Geri Dönüşüm (Back-Transformation):** İndirgenmiş matris üzerinde bulunan özvektörler, orijinal matrisin koordinat sistemine geri döndürülür.
5.  **Normalizasyon:** Tüm özvektörler Öklid normu 1 ($||v|| = 1$) olacak şekilde normalize edilerek standartlaştırılır.

---

## 4. UYGULAMA VE KARŞILAŞTIRMALI ANALİZ (3. SORU)

[cite_start]Ödevin uygulama aşamasında, `Eigen Vectors Values.ipynb` dosyası içerisinde Numpy'ın hazır fonksiyonları (eig) kullanılmadan bir özdeğer hesaplama süreci yürütülmüştür.

* [cite_start]**Metot:** Manuel olarak karakteristik denklem ve kök bulma (veya güç iterasyonu) yöntemi uygulanmıştır.
* [cite_start]**Gözlem:** Küçük boyutlu matrislerde manuel yöntemler başarılı olsa da, matris boyutu büyüdükçe (n > 4) nümerik kararlılık açısından `np.linalg.eig` (LAPACK tabanlı QR algoritması) fonksiyonunun çok daha hassas ve hızlı sonuçlar ürettiği kanıtlanmıştır.

---

## KAYNAKÇA
* [cite_start][1] Introduction to Matrices for Machine Learning - MachineLearningMastery.com 
* [cite_start][2] Gentle Introduction to Eigenvalues and Eigenvectors - MachineLearningMastery.com 
* [cite_start][3] NumPy linalg.eig Documentation: https://numpy.org/doc/2.1/reference/generated/numpy.linalg.eig.html 
* [cite_start][4] NumPy GitHub Source Code: https://github.com/numpy/numpy/tree/main/numpy/linalg 
* [cite_start][5] Eigenvalues-and-Eigenvectors Repository: https://github.com/LucasBN/Eigenvalues-and-Eigenvectors 
* [6] Principal Component Analysis (PCA) in Machine Learning - DigitalOcean.
* [7] Eigenvalues and Eigenvectors for Machine Learning - Dilip Kumar (Medium).  
