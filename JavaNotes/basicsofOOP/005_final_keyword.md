# 🔐 final Keyword – Derinlemesine ve Kurumsal Seviye Anlatım

## 📌 final Ne İşe Yarar?

__final__ , bir yapının değiştirilemez (immutable) olmasını garanti eder.

Java’da 3 temel yerde kullanılır:

| Kullanım Alanı   | Ne anlama gelir?                                       |
| ---------------- | ------------------------------------------------------ |
| `final` variable | Bir kez değer atanır, sonra değiştirilemez.            |
| `final` method   | Alt sınıflar override edemez.                          |
| `final` class    | Kalıtım (inheritance) engellenir, alt sınıf yapılamaz. |


## 🔒 1. final Variables – Sabit Değişkenler

### 📌 Tanım:

Değeri yalnızca 1 kez atanabilir. Sonradan değiştirmek derleme hatası üretir.

```java
final int yas = 30;
yas = 35; // ❌ Compile Error
```

#### 🎯 Nerede kullanılır?

- Sabit tanımlar (static final)
- Güvenli parametreler (method içinde)
- Constructor ile sadece bir kere atanacak alanlar

### 🧠 final vs static final

| Tanım          | Anlamı                                       |
| -------------- | -------------------------------------------- |
| `final`        | Değiştirilemez                               |
| `static`       | Sınıfa aittir                                |
| `static final` | Değeri sabit ve sınıfa aittir (global sabit) |

```java
public static final double PI = 3.14159;
```

🔐 Bu yapılar çoğu zaman sabitler (constants) için kullanılır. public static final yapısı Java'da constant naming convention'dır.

## 🧱 2. final Methods – Override Edilemez Fonksiyonlar

### 📌 Tanım:

Alt sınıflar bu method’u ezemez (override edemez).
Yani davranış kilitlenmiştir.

```java
public class Hayvan {
    public final void nefesAl() {
        System.out.println("Nefes alıyor");
    }
}

public class Kopek extends Hayvan {
    public void nefesAl() { } // ❌ Compile Error
}
```

__Bu sayede core davranışın bozulması engellenir.__

### 🎯 Ne zaman kullanılmalı?

- Güvenlik hassasiyeti varsa (örneğin banka işlemleri)
- API tasarımı yaparken bir davranışın değiştirilmesini istemiyorsan

## 🧱 3. final Class – Miras Alınamaz Sınıf

### 📌 Tanım:
Başka bir sınıf bu sınıftan kalıtım alamaz.

```java
public final class AyarYonetici {
    // yapılandırma işlemleri
}
```

```java
public class AltYonetici extends AyarYonetici {
    // ❌ Compile Error
}
```

### 🎯 Neden final class kullanılır?

- Güvenlik (örneğin java.lang.String bu şekilde tanımlıdır)
- Kodun stabil kalmasını istemek
- Performans (JVM bazı optimizasyonları daha agresif yapabilir)


## 🧪 Constructor'da final Field Kullanımı

```java
public class Kisi {
    private final String ad;

    public Kisi(String ad) {
        this.ad = ad; // ✅ Yalnızca constructor’da bir kere atanabilir
    }
}
```

```java
Kisi k = new Kisi("Ali");
System.out.println(k.ad); // "Ali"
```

## ⚠️ Önemli Not: final Nesne Değişkenlerinde Ne Olur?

```java
final List<String> isimler = new ArrayList<>();
isimler.add("Ahmet"); // ✅ OK
isimler = new ArrayList<>(); // ❌ HATA
```

`final, referansın değişmesini engeller. Ama içerik değişebilir.`

## 👨‍💼 Kurumsal Kullanım Senaryoları

| Kullanım Durumu       | Uygulama                                         |
| --------------------- | ------------------------------------------------ |
| Immutable sınıf       | Tüm field’lar `private final` olur               |
| Güvenli method        | `final` method override edilemez                 |
| Değiştirilemez config | `public static final` constant yapılır           |
| Thread-safe yapı      | `final` değişkenlerde visibility problemi yoktur |


## 🎯 final vs abstract vs static

| Keyword    | Anlamı                             | Overridable?                       | Inheritable?         |
| ---------- | ---------------------------------- | ---------------------------------- | -------------------- |
| `final`    | Sabit, değiştirilemez              | ❌ Hayır                            | ❌ Hayır (class için) |
| `abstract` | Tanımsız, alt sınıfta tanımlanmalı | ❌ (tanımsızdır)                    | ✅ Evet               |
| `static`   | Sınıfa ait, nesneye ait değil      | ❌ (override değil, shadowing olur) | ⚠️ Kapsamlıdır       |


