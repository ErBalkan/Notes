# 📦 Packages – Java'da Paket Yapısı (Uzman Seviye Anlatım)

## 🔍 1. Nedir Bu package?

Java’da package, ilgili sınıfların ve interface’lerin mantıksal olarak gruplandığı bir yapıdır.

Aynı modüldeki benzer işleri yapan sınıfları tek bir çatı altına toplar.

## 🎯 2. package Kullanmanın Amaçları

| Amaç                               | Açıklama                                                   |
| ---------------------------------- | ---------------------------------------------------------- |
| ✅ Kod organizasyonu                | Modüllere ayrılmış okunabilir yapı                         |
| 🔐 Erişim kontrolü                 | `protected` ve `default` erişimler package’a göre davranır |
| ♻️ Aynı isimli class’ların ayrımı  | Farklı paketlerde aynı class ismi olabilir                 |
| 🔧 Reusability                     | Ortak paketler başka projelerde de kullanılabilir          |
| 🧱 Büyük projede sürdürülebilirlik | Mikroservis mimarilerde vazgeçilmezdir                     |


## 🔧 3. Nasıl Tanımlanır?

Dosyanın en üst satırına package tanımı yazılır.

```java
package com.patron.utils;

public class MathUtils {
    public static int topla(int a, int b) {
        return a + b;
    }
}
```

📁 Dosya yolu bu pakete birebir uyumlu olmalıdır:
`/com/patron/utils/MathUtils.java`

## 📥 4. Nasıl Kullanılır? (Import)

Başka bir paketteki sınıfı kullanmak için `import` yapılır:

```java
import com.patron.utils.MathUtils;

public class Main {
    public static void main(String[] args) {
        int sonuc = MathUtils.topla(3, 5);
        System.out.println(sonuc);
    }
}
```

`import` bir klasördeki sınıfı, başka bir paket içinden erişilebilir hale getirir.

## 🔐 5. Erişim Seviyeleri ve Paket

| Erişim Belirleyici              | Aynı Paket | Farklı Paket         | Açıklama                       |
| ------------------------------- | ---------- | -------------------- | ------------------------------ |
| `public`                        | ✅          | ✅                    | Her yerden erişilebilir        |
| `protected`                     | ✅          | 🔸 (inheritance ile) | Sadece alt sınıflar            |
| `default` (hiçbir şey yazılmaz) | ✅          | ❌                    | Sadece aynı paketten erişim    |
| `private`                       | ❌          | ❌                    | Sadece kendi sınıfından erişim |


## 🧱 6. Paket İsimlendirme Standardı

Java’da ters domain adı kullanılır:

`com.firmaadi.projeadi.moduladi`

```java
package com.yoksoft.blog.post.controller;
```

__🌐 Ters domain: Çünkü domain isimleri unique’tir → Çakışma engellenir.__

## 📦 7. import Stratejileri

```java
// Tek class importu
import com.yoksoft.utils.MathUtils;

// Tüm class'ları import et (Wildcard)
import com.yoksoft.utils.*;
```

```
🧨 Wildcard import, readability düşürür, IDE ile yapılmalı ama manuelde önerilmez.
```

## ✅ Best Practices

| Kural                                 | Açıklama                                        |
| ------------------------------------- | ----------------------------------------------- |
| Paket isimleri **hepsi küçük harf**   | Standart gereği PascalCase yapılmaz             |
| Anlamlı gruplamalar kullan            | `controller`, `service`, `model`, `config` gibi |
| Ters domain konvansiyonu kullan       | `com.firma.proje.modul`                         |
| Her class doğru pakette olmalı        | `UserService` → `service` altında               |
| Utility class'ları `util` paketine at | Kod ayrışması net olur                          |


## 📚 Sık Yapılan Hatalar

- ✅ package satırı dosyanın en üstünde olmalı. import’tan bile önce.

- ❌ package ismi ile dosya yolu uyumsuz olursa ClassNotFoundException alırsın.

- ❌ Paketler arası erişimde default veya private kullanımı patlatabilir.

- ❌ Java'da iki farklı pakette aynı class ismi varsa import çatışmalarına dikkat et.


