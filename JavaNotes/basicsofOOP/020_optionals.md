# ⚡ Java Optionals – Derinlemesine Uzman Analizi

## 1️⃣ Optional Nedir?
- Optional<T>, bir değerin varlığını veya yokluğunu (null olmayı) temsil eden bir kapsayıcıdır.
- Null kontrolünü zorunlu ve okunabilir kılar, NullPointerException riskini minimize eder.
- Kodda “null mu, değil mi?” sorgusunu temiz, fonksiyonel ve hatasız şekilde yapmayı sağlar.
- Fonksiyonel programlama paradigmalarının Java’ya entegrasyonunda temel taşlardan biri.

## 2️⃣ Neden Optional?

- Null kullanımı tehlikelidir, kodu kırılganlaştırır.
- Optional, null ile uğraşmayı geliştiriciye zorunlu hale getirir, böylece:
- Null kontrolü atlanmaz.
- Daha okunabilir ve amaca uygun kod yazılır.
- Yanlışlıkla yapılan null erişim hataları azalır.

## 3️⃣ Optional Oluşturma Yöntemleri

```java
Optional<String> emptyOpt = Optional.empty();           // Boş Optional
Optional<String> nonEmptyOpt = Optional.of("Patron");  // Null olmayan değer
Optional<String> nullableOpt = Optional.ofNullable(null); // Null olabilir değer
```

- `of` null kabul etmez, null girersen `NullPointerException` fırlatır.

- `ofNullable` null olabilir, Optional boş olur.

## 4️⃣ Optional Metotları ve Anlamları

| Metot                 | Açıklama                                                                   |
| --------------------- | -------------------------------------------------------------------------- |
| `isPresent()`         | Değer var mı diye kontrol eder (boolean)                                   |
| `get()`               | Değeri alır, ama boşsa hata fırlatır                                       |
| `orElse(T other)`     | Değer yoksa alternatif değer döner                                         |
| `orElseGet(Supplier)` | Değer yoksa tembelleştirilmiş tedarikçi çağrılır                           |
| `orElseThrow()`       | Değer yoksa exception fırlatır                                             |
| `ifPresent(Consumer)` | Değer varsa işlem yapar                                                    |
| `map(Function)`       | İç değer üzerinde dönüşüm yapar, boşsa boş Optional döner                  |
| `flatMap(Function)`   | map’in düzleştirilmiş hali, Optional içinde Optional döndüğünde kullanılır |

## 5️⃣ Kurumsal İyi Pratikler

- Optional’ı null ile karıştırma. Optional, null değil; null’un önüne geçen kapsayıcıdır.

- Optional’ı alan ve dönen metotlarda kullan. Parametrelerde kullanımı tartışmalı, karmaşıklık yaratabilir.

- Performans kritik kodlarda Optional kullanımı dikkatli olmalı. Bazı durumlarda küçük performans kaybı olabilir.

- Null kontrolü gerektiren alanlarda Optional’ı tercih et. Örneğin, DB’den gelen opsiyonel veri.

- Optional ile null’dan kurtul, daha fonksiyonel ve temiz kod yaz.

## 6️⃣ Optional Kullanım Örnekleri

```java
// Kullanıcı ismi opsiyonel
Optional<String> userNameOpt = findUserNameById(id);

userNameOpt.ifPresent(name -> System.out.println("Kullanıcı adı: " + name));

String displayName = userNameOpt.orElse("Guest");

String upperName = userNameOpt.map(String::toUpperCase).orElse("UNKNOWN");
```

```
Modern Java mimarilerinde, özellikle mikroservislerde ve event-driven yapıda null güvenliği kritik önemde. Optionals kullanmak, kodun bakım maliyetini düşürür, hata oranını minimize eder, aynı zamanda geliştirici verimliliğini artırır.
```