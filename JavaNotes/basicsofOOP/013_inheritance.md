# 👑 INHERITANCE (KALITIM) — Java’da Miras Sistemi

## 📌 1. Nedir Inheritance?

`Inheritance`, bir sınıfın (child/subclass) başka bir sınıfın (parent/superclass) özelliklerini (attributes) ve davranışlarını (methods) devralmasına olanak tanır.

__🔁 "Kod tekrarını azaltır, ilişkili nesneleri organize eder."__

```java
class Hayvan {
    void sesCikar() {
        System.out.println("Bir hayvan ses çıkardı");
    }
}

class Kedi extends Hayvan {
    void miyavla() {
        System.out.println("Miyav!");
    }
}
```

```java
Kedi k = new Kedi();
k.sesCikar();  // 🟢 Inherited method
k.miyavla();   // ✅ Child method
```

## 🧬 2. Neden Kullanılır?

| Amaç                            | Faydası                                       |
| ------------------------------- | --------------------------------------------- |
| 🧼 Kod tekrarını azaltır        | DRY (Don’t Repeat Yourself) uygulanır         |
| 🧱 Ortak davranışları soyutlar  | Tüm alt sınıflar aynı temel yapıdan türetilir |
| 🔄 Polymorphism ile çalışır     | Farklı sınıflar tek arayüzle yönetilir        |
| 🧩 Sistemi modüler hale getirir | Genişletilebilir mimari sağlar                |


## 🔑 3. Temel Anahtar Kelime: extends

```java
class AltSinif extends UstSinif {
    // Yeni davranışlar tanımlanabilir
}
```

## 🧪 4. Basit Örnek:

```java
class Arac {
    int hiz = 60;
    void hareketEt() {
        System.out.println("Araç hareket ediyor.");
    }
}

class Araba extends Arac {
    void kornaCal() {
        System.out.println("Bip bip!");
    }
}
```

```java
Araba a = new Araba();
a.hareketEt();  // 👈 Üst sınıftan geldi
a.kornaCal();   // 👈 Kendi metodu
System.out.println(a.hiz); // 👈 Üst sınıf alanı
```

## 🔀 5. Overriding (Ezme)

Alt sınıf, üst sınıfın metodunu override ederek kendi versiyonunu tanımlar:

```java
class Hayvan {
    void sesCikar() {
        System.out.println("Hayvan sesi");
    }
}

class Kopek extends Hayvan {
    @Override
    void sesCikar() {
        System.out.println("Hav hav!");
    }
}
```

```java
Hayvan h = new Kopek();
h.sesCikar();  // 🔁 “Hav hav!”
```

✔️ `@Override` annotation’ı zorunlu değil, ama IDE ve compiler için önemlidir.

## 🧠 6. super Anahtar Kelimesi

### a) Üst sınıf constructor’ını çağırmak:

```java
class Hayvan {
    Hayvan() {
        System.out.println("Hayvan oluşturuldu");
    }
}

class Kedi extends Hayvan {
    Kedi() {
        super(); // 👈 üst sınıf constructor'ı
        System.out.println("Kedi oluşturuldu");
    }
}
```

### b) Üst sınıf metodunu çağırmak:

```java
@Override
void sesCikar() {
    super.sesCikar(); // Hayvan sesi
    System.out.println("Miyav!");
}
```

## 🧱 7. Constructor Mirası?

Java'da constructor’lar miras alınmaz, ama `super()` ile çağrılır.

## ⚙️ 8. IS-A İlişkisi

```java
class Araba extends Arac {}
```

`Araba IS-A Arac` - Bu, inheritance ilişkisini tanımlar.
Polymorphism için kritik!

## ❗ 10. Java’da Çoklu Kalıtım?

Java sınıf düzeyinde çoklu kalıtımı desteklemez. (C++ gibi değil.)

```java
class A {}
class B {}
// class C extends A, B ❌ Bu GEÇERSİZ!
```

Ama bunu interface ile çözeriz.

