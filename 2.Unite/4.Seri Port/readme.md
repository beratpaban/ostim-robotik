# 📡 Bölüm 6: Seri Port (Haberleşme) Uygulamaları

Gençler, şu ana kadar Arduino ile sadece ışık yakıp söndürdük. Peki Arduino'nun içinde neler olup bittiğini nasıl göreceğiz? İşte burada devreye **Seri Port Ekranı** giriyor. Bunu Arduino ile bilgisayarınız arasındaki bir "sohbet penceresi" (chat) gibi düşünebilirsiniz.

### 1\. Seri Haberleşme Nedir?

Mikrodenetleyici kart (Arduino) ile bilgisayarın USB kablosu üzerinden veri alışverişi yapmasına seri haberleşme denir.

  * **Arduino konuşur, Bilgisayar dinler:** Sensör verilerini ekrana yazar.
  * **Bilgisayar konuşur, Arduino dinler:** Klavyeden gönderdiğiniz komutla robotu yönetirsiniz.

> **⚠️ Önemli:** Seri port ekranını açmak için Arduino IDE'de sağ üst köşedeki **Büyüteç Simgesine** tıklayabilir veya `Ctrl+Shift+M` tuşlarına basabilirsiniz.

-----

### 2\. Haberleşmeyi Başlatmak: `Serial.begin()`

Seri haberleşmeyi kullanabilmek için `setup` kısmında mutlaka bir ayar yapmalıyız. İki tarafın (Arduino ve Bilgisayar) konuşma hızını eşitlemeliyiz.

  * **Komut:** `Serial.begin(9600);`
  * **Anlamı:** "Seri haberleşmeyi saniyede 9600 bit veri aktarım hızıyla (Baud Rate) başlat."
  * **Dikkat:** Seri Port ekranının sağ alt köşesindeki hız ayarı da **9600 baud** olmalıdır. Yoksa ekranda anlamsız semboller (¨?½$£) görürsünüz.

-----

## 📝 Uygulama 13: Ekrana Mesaj Yazdırma

**Amaç:** Bilgisayar ekranına "Robotik ve Kodlama Dersini Çok Seviyorum" yazdırmak.

Bu işlem için iki temel komutumuz var:

1.  **`Serial.print("Mesaj");`** : Parantez içindeki mesajı yazar ve imleci **aynı satırda** bırakır. Bir sonraki mesaj hemen yanına yazılır.
2.  **`Serial.println("Mesaj");`** : (Sonundaki 'ln', 'line/satır' demektir). Mesajı yazar ve imleci **bir alt satıra** geçirir.

### Kodlar ve Açıklamaları

```cpp
void setup() {
  // Haberleşmeyi 9600 hızında başlatıyoruz.
  Serial.begin(9600); 
}

void loop() {
  // "Robotik ve Kodlama" yaz, yanına devam et.
  Serial.print("Robotik ve Kodlama "); 
  
  // "Dersini" yaz, bir alt satıra geç (println).
  Serial.println("Dersini"); 
  
  // "Çok Seviyorum" yaz, bir alt satıra geç.
  Serial.println("Çok Seviyorum"); 
  
  // Mesajları okuyabilmek için biraz bekleme ekleyelim.
  // Yoksa ekran çok hızlı akar.
  delay(1000); 
}
```

> **Ekran Çıktısı Şöyle Olur:**
> Robotik ve Kodlama Dersini
> Çok Seviyorum
> *(1 saniye sonra tekrar eder)*

-----

## ⌨️ Uygulama 14: Klavyeden Veri Okuma (`Serial.read`)

**Amaç:** Bilgisayar klavyesinden bir harfe veya sayıya bastığımızda, Arduino'nun bunu algılamasını ve ekrana geri yazmasını sağlamak.

Burada bilmeniz gereken kritik bir detay var: Bilgisayarlar harfleri tanımaz, sayıları tanır. Siz klavyeden 'A' tuşuna bastığınızda, bilgisayar bunu bir sayısal kod (ASCII kodu) olarak gönderir.

  * Örneğin 'A' harfinin kodu 65'tir.
  * 'a' harfinin kodu 97'dir.

Bu yüzden gelen veriyi okurken bazen **Sayı (int)** bazen de **Karakter (char)** olarak göstermemiz gerekir.

### Kullanılan Komutlar

1.  **`Serial.available()`**: "Seri portta okunacak yeni bir veri var mı?" diye kontrol eder. Veri varsa 0'dan büyük bir değer döner.
2.  **`Serial.read()`**: Gelen veriyi okur. Veriyi tam sayı (int) formatında getirir.

### Kodlar ve Açıklamaları

```cpp
int girilen_deger = 0; // Gelen veriyi saklayacağımız değişken

void setup() {
  Serial.begin(9600); // Haberleşmeyi başlat
}

void loop() {
  // 1. ADIM: Veri geldi mi? Kontrol et.
  if (Serial.available() > 0) {
    
    // 2. ADIM: Veriyi oku ve değişkene kaydet.
    // DİKKAT: Bu komut harfin ASCII kodunu (sayısal değerini) okur.
    girilen_deger = Serial.read(); 
    
    // 3. ADIM: Sayısal (ASCII) değerini ekrana yaz.
    Serial.print("Girilen Deger (Sayisal): ");
    Serial.println(girilen_deger); 
    
    // 4. ADIM: Karakter halini ekrana yaz.
    // (char) komutu, sayıyı tekrar harfe dönüştürür.
    Serial.print("Girilen Deger (Karakter): ");
    Serial.println((char)girilen_deger); 
    
    Serial.println("-------------------------"); // Ayraç çizgi
  }
}
```


> **Deney:** Bu kodu yükleyip Seri Port ekranına "A" yazıp gönderirseniz:
>
>   * Girilen Deger (Sayisal): 65
>   * Girilen Deger (Karakter): A
>     çıktısını alırsınız.

-----

### 📝 Seri Port İçin İpuçları (Sınav Notları)

1.  **`setup` Kısmı:** `Serial.begin(9600);` komutunu `setup` içine yazmayı unutursanız haberleşme başlamaz, ekran boş kalır.
2.  **`println` Farkı:** Alt alta yazdırmak istiyorsanız `println`, yan yana yazdırmak istiyorsanız `print` kullanın.
3.  **Hız Ayarı:** Kodda 9600 yazdıysanız, Seri Port penceresinin altındaki hız ayarı da 9600 olmalıdır.
4.  **ASCII Tablosu:** Arduino, klavyeden girilen "1" rakamını matematiksel 1 olarak değil, karakter kodu olan 49 olarak okur. Bu yüzden matematik işlemi yapacaksanız dönüşüm yapmanız gerekir.
