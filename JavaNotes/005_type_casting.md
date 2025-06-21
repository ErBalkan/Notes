# 🔄 Type Casting (Tür Dönüştürme)

Java'da değişkenleri farklı veri tiplerine dönüştürme işlemine `type casting` denir. Bu, özellikle sayısal işlemler, veri transferi, API dönüşleri ve bellek optimizasyonunda çok sık kullanılır. Kurumsal projelerde, hatasız ve bilinçli dönüşüm yapmak veri kaybı, hata ve performans sorunlarını önlemek için kritiktir.

__🔎 Type Casting Nedir?__

Bir veri tipini başka bir veri tipine dönüştürme işlemidir.

__Java'da iki tür type casting vardır:__

```java
1. Implicit Casting (Otomatik)
2. Explicit Casting (Manuel)
```

## ✅ 1. Implicit Casting (Widening Casting)

- Küçük veri tipi __→__ büyük veri tipine dönüştürülür.
- Otomatik gerçekleşir.
- Veri kaybı yaşanmaz.

`🧱 Küçük → Büyük:`

`byte` __→__ `short` __→__ `int` __→__ `long` __→__ `float` __→__ `double`


`🔧 Örnek:`

```java
int x = 10;
double y = x; // Otomatik dönüşüm (int → double)

System.out.println(y); // 10.0
```

## ✅ 2. Explicit Casting (Narrowing Casting)

- Büyük veri tipi __→__ küçük veri tipine dönüştürülür.
- Elle belirtilmesi gerekir.
- Veri kaybı olabilir!

`🔧 Örnek:`

```java
double price = 99.99;
int wholePrice = (int) price; // double → int dönüşüm

System.out.println(wholePrice); // 99 → ondalık kısmı kayboldu
```

## 🧪 String ↔ Primitive Dönüşüm (Wrapper Classes ile)

Java’da `String` türündeki verileri sayıya çevirmek istiyorsan `Wrapper Class` kullanırsın.

```java
String ageStr = "25";
int age = Integer.parseInt(ageStr);

String priceStr = "19.99";
double price = Double.parseDouble(priceStr);
```

__Tersi için:__

```java
int count = 100;
String countStr = String.valueOf(count);
```

## 📦 Wrapper Classes – Primitive ↔ Object

| Primitive | Wrapper Class |
| --------- | ------------- |
| `int`     | `Integer`     |
| `double`  | `Double`      |
| `boolean` | `Boolean`     |
| `char`    | `Character`   |


__Otomatik dönüşümler:__

```java
int x = 5;
Integer obj = x; // Auto-boxing

int y = obj;     // Auto-unboxing
```

## 💡 Best Practices (Kurumsal Bakış)

- __Type casting__ işlemlerini her zaman kontrollü yap. Özellikle dışardan gelen verilerde (API, JSON).
- __double → int__ dönüşümünde ondalık kısmın kaybolacağını unutma.
- __byte, short, char__ gibi küçük tiplerde taşma __(overflow)__ riski yüksek __→__ test etmeden kullanma.
- __Wrapper class__ kullanımı, null değere izin verir __→__ dikkatli yönetilmeli.


