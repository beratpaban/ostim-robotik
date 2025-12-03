

# 🔘 Bölüm 5: Buton (Push Button) ile Dijital Giriş

Gençler, robotik projelerin vazgeçilmezi olan butonlara geçiyoruz. Butonlar, anlık komutlar vermek için kullanılır.

### ⚠️ Çok Önemli: Direnç Kullanımı (Pull-Down)

Buton bağlarken sadece kablo yetmez, mutlaka bir **Direnç (Genelde 10kΩ)** kullanmalıyız.

  * **Neden?** Eğer direnç kullanmazsak, butona basmadığımız zaman Arduino "Acaba elektrik var mı yok mu?" diye kararsız kalır (Buna "Floating" denir).
  * **Pull-Down Mantığı:** Direnci toprağa (GND) bağlarız. Böylece butona basmadığımızda Arduino kesinlikle **0 (LOW)** okur. Bastığımızda **1 (HIGH)** okur.


-----

## 🟢 Uygulama 11: Buton ile LED Durumunu Değiştirme

**Senaryo:** Butona basılı tuttuğumuz sürece 1. LED yansın, elimizi çektiğimizde 2. LED yansın.

**Devre Bağlantısı (Kitap Sayfa 81):**

  * **Giriş:** Buton, **4** numaralı pine bağlı (10k direnç ile).
  * **Çıkış:** 1. LED **2** numaralı pine, 2. LED **3** numaralı pine bağlı.

### Kodlar ve Açıklamaları

```cpp
void setup() {
  // LED'ler yine ÇIKIŞ (OUTPUT)
  pinMode(2, OUTPUT); 
  pinMode(3, OUTPUT);
  
  // Butonun bağlı olduğu 4. pin GİRİŞ (INPUT) olarak ayarlanmalı
  pinMode(4, INPUT); 
}

void loop() {
  // Butona basılıp basılmadığını kontrol et (1 mi geliyor?)
  if (digitalRead(4) == 1) { 
    // EĞER BASILDIYSA:
    digitalWrite(2, 1); // 1. LED'i Yak
    digitalWrite(3, 0); // 2. LED'i Söndür
  } 
  else { 
    // EĞER BASILMADIYSA (Elimizi çektiysek):
    digitalWrite(2, 0); // 1. LED'i Söndür
    digitalWrite(3, 1); // 2. LED'i Yak
  }
}
```



> **💡 Özet:** Bu kodda `else` (değilse) yapısı çok önemlidir. Butona basmadığımız her an `else` bloğu çalışır ve sistem varsayılan haline (2. LED yanık) döner.

-----

## 🎹 Uygulama 12: İki Butonlu Kontrol (Start/Stop Mantığı)

**Senaryo:** Bu, endüstriyel makinelerdeki mantıktır.

  * **1. Butona (Start)** basınca makine (LED) çalışsın ve çalışmaya devam etsin.
  * **2. Butona (Stop)** basınca makine (LED) dursun.

**Devre Bağlantısı (Kitap Sayfa 83-84):**

  * **Çıkış:** LED **2** numaralı pine bağlı.
  * **Giriş 1:** Birinci buton **3** numaralı pine bağlı.
  * **Giriş 2:** İkinci buton **4** numaralı pine bağlı.

### Kodlar ve Açıklamaları

```cpp
void setup() {
  pinMode(2, OUTPUT); // LED Çıkış
  
  pinMode(3, INPUT);  // 1. Buton Giriş (Açma)
  pinMode(4, INPUT);  // 2. Buton Giriş (Kapama)
}

void loop() {
  // SENARYO 1: 1. Butona (3. pin) basıldı mı?
  if (digitalRead(3) == 1) {
    digitalWrite(2, 1); // LED'i Yak (Ve öyle bırak, söndürme komutu yok!)
  }
  
  // SENARYO 2: 2. Butona (4. pin) basıldı mı?
  if (digitalRead(4) == 1) {
    digitalWrite(2, 0); // LED'i Söndür
  }
}
```

> **🧠 Kritik Fark:** Bir önceki uygulamada `else` kullanmıştık, elimizi çekince sönüyordu. Burada `else` **YOK**.
>
>   * Buton 1'e bastığımızda LED yanar. Elimizi çeksek bile Arduino'ya "söndür" demediğimiz için yanmaya devam eder (Hafızada tutar).
>   * Ta ki Buton 2'ye basıp "Söndür" emrini verene kadar.

-----

### 📝 Buton Kullanımı İçin İpuçları (Sınav Notları)

1.  **Switch vs Buton:** Anahtar kalıcıdır, buton anlıktır. Kodlamada butona basılı tutma süresi önemlidir.
2.  **Pull-Down Direnci:** Buton ile GND arasına takılan 10k dirençtir. Takmazsanız LED kendi kendine yanıp sönebilir (Parazit yapar).
3.  **Hafıza Mantığı:** Bir butona basıp çektiğimizde ışığın yanık kalmasını istiyorsak, `else` kullanmamalıyız. `if` ile durumu değiştirip öyle bırakmalıyız.
