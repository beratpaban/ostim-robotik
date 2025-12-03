

# 🎚️ Bölüm 4: Sürgülü Anahtar ile Dijital Giriş

Gençler, şu ana kadar biz Arduino'ya "Işığı yak" dedik ve o da yaptı. Şimdi ise biz Arduino'ya bir soru soracağız: **"Anahtar açık mı kapalı mı?"**. O da bize cevap verecek ve ona göre işlem yapacak.

### 🤔 Mantık Nedir? (INPUT Kavramı)

  * **OUTPUT (Çıkış):** Arduino dışarıya elektrik verir (LED yakar).
  * **INPUT (Giriş):** Arduino dışarıdan gelen elektriği okur (Anahtara basıldı mı?).
      * Eğer anahtar açıksa (5V geliyorsa) sonuç **1 (HIGH)** olur.
      * Eğer anahtar kapalıysa (0V/GND geliyorsa) sonuç **0 (LOW)** olur.

-----

## 🛠️ Uygulama 9: Anahtar ile LED Seçimi

**Senaryo:** Elimizde bir anahtar var. Anahtarı sağa çekersek bir LED grubu, sola çekersek diğer LED grubu yanacak.

**Devre Bağlantısı (Kitap Sayfa 76-77):**

  * **Girişler:** Anahtarın bacakları Arduino'nun **4** ve **5** numaralı pinlerine bağlı.
  * **Çıkışlar:** LED'ler **2** ve **3** numaralı pinlere bağlı.

### Kodlar ve Açıklamaları

```cpp
void setup() {
  // LED'ler yine ÇIKIŞ (OUTPUT) çünkü ışık verecekler.
  pinMode(2, OUTPUT); 
  pinMode(3, OUTPUT);
  
  // DİKKAT! İşte yeni komutumuz: INPUT (GİRİŞ)
  // 4 ve 5 numaralı pinlere anahtar bağladık, buradan veri OKUYACAĞIZ.
  pinMode(4, INPUT);
  pinMode(5, INPUT);
}

void loop() {
  // digitalRead(pin): Belirtilen pindeki elektriği okur. (Var mı yok mu?)
  
  // DURUM 1: Eğer 4 numaralı pinden "1" (Enerji) geliyorsa...
  if (digitalRead(4) == 1) { 
    digitalWrite(2, 1); // 2. LED'i Yak
  } 
  else { 
    digitalWrite(2, 0); // Değilse Söndür
  }

  // DURUM 2: Eğer 5 numaralı pinden "1" (Enerji) geliyorsa...
  if (digitalRead(5) == 1) { 
    digitalWrite(3, 1); // 3. LED'i Yak
  } 
  else { 
    digitalWrite(3, 0); // Değilse Söndür
  }
}
```

> **💡 Özet:** Arduino sürekli olarak 4 ve 5 numaralı pinleri dinliyor. "Elektrik var mı?" diye soruyor. Varsa `if` bloğunun içine girip LED'i yakıyor.

-----

## 🌊 Uygulama 10: Anahtar ile Animasyon Değiştirme

**Senaryo:** Bu proje çok daha havalı\! Anahtarın konumuna göre LED'lerin yanma şeklini (Animasyonu) değiştireceğiz.

  * **Anahtar Sola:** LED'ler soldan sağa aksın.
  * **Anahtar Sağa:** LED'ler sağdan sola aksın.

**Devre Bağlantısı (Kitap Sayfa 78-79):**

  * **LED'ler:** 2, 3, 4, 5, 6 numaralı pinlere bağlı (5 adet).
  * **Anahtar:** 11 numaralı pine bağlı.

### Kodlar ve Açıklamaları

```cpp
int i; // Döngü için sayaç değişkeni

void setup() {
  // 2'den 6'ya kadar tüm LED pinlerini hızlıca OUTPUT yapalım (For döngüsü ile)
  for (i = 2; i <= 6; i++) {
    pinMode(i, OUTPUT);
  }
  
  // Anahtarın bağlı olduğu 11. pini GİRİŞ yapıyoruz.
  pinMode(11, INPUT);
}

void loop() {
  
  // SENARYO 1: Anahtardan "1" geliyorsa (Anahtar Bir Yöne Çekili)
  // LED'leri 2'den 6'ya doğru (Soldan Sağa) yak ve söndür.
  if (digitalRead(11) == 1) {
    
    // Yakma Döngüsü
    for (i = 2; i <= 6; i++) { 
      digitalWrite(i, 1); // Sıradaki LED'i yak
      delay(1000);        // 1 saniye bekle
    }
    
    // Söndürme Döngüsü
    for (i = 2; i <= 6; i++) { 
      digitalWrite(i, 0); // Sıradaki LED'i söndür
      delay(1000);        // 1 saniye bekle
    }
  } // if sonu

  // SENARYO 2: Anahtardan "0" geliyorsa (Anahtar Diğer Yöne Çekili)
  // LED'leri 6'dan 2'ye doğru (Sağdan Sola) yak ve söndür.
  // Dikkat: Burada döngü geriye doğru sayıyor (i--).
  if (digitalRead(11) == 0) {
    
    // Yakma Döngüsü (Tersten)
    for (i = 6; i >= 2; i--) { 
      digitalWrite(i, 1); 
      delay(1000); 
    }
    
    // Söndürme Döngüsü (Tersten)
    for (i = 6; i >= 2; i--) { 
      digitalWrite(i, 0); 
      delay(1000); 
    }
  } // if sonu

} // loop sonu
```

-----

## 📝 Sürgülü Anahtar İçin Önemli Notlar

1.  **`pinMode(pin, INPUT)`:** Bir parçadan (anahtar, sensör, buton) bilgi okuyacaksanız, o pini mutlaka `setup` kısmında `INPUT` olarak tanıtmalısınız.
2.  **`digitalRead(pin)`:** Bu komut Arduino'nun kulağıdır. Pini dinler. Cevap olarak sadece **1 (Var)** veya **0 (Yok)** döner.
3.  **Karar Yapısı (`if`):** Gelen bilgiye göre işlem yapmak için `if` (eğer) komutu kullanılır. "Eğer okunan değer 1 ise şunu yap" demektir.