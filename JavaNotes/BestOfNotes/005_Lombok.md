# LOMBOK

## 🔧 1. LOMBOK NEDİR?

Lombok, Java'da sık sık yazmak zorunda kaldığımız:

- Getter/Setter
- Constructor (Yapıcı metodlar)
- toString()
- equals() & hashCode()
- Builder Pattern
- Immutable objeler

gibi kodları otomatik olarak üretmek için kullanılan bir Java annotation (anotasyon) kütüphanesidir.

## 🧠 2. NEDEN KULLANILIR?

| Geleneksel Java               | Lombok ile Java                                 |
| ----------------------------- | ----------------------------------------------- |
| Kendi getter/setter yazılır   | `@Getter`, `@Setter` ile otomatik oluşur        |
| Constructor elle yazılır      | `@AllArgsConstructor`, `@NoArgsConstructor` ile |
| toString elle override edilir | `@ToString` ile otomatik                        |
| Kod karmaşıklaşır             | Kod daha okunabilir olur                        |
| Refactor zorlaşır             | Lombok ile bakımı kolaylaşır                    |


```
Amaç: Kod tekrarını azaltmak, sınıfları sadeleştirmek, geliştirme süresini kısaltmak.
```

## 🏗️ 3. MAVEN PROJESİNE LOMBOK EKLEME

`pom.xml` dosyasına şu bağımlılığı `(dependency)` ekle:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.32</version> <!-- En güncel versiyonu kontrol et -->
    <scope>provided</scope>
</dependency>
```

```
scope: provided = Lombok sadece derleme (compile) zamanında gereklidir, çalıştırma (runtime) için değil.
```

## 🧩 4. LOMBOK ANOTASYONLARI VE AÇIKLAMALARI

### 📌 A. @Getter / @Setter

```java
@Getter
@Setter
public class User {
    private String name;
    private int age;
}
```

Bu anotasyonlar sayesinde `getName()`, `setName()`, `getAge()`, `setAge()` otomatik oluşur.

### 📌 B. @NoArgsConstructor / @AllArgsConstructor / @RequiredArgsConstructor

```java
@NoArgsConstructor           // Parametresiz constructor
@AllArgsConstructor          // Tüm field'lar için constructor
@RequiredArgsConstructor     // final ve @NonNull alanlar için
```

```java
@RequiredArgsConstructor
public class Product {
    private final String name;
    private double price;
}
```

__Sadece `name` alanı için constructor üretir, çünkü o `final`.__

### 📌 C. @ToString

```java
@ToString
public class Person {
    private String name;
    private int age;
}
```

__Otomatik `toString()` metodu üretir:__

### 📌 D. @EqualsAndHashCode

```java
@EqualsAndHashCode
public class Role {
    private int id;
    private String name;
}
```

__`equals()` ve `hashCode()` otomatik tanımlanır — bu özellikle Set koleksiyonlarında önemlidir.__

### 📌 E. @Data

```java
@Data
public class Employee {
    private String firstName;
    private String lastName;
}
```

__Şu anotasyonların hepsini birleştirir:__

- `@Getter`
- `@Setter`
- `@ToString`
- `@EqualsAndHashCode`
- `@RequiredArgsConstructor`

Yani full-featured POJO sınıfı üretir.

### 📌 F. @Builder

```java
@Builder
public class Customer {
    private String name;
    private int age;
}
```

__`"Builder pattern"` ile nesne oluşturmanı sağlar:__

```java
Customer c = Customer.builder()
                     .name("Ali")
                     .age(25)
                     .build();
```

### 📌 G. @Value

```java
@Value
public class Address {
    String street;
    String city;
}
```

__Immutable sınıf oluşturur:__

- Tüm field'lar `private final`
- Class `final`
- Getter’lar var, Setter yok
- `toString`, `equals`, `hashCode`, `constructor` var

### 📌 H. @SneakyThrows

```java
@SneakyThrows
public void riskyMethod() {
    throw new IOException("Oops");
}
```

__Checked exception’ları explicit olarak declare etmeden kullanmanı sağlar (kullanımı tartışmalıdır, dikkatli olun).__

## 💡 5. KULLANIMDA DİKKAT EDİLMESİ GEREKENLER

| Konu               | Açıklama                                                                 |
| ------------------ | ------------------------------------------------------------------------ |
| IDE Desteği        | IntelliJ IDEA veya Eclipse için Lombok plugin’i yüklenmeli               |
| Okunabilirlik      | Kodun ne yaptığı IDE dışında gözükmez, ekip arkadaşların anlayamayabilir |
| Debug              | Üretilen kod görünmez olduğu için hata ayıklamak zorlaşabilir            |
| Immutable Nesneler | `@Value` ile güvenli modeller oluşturulabilir                            |
| Serialization      | Lombok bazen Jackson gibi kütüphanelerle uyumsuz olabilir, dikkat!       |


## 🔍 6. UZMAN GÖZÜYLE DEĞERLENDİRME

### ✅ Avantajlar:

- Hızlı geliştirme
- Temiz kod
- Bakımı kolay projeler
- DRY prensibine uygun

### ❌ Dezavantajlar:

- IDE’ye bağımlı
- Anotasyon abuse (her yere koyma hastalığı)
- Performans profillemesi zor
- Karmaşık üretkenlik durumlarında aşırı soyutlama


## 📎 KURUMSAL SEVİYEDE KULLANIM STRATEJİSİ

- `Entity` sınıflarında `@Getter`, `@Setter`, `@NoArgsConstructor` ayrı ayrı yazılır. `@Data` tavsiye edilmez (fazla özellik getirir).

- `DTO` sınıflarında `@Data` veya `@AllArgsConstructor` kullanılabilir.

- Model class'larında `@Builder` ile obje üretimi şeffaflaştırılır.

- `@SneakyThrows` gibi sakıncalı anotasyonlar prod ortamda önerilmez.

