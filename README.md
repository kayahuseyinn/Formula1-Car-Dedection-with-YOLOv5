# YoloV5 kullanarak kendi veri setimizle Formula 1 araçlarının tespiti
## Projenin Amacı
Farklı açı ve yükseklik farketmeksizin Formula 1 araçlarını kendi veri setimizi kullanarak tespit etmek.


## Ana konular:
1) Kendi veri setimizi oluşturmak
2) Kendi veri setimizi etiketlemek ve algoritmaya uygun formata getirmek
3) Yolov5 kullanarak modelimizi eğitmek
4) Modelimizi video üzerinden test etmek


### Kendi veri setimizi oluşturmak
Proje kapsamında kendi veri setimi oluştururken, yüksek çözünürlüklü Formula 1 yarış videolarını kullandım. 
Öncelikle farklı açılardan ve yüksekliklerden görüntüler içeren videoları indirdim. Özellikle Formula 1 organizasyonunun kendi paylaştığı videoları kullanmaya özen gösterdim. Çünkü yarışlarda kullanılan tüm kamera açılarını içeren videolar bulunmaktaydı.Aşağıda bazı örnek video linkleri bulunmaktadır.
 - [Video Linki](https://www.youtube.com/watch?v=-Ee08uFurok)
 - [Video Linki](https://www.youtube.com/watch?v=ZGRpHy0qoN4&t=354s)

Sonrasında elimde bulunan videolardan, .jpg formatında görüntüler elde etmek istediğim için [VLC media player](https://www.videolan.org/vlc/index.tr.html) kullandım. Bu aşamada VLC media player'ın videoyu kare kare oynatmaya ve ekran görüntüsü almaya izin vermesi özelliklerini kullandım. 
1000'e yakın görüntü elde ettikten sonra etiketleme aşamasına geçtim.

### Kendi veri setimizi etiketlemek ve algoritmaya uygun formata getirmek
Nesne tespiti algoritmalarıyla model geliştirebilmek için elimizdeki verileri etiketlememiz gerekir. Ben bu aşamada LabelImg aracını kullandım. 
![](https://github.com/kayahuseyinn/Formula1-Car-Dedection-with-YOLOv5/blob/main/images/LabelImg.png)
LabelImg, sade ve kullanışlı bir arayüzü bulunan bir etiketleme aracıdır. 

LabelImg'ta etiketlenen her görüntü için aynı görüntüye ait etiketlenen pixel koordinatlarının bulunduğu birer .txt dosyası oluşur. Buna etiket dosyaları demek yanlış olmaz diye düşünüyorum. Örneğin, "Formula1_1.jpg" dosyasını etiketledikten ve kaydettikten sonra "Formula1_1.txt" dosyası oluşur.

Eğitim-test ayrımı yaparken hem görüntüler için hem de etiket dosyaları için bu ayrım yapılmak zorundadır.

Ben eğitim-test ayrımını elle yaparak farklı sahnelerdeki tüm ihtimallerin göz önünde aynı derecede bulunmasını sağlamaya çalıştım. 900'a yakın görüntüyü eğitim için 100'e yakın görüntüyü de test için ayırdı. En sonunda algoritmayı uygulamak adına dosya formatını ayarladım.

Kullandığım veri setimin son hali: 

