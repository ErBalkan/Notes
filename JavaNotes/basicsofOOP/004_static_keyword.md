# ⚙️ static Keyword – Detaylı ve Kurumsal Seviye Anlatım

## 📌 1. static Nedir?

`static`, bir üyeyi (method, field, block veya class) doğrudan sınıfa bağlar.

Yani:

`“Bu alan bir nesneye değil, sınıfın kendisine aittir.”`

### 🔎 Ne demek bu?

Normalde bir sınıfı kullanmak için nesne oluşturman gerekir:

```java
Person p = new Person();
p.sayHello();
```

Ama `static` bir yapı nesneye ihtiyaç duymadan çalışır:

```java
Person.sayHi(); // doğrudan sınıf üzerinden
```

### 🔢 static Nerelerde Kullanılır?

| Kullanım Alanı       | Açıklama                             |
| -------------------- | ------------------------------------ |
| `static` field       | Sınıfa ait ortak değişken            |
| `static` method      | Nesneye bağlı olmayan işlev          |
| `static` block       | Sınıf yüklenirken bir kere çalışır   |
| `static` inner class | Nesne olmadan erişilebilen alt sınıf |


## 🧪 2. static Fields – Sınıfa Ait Değişkenler

### 🧠 Amaç:

Tüm nesneler arasında ortak olan verileri tutmak.

```java
public class Araba {
    public static int tekerSayisi = 4;
    public String marka;
}
```

```java
System.out.println(Araba.tekerSayisi); // 4
```

```java
Araba bmw = new Araba();
Araba audi = new Araba();
bmw.tekerSayisi = 6;

System.out.println(audi.tekerSayisi); // 6 ✅
```

```
ÖNEMLİ !!!

Statik değişkenler tüm nesneler arasında paylaşılır. Değeri bir yerde değişirse her yerde değişir.
```

## ⚙️ 3. static Methods – Sınıfa Ait Fonksiyonlar

### 🧠 Amaç:

- Nesneye bağımlı olmayan işlevleri barındırmak
- Utility / helper fonksiyonları oluşturmak

```java
public class MathUtils {
    public static int kare(int x) {
        return x * x;
    }
}
```

```java
int sonuc = MathUtils.kare(5); // 25
```

### 📛 Dikkat: static method içinde non-static üyeye erişemezsin ❌

```java
public class Araba {
    int hiz;

    public static void gosterHiz() {
        System.out.println(hiz); // ❌ HATA
    }
}
```

`Çözüm: ya method static olmayacak, ya da hiz static olacak.`

## 🧱 4. static Blocks – Sınıf İlk Yüklendiğinde Çalışır

```java
public class Veritabani {
    static {
        System.out.println("Veritabanı bağlantısı kuruldu.");
    }
}
```

Bu blok, sınıf belleğe ilk kez yüklendiğinde bir kere çalışır.

## 📦 5. static Inner Class – Nested Class Kullanımı

```java
public class DisSinif {
    static class IcSinif {
        void yazdir() {
            System.out.println("Static inner class");
        }
    }
}
```

__Kullanım:__

```java
DisSinif.IcSinif obj = new DisSinif.IcSinif();
obj.yazdir();
```

Inner class’ı nesne oluşturmadan kullanmak için `static` yapılır.


## 🧠 Avantajları – static Kullanmanın Gerekçeleri

| Gerekçe                                    | Açıklama                              |
| ------------------------------------------ | ------------------------------------- |
| Bellekte sadece 1 defa oluşturulur         | Hafıza dostudur                       |
| Global değişken gibi erişim sağlar         | Utility class mantığı kurulabilir     |
| Nesneye bağlı olmayan mantık ayrılır       | Daha temiz kod, daha düşük bağımlılık |
| OOP prensiplerini destekler (low coupling) | Sınıflar arası bağlılık azalır        |


## 🚫 Dezavantajları

| Durum                        | Sonuç                                        |
| ---------------------------- | -------------------------------------------- |
| Çok fazla `static` kullanımı | OOP yapısını bozar, test edilemez hale gelir |
| Global state oluşturma       | Kodun davranışı tahmin edilemez olabilir     |
| Mocking (test) zorluğu       | Dependency Injection ile çakışır             |


## 🧬 Gerçek Hayat Örneği

`UserService` içinde statik bir validator:


```java
public class Validator {
    public static boolean isEmailValid(String email) {
        return email.contains("@");
    }
}
```

```java
public class UserService {
    public void kaydet(String email) {
        if (Validator.isEmailValid(email)) {
            // kaydet
        }
    }
}
```

`✅ Validator sınıfını nesne oluşturmadan doğrudan kullanıyoruz.`

## ☑️ Best Practices (Kurumsal Kullanım Kuralları)

| Kural                                         | Açıklama                                |
| --------------------------------------------- | --------------------------------------- |
| Field’ları `static` yapmadan önce 2 kez düşün | Ortak mı gerçekten? Yoksa veri çakışır. |
| Utility method’lar için `static` ideal        | Örn: `Math.max()`, `UUID.randomUUID()`  |
| Business logic method’ları `static` yapma     | Test ve yapılandırma zorlaşır           |
| Constant değerler → `static final`            | Değişmeyen sabitleri böyle tanımla      |


```java
public static final int MAX_USER_COUNT = 1000;
```

## 🧠 Sık Sorulan Sorular

- ❓ static method neden non-static field’ı kullanamaz?

Çünkü static method çalışırken, nesneye ait alanlar bellekte olmayabilir. Bağımsız çalışması gerekir.

- ❓ static mi yoksa instance mı olmalı?

Eğer değer/işlev tüm nesneler arasında ortaksa, static olabilir.
Aksi halde instance yapısı (non-static) tercih edilmeli.

- ❓ static method override edilebilir mi?

Hayır, static method’lar miras alınabilir ama override edilemez. Shadowing olur.


