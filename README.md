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
![](https://github.com/kayahuseyinn/Formula1-Car-Dedection-with-YOLOv5/blob/master/images/LabelImg.png)
LabelImg, sade ve kullanışlı bir arayüzü bulunan bir etiketleme aracıdır. 

LabelImg'ta etiketlenen her görüntü için aynı görüntüye ait etiketlenen pixel koordinatlarının bulunduğu birer .txt dosyası oluşur. Buna etiket dosyaları demek yanlış olmaz diye düşünüyorum. Örneğin, "Formula1_1.jpg" dosyasını etiketledikten ve kaydettikten sonra "Formula1_1.txt" dosyası oluşur.

Eğitim-test ayrımı yaparken hem görüntüler için hem de etiket dosyaları için bu ayrım yapılmak zorundadır.

Ben eğitim-test ayrımını elle yaparak farklı sahnelerdeki tüm ihtimallerin göz önünde aynı derecede bulunmasını sağlamaya çalıştım. 900'a yakın görüntüyü eğitim için 100'e yakın görüntüyü de test için ayırdı. En sonunda algoritmayı uygulamak adına dosya formatını ayarladım.

Kullandığım veri setimin son hali: [Formula1 Veri Seti](https://github.com/kayahuseyinn/Formula1-Car-Dedection-with-YOLOv5/tree/master/Formula1Dataset)

### Yolov5 kullanarak modelimizi eğitmek
Yolov5 reposunu klonluyoruz.

`$ git clone https://github.com/ultralytics/yolov5.git`

Gereksinimleri kuruyoruz.

`$ cd yolov5`

`$ pip install -r requirements.txt`

custom.yaml dosyası oluşturuyoruz. Bu dosya algoritmanın veri setimizin kaynağını bulurken kullandığı dosya olacak.

<pre>
train: ../Formula1Dataset/images/train/
val: ../Formula1Dataset/images/val/
nc: 1
names: ['Formula1 Car']</pre>

Yukarıda içeriği verilen custom.yaml dosyası veri setimizde eğitim ve test bölümlerini algoritmaya tanıtmaya yarıyor, "nc" kaç adet nesnenin tespit edileceğini, "names" ise bu nesnelerin adını belirtiyor. Bu dosyayı klonladığımız /yolov5 klasörüne atıyoruz.

Artık eğitim için hazır durumdayız. Aşağıdaki komutla modelimizi oluşturmaya başlayabiliriz.

`$ python train.py --img 640 --batch 16 --epochs 300 --data custom.yaml --weights yolov5s.pt --cache`

epochs: Epoch(döngü) sayısı, eğitim sırasında tüm eğitim verilerinin ağa gösterilme sayısıdır. Eğitimin doğruluğu arttığında bile, validation(doğrulama) doğruluğu azalmaya başlayana kadar epoch sayısını artırın. Doğruluğun en yüksek olduğu yerde epoch sayınız idealdir.


batch: parametre güncellemesinin gerçekleştiği ağa verilen alt örneklerin sayısıdır. Toplu boyut için iyi bir varsayılan değer 16 olabilir. Ayrıca 32, 64, 128, 256 ve benzeri değerleri de deneyin.

weights: Eğitimde kullanmak istediğimiz ağırlığı belirtiyor. [YoloV5](https://github.com/ultralytics/yolov5) Buradan farklı ağırlıkların başarım kıyaslamasını inceleyebilirsiniz.

### Modelimizi video üzerinden test etmek
Eğitim aşaması bittikten sonra /yolov5 klasöründe "/runs/train/exp" dizininde modelimizin ağırlıklarını (best.pt, last.pt) ve modelimizin farklı ölçütlere göre başarım oranını bulabilirsiniz. 

Kendi çalışmamdaki model ve başarım oranları: 
