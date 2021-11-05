# YoloV5 kullanarak kendi veri setimizle Formula 1 araçlarının tespiti
## Projenin Amacı
Farklı açı ve yükseklik farketmeksizin Formula 1 araçlarını kendi veri setimizi kullanarak tespit etmek.


## Ana konular:
1) Kendi veri setimizi oluşturmak
2) Kendi veri setimizi nesne tespiti yapabilmek adına etiketlemek
3) Yolov5 kullanarak modelimizi eğitmek
4) Modelimizi video üzerinden test etmek


### Kendi veri setimizi oluşturmak
Proje kapsamında kendi veri setimi oluştururken, yüksek çözünürlüklü Formula 1 yarış videolarını kullandım. 
Öncelikle farklı açılardan ve yüksekliklerden görüntüler içeren videoları indirdim. Özellikle Formula 1 organizasyonunun kendi paylaştığı videoları kullanmaya özen gösterdim. Çünkü yarışlarda kullanılan tüm kamera açılarını içeren videolar bulunmaktaydı.Aşağıda bazı örnek video linkleri bulunmaktadır.
 - [Video Linki](https://www.youtube.com/watch?v=-Ee08uFurok)
 - [Video Linki](https://www.youtube.com/watch?v=ZGRpHy0qoN4&t=354s)

Sonrasında elimde bulunan videolardan, .jpg formatında görüntüler elde etmek istediğim için [VLC media player](https://www.videolan.org/vlc/index.tr.html) kullandım. Bu aşamada VLC media player'ın videoyu kare kare oynatmaya ve ekran görüntüsü almaya izin vermesi özelliklerini kullandım. 
1000'e yakın görüntü elde ettikten sonra etiketleme aşamasına geçtim.

### Kendi veri setimizi nesne tespiti yapabilmek adına etiketlemek
Nesne tespiti algoritmalarıyla model geliştirebilmek için elimizdeki verileri etiketlememiz gerekir. Ben bu aşamada LabelImg aracını kullandım. 
[](
