# 💻 2. Ünite: Mikrodenetleyici Kart Programlama

Merhaba Gençler\! 👋
Bu ünitede artık "Robotun Beyni"ne emir vermeyi öğreniyoruz. Kod yazmak aslında bir yemek tarifi yazmak gibidir; işlemciye hangi malzemeyi (pinleri) ne zaman ve nasıl kullanacağını adım adım anlatacağız.

-----

## 🛠️ Bölüm 1: Kod Nasıl Yazılır ve Yüklenir?

Kodlarımızı **Arduino IDE** (Integrated Development Environment - Tümleşik Geliştirme Ortamı) adı verilen programda yazarız.

### 1\. Arduino IDE Ekranını Tanıyalım

  * **Doğrulama (Tik İşareti - ✔️):** Yazdığınız kodda yazım hatası var mı diye kontrol eder ("Derleme" işlemi).
  * **Yükleme (Ok İşareti - ➡️):** Kodu kontrol eder ve USB kablosu üzerinden karta gönderir.

### 2\. Kodu Karta Yükleme Adımları

Kodu yazdıktan sonra şu 3 adımı mutlaka kontrol etmelisiniz:

1.  **Bağlantı:** Kartınızı USB kablosu ile bilgisayara bağlayın.
2.  **Kart Seçimi:** `Araçlar` \> `Kart` menüsünden kullandığınız kartı seçin (Genelde "Arduino Uno").
3.  **Port Seçimi:** `Araçlar` \> `Port` menüsünden kartınızın bağlı olduğu portu (Örn: COM3, COM5) seçin. Port görünmüyorsa bağlantı hatası var demektir.
4.  **Yükle:** Yükle (➡️) butonuna basın. Altta "Yükleme Tamamlandı" yazısını görmelisiniz.

-----

## 🧠 Bölüm 2: Arduino Kodunun İskeleti

Her Arduino programı iki temel bloktan (fonksiyondan) oluşur. Bu yapıyı adınız gibi bilmelisiniz:

```cpp
void setup() {
  // Buradaki kodlar SADECE BİR KEZ çalışır.
  // Ayarlar burada yapılır (Hangi pin giriş, hangi pin çıkış olacak?).
}

void loop() {
  // Buradaki kodlar SONSUZ DÖNGÜDE çalışır.
  // Ana görevler (ışığı yak, bekle, söndür) burada yapılır.
  // Elektrik kesilene kadar burası tekrar eder.
}
```

-----

## 🚦 Bölüm 3: LED Uygulamaları ve Kod Açıklamaları

### Uygulama 1: Merhaba Dünya (Blink - Tek LED)

Bu, programlamanın "Merhaba Dünya"sıdır. 2 numaralı pine bağlı bir LED'i 1 saniye yakıp söndüreceğiz.

**Devre Kurulumu:**

  * LED'in uzun bacağı (+) -\> 220 Ohm Direnç -\> Arduino Pin 2
  * LED'in kısa bacağı (-) -\> Arduino GND (Toprak).

**Kodlar ve Anlamları:**

```cpp
void setup() {
  // pinMode komutu pinin görevini belirler.
  // 2 numaralı pini OUTPUT (ÇIKIŞ) olarak ayarla. Çünkü dışarıya elektrik vereceğiz.
  pinMode(2, OUTPUT); 
}

void loop() {
  // digitalWrite: Dijital bir pine enerji verir (1/HIGH) veya keser (0/LOW).
  
  digitalWrite(2, 1);   // 2 numaralı pine elektrik ver (LED YANAR). 1 = HIGH = 5V.
  delay(1000);          // 1000 milisaniye (yani 1 saniye) bekle. (Hiçbir şey yapmadan dur).
  
  digitalWrite(2, 0);   // 2 numaralı pinden elektriği kes (LED SÖNER). 0 = LOW = 0V.
  delay(1000);          // 1 saniye daha bekle (Sönük kalsın).
  
  // Döngü bitti, loop olduğu için başa döner ve tekrar yakar.
}
```

-----

### Uygulama 2: İki LED'i Sırayla Yakma (Flip-Flop)

Biri yanarken diğeri sönsün. Polis çakarı mantığı.

  * **Pinler:** 2 ve 3.

**Kodlar:**

```cpp
void setup() {
  pinMode(2, OUTPUT); // 2. pini çıkış yap
  pinMode(3, OUTPUT); // 3. pini çıkış yap
}

void loop() {
  digitalWrite(2, 1); // 1. LED YANSIN
  digitalWrite(3, 0); // 2. LED SÖNSÜN
  delay(1000);        // 1 saniye bu halde bekle
  
  digitalWrite(2, 0); // 1. LED SÖNSÜN
  digitalWrite(3, 1); // 2. LED YANSIN
  delay(1000);        // 1 saniye bu halde bekle
}
```

-----

### Uygulama 3: 5 LED ile Kara Şimşek (Sıralı Yanma)

5 tane LED'i sırayla yakıp söndüreceğiz.

  * **Pinler:** 2, 3, 4, 5, 6.

**Kodlar (Uzun Yöntem):**
*Bu yöntemde her şeyi tek tek yazarız. Kod uzundur.*

```cpp
void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
}

void loop() {
  // Sırayla yak
  digitalWrite(2, 1); delay(1000);
  digitalWrite(3, 1); delay(1000);
  digitalWrite(4, 1); delay(1000);
  digitalWrite(5, 1); delay(1000);
  digitalWrite(6, 1); delay(1000);
  
  // Sırayla söndür
  digitalWrite(2, 0); delay(1000);
  digitalWrite(3, 0); delay(1000);
  digitalWrite(4, 0); delay(1000);
  digitalWrite(5, 0); delay(1000);
  digitalWrite(6, 0); delay(1000);
}
```

-----

### Uygulama 4: 7 LED ve "for" Döngüsü (Kısa Yöntem)

7 tane LED için yukarıdaki gibi tek tek yazarsak kod çok uzar. Bunun yerine **`for` döngüsü** kullanırız. `for` döngüsü, bir işlemi istediğimiz sayıda tekrar ettirir.

  * **Pinler:** 2'den 8'e kadar.

**Kodlar:**

```cpp
int i; // "i" adında bir sayaç değişkeni tanımladık.

void setup() {
  // i değişkeni 2'den başlasın, 8 olana kadar birer birer artsın (i++)
  for(i=2; i<=8; i++) {
    pinMode(i, OUTPUT); // Önce 2'yi, sonra 3'ü... en son 8'i çıkış yapar. Tek satırda iş biter!
  }
}

void loop() {
  // LED'leri sırayla yakma döngüsü
  for(i=2; i<=8; i++) {
    digitalWrite(i, 1); // Sıradaki pini yak
    delay(1000);        // Bekle
  }
  
  // LED'leri sırayla söndürme döngüsü
  for(i=2; i<=8; i++) {
    digitalWrite(i, 0); // Sıradaki pini söndür
    delay(1000);        // Bekle
  }
}
```

-----

### Uygulama 5: Trafik Lambası 🚦

Gerçek hayattan bir simülasyon yapalım. Kırmızı, Sarı ve Yeşil LED kullanacağız.

  * **Pinler:** Kırmızı(2), Sarı(3), Yeşil(4).

**Kodlar:**

```cpp
// Değişken Tanımlama: Kodun okunabilirliğini artırır.
int k = 2; // Kırmızı LED 2. pinde
int s = 3; // Sarı LED 3. pinde
int y = 4; // Yeşil LED 4. pinde

void setup() {
  pinMode(k, OUTPUT); // Kırmızı çıkış
  pinMode(s, OUTPUT); // Sarı çıkış
  pinMode(y, OUTPUT); // Yeşil çıkış
}

void loop() {
  // 1. Durum: KIRMIZI YAN (Diğerleri sönük)
  digitalWrite(k, 1);
  digitalWrite(s, 0);
  digitalWrite(y, 0);
  delay(5000); // 5 saniye bekle
  
  // 2. Durum: SARI YAN (Hazırlan) - Kırmızı sönsün mü? Genelde Türkiye'de Kırmızı+Sarı yanar ama kitapta tek tek yakmış.
  digitalWrite(k, 0);
  digitalWrite(s, 1);
  delay(1000); // 1 saniye bekle
  digitalWrite(s, 0); // Sarıyı söndür
  
  // 3. Durum: YEŞİL YAN (Geç)
  digitalWrite(y, 1);
  delay(5000); // 5 saniye bekle
  digitalWrite(y, 0); // Yeşili söndür
  
  // 4. Durum: Tekrar SARI (Durmaya hazırlan)
  digitalWrite(s, 1);
  delay(1000);
  // Döngü başa döner ve tekrar Kırmızı yanar.
}
```

*(Not: Kitaptaki kod örneğinde sarı yandığında diğerlerini söndürme mantığı kullanılmıştır)*

-----

### 📝 Önemli İpuçları (Sınav Notları)

1.  **Noktalı Virgül (;):** Her komut satırının sonuna mutlaka konur. Unutursanız hata alırsınız\!
2.  **Büyük/Küçük Harf:** `pinMode` ile `pinmode` aynı değildir. Arduino büyük/küçük harfe duyarlıdır. (Deve hörgücü gibi: pin**M**ode, digital**W**rite).
3.  **setup vs loop:** `setup` bir kere (hazırlık), `loop` sonsuza kadar (uygulama) çalışır.
4.  **Direnç:** LED bağlarken mutlaka direnç kullanmalıyız, yoksa LED patlayabilir (Genelde 220 Ohm).
