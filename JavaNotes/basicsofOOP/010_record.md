# 📘 record – Java'nın Immutable Veri Taşıyıcısı (DTO Devrimi)

## 🔍 1. record Nedir?

Java’da record, sadece veri tutmak için oluşturulan, immutable (değiştirilemez) lightweight class tanımlamaya yarayan yeni bir yapıdır.
İlk kez Java 14 ile geldi, Java 16 itibariyle stable (resmi) oldu.

```java
public record Kullanici(String isim, int yas) {}
```

Bu tanımlama ile Java senin için otomatik olarak:

- private final field’lar
- Constructor
- get method’ları
- toString()
- equals() & hashCode()

otomatik üretir.

## ⚙️ 2. Neden record?

| Geleneksel Class                                | `record` ile                        |
| ----------------------------------------------- | ----------------------------------- |
| Bolca boilerplate kod                           | Sadece 1 satır tanım                |
| `getter`, `toString()`, `equals()` elle yazılır | JVM tarafından otomatik oluşturulur |
| Mutable (değişebilir)                           | Immutable (değiştirilemez)          |
| DTO yazımı zahmetli                             | DTO yazımı ultra kolay              |


## 🧱 3. record Özellikleri

`🔒 Immutable’dır`

```java
Kullanici k = new Kullanici("Ali", 30);
k.isim() = "Veli"; // ❌ Derlenmez çünkü immutable
```

`📥 Constructor Otomatik`

```java
public record Kullanici(String isim, int yas) {}
```

__şu anlama gelir:__

```java
public final class Kullanici {
    private final String isim;
    private final int yas;

    public Kullanici(String isim, int yas) {
        this.isim = isim;
        this.yas = yas;
    }

    public String isim() { return isim; }
    public int yas() { return yas; }

    // toString(), equals(), hashCode() JVM tarafından otomatik eklenir
}
```

## 🧪 4. Kullanım Örneği

```java
public record Kisi(String ad, String soyad, int yas) {}

public class Main {
    public static void main(String[] args) {
        Kisi kisi = new Kisi("Zeynep", "Demir", 25);

        System.out.println(kisi.ad());       // Zeynep
        System.out.println(kisi);            // Kisi[ad=Zeynep, soyad=Demir, yas=25]
    }
}
```

## 🎯 5. record Ne Zaman Kullanılır?

| Kullanım Durumu         | record İdeal mi?     |
| ----------------------- | -------------------- |
| DTO (Data Transfer Obj) | ✅ Mükemmel           |
| REST API response body  | ✅ Mükemmel           |
| Immutable objeler       | ✅ Süper              |
| Entity/Service sınıfı   | ❌ Hayır              |
| İş mantığı içeriyorsa   | ❌ record uygun değil |


## 🧠 6. record ile validation veya custom constructor

```java
public record Urun(String isim, double fiyat) {
    public Urun {
        if (fiyat < 0)
            throw new IllegalArgumentException("Fiyat negatif olamaz!");
    }
}
```

Bu constructor, JVM’in default constructor’ı çağırmadan önce çalışır. `“Compact constructor”` denir.

## 🧪 7. Metot Eklemek Mümkün

Evet, metot ekleyebilirsin:

```java
public record Urun(String isim, double fiyat) {
    public String etiket() {
        return isim + " - " + fiyat + "₺";
    }
}
```

## ❗ 8. Dikkat Edilmesi Gerekenler

| Uyarı                                     | Açıklama                            |
| ----------------------------------------- | ----------------------------------- |
| Fields final'dır, set edilemez            | Immutable yapı                      |
| Inheritance (miras alma) yoktur           | `record` başka sınıfı extend edemez |
| Class yerine interface implement edebilir | Evet, `record` → interface          |
| State saklama dışında kullanılmamalı      | İş mantığı içermez                  |


## 🧠 9. record vs class

| Özellik         | `class`              | `record`          |
| --------------- | -------------------- | ----------------- |
| Mutable mı?     | Evet                 | Hayır             |
| equals/hashCode | Elle yazılır         | Otomatik          |
| Constructor     | Kendin yazarsın      | JVM üretir        |
| Field tanımı    | `private` + getter   | Sadece parametre  |
| Kod miktarı     | Yüksek (boilerplate) | Minimum (1 satır) |


## 🔐 10. record ile Interface Kullanımı

```java
public interface Entity { }

public record Kullanici(String isim, int yas) implements Entity { }
```

## 🧰 11. JSON & Spring Boot ile Kullanımı

Spring Boot’ta record, `@RestController` içindeki DTO’lar için çok kullanışlıdır:

```java
public record KullaniciDto(String isim, int yas) {}
```

`Controller:`

```java
@PostMapping("/kullanici")
public ResponseEntity<Void> ekle(@RequestBody KullaniciDto dto) {
    service.kaydet(dto);
    return ResponseEntity.ok().build();
}
```

## 🚀 12. Best Practices

| Tavsiye                                        | Neden?                         |
| ---------------------------------------------- | ------------------------------ |
| DTO’larda record kullan                        | Kod sadeleşir                  |
| `record`'ları servis veya entity için kullanma | Mantıksal karmaşa yaratır      |
| Parametre isimleri anlamlı tut                 | getter isimleri de bunlar olur |
| Interface ile kombinle                         | Type abstraction sağlar        |


## 🔚 Özetle

| Özellik                                 | Detay                              |
| --------------------------------------- | ---------------------------------- |
| Immutable veri türü                     | Değiştirilemez                     |
| DTO için mükemmel                       | Clean ve sade                      |
| Java 16+                                | Stable versiyon                    |
| Constructor, equals, hashCode, toString | Otomatik                           |
| İş mantığı içermez                      | Veri nesnesi (POJO) olarak kalmalı |


