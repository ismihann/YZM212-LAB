# Kolmogorov Karmaşıklığı:Ödev 7
  ### Ödev Sorusu:
  Proje: Bir dizinin (string) Kolmogorov karmaşıklığının $K(x)$, o diziyi çıktı veren en kısa programın uzunluğu olduğunu varsayalım. "Sıkıştırılamayan" (incompressible) dizilerin varlığını ispatlayın. Ardından, Berry Paradoksu'nu ("The smallest positive integer not definable in fewer than twenty words") kullanarak, $K(x)$ fonksiyonunun hesaplanamaz (non-computable) olduğunu gösteren formel bir çelişki (contradiction) kanıtı oluşturun.
### 1- Sıkıştıralamayan dizilerin varlığını ispatla.
### 2- Kolmogorov karmaşıklığın hesaplanamaz olduğunu çelişki yoluyla açıkla.

### Teorem1:
  Her n için sıkıştırılamayan string vardır.

### İspat:
    Uzunluğu n olan 2^n string vardır, fakat uzunluğu < n olan yalnızca 2^n - 1 program vardır.  
    -2^n-1  geometrik seri toplamından gelir-
    -uzunluk<n dememizin sebebi de aslında sıkıştırma yapmak istememiz-
    sonuç: bizim 2^n kadar stringimiz var ve 2^n-1 kadar da bu stringleri çalıştırıcak programımız var.O zaman:
    En az 1 string, hiçbir kısa program tarafından üretilemez. yani:Bu string: K(x)≥n'dir sıkıştırılamaz.

### Teorem2:
      Kolmogorv karmaşıklık hesaplanamaz.

### İspatı:
    -Çelişki yoluyla-
    Önce Kolmogorv karmaşıklık ne: K(x) : x’i üreten en kısa programın uzunluğu.
    Berry Parodoksu ne:“En küçük sayı ki, kendisini tanımlayan sözcüklerin sayısı 100’den fazla.”
    Bu ifade paradoks oluşturur çünkü:
    Eğer böyle bir sayı varsa, cümlemiz ile onu 100 kelime ile tanımlamış oluyoruz → çelişki.
    Mantık burada: “Bir şeyi tanımlayan en kısa açıklama” ile “tanımın kendisi” çelişiyor.
   
    Varsayım yapıyoruz, "Kolmogorov karmaşıklığı hesaplanabilir olsun."Yani her string için Kolmogorov karmaşıklığını veren bir Turing makinesi 𝑀(program) vardır.
    Ve diyelim ki n uzunluğunda sıkıştıralamayan bir dizi bulmak istiyoruz.
    Sıkıştıralamayan = Kolmogorov karmaşıklığı ≥ n.
    Yani diziyi daha kısa bir programla yazamayız.
    Şimdi bu  hesaplamayı yapan programı(algoritmayı) bulmak isityoruz:
    Algoritma şöyle olabilir:
       1-Tüm 𝑛 uzunluğundaki dizileri sırayla ele al.
       2-Her dizinin K(x) değerini hesapla.
       3-K(x)≥n ise, bu diziyi seç ve yazdır.
    Biz bunu bir programlama dilinde yazarsak bu programın uzunluğu yaklaşık olaran logn+c kadar olucak.
    Porgramın uzunluğu= logn+c <n oldu 
    Berry Paradoksu burda devreye giriyor.
    Porgramın uzunluğu= logn+c <n oldu programla ürettiğimiz k(x)> n oldu.
    Yani k(x)>n dediğimiz burada sıkıştıralamayan bir string var ve bunu daha kısa bir program uzunluğu ile yazamayız n ve n'den büyük bir uzunlukta yazabiliriz 
    Ama oluşturduğumuz programın uzunluğu logn+c yani n'den küçük.

    İşte burada Berry paradoksu devreye giriyor:
       " En küçük n uzunluğunda sıkıştıralamayan diziyi üreten programın uzunluğu n’den küçük olamaz."
       Ama bizim algoritmamız tam olarak bunu yapıyor → çelişki
	​

   
