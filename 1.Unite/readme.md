# 🤖 1. Ünite: Robotik İçin Mikrodenetleyici Kart

Merhaba Gençler\! 👋
Bu ünitede robotların "beyni" olan mikrodenetleyicileri, robotun "iskeleti" olan mekanik parçaları ve robot dünyasının temellerini öğreneceğiz. Hazırsanız başlayalım\!

-----

## 1\. Mikrodenetleyici Nedir? (Robotun Beyni)

Mikrodenetleyiciyi, elektronik cihazların görevlerini yerine getirmesini sağlayan minik bir bilgisayar gibi düşünebilirsiniz.

> **💡 Tanım:** Bir programı hafızasına alıp derleyen, giriş/çıkış portları ile dış dünyadan veri alıp (sensörler) dış dünyaya tepki veren (motorlar, ışıklar) entegre devredir.

### Mikrodenetleyicinin İç Yapısı

Bir mikrodenetleyicinin içinde neler var? Tıpkı bir insan beyni veya bilgisayar gibi bölümleri vardır:

  * **MİB (CPU):** İşlemci. Karar verme mekanizması.
  * **RAM (Geçici Bellek):** Elektrik gidince silinen, anlık hesaplamaların yapıldığı defter.
  * **ROM (Kalıcı Bellek):** Programın kaydedildiği, elektrik gitse de silinmeyen kütüphane.
  * **G/Ç Portları (I/O):** Robotun eli, kolu, gözü. Dışarıya sinyal gönderir veya alır.

**🌍 Gerçek Hayat Örneği:**
Çamaşır makinesi bir mikrodenetleyici kullanır.

1.  **Giriş:** Siz düğmeye basarsınız (Sinyal gelir).
2.  **İşlem:** Mikrodenetleyici suyun sıcaklığını ve süreyi RAM'de hesaplar.
3.  **Çıkış:** Motora "dön" emri verir (Yıkama başlar).

-----

## 2\. Uygulama Kartları (Arduino vb.)

Mikrodenetleyici tek başına küçük siyah bir çiptir (böcek gibi görünür). Bunu kullanmak zordur. Bu çipi alıp, üzerine USB girişi, güç girişi ve bağlantı pinleri ekleyerek kullanımı kolay hale getirdikleri kartlara **Uygulama Kartı** denir.

  * **En Popüler Örnek:** Arduino Uno (Görsel 1.4).
  * **Avantajı:** Lehim yapmadan, USB ile bilgisayara bağlayıp hemen kodlayabilirsin.

### 🛠️ Simülasyon: Tinkercad

Elinizde kart yoksa üzülmeyin\! **Tinkercad** gibi siteler üzerinden sanal devreler kurup kodlarınızı test edebilirsiniz.

-----

## 3\. Robot Nedir ve Türleri

**Robot:** Algılayan (Sensör), Düşünen (İşlemci) ve Hareket Eden (Aktüatör/Motor) makinedir.

### Robot Kontrol Yöntemleri

Robotlar nasıl karar verir?

1.  **Tepkisel (Refleks):** Etki-Tepki. (Örn: Elin yanınca çekmen).
2.  **Bilinçli (Planlı):** Algıla -\> Planla -\> Hareket Et. (Örn: Satranç oynayan robot).
3.  **Hibrit (Karma):** Hem düşünür hem tepki verir.

### Kullanım Alanlarına Göre Robotlar

  * **Endüstriyel:** Fabrikalarda araba parçası birleştiren robot kollar.
  * **Ev Robotları:** Robot süpürgeler.
  * **Tıbbi Robotlar:** Ameliyat yapan robotlar (Da Vinci).
  * **Uzay Robotları:** Mars'taki "Perseverance" aracı.
  * **Hobi/Yarışma:** Çizgi izleyen, mini sumo robotlar.

-----

## 4\. Robotun Bileşenleri (Anatomi)

Bir robotu insan vücuduna benzetirsek bileşenler şöyledir:

| Robot Parçası | İnsan Karşılığı | Görevi | Örnek Parça |
| :--- | :--- | :--- | :--- |
| **Gövde** | İskelet | Parçaları bir arada tutar. | 3D baskı, Pleksi |
| **Sensörler** | Duyu Organları | Dış dünyayı algılar. | Mesafe, Çizgi, Işık Sensörü |
| **Mikrodenetleyici** | Beyin | Karar verir. | Arduino, PIC  |
| **Motor Sürücü** | Sinir Sistemi | Beyinden gelen emri güçlendirip kaslara iletir. | L298N Kartı |
| **Motorlar** | Kaslar | Hareketi sağlar. | DC Motor, Servo Motor |
| **Pil/Güç** | Kalp/Kan | Enerji sağlar. | Li-Po, Li-Ion Piller |

### 🔩 Önemli Mekanik Parçalar

  * **DC Motor:** Elektriği harekete çevirir. Tekerlekleri döndürür.
  * **Servo Motor:** Belirli bir açıya (0-180 derece) dönen motordur. Robot kollarda kullanılır.
  * **Tekerlek/Palet:** Hareketi yere iletir. Engebeli yollar için palet, düz yollar için tekerlek kullanılır.

-----

## 💻 Kodlama Köşesi: İlk Göz Kırpma (Blink)

Bir LED'i yakıp söndürmek, robotik dünyasının "Merhaba Dünya"sıdır. İşte mantığı:

**Senaryo:** 13 numaralı pine bağlı bir LED'i 1 saniye yak, 1 saniye söndür.

```cpp
// Arduino (C++) Kodu - Kitap Sayfa 27 

void setup() {
  // 13 numaralı pini ÇIKIŞ (Output) olarak ayarla.
  // Yani buradan dışarıya elektrik vereceğiz.
  pinMode(13, OUTPUT); 
}

void loop() {
  // LED'i yak (Yüksek Voltaj - 5V ver)
  digitalWrite(13, HIGH); 
  
  // 1000 milisaniye (1 saniye) bekle
  delay(1000); 
  
  // LED'i söndür (Düşük Voltaj - 0V ver)
  digitalWrite(13, LOW); 
  
  // 1 saniye bekle
  delay(1000); 
}
```

> **❓ Soru:** Eğer `delay(1000)` yerine `delay(500)` yazsaydık ne olurdu?
> *Cevap: LED daha hızlı yanıp sönerdi (Yarım saniyede bir).*

-----

## 📝 Ünite Özeti & Kontrol Listesi

Sınav öncesi bu kavramları bildiğinden emin ol:

  - [ ] **Mikrodenetleyici vs Uygulama Kartı:** Mikrodenetleyici çiptir, uygulama kartı (Arduino) o çipin kullanıma hazır halidir.
  - [ ] **Giriş/Çıkış Birimleri:** Sensörler "Giriş" (veri verir), Motorlar ve LED'ler "Çıkış" (iş yapar) birimidir.
  - [ ] **Simülasyon:** Fiziksel parçalar yoksa Tinkercad kullanılır.
  - [ ] **Motor Sürücü:** Mikrodenetleyicinin gücü motorları döndürmeye yetmez, arada güçlendirici olarak "Motor Sürücü" (L298N gibi) kullanılır.
  - [ ] **Sensörler:** Robotun gözü kulağıdır. Mesafe (Ultrasonik), Renk, Çizgi sensörleri vardır.

-----

**Öğretmenim, bir sonraki adımda ne yapmamı istersiniz?**

  * *Seçenek A:* 2. Ünite (Programlama) için benzer notlar hazırlayabilirim.
  * *Seçenek B:* Bu ünite için çoktan seçmeli bir test (quiz) hazırlayabilirim.
  * *Seçenek C:* Tinkercad üzerinde yapılacak bir "Trafik Işığı" projesi için adım adım yönerge oluşturabilirim.