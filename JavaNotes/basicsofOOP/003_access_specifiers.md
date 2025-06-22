# 🔐 Access Specifiers (veya Access Modifiers) konusuna detaylıca giriyoruz.

Bu konu kurumsal kod yazımının temelidir.
Hangi veriye nereden erişileceği, projenin güvenliği, ölçeklenebilirliği ve modülerliği açısından hayati öneme sahiptir.

## 🧩 1. Nedir Access Specifier?

Access Specifier’lar, sınıf üyelerinin __(attribute, method, constructor, class vs.)__ nereden erişilebileceğini tanımlar.

Yani:

- “Bu alana kim dokunabilir, kim dokunamaz?”
- “Kodun dışına ne kadar açığım?”

## 🔒 2. Java’daki 4 Erişim Seviyesi

| Modifier    | Aynı Sınıf | Aynı Paket | Alt Sınıf (Subclass) | Diğer Paket            |
| ----------- | ---------- | ---------- | -------------------- | ---------------------- |
| `public`    | ✅          | ✅          | ✅                    | ✅                      |
| `protected` | ✅          | ✅          | ✅                    | ❌ (sadece miras varsa) |
| *default*   | ✅          | ✅          | ❌                    | ❌                      |
| `private`   | ✅          | ❌          | ❌                    | ❌                      |


## 1️⃣ public

Her yerden erişilebilir. Kodun tamamına açık.

```java
public class Araba {
    public int hiz;

    public void calistir() {
        System.out.println("Araba çalıştı.");
    }
}
```

➡️ public metotlara ve field’lara farklı paketlerden, farklı sınıflardan erişilebilir.

## 2️⃣ private

Sadece tanımlandığı sınıf içinde geçerlidir.
Encapsulation’ın temel taşıdır.

```java
public class Araba {
    private int hiz;

    private void calistir() {
        System.out.println("Çalıştı ama dışarıdan çağrılamaz.");
    }
}
```

__✅ Doğrudan erişim engellenir:__

```java
Araba a = new Araba();
a.hiz = 100;          // ❌ HATA
a.calistir();         // ❌ HATA
```

__👨‍💻 Çözüm: Getter / Setter yazılır:__

```java
public int getHiz() { return hiz; }
public void setHiz(int h) { hiz = h; }
```

## 3️⃣ protected

Aynı paketten erişim mümkün ✅

Farklı paketten sadece alt sınıflar erişebilir ✅

```java
public class Araba {
    protected int hiz;

    protected void calistir() {}
}
```

➡️ Farklı pakette, ama subclass ise erişebilir:

```java
// Paket: araba
public class Araba {
    protected int hiz = 100;
}

// Paket: uygulama
public class SporAraba extends Araba {
    void test() {
        System.out.println(hiz); // Erişilir ✅
    }
}
```

## 4️⃣ default (no modifier)

Hiçbir şey yazmazsan, varsayılan olarak bu geçerlidir.
Sadece aynı pakette geçerlidir.

```java
class Araba {
    int hiz; // default
}
```

```java
// aynı pakette
Araba a = new Araba();
System.out.println(a.hiz); // ✅
```

```java
// farklı pakette
Araba a = new Araba();
System.out.println(a.hiz); // ❌ erişim HATASI
```

## 🧠 Nerede Hangi Modifier Kullanılır?

| Kullanım Amacı             | En Uygun Modifier |
| -------------------------- | ----------------- |
| Field → dışarı kapalı      | `private`         |
| Method → herkes kullansın  | `public`          |
| Utility method             | `public static`   |
| Miras + sınırlı görünürlük | `protected`       |
| Sadece aynı pakette kalsın | *default*         |


## ✅ Best Practices

| Kural                                   | Neden?                                  |
| --------------------------------------- | --------------------------------------- |
| Field → daima `private` olmalı          | Encapsulation sağlar                    |
| Method → genellikle `public` olur       | Erişim ihtiyacı doğrudan                |
| Utility method → `public static`        | Sınıf olmadan erişilebilir              |
| Kalıtım sınıfları → `protected` kullan  | Mirasla kullanılabilir, ama dışa kapalı |
| Sınıf → `public` veya *default* kalmalı | Modüler paketleme için yeterlidir       |


## 🚨 Sık Yapılan Hatalar

| Hata                       | Sonuç                                      |
| -------------------------- | ------------------------------------------ |
| Field’ları `public` yapmak | Güvenlik açığı + veri kontrolü yok         |
| Her şeyi `private` yapmak  | Test ve genişletme zorluğu                 |
| `protected` yanlış anlamak | Farklı paketten erişim yok, sadece mirasla |
| class’a `private` yazmak   | Derlenmez! Sadece iç sınıflarda geçerli    |

## 🎯 Özet Tablo

| Modifier    | Aynı Sınıf | Aynı Paket | Subclass (farklı pakette) | Diğer Paket |
| ----------- | ---------- | ---------- | ------------------------- | ----------- |
| `public`    | ✅          | ✅          | ✅                         | ✅           |
| `protected` | ✅          | ✅          | ✅                         | ❌           |
| `default`   | ✅          | ✅          | ❌                         | ❌           |
| `private`   | ✅          | ❌          | ❌                         | ❌           |



