# Lossy compression of a jpeg image
 Bu proje, DCT (Discrete Cosine Transform) temelli bir algoritma kullanarak görüntüler üzerinde kayıplı JPEG sıkıştırma işlemini gerçekleştirmektedir. Amaç, görüntü kalitesinde kabul edilebilir seviyede bozulma ile dosya boyutunu önemli ölçüde azaltmaktır.

 GÖRÜNTÜ SIKIŞTIRMA NEDİR?

Görüntü sıkıştırma,bir görüntü dosyasının orijinal dosyadan daha az yer kaplayacak hale dönüştürülmesidir. İki tür sıkıştırma yöntemi vardır. Kayıplı sıkıştırma ve kayıpsız sıkıştırma

Kayıplı sıkıştırma: Görüntüdeki verilerin bir kısmını kalıcı olarak silerek dosya boyutunun düşürülmesidir. Sıkıştırıldıktan sonra verinin orijinaline göre görüntü kalitesinde düşüşler olur.
Ama genellikle fark insan algısıyla fark edilmez. 

Kullanılan Formatlar ve Yöntemler

1. JPEG (Joint Photographic Experts Group)
 
JPEG sıkıştırma,görüntüyü küçük bloklara bölerek,Ayrık Kosinüs Dönüşümü(DCT) algoritmasını kullanarak bunları bir frekans alanına dönüştürerek ve daha sonra daha az önemli bileşenlerini kaldırarak görüntü boyutunu küçültür.

2. WebP

DCT +Entropi + tahmin ile görüntüyü sıkıştırır.



Kayıplı Sıkıştırma Avantajları

- Küçük dosya boyutları
- Küçük dosyaların gönderim hızı daha hızlı
- Kalite ayarlandığında gözle fark edilmeyen görüntü kalitesi
- Bilindik formatlar sayesinde yazılım ve cihaz desteği çok 

Dezavantajları

- Kalite Düşüşü
- Veri Kaybı
- Hassas görüntüler içi uygun değil (Tıbbi görüntüler)
- Sıkıştırma oranına bağlı bozulmalar


Bir JPEG'li görüntüye  DCT (Ayrık Kosinüs Dönüşümü) ile kayıplı sıkıştırma işlemi yapılacaktır.

DCT, gerçek sinyalleri frekans alanındaki karşılık gelen değerlere eşleyen bir tür hızlı hesaplama dönüşümüdür.

Bir DCT ile sıkıştırma aşamaları

![image](https://github.com/user-attachments/assets/69eb25c3-bb90-43c5-8d0f-c19dadaf6efd)

![image](https://github.com/user-attachments/assets/be3f590f-133b-4fe5-8572-86df0cc3e749)
Görüntü verilerinde kullanılan opencv, diziler için numpy ve grafiklerde kullanmak için matplotlib kütüphanelerini yükledik.

![image](https://github.com/user-attachments/assets/4183d21a-3041-46a3-9fe6-f0aee95ef553)
Bir kuantizasyon matrisi, her bir DCT bileşenini bölme işlemi için kullanılan bir dizi değeri içerir. Yüksek frekans bileşenleri genellikle daha büyük sayılarla bölünerek daha fazla sıkıştırılır ve dolayısıyla görsel detaylar kaybolur. Matristeki her bir sayının değerini arttırarak sıkıştırma oranı arttırabilir.

![image](https://github.com/user-attachments/assets/bc13c3fc-9941-4503-b9a0-ce2b6554ebea)
Görüntü dosyası sıkıştırma yapabilmek için gri tonlamaya çevirildi.

![image](https://github.com/user-attachments/assets/48d3c23e-d3c2-4d38-ae52-a45d1e330d78)
DCT'de çalışabilmek için görüntünün boyutlarını 8x8'lik bloklar halinde bölüyoruz.Genellikle DCT uygularken 8x8 bloklar haline getirilir. Görüntü bloku ile cv2.dct fonskiyonu kullanılarak düşük ve yüksek frekans bileşenleri ayrıştırarak, düşük frekansların daha fazla bilgi taşımasını sağlarız. Frekans bileşenlerini kuantizasyon matrisine bölerek yüksek frekans bilgilerini daha fazla sıkıştırırız. Bu görüntüdeki bazı görsel detayların kaybolmasına yol açar.Ama insan gözüyle fark edilmez.

![image](https://github.com/user-attachments/assets/5ad92364-a81e-4dcb-81c1-72db0f955db9)
Görüntüye 8x8'lik parçalara bölerek DCT uygulanır.

![image](https://github.com/user-attachments/assets/7033c646-ebe2-4d6e-9155-8db29311dd27)
Ters DCT uygulanır yani DCT de yapılanların tersini yaparak sıkıştırılmış verilerden orijinal görüntüyü oluşturulur.Pikselleri (0-255) aralığında tutulur. Olası piksel hatalarını engellemek için.

![image](https://github.com/user-attachments/assets/8168e776-6f00-4248-b15c-baa61064dccf)
Görüntü yeniden oluşturuldu.

![image](https://github.com/user-attachments/assets/e43bbaca-6f82-4b69-81d2-d646364c5bca)
Sıkıştırılmış görüntüyü gösterdik.
![image](https://github.com/user-attachments/assets/3e8452c1-acd1-486c-92a3-51178e2c2eda)
Sıkıştırma oranı ve görüntünün ne kadar kalite kaybı olduğunu  görmüş olduk.

Fourier Dönüşümü: Görüntüdeki frekans bileşenlerini çıkaran bir matematiksel dönüşümdür. Görüntüdeki düşük ve yüksek frekansları analiz etmemize yardımcı olur. Sıkıştırılmış görüntüyü analiz etmemizi sağlar.

Histogram Analizi: Görüntüdeki piksellerin dağılımını gösterir. Histogramın pürüzlü ve dikenli yapısı kayıplı sıkıştırıldığını gösterir.
![image](https://github.com/user-attachments/assets/99d4ab1a-9b19-43c0-a915-68c548be11c7)
![image](https://github.com/user-attachments/assets/de9b7336-4fd2-44c1-8af7-c618f7b3b2b3)
