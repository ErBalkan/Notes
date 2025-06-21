# 🔢 Java Data Types (Veri Tipleri)

Bu konu, Java’nın temel taşlarından biridir. Bir değişken tanımlarken ne tür bir veri saklayacağını belirtmek zorundasın. Java, __statik ve güçlü tipli (strongly typed)__ bir dil olduğu için tip belirtmeden kod yazamazsın.

Kurumsal projelerde doğru veri tipi seçimi, performans ve bellek optimizasyonu açısından çok önemlidir.

## 📚 Java Veri Tipleri – Genel Bakış

Java’da veri tipleri iki ana kategoriye ayrılır:

1. __Primitive Types (ilkel)__
2. __Non-Primitive Types (referans)__

## ✅ 1. Primitive Data Types (8 Adet)

| Tip       | Boyut  | Açıklama                     | Örnek                            |
| --------- | ------ | ---------------------------- | -------------------------------- |
| `byte`    | 1 byte | -128 ile 127 arası           | `byte age = 25;`                 |
| `short`   | 2 byte | -32K ile +32K arası          | `short temp = 32000;`            |
| `int`     | 4 byte | En çok kullanılan tamsayı    | `int number = 1000;`             |
| `long`    | 8 byte | Çok büyük tamsayılar için    | `long population = 8000000000L;` |
| `float`   | 4 byte | Ondalıklı, düşük hassasiyet  | `float pi = 3.14f;`              |
| `double`  | 8 byte | Ondalıklı, yüksek hassasiyet | `double price = 99.99;`          |
| `char`    | 2 byte | Tek karakter (Unicode)       | `char gender = 'M';`             |
| `boolean` | 1 bit  | true / false                 | `boolean isActive = true;`       |

__🧠 Notlar:__

- `float` tanımında `f` sonuna eklenmeli: `float x = 1.23f;`
- `long` tanımında `L` sonuna eklenmeli: `long y = 123456789L;`
- `char` sadece tek karakter alır: `'A', '3', '#'`

## ✅ 2. Non-Primitive (Reference) Data Types

Bunlar `class, array, enum, interface` gibi referansla çalışan yapıları içerir.

__En yaygın olanı: String__

```java 
String name = "Patron";
```

`String`, Java'da __nesne (object)__ olarak çalışır. Bu yüzden `new String("abc")` şeklinde de tanımlanabilir.

## 🆚 Primitive vs Non-Primitive

| Özellik                      | Primitive | Non-Primitive       |
| ---------------------------- | --------- | ------------------- |
| Bellek boyutu küçük          | ✅         | ❌                   |
| Sadece veri tutar            | ✅         | ❌                   |
| Metot içermez                | ✅         | ❌ (metot içerir)    |
| Null olamaz                  | ✅         | ✅ (null olabilir)   |
| Heap yerine stack’te tutulur | ✅         | ❌ (heap'te tutulur) |


```
int vs long seçimini doğru yap. Performans kritikse long kullanma.

Parasal işlemlerde double yerine BigDecimal tercih et (precision problemi için).

boolean tipini sadece mantıksal kararlar için kullan, sayı yerine kullanmak hatadır.
```

## 🚨 Dikkat Etmen Gereken Hatalar

```java
float pi = 3.14;       // Hata: float olduğu belirtilmemiş
long population = 10000000000; // Hata: L harfi yok
char letter = "A";     // Hata: çift tırnak yerine tek tırnak kullanılmalı
```

__Doğrusu:__

```java
float pi = 3.14f;
long population = 10000000000L;
char letter = 'A';
```

## 🔥 Bonus: var Keyword (Java 10+)

Java 10 ile birlikte `var` geldi. Tip belirtmeden derleyici otomatik algılar:

```java
var city = "Istanbul"; // String olarak algılanır
var age = 25;          // int olarak algılanır
```

Ama değişken tipi sabittir, dinamik değildir. Bu JavaScript değil.

## 📦 Bellek Kullanımı (Stack vs Heap)

| Veri Tipi                   | Nerede Tutulur | Açıklama                       |
| --------------------------- | -------------- | ------------------------------ |
| `int`, `boolean`            | Stack          | Hızlı, küçük veri alanı        |
| `String`, `Array`, `Object` | Heap           | Daha büyük ve karmaşık veriler |


